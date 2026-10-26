## What

Fixes smaramwbc/statewave#485.

`timeline_inspector.py` builds its "AGENT CONTEXT RETRIEVALS" section from `context_retrieval` episodes, but nothing in the repo wrote one: `SharedContext.before_acting()` only read context. So the section never appeared and `Context reads` was always 0.

This PR:
- has `before_acting()` write a `context_retrieval` episode after each read, with the retrieved memories in `retrieved_memories`. It goes to a sibling subject, `<subject_id>:reads`, which is never compiled.
- writes the row text in the README sample's format: `Retrieved N memories`, plus ` (incl. deprecation)` when one of the memories is a deprecation decision.
- has `timeline_inspector.py` merge that subject's events into the timeline, so the section and the `Context reads` count see them.

## Before / after

Same script on both sides against a local Statewave server: the Planner, Coder and Reviewer each call `before_acting()` and then `note()`, then `print_timeline()` runs.

Before (`main` @ `eb66ddc`, trimmed): only the notes show, with no retrieval rows and no AGENT CONTEXT RETRIEVALS section.

```
──────────────────── CHRONOLOGICAL EVENT LOG ────────────────────
  04:08:24.823Z    T+0.0s     Planner      implementation_note      Planner done
  04:08:25.391Z    T+0.6s     Coder        implementation_note      Coder done
  04:08:25.922Z    T+1.1s     Reviewer     implementation_note      Reviewer done
────────────────── FINAL COMPILED MEMORY STATE ──────────────────
  →  Run ID          : sw-84af58f6
  →  Context reads   : 0
```

After (this branch, trimmed): each agent's read appears before its note, and the AGENT CONTEXT RETRIEVALS section appears.

```
──────────────────── CHRONOLOGICAL EVENT LOG ────────────────────
  04:08:28.980Z    T+0.0s     Planner      context_retrieval        Retrieved 0 memories
  04:08:28.985Z    T+0.0s     Planner      implementation_note      Planner done
  04:08:29.518Z    T+0.5s     Coder        context_retrieval        Retrieved 0 memories
  04:08:29.525Z    T+0.5s     Coder        implementation_note      Coder done
  04:08:30.066Z    T+1.1s     Reviewer     context_retrieval        Retrieved 0 memories
  04:08:30.072Z    T+1.1s     Reviewer     implementation_note      Reviewer done
─────────────────── AGENT CONTEXT RETRIEVALS ────────────────────
────────────────── FINAL COMPILED MEMORY STATE ──────────────────
  →  Run ID          : sw-b8b2fd2c
  →  Context reads   : 3
```

The counts read 0 because of smaramwbc/statewave#475 (retrieved memories come back empty), not because of this change. The row reports whatever `before_acting()` returned, so rows like the README's `Retrieved 2 memories (incl. deprecation)` will appear once #475 is fixed.

## Building on the issue's suggested fix

This follows the approach in the issue: `before_acting()` writes a `context_retrieval` episode with the retrieved memories, and nothing compiles right after that write. The one change is *where* the episode goes.

When I tried it on the shared subject, the record stayed out of memory only until the next agent action. A compile picks up every uncompiled episode on the subject, not just the newest one, and the pipeline compiles on every `decide()` and `note()`:

1. The Coder reads context, and the retrieval record is written without a compile.
2. The Coder writes its note with `note()`, which compiles the subject.
3. That compile picks up the retrieval record along with the note, so the record becomes a memory.

From then on, `get_context()` returns it. In the check below, the Reviewer's top retrieved fact was the Coder's retrieval log, ranked above the Coder's work and the Planner's decision. I think that's what the issue's "don't compile" note is meant to prevent: an audit record ending up in what the next agent reasons from.

Writing the record to `<subject_id>:reads` keeps the issue's approach and closes that gap. Nothing compiles that subject and no agent reads from it; only `timeline_inspector.py` does. The cost is one extra `get_timeline` call per inspector run. If you'd rather keep everything in one subject, I'm happy to switch; the change lives in one helper.

One smaller difference: the suggestion stores `memories` as-is, but the inspector reads `type`, `confidence` and `content` from each one and formats confidence with `:.2f`. This PR maps those fields explicitly (`kind` or `type`, and `confidence or 0`), so a memory with no confidence shows 0.00 instead of crashing the inspector.

<details>
<summary>What I ran to check that (on <code>main</code> @ <code>eb66ddc</code>)</summary>

```python
import sys, uuid
sys.path.insert(0, ".")
from core.statewave_client import StatewaveClient
from statewave_agents.context import SharedContext

c = StatewaveClient(base_url="http://localhost:8100")
run = f"sw-{uuid.uuid4().hex[:8]}"
ctx = SharedContext(subject_id=run, client=c)

# 1. The Planner decides. decide() compiles, so this becomes a memory.
ctx.decide("Planner", "Deprecation: legacy-session-token", kind="deprecate")

# 2. The issue's suggestion: write the retrieval record to the shared subject, no compile.
c.write_episode(subject_id=run, caller_id="Coder", content="Retrieved 1 memories for: Build auth",
                episode_type="context_retrieval", metadata={"retrieved_memories": []})
print("before next compile:", [m["content"] for m in c.get_timeline(run)["memories"]])

# 3. The Coder's next note(), which compiles the subject as usual.
ctx.note("Coder", "Built: jwt-auth", episode_type="implementation_note")
print("after next compile :", [m["content"] for m in c.get_timeline(run)["memories"]])

# 4. What the Reviewer gets back before acting (facts read directly because of #475).
facts = c._sdk.get_context(run, task="Build auth", caller_id="Reviewer").model_dump()["facts"]
print("Reviewer get_context facts:", [f["content"] for f in facts])
```

```
before next compile: ['Deprecation: legacy-session-token']
after next compile : ['Deprecation: legacy-session-token', 'Built: jwt-auth', 'Retrieved 1 memories for: Build auth']
Reviewer get_context facts: ['Retrieved 1 memories for: Build auth', 'Built: jwt-auth', 'Deprecation: legacy-session-token']
```

The record isn't a memory until the Coder's `note()`. After that it is, and it comes back first for the Reviewer.

</details>

## Scope

Changed:
- `statewave_agents/context.py`: a `reads_subject_id()` helper, and the write in `before_acting()`
- `timeline_inspector.py`: fetch and merge the sibling subject's events
- `tests/test_context_retrieval.py`: new

Deliberately not touched:
- compile behaviour, `decide()`, or any agent in `agents/`
- smaramwbc/statewave#475, which is a separate bug
- the README. Its sample already shows these rows, and the row text now matches its format. The one difference is that the sample has no Planner row, though the Planner also calls `before_acting()` first. Happy to add that row here if you'd like.

I also didn't take the issue's alternative of deleting the section: the README presents this audit trail as what the repo demonstrates, so recording it seemed closer to the intent.

## Testing

The repo had no test suite, so I added `tests/test_context_retrieval.py` (stdlib `unittest` with a fake client, no new dependency). Its three tests check that:
- `before_acting()` records the retrieval in the `:reads` subject, never compiles it, and writes `Retrieved 1 memories (incl. deprecation)` when a deprecation is among the memories.
- without a deprecation, the text is just `Retrieved 2 memories`.
- the inspector renders retrieval rows merged in from the `:reads` subject.

Results:
- `python -m unittest tests.test_context_retrieval`: 3 tests, OK. CI doesn't run unit tests, so I ran them locally.
- `pip install -r requirements.txt` and the `py_compile` check over every `.py` file (what CI runs): both clean.
- Separation check (`sw-ce4f5ccd`): after a Planner/Coder/Reviewer run, the shared subject holds only the `architectural_decision`, `implementation_note` and `review_finding` episodes, the `:reads` subject holds the three `context_retrieval` episodes, and a later `get_context()` on the shared subject does not surface them (`leak in assembled_context: False`).
- Older runs still display: the new inspector on `sw-f7b75257`, a run from before this change with no `:reads` subject, renders as before and exits 0.
- End-to-end through `main.py` with `LLM_MODEL=groq/openai/gpt-oss-120b` (the default `groq/llama-3.3-70b-versatile` now returns `model_not_found` on Groq), same command on both sides: `Context reads` went from 0 (`sw-f7b75257`, on `main`) to 3 (`sw-d2893eea`, this branch), with one retrieval row per agent. This run predates the row-text change above, which only affects the wording.

Environment: macOS 15.7.5, Python 3.11.14, statewave SDK 1.5.0, `statewavedev/statewave:latest` (image built 2026-10-16).

Not run locally: CI's markdown link check, which is a GitHub Action, so I'm relying on this PR's CI run for it.

## AI-assistance disclosure

AI-assisted: Claude Code was used to help reproduce the bug, write the fix and tests, and draft this description. I reviewed, ran, and verified every change above myself before opening this PR. (This repo states no AI-use policy; disclosing anyway.)

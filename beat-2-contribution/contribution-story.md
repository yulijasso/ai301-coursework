# Contribution: timeline_inspector's context-retrieval section is always empty - nothing writes context_retrieval episodes

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Yuliana Jasso
**GitHub Username:** yulijasso
**Issue:** https://github.com/smaramwbc/statewave/issues/485
**Pull Request:** https://github.com/smaramwbc/statewave-multi-agent-shared-context/pull/7

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: built issue-scout and fixed what my first real scan broke**

2026-10-11: I turned my Unit 1 issue-select skill into issue-scout and pointed its search
strategy at retrieval and RAG work, with one TypeScript-only query to leave room for surprises.
My first scan graded five issues and accepted all five, but none of them were about RAG,
because the TypeScript query kept returning brand-new issues with zero comments and those took
every slot. Two of the accepted repos had been created that same day with no stars and no
releases, and my repo-in-use check still passed them, since all it needed was a few recent
commits. I fixed the rubric so a repo without a recent release also needs at least 10 stars,
and changed the ranking so each query takes turns filling the top five. On the second scan my
RAG queries got four of the five slots, the new rule rejected two more tiny repos, and the
patched rubric still scores 20/20 on the Unit 1 eval.

**Unit 6: the voice-guard stopped my claim once, and the repo memory dropped the AGENTS.md import**

2026-10-18: The voice-guard stopped my first claim for statewave#485 because it promised a
timeline ("I'm aiming to have it up within the next week"), which breaks my own rule against
posting a date or ETA. I removed that sentence, and the revised claim passed. I posted it from
the browser, which the guard can't watch, so I ran the guard by hand on the exact text first;
both the stop and the pass are in `guard-log.md`.

For the repo memory, I wrote a 51-line `CLAUDE.local.md` using statewave's CONTRIBUTING.md and
one scoped look at the files my issue touches. One change from the template: I removed the
`@AGENTS.md` line, because this repo's AGENTS.md isn't contributor guidance. It's an
auto-generated note telling AI tools to use a Statewave server I don't have set up. The scoped
look also warned that my fix could accidentally save retrieval logs as memories, and I
confirmed that while reproducing the bug.

**Unit 7: Installed the ship-gate, wrote my manifest, and shipped before it passed**

My manifest runs two checks taken from the repo's CI, the dependency install and a
`py_compile` sweep, written as `.venv/bin/...` so they work in a fresh shell; I excluded
CI's lychee link check with a date and reason, since it only runs as a GitHub Action. The
code passed every gate run, but the gate blocked my branch five times, and every block was
my evidence or description describing a branch I no longer had: no description, a test
count that no longer matched, transcripts I said were in the issue thread when they weren't,
and live output captured before my last commit. What confused me most was that I opened PR #7
on a pass from an earlier three-file version of the branch, so I had to re-gate against the
live PR body afterwards, and it passed at `8ad4b87` on 10-26. Because of that, I now
regenerate `test_evidence.md` at HEAD before every gate run and re-gate after every amend
or force-push.

**Unit 8: Installed the PR-monitor, wrote my playbook, and it told me to wait**

2026-11-03: The other outside PRs in this repo have waited 17–29 days with no review, but the
same maintainer answers in `statewave` within a day or two, so my playbook says no nudge
before 21 days, only one ever, and it goes on #485 instead of the PR. The monitor read my PR
as quiet (open 9 days, no conflicts, no comments) and didn't draft a message, just a wait
note that quoted my 21-day rule and said the earliest I could nudge is 2026-11-15, so I
didn't post anything. It also showed me that GitHub has no CI checks on my PR, but my nudge
rule said I'd tell the maintainer "the checks still pass," so I changed it to say my checks
pass locally. The one thing it can't do is read #485, where my nudge would go, so I'll check
that thread myself before 11-15.

---

## Why I Chose This Issue

On 2026-10-18 I ran a fresh scan with my scout. Out of 306 issues, it graded the top five and
accepted two: a page of interview questions to write, and a small Makefile task. Neither was
the kind of retrieval code I wanted to work on, so I kept going down the list and graded five
more. That's where I found statewave#485. Statewave is a memory system for AI agents, and this
demo shows several agents sharing one memory. Its timeline tool has a section meant to show
what each agent retrieved before acting, but that section is always empty, because nothing in
the code ever records a retrieval. My scout accepted it, with every required check passing.

I chose it because it's a real bug I can see happen and then see fixed, the issue already
suggests a fix, and it sits right in the retrieval side of an AI memory system, which is
what I want to get better at. I'm hoping to learn how a system like this turns what agents
write into memories and hands the right ones back when an agent asks.

My scout didn't handle this search perfectly. It only grades five issues, and #485 wasn't one
of them, so I had to go past its limit to find the best fit. It also checked the wrong repo:
the issue is filed in the main `statewave` repo, where the maintainer responds quickly, but the
code lives in a separate repo where four PRs from other contributors are still waiting for
review. I only noticed that after I had claimed it, so I'm expecting the review to take a while.
I wrote both problems down in `scan-notes.md`. Next time, I'd have the scout check the repo
where the code actually lives, and grade more than five issues when the first five don't
include much real code work.

**Claim comment:** https://github.com/smaramwbc/statewave/issues/485#issuecomment-6248332834 (posted 2026-10-18)

**Toolkit**

- Tool: issue-scout in live scan mode with my iteration-2 strategy and rubric, then the same
  rubric on five more candidates from further down the same ranking.
- What it produced: scan 3 in `tools/issue-scout/scan-output.md`. Six of ten graded issues
  were accepted. #485 passed every required check, with `maintainer-responsive` failing (the
  only replies in the sample came from other contributors).
- Difficulties: the top-five limit hid #485; the tracker repo and the code repo differ, so the
  responsiveness sample read the wrong repo; Q3 returned nothing again.
- What changed: logged as scan-notes entries 8 to 11, not patched yet. Scan 3 ran on the
  rubric from before the 2026-10-18 scope patch (`scope-fits-newcomer` became
  `scope-feasible`); the patched rubric scores 19/20 in `rubric-regression-run.txt`.

---

## Understanding the Issue

**In short.** The demo's timeline report has a section meant to show what each agent read
from shared memory before acting. Nothing in the repo ever wrote those records, so the
section was always empty and the run summary always said `Context reads : 0` — while the
README advertised a sample full of rows the code could not produce.

**Problem Description**

`statewave-multi-agent-shared-context` is not an app anyone uses; it is a demo in the
Statewave project, the open-source memory runtime for AI agents. Its argument is that
agents working in parallel contradict each other when they only pass messages around — one
deprecates a token while another is still building on it — and that they stop contradicting
each other when they all read and write one shared context layer instead. `main.py` stages
that with three agents, a Planner, a Coder and a Reviewer, building a fake auth service:
once in naive mode where they collide, once through Statewave where they do not. Each agent
asks the shared memory "what has anyone decided so far?" before it acts, and writes back
what it decided afterwards.

`timeline_inspector.py` is the demo's last moment: the report that shows both halves, who
decided what and who looked at what before deciding. Only the first half was ever written
down. Deciding was recorded; looking was not. The report still had a section for the
looking, so that section was always empty, and the README showed an example of it full of
rows the code had no way to produce. Nobody noticed, because an empty section simply does
not render — there is no error, and the demo runs fine. The fix is to write a note every
time an agent looks; where that note goes turned out to be the whole problem, and that is
Solution Approach's story.

The section looks for episodes of type `context_retrieval` (`timeline_inspector.py:107`)
and reads `retrieved_memories` out of their metadata (`core/statewave_client.py:76`).
Nothing in the repo ever wrote one: `SharedContext.before_acting()` only reads context, and
grepping for `episode_type="context_retrieval"` or `retrieved_memories` returns the two
readers and no writer at all. So the feature existed in the renderer and in the README, and
nowhere else. The module's own docstring calls this "the audit artifact that does not exist
in any message-passing setup", which is the part I found funny in a useful way: it did not
exist here either. Severity is low — nothing crashes. What is missing is the evidence for
the claim the project is built to make.

**Expected Behavior**

After a run (`python main.py --mode statewave`, then
`python timeline_inspector.py --run <run_id>`), the timeline shows one retrieval row per
agent that called `before_acting()`, the AGENT CONTEXT RETRIEVALS section lists what each
of them retrieved, and the summary's `Context reads` count matches the number of reads that
actually happened — the shape the README's own sample output advertises.

This is the fixed run `sw-b8b2fd2c`, trimmed, which is what that looks like:

```
─────────────────── CHRONOLOGICAL EVENT LOG ───────────────────
  04:08:28.980Z   T+0.0s   Planner    context_retrieval      Retrieved 0 memories
  04:08:28.985Z   T+0.0s   Planner    implementation_note    Planner done
  04:08:29.518Z   T+0.5s   Coder      context_retrieval      Retrieved 0 memories
  04:08:29.525Z   T+0.5s   Coder      implementation_note    Coder done
  04:08:30.066Z   T+1.1s   Reviewer   context_retrieval      Retrieved 0 memories
  04:08:30.072Z   T+1.1s   Reviewer   implementation_note    Reviewer done
────────────────── AGENT CONTEXT RETRIEVALS ───────────────────
╭──── Planner retrieved context at 04:08:28.980Z (T+0.0s) ────╮
╭───── Coder retrieved context at 04:08:29.518Z (T+0.5s) ─────╮
╭──── Reviewer retrieved context at 04:08:30.066Z (T+1.1s) ───╮
──────────────────────────── SUMMARY ──────────────────────────
  →  Context reads   : 3
```

Each row reads "Retrieved 0 memories" because of smaramwbc/statewave#475, a separate bug
where retrieved memories come back empty; the row reports whatever `before_acting()`
returned.

**Current Behavior**

The section never appears. `print_timeline()` filters the event list for
`context_retrieval` episodes, finds none, and skips the block entirely, so there is no
error and nothing missing-looking on screen. `Context reads` reads 0 in every run, even
when the run's own console log shows the Coder and the Reviewer each reading shared context
first. The README's sample shows rows like `Retrieved 2 memories (incl. deprecation)` that
the code as written could not have produced.

The same script on `main` @ `eb66ddc`, run `sw-84af58f6`, trimmed — only the notes survive,
there is no AGENT CONTEXT RETRIEVALS section at all, and the count is 0:

```
─────────────────── CHRONOLOGICAL EVENT LOG ───────────────────
  04:08:24.823Z   T+0.0s   Planner    implementation_note    Planner done
  04:08:25.391Z   T+0.6s   Coder      implementation_note    Coder done
  04:08:25.922Z   T+1.1s   Reviewer   implementation_note    Reviewer done
──────────────────────────── SUMMARY ──────────────────────────
  →  Run ID          : sw-84af58f6
  →  Context reads   : 0
```

**Affected Components**

- `statewave_agents/context.py` — `SharedContext.before_acting()` (`:102-113` on `main` @
  `eb66ddc`), the read path. It calls `get_context` and returns the bundle; it never writes
  an episode. This is where the record has to start.
- `timeline_inspector.py` — the filter at line 107 that collects `context_retrieval`
  episodes, the panel block that is skipped whenever that list is empty, and the
  `Context reads` line in the summary that counts them.
- `core/statewave_client.py` — `write_episode` (`:26`), the only way an episode gets
  written, and the metadata read at `:76` that the renderer depends on. Before this change
  `write_episode`'s only callers were `SharedContext.decide` (`context.py:73`) and `.note`
  (`:92`), and both compile the subject afterwards when `auto_compile` is on — which is why
  compile behaviour became part of this issue rather than a detail.
- `README.md` — the sample timeline at lines 158 and 160, which shows rows like
  `Coder  context_retrieval  Retrieved 2 memories (incl. deprecation)`. The sample
  documented behaviour the code could not produce, so it was evidence of intent as much as
  a doc bug.

**Toolkit**

- Tool: the repo memory, `CLAUDE.local.md`, written from statewave's CONTRIBUTING (this
  repo has none of its own) plus one orientation run scoped to the subsystem the issue
  touches, so every later session loads the map instead of re-reading the repo.
- What it produced: a 51-line file with the repo's conventions, the build and test
  commands, and the part that did the work here — the call graph around episodes: who
  writes them, who reads them, and which calls compile. That is what turned "the section is
  empty" into "there is no writer, and the two writers that exist both compile".
- Difficulties: the template imports the repo's `AGENTS.md`, and here that file is
  auto-generated instructions for calling a Statewave MCP server I do not have, not
  contributor conventions. Importing it would have fed every session a page of irrelevant
  setup.
- What changed: I deleted the `@AGENTS.md` import and kept the file to what I verified
  myself, which also kept it under the length where a memory file stops being read.

---

## Reproduction Process

**Environment Setup**

macOS 15.7.5 (arm64), Python 3.11.14, with the project's own venv
(`python3.11 -m venv .venv && .venv/bin/pip install -r requirements.txt`), which brings in
the statewave SDK 1.5.0 and litellm 1.106.0. The demo needs a running Statewave server, so I
started `statewavedev/statewave:latest` (image built 2026-10-16) with
`pgvector/pgvector:pg16` under `docker compose` on `:8100`, and copied `.env.example` to
`.env` with a free-tier Groq `LLM_API_KEY` and `STATEWAVE_BASE_URL`.

Two problems came up during setup. The default model in the repo,
`groq/llama-3.3-70b-versatile`, now
returns `model_not_found` on Groq, so I set `LLM_MODEL=groq/openai/gpt-oss-120b` and
disclosed that override everywhere I report a run; nothing else about the steps changes.
And with that model the Planner's and Coder's replies did not match the formats their
parsers expect, so they published no decisions — which is unrelated to this bug, but it
means the timeline in my runs shows fewer notes than the README's sample.

**Steps to Reproduce**

1. Start the Statewave server on `:8100` and set `LLM_API_KEY` in `.env`.
2. `LLM_MODEL=groq/openai/gpt-oss-120b python main.py --mode statewave`
3. `python timeline_inspector.py --run <run_id>`
4. Observed: no "AGENT CONTEXT RETRIEVALS" section anywhere in the output, and the summary
   reads `Context reads : 0`, even though the run's own log shows the Coder and the
   Reviewer each reading shared context before acting.

**Reproduction Evidence**

- **Reproduction comment upstream:**
  https://github.com/smaramwbc/statewave/issues/485#issuecomment-6394341177 (posted
  2026-10-25), with the full `main.py` and `timeline_inspector.py` transcripts.
- **The reproducing run:** `sw-f7b75257` on `main` @ `eb66ddc` — `Context reads : 0`, no
  retrieval rows. The fixed run for comparison is `sw-d2893eea`, `Context reads : 3`.
- **Logs:** `test_evidence.md` at my clone root holds the captured before/after output, the
  separation check (`sw-ce4f5ccd`, `leak in assembled_context: False`), and the
  older-run compatibility check (`sw-f7b75257` rendered by the fixed inspector, exit 0).
- **My findings:** the bug is not that the section renders wrong, it is that nothing ever
  writes the episode it renders from. `timeline_inspector.py` reads `context_retrieval`
  episodes (line 107) and `SharedContext.before_acting()` only ever read context — grep
  returns two readers and no writer. So the section was dead code from the start, and the
  README's sample output showed rows the code could not produce. I also found that the
  issue's suggested fix, writing the episode to the run's own subject without compiling,
  does not hold: the next `note()` or `decide()` compiles the whole subject, and in my
  check the retrieval log came back as the Reviewer's top retrieved fact. That finding is
  what sent the fix to a sibling `<subject_id>:reads` subject.

**Toolkit**

- Tool: `repro-check` in live mode, with the wild scope that replaced its unit-2 sandbox
  scope, run on my claim comment and then on the full repro package before I posted it.
- What it produced: `accept`, with per-check evidence lines — environment recorded, steps
  followable, artifacts present, outcome matching the artifacts, and the model-override
  deviation named. The run is saved as `repro-check-485.md` at my clone root.
- Difficulties: the first draft of my repro report described what I saw rather than showing
  it, and `artifact-present` is written to fail exactly that. It also made me name the
  model override as a deviation instead of quietly using it, which is the line that ended up
  in the upstream comment too.
- What changed: I rewrote the report around pasted transcripts instead of narration, and I
  added the control comparison (a run with one chunk, and later the `:reads` separation
  check) so the evidence shows the trigger rather than just the failure.

---

## Solution Approach

**Analysis**

The renderer and the writer never met. `timeline_inspector.py` (L107-108) collects episodes
of type `context_retrieval` and reads `retrieved_memories` out of their metadata
(`core/statewave_client.py` L76), but the only two callers of `write_episode` were
`SharedContext.decide()` (`statewave_agents/context.py` L73) and `.note()` (L92).
`before_acting()` (L102-113) calls `get_context()` and returns the bundle without writing
anything. So no episode of that type has ever existed in this repo, the section is skipped
every time, and the summary reports `Context reads : 0` by arithmetic rather than by
accident.

The second half of the analysis is about compiling, and it is the part that decided the
design. Statewave compiles a subject into retrievable memory, and `SharedContext` does that
automatically on `decide()` and `note()` when `auto_compile` is on. A compile picks up every
uncompiled episode on the subject, not just the newest one — so an audit record written to
the shared subject does not stay out of memory by having no compile after it; it waits until
the next agent action and gets compiled then.

**Proposed Solution**

Write the retrieval record, but to a sibling subject that nothing compiles and no agent
reads: `<subject_id>:reads`, behind a `reads_subject_id()` helper so the name exists in one
place. `before_acting()` writes a `context_retrieval` episode there after each read, with
`metadata["retrieved_memories"]` shaped as `{type, confidence, content}` per memory, which
is what the inspector expects. `timeline_inspector.py` fetches that subject alongside the
run's own and merges its events, so both the section and the `Context reads` count see them;
memories still come only from the shared subject.

Deliberately not changed: compile behaviour, `decide()`, `note()`, any agent in `agents/`,
smaramwbc/statewave#475 (where `before_acting()` reads a `memories` key the SDK never
returns, which is why every row currently reads "Retrieved 0 memories"), and `get_context`
ignoring `top_k` (`core/statewave_client.py` L57-61). Both of those are real, and both are
separate issues.

**Implementation Plan**

1. `statewave_agents/context.py`: add `reads_subject_id(subject_id)` returning
   `"<subject_id>:reads"`, and write the `context_retrieval` episode at the end of
   `before_acting()`.
2. `timeline_inspector.py`: fetch the reads subject's timeline and merge its events into the
   event list.
3. `tests/test_context_retrieval.py`: unit tests with a fake client, stdlib `unittest`, so
   the repo gains no dependency.

**Deviation from the issue's suggested fix.** The issue proposed writing the episode to the
run's own subject and simply not compiling afterwards. I tried that first and it does not
hold: on a probe run, the Coder's retrieval record was not a memory until the Coder's next
`note()`, and after that compile it was — and the Reviewer's `get_context()` then returned
that retrieval log as its *top* fact, ranked above the Coder's actual work and the Planner's
decision. The server has no per-type compile skip, and `assembled_context` is assembled
server-side, so filtering on the client cannot clean what the next agent reasons from. The
sibling subject makes the separation structural instead of conventional. I reported this on
the issue before opening the PR and offered to move the write back if the maintainer prefers
one subject; it is a helper and one call site.

**Toolkit**

- Tool: `plan-check` in live mode on `plan.md` and the plan comment, with the wild scope that
  replaced its unit-3 sandbox scope.
- What it produced: an accept, and before that the push to make the root cause point at
  specific lines rather than at a file — the check wants the cause traced to code, so "the
  inspector reads an episode type nothing writes" had to become L107-108 against L73 and L92.
- Difficulties: my first plan had the fix and the compile problem tangled in one paragraph,
  so the deviation was invisible — it read as the plan, not as a departure from the issue's
  plan. A plan whose deviation cannot be seen is the plan-fidelity failure the sandbox eval
  set is built around, and my own rubric would have caught it on a package.
- What changed: I split the deviation into its own section with the probe output behind it,
  which is the shape it then kept in the issue comment and in the PR description. I also
  started keeping a dated deviations list at the bottom of `plan.md` and writing to it the
  day something changes, rather than reconstructing the build at the end.

---

## Testing Strategy

**The change under test.** Three files, +183/−2 on `8ad4b87`: a `reads_subject_id()` helper
and a `write_episode(..., episode_type="context_retrieval")` call at the end of
`before_acting()` in `statewave_agents/context.py`; a second `get_timeline()` fetch in
`timeline_inspector.py` that merges the sibling subject's events; and a new
`tests/test_context_retrieval.py`.

Proving that works means two things: a read that happened now shows up in the report, and
nothing else changed. I ran four checks.

**1. The reproduction, re-run on both sides.** Same script each time: Planner, Coder and
Reviewer each call `before_acting()` and then `note()`, then `print_timeline()` runs.

| | Run | AGENT CONTEXT RETRIEVALS | `Context reads` |
|---|---|---|---|
| `main` @ `eb66ddc` | `sw-84af58f6` | no section | 0 |
| This branch | `sw-b8b2fd2c` | one panel per agent | 3 |

On the branch, each agent's `context_retrieval` row appears just before its note. The count
is one record per `before_acting()` call, so 3 here is three reads by the demo's three
agents, not a fixed number — check 5 below is where that is shown. Both transcripts are in
`test_evidence.md` and in the PR.

**2. No leak into what the next agent reads.** Run `sw-ce4f5ccd`:

```
shared subject episode types: ['architectural_decision', 'implementation_note', 'review_finding']
reads subject episode types : ['context_retrieval', 'context_retrieval', 'context_retrieval']
leak in assembled_context: False
```

The retrieval records are only in the `:reads` subject, and a later `get_context()` on the
shared subject does not return them.

**3. Four unit tests** (`tests/test_context_retrieval.py`, fake client, stdlib `unittest`,
no new dependency):

- `test_records_retrieval_in_reads_subject_without_compiling` — the episode goes to
  `<subject_id>:reads` with the retrieved memories mapped to the
  `{type, confidence, content}` shape the inspector reads, and that subject is never
  compiled.
- `test_summary_omits_deprecation_note_when_none_retrieved` — the row reads
  `Retrieved N memories`, and gains ` (incl. deprecation)` only when a deprecation is among
  the memories.
- `test_each_read_records_its_own_episode` — three `before_acting()` calls write three
  episodes, in call order, all to the `:reads` subject, including a repeat caller. This is
  check 5 below at unit level: the count follows reads, not distinct agents.
- `test_shows_retrievals_from_reads_subject` — the inspector renders rows merged in from the
  sibling subject.

```
.venv/bin/python -m unittest tests.test_context_retrieval -v
Ran 4 tests in 0.007s
OK
```

**Negative control.** A green suite proves nothing unless it goes red on a broken fix, so I
broke the change three ways, one at a time, and ran the tests after each: writing the
episode to the shared subject instead of `:reads` fails two tests, dropping the
` (incl. deprecation)` suffix fails one, and removing the merge in `timeline_inspector.py`
fails one. Restored, the suite is green again and `git diff` shows no source change.

**4. The repo's own checks.** The repo has no test suite, so its checks are what CI runs:
the dependency install and `py_compile` over every tracked `.py`
(`.github/workflows/ci.yml`). Both exit 0 at `8ad4b87`. CI's markdown link check runs as a
GitHub Action with no local command, so I left it to the PR; it is the one dated exclusion
in my `ship-manifest.md`.

**5. More than three reads.** Three agents each reading once leaves `Context reads : 3`
ambiguous: is the section counting agents or reads? Run `sw-4d84f50a` has four agents and
six `before_acting()` calls, with the Coder and Reviewer each acting twice in a review
round-trip:

```
retrieval records: 6
per agent: ['Planner', 'Architect', 'Coder', 'Reviewer', 'Coder', 'Reviewer']
  →  Agents active   : Architect, Coder, Planner, Reviewer
  →  Context reads   : 6
```

Six panels render, with the Coder and Reviewer each appearing twice at different
timestamps, so the section tracks reads rather than agents: a second read by the same agent
is a second row, which is the point — the Coder's two reads returned different context,
one before the review existed and one after `STATUS: NEEDS WORK` was published. The summary
counts three different things: `Agents active : 4` is distinct names, `Context reads : 6` is
`before_acting()` calls, and `Episodes written : 6` is decisions and notes published. The separation holds at that size too:
`leak in assembled_context: False`, and the shared subject still holds only the two
decisions, the two notes and the two review findings.

**Older runs still work.** The fixed inspector on `sw-f7b75257`, a run from before this
change with no `:reads` subject, renders as before and exits 0.

**What this does not cover.** Every row currently reads "Retrieved 0 memories" because of
smaramwbc/statewave#475, where the SDK returns memories under a key `before_acting()` does
not read. The row reports whatever `before_acting()` returned. The non-zero path is covered
by the unit tests, not by a live run, and the PR says so.

**Toolkit**

- Tool: `repro-check` for the before/after shape, and the `ship-manifest.md` rows the
  ship-gate runs before any ship.
- What it produced: two must-pass rows in fresh-shell form
  (`.venv/bin/pip install -q -r requirements.txt`, then the `py_compile` sweep), a dated
  exclusion for the link check, and a re-run of both on every gate attempt.
- Difficulties: my evidence kept going stale, and the gate blocked me three times for it:
  output captured at `5d688bf` when the branch was `b3c0f88`, a test count of three when a
  commit had dropped one to two, and a live transcript whose row text predated the change
  that made it match the README. None of those were the code being wrong.
- What changed: `test_evidence.md` is no longer written once. I regenerate it at the tip
  commit before any gate run, and every run id in it is one I can still look up on the
  server — which is how I confirmed `sw-f7b75257` and `sw-d2893eea` were real when the gate
  questioned them.

---

## Implementation Notes

**2026-10-24**

I made the branch `fix/485-record-context-retrievals` and started with what the issue
suggested: write the `context_retrieval` episode to the shared subject and just don't
compile after it. I wrote a small probe to test that first (`.repro-485/compile_probe_485.out`),
and it didn't work. The next `note()` compiled everything on the subject, and the Reviewer's
`get_context()` came back with the Coder's retrieval log as its top fact. So I moved the
write to a separate `<subject_id>:reads` subject that nothing ever compiles, with a
`reads_subject_id()` helper so the name only lives in one place. My first commit was
`5d688bf`: `context.py`, `timeline_inspector.py`, a README sample update, and three tests.
Later that night I made another commit (`b3c0f88`) that added the Planner to the README
sample and removed a test I thought was extra. After that, my evidence file still listed a
test that wasn't on the branch anymore.

**2026-10-25**

I posted my repro and the `:reads` change on #485, so the maintainer would know I was doing
something different from the issue before seeing the PR. Then I reset the branch to
`3ff3c0d` and rebuilt it as one commit without touching the README. I realized I was
changing the README to fit my output, when I should change my output to fit the README. So
I made the row text match the format the sample already uses (`Retrieved N memories`, plus
` (incl. deprecation)`), and the README step wasn't needed anymore. I wrote that down in
`plan.md` with the date. That gave me commit `ef06cad` with three files, and I opened PR #7
at 23:12.

**2026-10-26**

I ran everything again on the latest commit and redid the live runs the PR points to:
`sw-84af58f6` before and `sw-b8b2fd2c` after (`Context reads` went from 0 to 3), and
`sw-ce4f5ccd` to show the reads stay out of memory (`leak in assembled_context: False`). I
added a commit (`c1f5f19`) with tests for memories with no confidence and for one record per
read. Then I squashed it all into one commit with five tests, and amended it to `8ad4b87`,
where I moved the no-confidence check into the main test, so there are four. To make sure the
tests actually catch something, I broke the fix on purpose three ways: writing to the shared
subject fails two tests, removing the deprecation note fails one, and removing the inspector
merge fails one. I also did a run with six reads (`sw-4d84f50a`, where the Coder and Reviewer
each act twice) to show the count follows reads, not agents. I force-pushed, so the PR is now
`8ad4b87`.

**Toolkit**

- Tool: Claude Code on my branch, working from `plan.md`. I kept a dated list of changes to
  the plan at the bottom of it and checked each change against the plan before committing.
- What it produced: the three-file change in `8ad4b87` (+183/−2), the probe that showed the
  write had to go to `:reads`, and the dated note in `plan.md` about dropping the README step.
- Difficulties: I rebuilt the branch three times (`5d688bf` → `ef06cad` → `8ad4b87`), and
  every time, my evidence and descriptions still pointed at a commit that was gone. The
  README change also snuck in. I told myself it was keeping the docs up to date, but really I
  was changing the docs to match my output.
- What changed: now I write down a plan change the same day I make it. If my code and the
  docs disagree, I fix the code to match the docs first. After every rebuild I check that the
  test count and commit id are the same everywhere I mention them.

---

## Pull Request

**PR Link:** https://github.com/smaramwbc/statewave-multi-agent-shared-context/pull/7
(opened 2026-10-25 with one commit, `ef06cad`. The branch is now the single commit
`8ad4b87` "fix: record context retrievals so the timeline can show them".)

**PR Description:** The PR fixes statewave#485. `before_acting()` now writes a
`context_retrieval` episode after each read, with the row text in the README sample's format
(`Retrieved N memories`, plus `(incl. deprecation)` when a deprecation is among them), and
`timeline_inspector.py` merges those episodes into the timeline. It builds on the issue's
suggested fix but writes the record to a sibling subject, `<subject_id>:reads`, because on
the shared subject the next `note()` or `decide()` compiles it into memory, and in my check
it became the Reviewer's top retrieved fact. The description shows before/after inspector
output (`Context reads` 0 → 3), the check behind the sibling subject, the scope I left
alone (the README, #475, compile behaviour, the agents), four new unit tests with a negative
control, a six-read check showing the count follows reads rather than agents, and an
AI-assistance disclosure. The full text is in `pull-request-485.md` next to this file.

**Maintainer Feedback:**

- 2026-10-26: none yet.
- 2026-11-03: still no review, comment, or reaction on the PR or on #485 (8 days). That's
  normal for this repo: its four other outside PRs (#2–#5) have had no review in 17–29 days,
  and its last commit was 2026-07-28. My PR-monitor read it as QUIET and drafted a wait
  note, not a nudge: my playbook's threshold is 21 days, so the earliest nudge is 2026-11-15,
  on #485.

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate (`check_gate.py --branch`). It runs the two checks in my manifest, then
  my pr-precheck on my branch, plan, evidence, and PR description. My voice guard also checks
  the description when I run `gh pr create`.
- What it produced: I ran it eleven times (`gate-log.md`). It blocked me five times and passed
  six. The last pass was at 02:08 on 10-26, on `8ad4b87` with the real PR description, and
  all four checks passed: plan-fidelity, test-evidence, diff-quality, and standards-and-comms.
- Difficulties: my code never failed. Every block was because my evidence or description was
  out of date. The first time I had no description at all. Then it said three tests when the
  branch had two, it said my transcripts were on the issue thread when only my claim was
  there, and my output was from before my last commit. I also opened the PR on a pass from an
  older version of the branch, so I had to run the gate again on the real PR afterward.
- What changed: I remake `test_evidence.md` on the latest commit before every gate run, and I
  run the gate again after every amend or force-push, not just once before opening the PR.

---

## Learnings and Reflections

**Technical Skills Gained**

- **How Statewave compiles memory.** When it compiles a subject, it picks up every episode
  that hasn't been compiled yet, not just the newest one. So skipping the compile right after
  a write doesn't keep it out of memory, because the next `note()` compiles it anyway. I only
  found that out because I tested the issue's idea with a probe (`compile_probe_485.py`)
  before building it, and it's the reason my fix uses a separate `:reads` subject.
- **Finding a bug that doesn't throw an error.** The empty section never crashed anything,
  it just didn't show up. I found the cause by listing everything that calls `write_episode`
  and comparing it to the one episode type the inspector looks for. Nothing ever wrote it.
- **Testing without a test suite or an LLM.** The repo had no tests, so I wrote four using a
  fake client and Python's built-in `unittest`, so I didn't add any dependencies. Then I broke
  my fix on purpose three ways to make sure the tests actually fail when they should.
- **Running everything locally.** I ran the Statewave server and pgvector with
  `docker compose`, and switched the LLM model when the repo's default one was gone from Groq.
  I said so every time I reported a run.

**Challenges Overcome**

The hardest part wasn't the code. It was keeping my evidence accurate while the branch kept
changing. The ship-gate blocked me five times, and every time it was because my evidence or
PR description was talking about a commit I didn't have anymore (see my Unit 7 entry and the
Pull Request Toolkit block). I fixed it by remaking `test_evidence.md` on the latest commit
before every gate run. The second hard part was disagreeing with the issue's suggested fix
without being rude about it. I posted my probe output on #485 before opening the PR, gave the
change its own section in my plan and in the PR, and said I'd move it back to one subject if
the maintainer prefers that. The third was setup. The repo's default model gave
`model_not_found`, and with the model I switched to, the Planner and Coder didn't publish any
decisions. I said I'd changed the model, and I left that parsing problem alone since it's not
part of this bug.

**What I'd Do Differently Next Time**

First, I'd check how fast the code repo reviews PRs before I claim an issue, not after. The
issue is in `statewave`, where the maintainer merges in a day or two, but the code is in a
demo repo where no outside PR has ever been reviewed. Second, I'd figure out what my branch
should look like before writing any evidence. I rebuilt it three times (`5d688bf` →
`ef06cad` → `8ad4b87`), and each time my evidence went out of date. Third, I wouldn't open a
PR on an old gate pass. I'd run the gate again on exactly what I'm about to open.

---

## Resources Used

- [smaramwbc/statewave#485](https://github.com/smaramwbc/statewave/issues/485): the issue
  itself. It pointed me to `timeline_inspector.py` L107-108 and suggested a fix, which gave me
  a place to start. Testing that suggestion is how I found the compile problem.
- [smaramwbc/statewave#475](https://github.com/smaramwbc/statewave/issues/475): this explained
  why every row says "Retrieved 0 memories" (`before_acting()` reads a key the SDK never
  returns), so I knew that wasn't part of my bug.
- [statewave's CONTRIBUTING.md](https://github.com/smaramwbc/statewave/blob/main/CONTRIBUTING.md):
  I used it to write my `CLAUDE.local.md`, because the demo repo doesn't have its own.
- The demo repo's `.github/workflows/ci.yml`: where I got the two checks for my manifest.
- The demo repo's README sample timeline: I matched my row text to its format
  (`Retrieved N memories`, ` (incl. deprecation)`) instead of changing the README.

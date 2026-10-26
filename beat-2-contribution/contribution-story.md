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

2026-10-24: I installed the ship-gate, which runs my manifest's checks and then my own
pr-precheck before any `gh pr create` goes out. The install swapped pr-precheck to the
real-world scope and kept the old one as `scope.md.sandbox`. My manifest has two rows that
run, both mined from the repo's `.github/workflows/ci.yml`: the dependency install and the
`py_compile` check over every tracked `.py` file, written as `.venv/bin/pip` and
`.venv/bin/python` so they run in a cold shell instead of my activated one. I excluded CI's
markdown link check with the date and the reason: it runs as a GitHub Action
(`lycheeverse/lychee-action@v2`), there is no command the repo asks a contributor to run,
and `lychee` is not installed here. There is no test row in the first table because the repo
has no test suite of its own; the tests on my branch are mine, and I run them separately.

My first gate run stopped because I had no PR description at all. The second stopped
because the description I then wrote said the before/after transcripts were in the issue
thread and cited `main.py` runs, while my own `test_evidence.md` still said "Not yet run
through `main.py` (no LLM key)" and the thread had only my claim comment. The runs were
real: I checked my local Statewave server and `sw-f7b75257` and `sw-d2893eea` were both
still there, with three `context_retrieval` episodes in `sw-d2893eea:reads`. So the stale
thing was my evidence file, and I fixed it rather than the claim. The third run passed. Then
I added a commit that dropped a redundant test, and the next run stopped again: my evidence
still said three tests when the branch had two, and the thread still had no deviation note.
I posted the repro and the `:reads` deviation on #485 on 2026-10-25, then rebuilt the branch
as one commit, `ef06cad`, with three tests and no README change.

2026-10-25: I opened pull request #7 at 23:12. My gate had passed on 10-24 at 23:32, but on
an earlier shape of this branch: four files including a README change, before I rebuilt the
work as the single commit `ef06cad` with three tests and no README edit. So the pass I had
did not cover what I shipped, and I ran the gate again against the live PR body afterwards.
That retroactive run took two more blocks to get right: first my `test_evidence.md` was still captured at the old commits and named a
test that no longer exists, then its live output read `Retrieved 0 memories for: Build
auth…` while the shipped code writes `Retrieved N memories` with no task suffix, so the
output predated the tip. I re-ran all three checks at `ef06cad`, re-captured the live runs
the PR actually cites (`sw-84af58f6` before, `sw-b8b2fd2c` after, `Context reads` 0 to 3,
and `sw-ce4f5ccd` for the separation check with `leak in assembled_context: False`), and the
gate passed at 00:55 on 10-26, against the live PR body. That pass is in `guard-log.md`'s sibling,
`gate-log.md`, and so are the five blocks before it. What I changed because of all this: I
now re-run the manifest checks at HEAD before every gate run instead of trusting output
captured at an earlier commit, because every single block the gate gave me was my evidence
file describing a branch I no longer had.

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** https://github.com/smaramwbc/statewave-multi-agent-shared-context/pull/7
(opened 2026-10-26, one commit: `ef06cad` "fix: record context retrievals so the timeline
can show them")

**PR Description:** The PR fixes statewave#485. `before_acting()` now writes a
`context_retrieval` episode after each read, with the row text in the README sample's format
(`Retrieved N memories`, plus `(incl. deprecation)` when a deprecation is among them), and
`timeline_inspector.py` merges those episodes into the timeline. It builds on the issue's
suggested fix but writes the record to a sibling subject, `<subject_id>:reads`, because on
the shared subject the next `note()` or `decide()` compiles it into memory, and in my check
it became the Reviewer's top retrieved fact. The description shows before/after inspector
output (`Context reads` 0 → 3), the check behind the sibling subject, the scope I left
alone (the README, #475, compile behaviour, the agents), three new unit tests, and an
AI-assistance disclosure. The full text is in `pull-request-485.md` next to this file.

**Maintainer Feedback:**

- 2026-10-26: none yet.

**Status:** Awaiting review

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

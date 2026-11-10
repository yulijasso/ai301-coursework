# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Yuliana Jasso

## Featured Tools

I chose **issue-scout** because it helps me find GitHub issues that match my interests and skill level. When I ran it for real, I noticed that TypeScript issues were taking up all five results, and some repositories were brand new with 0 stars. I improved the search strategy and filtering, which increased the number of RAG-related issues from 0 to 4 out of 5. I eventually found issue #485 through issue-scout, which became my open-source contribution.

I chose **ship-gate and pr-precheck** because they work together to make sure my pull request is ready for submission. Ship-gate runs the required checks, while pr-precheck verifies that my PR description and evidence are accurate and up to date. On my real PR, I ran the gate 11 times, and it blocked me 5 times, even though my code passed every check. These failures helped me catch outdated evidence, incorrect test counts, and missing descriptions. Using both tools taught me to regenerate evidence after code changes and verify everything before submitting my PR.

I featured these tools because they had the biggest impact on my workflow and required improvements based on real use, while my other tools needed fewer changes.

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout is a tool I built to help me find GitHub issues that match my interests and skill level. It searches for potential first contributions, ranks them, and evaluates the top five using my rubric. I designed the search strategy, scope, and grading criteria to help me identify issues worth working on.

**How it evolved, dated:**

2026-10-11: I turned my Unit 1 issue-select skill into issue-scout and pointed its search strategy at retrieval and RAG work, with one TypeScript-only query to leave room for surprises. My first scan graded five issues and accepted all five, but none of them were about RAG, because the TypeScript query kept returning brand-new issues with zero comments and those took every slot. Two of the accepted repos had been created that same day with no stars and no releases, and my repo-in-use check still passed them, since all it needed was a few recent commits. I fixed the rubric so a repo without a recent release also needs at least 10 stars, and changed the ranking so each query takes turns filling the top five. On the second scan my RAG queries got four of the five slots, the new rule rejected two more tiny repos, and the patched rubric still scores 20/20 on the Unit 1 eval.

2026-10-18: The round-robin top five held one code task in a used repo (readprism#199). Going further down Q1 and Q2 found production-rag-assistant#147 and statewave#485, both real retrieval bugs. #485 is the issue I claimed. Scan 3 ran on the rubric from before the 2026-10-18 scope patch (`scope-fits-newcomer` became `scope-feasible`); the patched rubric scores 19/20 in `rubric-regression-run.txt`.

**Evidence:**

codercops/discord-bot and jeganxthan/aether were both created on 2026-10-11. Each had 0 stars and no release. They passed on the commits-only path ("3 of the last 5 commits within 90 days"). That proves the author was busy, not that anyone uses the software.

Before: scan 1, 2026-10-11, with the old rubric (both issues were accepted):

```
{"item": "https://github.com/codercops/discord-bot/issues/5", ...
  {"name": "repo-in-use", "grade": "pass", "evidence": "No release; 5 of last 5 commits dated 2026-10-11"},
  ... "verdict": "accept"}
{"item": "https://github.com/jeganxthan/aether/issues/1", ...
  {"name": "repo-in-use", "grade": "pass", "evidence": "No release; 5 of last 5 commits dated 2026-10-02 to 2026-10-11"},
  ... "verdict": "accept"}
```

After: scan 2, same day, with the 10-star rule (both issues were rejected):

```
{"item": "https://github.com/langchengit/leavy/issues/4", ...
  {"name": "repo-in-use", "grade": "fail", "evidence": "No release; commits recent but only 1 star (repo created 2026-10-11)"},
  ... "verdict": "reject"}
{"item": "https://github.com/aniruddhaadak80/skills/issues/261", ...
  {"name": "repo-in-use", "grade": "fail", "evidence": "No release; commits recent but only 2 stars"},
  ... "verdict": "reject"}
```

In scan 2, the patch rejected langchengit/leavy (1 star) and aniruddhaadak80/skills (2 stars).

Dated commit references:

1d33d35 (2026-10-11): added issue-scout to tools/.
3e5aa35 (2026-10-18): claimed statewave#485 and patched the scope check. The patched rubric still scores 19/20 in rubric-regression-run.txt.

**ship-gate**

**What it is, and the judgment hole I wrote:** The ship-gate (`check_gate.py --branch`) runs the two checks in my manifest, then my pr-precheck on my branch, plan, evidence, and PR description. My manifest runs two checks taken from the repo's CI, the dependency install and a `py_compile` sweep, written as `.venv/bin/...` so they work in a fresh shell; I excluded CI's lychee link check with a date and reason, since it only runs as a GitHub Action.

**How it evolved, dated:**

2026-10-24 to 2026-10-26: I ran it eleven times (`gate-log.md`). It blocked me five times and passed six. My code never failed. Every block was because my evidence or description was out of date. The first time I had no description at all. Then it said three tests when the branch had two, it said my transcripts were on the issue thread when only my claim was there, and my output was from before my last commit. I also opened the PR on a pass from an older version of the branch, so I had to run the gate again on the real PR afterward.

2026-10-26: I remake `test_evidence.md` on the latest commit before every gate run, and I run the gate again after every amend or force-push, not just once before opening the PR.

**Evidence:**

My evidence kept going stale: output captured at `5d688bf` when the branch was `b3c0f88`, a test count of three when a commit had dropped one to two. None of those were the code being wrong.

From `gate-log.md`, 2026-10-25 00:06:

```
- verdict: BLOCK (block)
  - test-evidence [fail]: Unit-test output was captured at 5d688bf (not in main..HEAD) and lists 3 tests, but the branch diff has only 2 after b3c0f88 dropped one; the required checks were not re-run at HEAD.
```

From `gate-log.md`, 2026-10-26 02:08:

```
- verdict: PASS
- package: head 8ad4b87638b793ddc0fe1378041bfe6811df47a1 ...
  - test-evidence [pass]: unittest 4 tests OK, pip install and py_compile exit 0, and live before/after runs show Context reads 0 -> 3 with the retrievals section appearing; lychee exclusion is disclosed with a reason.
```

The last pass was at 02:08 on 10-26, on `8ad4b87` with the real PR description, and all four checks passed: plan-fidelity, test-evidence, diff-quality, and standards-and-comms.

**pr-precheck**

**What it is, and the judgment hole I wrote:** pr-precheck grades my pull request before I open it. I wrote all four graded components — `SKILL.md`, `rubric.md`, `procedure.md`, and `references/evidence-guide.md` — against the five scoring categories named in the eval README before spending anything. The `test-evidence` check, as it currently reads:

> Pass if the evidence shows an observable result relevant to the issue and shows the required repository checks were run with visible outcomes. A bare claim such as "tests pass" is not enough. An honestly disclosed shortfall does not automatically fail unless the issue, plan, or required checks make that shortfall blocking.

**How it evolved, dated:**

Before 2026-10-04: Two phrasings got rejected on the way to this one. The first was "the evidence shows the issue's behavior fixed." It would have rejected `pkg-13` and `pkg-16`, both gold accepts. The second was "the repository's required checks pass." The check as written asks for the outcome to be *visible*, not green, so a disclosed pre-existing failure passes while a silent one does not. The first full run agreed on all 20 packages with every category matched, so no revision was ever applied.

2026-10-04: `standards-and-comms` failed because the draft had no PR title, and the commit subject `fix(retriever): ...` used a scope outside CONTRIBUTING's list (`ingestion`, `rag`, `agent`, `safety`, `api`, `frontend`). The commit was reworded to `fix(rag): ...` with the code unchanged, and the title `fix(rag): guard KeywordSearcher.index against an empty corpus` was added to the draft.

2026-10-24 to 2026-10-26: When I ran ship-gate on my real PR, I completed 11 runs, with 5 blocks and 6 passes. My code passed the manifest checks every time, including pip install and py_compile. All five blocks came from pr-precheck, which caught issues with my PR description and evidence. These included a missing PR description, incorrect test counts, claims about transcripts that weren't actually posted, and outdated output from earlier commits. I also learned that after making changes to my branch, I needed to regenerate my evidence and rerun the gate against the latest commit. My final run passed all four checks: plan-fidelity, test-evidence, diff-quality, and standards-and-comms. This experience taught me that having working code isn't enough; I also need accurate documentation and up-to-date evidence before submitting a PR.


**Evidence:**

The first code block shows pr-precheck passing in my sandbox after I updated my commit message to `fix(rag):` and added a title. The second shows pr-precheck catching a missing PR description on my real PR #7. Together, they show how the same tool worked in practice, first passing in the sandbox and then catching an actual mistake in my contribution.

From `beat-1-sandbox/unit-4/precheck-run.md`, the accepting run on 2026-10-04 after the reword:

```
{"name": "standards-and-comms", "grade": "pass",
 "evidence": "Title and commit subject 'fix(rag): guard KeywordSearcher.index against an empty corpus' use an allowed scope; all six template sections filled, 'Closes #68', AI-use disclosure present."}
```

From `gate-log.md`, 2026-10-24 23:20, its first catch on my real PR:

```
  - standards-and-comms [fail]: Draft PR description is absent ('no description supplied'), so there is no motivation/approach/tradeoffs, no AI-use disclosure, and no report of the plan deviation, which scope.md requires in the description and the issue thread.
```

## Inventory

- **issue-select:** My skill confirmed the things I can check from outside: the repo is alive, the work is bounded and maintainer-filed, nobody has claimed it, and the contribution policy says nothing that blocks an AI-assisted workflow. What it could not weigh is anything about me.
- **repro-check:** I ran `repro-check` in live mode, with the wild scope that replaced its unit-2 sandbox scope, on my claim comment and then on the full repro package before I posted it. I rewrote the report around pasted transcripts instead of narration.
- **plan-check:** I ran `plan-check` in live mode on `plan.md` and the plan comment, with the wild scope that replaced its unit-3 sandbox scope. It pushed me to make the root cause point at specific lines rather than at a file.
- **voice-guard:** The voice-guard stopped my first claim for statewave#485 because it promised a timeline. I removed that sentence, and the revised claim passed.
- **repo memory (`CLAUDE.local.md`):** I wrote a 51-line `CLAUDE.local.md` using statewave's CONTRIBUTING.md and one scoped look at the files my issue touches. I removed the `@AGENTS.md` line, because this repo's AGENTS.md isn't contributor guidance.
- **PR-monitor:** My playbook says no nudge before 21 days, only one ever, and it goes on #485 instead of the PR. The one thing it can't do is read #485, where my nudge would go, so I'll check that thread myself before 11-15.

## The Arc

**Beat 1**
Date: 2026-10-11
Friction: My first scan graded five issues and accepted all five, but none of them were about RAG, because the TypeScript query kept returning brand-new issues with zero comments and those took every slot.
Change: I changed the ranking so each query takes turns filling the top five.
Result: On the second scan my RAG queries got four of the five slots.

**Beat 2**
Date: 2026-10-11
Friction: Two of the accepted repos had been created that same day with no stars and no releases, and my repo-in-use check still passed them, since all it needed was a few recent commits.
Change: I fixed the rubric so a repo without a recent release also needs at least 10 stars.
Result: On the second scan the new rule rejected two more tiny repos, and the patched rubric still scores 20/20 on the Unit 1 eval.

**Beat 3**
Date: 2026-10-18
Friction: The voice-guard stopped my first claim for statewave#485 because it promised a timeline ("I'm aiming to have it up within the next week"), which breaks my own rule against posting a date or ETA.
Change: I removed that sentence. I posted it from the browser, which the guard can't watch, so I ran the guard by hand on the exact text first.
Result: The revised claim passed, and both the stop and the pass are in `guard-log.md`.

**Beat 4**
Date: 2026-10-26
Friction: The code passed every gate run, but the gate blocked my branch five times, and every block was my evidence or description describing a branch I no longer had: no description, a test count that no longer matched, transcripts I said were in the issue thread when they weren't, and live output captured before my last commit.
Change: I now regenerate `test_evidence.md` at HEAD before every gate run and re-gate after every amend or force-push.
Result: I re-gated against the live PR body afterwards, and it passed at `8ad4b87` on 10-26.

**Beat 5**
Date: 2026-11-03
Friction: The monitor showed me that GitHub has no CI checks on my PR, but my nudge rule said I'd tell the maintainer "the checks still pass."
Change: I changed it to say my checks pass locally.
Result: I did not post a follow-up nudge because the PR-monitor determined that November 15 was the earliest appropriate date to follow up. Although I did not send a message, the tool helped me avoid following up too early and gave me a clear date for my next action.

## Limitations and What's Next

One limitation of my toolkit is that it can only evaluate the information it receives. For example, issue-scout initially returned repositories that were brand new with 0 stars, and ship-gate could pass an older version of my branch without knowing I would make more changes later. If I could improve one thing next, I would update issue-scout to evaluate more than five issues when the initial results are weak and make sure it checks the repository where the code actually lives. This would help me find more reliable contribution opportunities.

**Tool limits.**

issue-scout: the top-five limit hid #485; the tracker repo and the code repo differ, so the responsiveness sample read the wrong repo.
ship-gate: One limitation of ship-gate is that it only checks my work when I run it. It cannot prevent me from opening a PR using an outdated pass. I experienced this when I opened PR #7 based on an earlier gate result and had to rerun the checks. In the future, I would improve it by requiring a fresh gate pass that matches the latest commit before submitting a PR.
pr-precheck: a PR that discloses a large gap can still pass as long as the plan recorded the deferral.

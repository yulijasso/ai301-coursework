# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68

**Verdict output**

Live-mode run of the installed `issue-select` skill on 2026-09-15, graded against
#68, #69 and #60; pasted verbatim below. #68 is the chosen issue.

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
**Ranked read-out — 3 candidates, all in scope (`codepath/pathreview-ai301-fa26-s1`), Path Review house rule noted (classmate claim comments don't block; none exist on any of the three).**

Accepted, in fit order:

1. **#68** — `ZeroDivisionError` in `KeywordSearcher.search()` on an empty index. Fit: BM25 keyword search in `rag/retriever/` is the retrieval half of hybrid retrieval, the thing your profile names first.
2. **#60** — `TypeError` in the faithfulness checker when a chunk has `text: None`. Fit: RAG evaluation, adjacent to retrieval quality.
3. **#69** — `AttributeError` when the parser gets a top-level JSON array. Fit: generation-side, furthest from retrieval.

Rejected: none.

Per-check grades, identical across all three (same repo, same day, same shape):

| Check | Grade | Evidence |
|---|---|---|
| `repo-alive` | pass | `isArchived: false`; newest default-branch commit 2026-08-24, 22 days ago |
| `repo-in-use` | pass | No releases published; all 5 most recent commits (2026-08-18 → 08-24) within 90 days |
| `scope-fits-newcomer` | pass | Single bounded bug, maintainer-filed (`Aburke225`, COLLABORATOR), names the two files to touch |
| `unclaimed` | pass | `assignees: none`, no linked PRs, 0 comments |
| `ai-policy-allows` | pass | `docs/CONTRIBUTING.md` states nothing on AI tooling; no `AI_POLICY.md`; no disclosure box in the PR template — silence passes |
| `maintainer-responsive` (preferred) | unclear | No issue in the repo has a single comment, so no first-response latency exists to measure |
| `newcomer-signposted` (preferred) | pass | `good first issue` + `tier-1` labels; body names relevant files and effort estimate |

```json
[
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
   "checks": [
     {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-08-24 (22 days before 2026-09-15)"},
     {"name": "repo-in-use", "grade": "pass", "evidence": "no releases published; all 5 latest commits (2026-08-18..2026-08-24) within 90 days"},
     {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "maintainer-filed bounded bug naming rag/retriever/keyword_search.py and its xfail test; no disqualifier applies"},
     {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no linked PRs; 0 comments"},
     {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has no statement on AI tooling; no AI policy file; silence passes"},
     {"name": "maintainer-responsive", "grade": "unclear", "evidence": "no issue in the repo has any comment, so no first-response latency exists"},
     {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels 'good first issue', 'tier-1'; body names the two files and a 2-4 hour estimate"}
   ],
   "verdict": "accept"},
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
   "checks": [
     {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-08-24"},
     {"name": "repo-in-use", "grade": "pass", "evidence": "no releases; all 5 latest commits within 90 days"},
     {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "maintainer-filed bug with runnable repro and named test test_none_context_chunk_text"},
     {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no linked PRs; 0 comments"},
     {"name": "ai-policy-allows", "grade": "pass", "evidence": "no AI statement in docs/CONTRIBUTING.md or PR template"},
     {"name": "maintainer-responsive", "grade": "unclear", "evidence": "no commented issues in the repo to sample"},
     {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels 'good first issue', 'tier-1'; body names file and failing test"}
   ],
   "verdict": "accept"},
  {"item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
   "checks": [
     {"name": "repo-alive", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-08-24"},
     {"name": "repo-in-use", "grade": "pass", "evidence": "no releases; all 5 latest commits within 90 days"},
     {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "maintainer-filed bounded bug naming rag/generator/output_parser.py and its xfail test"},
     {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no linked PRs; 0 comments"},
     {"name": "ai-policy-allows", "grade": "pass", "evidence": "no AI statement in docs/CONTRIBUTING.md or PR template"},
     {"name": "maintainer-responsive", "grade": "unclear", "evidence": "no commented issues in the repo to sample"},
     {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels 'good first issue', 'tier-1'; body names the two files and a 2-4 hour estimate"}
   ],
   "verdict": "accept"}
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

One run. The rubric was drafted against the 20 bundles before the first run, so the
first full run was also the confirming one:

`agreement: 20/20 scored items  (bar: 18/20: PASS)`

`categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4`

That is the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-15` (zulip/zulip#19589). My rubric's decision: **reject**. Gold label:
**reject**, noted as "years of design debate and two abandoned PRs behind a friendly
label."

The check that produced the reject was `scope-fits-newcomer`, on the stalled-history
disqualifier. The run's evidence line reads:

> opened 2021-08-18 (>24 months open); 2 linked PRs (#20840, #23123) both closed and
> not noted as merged, plus 10+ distinct claimants over the thread with nothing merged
> — stalled-history disqualifier

This is the issue that forced that disqualifier to exist. It looks friendly on every
surface a newcomer checks first: `good first issue` and `help wanted` labels, an active
repo (`repo-alive` and `repo-in-use` both passed), and a clear one-paragraph
description. What sinks it is only visible in the history — five years open, two PRs
that died, and a long chain of `@zulipbot claim` comments followed by
auto-unassignments. I had to write the disqualifier as counts (>24 months AND either 2+
closed-unmerged linked PRs or 3+ dropped claimants) rather than as "looks stalled,"
because `issue-09` is also old, also labeled `good first issue`, and also has a closed
PR behind it — but it is gold **accept**. One abandoned attempt is normal; two or more
plus a crowd of dropped claimants is the repo telling you the issue is harder than its
label.

**Check rationale**

The `unclaimed` check, quoted as currently written:

> No assignee is set, AND no linked PR (including one from a fork) is in the `open`
> state, AND no claim comment in the thread is dated within 180 days of the capture
> date. Closed or merged linked PRs are abandoned or superseded attempts, not claims; a
> claim older than 180 days with no open PR behind it is stale and does not block,
> especially when a maintainer has since invited takers.

The two halves of that condition come from opposite directions in the eval set. The
strict half — assignee or any open linked PR is a blocking claim — is what rejects
`issue-08` (assignee set plus open PR), `issue-13` (two open PRs racing hours after the
issue opened) and `issue-18` (open PRs plus a stack of claim comments). The forgiving
half exists because of `issue-09`, which is gold accept and yet carries both a claim
comment and a linked PR: the claim is from 2022 and the PR is closed. Without a
staleness window, the same check that correctly rejects four issues would have wrongly
rejected that one. 180 days is my line for how long a silent claim keeps an issue
reserved.

**Trade-offs**

Two things, one I chose and one the run showed me.

The case I accept it will miss: someone who claimed an issue eight months ago and is
still quietly working on it, without an open PR to show for it. My check calls that
claim stale and reports the issue as free, so I would start work and collide with them.
I took that trade knowingly — `issue-09` proves the opposite default (any claim ever
blocks) is worse, and a claim with nothing behind it after six months is much more often
abandoned than active.

The one the run showed me: on `issue-15`, `unclaimed` came back `unclear`, not `fail`.
The evidence line reads "no assignee and no open linked PR, but only 40 of 97 comments
shown, so a claim within 180 days of the 2026-08-05 capture date cannot be ruled out."
My verdict rule counts `unclear` on a required check as a fail, so the issue was
rejected anyway — and `scope-fits-newcomer` had already failed it outright, so the
verdict never depended on the ambiguity. But it shows the 180-day window needs the whole
thread to be readable, and a truncated thread quietly converts into a reject. On a long
live thread I should read the tail myself rather than trust the window.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

**1. The issue's fit to your interests and to the time available.**

Issue #68 fits me because I want to get better at retrieval-augmented generation, and this
bug sits in the retrieval half of it. `KeywordSearcher.search()` raises a `ZeroDivisionError`
inside rank-bm25's IDF computation when the index was built from an empty corpus, so the fix
is in `rag/retriever/keyword_search.py` and its test in `tests/unit/test_keyword_search.py`.
I have used embeddings and vector stores like ChromaDB, pgvector and Pinecone, but mostly on
the dense-retrieval side, so a BM25 bug is a good way to learn the sparse half of hybrid
retrieval that I want to understand better. The issue is estimated at 2–4 hours and the fix
is one guard plus removing an `xfail` marker, which is realistic alongside my other
coursework this week.

**2. What the verdict identified correctly, and what you weighed that the rubric could not.**

My skill confirmed the things I can check from outside: the repo is alive (newest commit 22
days old, not archived), the work is bounded and maintainer-filed with the two files named,
nobody has claimed it (no assignee, no linked PRs, 0 comments), and the contribution policy
says nothing that blocks an AI-assisted workflow. What it could not weigh is anything about
me. It doesn't know that I am comfortable in Python but have not used rank-bm25 before, or
that I will need to read how pytest's `xfail` markers work before removing one. It also
can't judge how much time I actually have this week, or that I wanted a retrieval issue
specifically rather than the other two candidates it accepted, #60 and #69, which it ranked
below this one only because my fit profile puts retrieval first.

**3. The anticipated difficulty in claiming it.**

The main risk is that it is an obvious pick. #68 is labeled `good first issue` and `tier-1`
and names its own files, so classmates are likely to choose it too. The Path Review house
rule says shared issues are fine and that credit attaches to the pull request I open, so I
plan to claim it anyway in Unit 2 even if someone else has commented first. The other thing
I noticed is that `maintainer-responsive` came back `unclear`: no issue in the whole repo has
a single comment, so there is no response history to go by. That means I can't count on a
fast reply if I get stuck or need my claim acknowledged, and I should reproduce the bug and
start work rather than wait on confirmation.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

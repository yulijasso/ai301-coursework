# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/89

Opened 2026-10-05 from my fork `yulijasso/pathreview-ai301-fa26-s1` against
`codepath/pathreview-ai301-fa26-s1`, fixing issue #68. Two files, +5/−4. All six CI jobs
pass on the PR: lint, typecheck, test-unit, test-integration, eval, frontend.

**Branch**

`fix/68-empty-corpus-guard`

Type prefix `fix`, issue number `68` — the issue this pull request closes — and a short
description. Head commit `79b6a16`, off base `f89c06f`.

**pr-precheck verdict on my draft**

Live mode, run from the fork clone against the issue, `beat-1-sandbox/unit-3/plan.md` with
its Deviations section, the branch diff (`git diff main...HEAD`), `pr-draft.md`, and the
repo's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. Four runs: the first
rejected, the next three accepted. The full transcript is in `precheck-run.md` in this
directory.

1. **reject** — `standards-and-comms` failed: the draft had no PR title, and the commit
   subject `fix(retriever): ...` used a scope outside CONTRIBUTING's list (`ingestion`,
   `rag`, `agent`, `safety`, `api`, `frontend`). The other three checks passed.
2. **accept** — the commit was reworded to `fix(rag): ...` with the code unchanged, and the
   title was added to the draft.
3. **accept** — re-graded after the AI-use disclosure was shortened; every required section
   still had real content.
4. **accept** — re-graded after the PR description was updated to record the CI outcome (all
   six jobs green, per-job block with workflow links, typecheck note rewritten from a local
   failure to green-in-CI). `test-evidence` now rests on visible CI outcomes rather than a
   disclosed local failure, and CONTRIBUTING's "CI must be green" requirement is satisfied in
   fact.

The accepting run, verbatim:

````
All four required checks pass.

- **plan-fidelity:** the diff changes exactly the two files in plan section 3 and does what
  section 4 describes. The Deviations section records that the code held to the plan.
- **test-evidence:** observable before/after for `index([])`, a byte-identical one-chunk
  control, the unit test going from `16 passed, 1 xfailed` to `17 passed`, the full suite at
  `376 passed, 52 xfailed`, and a negative control. The pre-existing mypy failure is shown on
  unmodified `f89c06f` and disclosed, as CONTRIBUTING directs.
- **diff-quality:** 2 files, +5/−4, with no unrelated hunks or debris.
- **standards-and-comms:** all six template sections are filled, `Closes #68` is present, the
  AI-use disclosure is present, and the branch name and commit/title scope follow CONTRIBUTING.

Voice guide: no violations found.

Notes (they don't change the verdict): lint is shown only as a ticked box with no pasted
output. The local branch must be force-pushed to the fork before opening the PR, since the
fork still holds the earlier `fix(retriever)` commit.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68 (draft PR from fix/68-empty-corpus-guard @ 79b6a16)",
  "checks": [
    {"name": "plan-fidelity", "grade": "pass",
     "evidence": "Diff touches only keyword_search.py (guard: bm25=None, log keyword_index_empty, return) and removes the test_empty_index xfail, exactly plan sections 3-4; Deviations note says the code held to plan."},
    {"name": "test-evidence", "grade": "pass",
     "evidence": "Before ZeroDivisionError traceback, after '[]' exit=0, byte-identical one-chunk control, 16 passed+1 xfailed -> 17 passed, make test-unit 376 passed; pre-existing mypy stub failure shown on f89c06f and disclosed as CONTRIBUTING directs."},
    {"name": "diff-quality", "grade": "pass",
     "evidence": "2 files, +5/-4; no unrelated hunks, debug output, or formatting churn."},
    {"name": "standards-and-comms", "grade": "pass",
     "evidence": "Title and commit subject 'fix(rag): guard KeywordSearcher.index against an empty corpus' use an allowed scope; all six template sections filled, 'Closes #68', AI-use disclosure present."}
  ],
  "verdict": "accept"
}
```
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

One run. I wrote all four graded components — `SKILL.md`, `rubric.md`, `procedure.md`, and
`references/evidence-guide.md` — against the five scoring categories named in the eval README
before spending anything, so the first full run was also the confirming one:

`agreement: 20/20 scored items  (bar: 18/20: PASS)`

`categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`

That is the agreement line in the committed `eval-run.txt`, whose header fingerprints the
same files I uploaded to `tools/pr-precheck/`: `rubric.md sha256:989c6876120ac40c`,
`procedure.md sha256:d2e12dc5aea0d041`, `SKILL.md sha256:dbee30c0f5d912f1`, and
`evidence-guide.md sha256:941a59199417d728`. No `--only` runs were needed: nothing
disagreed, so there was no package to re-grade and no loosened check that would have called
for a canary.

**Package analysis**

`pkg-13` (neovim/neovim#41337). My rubric's decision: **accept**. Gold label: **accept**,
noted as "honestly disclosed shortfall: caret-escapes cmd metacharacters with before/after
evidence; `%VAR%` expansion explicitly deferred in the plan's note AND restated in the
description; arguable on the deferral, ready as scoped."

This is the package my `test-evidence` check was written for. The PR fixes the `&` splitting
by caret-escaping cmd.exe metacharacters, shows a before/after transcript, and then says
outright that percent-sign expansion is not covered — a URL like `?q=%PATH%` still expands —
pointing at the deferral the plan had already recorded. So the PR demonstrably does less than
the whole issue, and says so in both the plan and the description.

A check that reads "the evidence must show the issue fixed" rejects that, because the issue
is not fully fixed. My check instead asks whether the evidence shows an observable result
relevant to the issue and whether the required repository checks ran with visible outcomes,
and then carries an explicit non-disqualifier: "An honestly disclosed shortfall does not
automatically fail unless the issue, plan, or required checks make that shortfall blocking."
Under that reading `pkg-13` passes on the strength of the disclosure rather than in spite of
the gap. `pkg-16` is the same shape — an image-load path that fails loudly, with the
remaining case disclosed — and both are gold accepts, so writing the check the obvious way
would have cost two of the seven `clear-accept` packages and dropped the run to 18/20.

The clause is not a blanket pass. `pkg-10` discloses nothing and offers "verified working on
my machine for a full day" with the plan's delayed-connect before/after never run, and
`pkg-14`'s evidence exercises a GET with header casing — the path the diff does not change —
while the issue's single-header POST repro is never re-run. Both fail the first half of the
same condition, because neither shows an observable result relevant to the issue.

**Check rationale**

The `test-evidence` check, quoted as it currently reads:

> Read the submitted test evidence against the plan's test plan, the issue's expected
> observable behavior, and any repository checks the plan or repo requires. | Pass if the
> evidence shows an observable result relevant to the issue and shows the required repository
> checks were run with visible outcomes. A bare claim such as "tests pass" is not enough. An
> honestly disclosed shortfall does not automatically fail unless the issue, plan, or
> required checks make that shortfall blocking.

Two phrasings got rejected on the way to this one.

The first was "the evidence shows the issue's behavior fixed." That is the natural way to
write a test check, and it fails the honest-outcome rule this course has taught in each of
the last three units — the Unit 2 evidenced cannot-reproduce, the Unit 3 recorded deviation,
and now the disclosed shortfall. It would have rejected `pkg-13` and `pkg-16`, both gold
accepts.

The second was "the repository's required checks pass." That reads as rigour and is wrong in
the other direction: it makes a tool that cannot distinguish a failure caused by the change
from a failure that predates it. My own PR is the case in point. `make typecheck` failed in
my environment because the repo pins mypy to Python 3.11 while numpy 2.5.3's stubs need
3.12, a failure identical on unmodified `f89c06f`. The check as written asks for the outcome
to be *visible*, not green, so a disclosed pre-existing failure passes while a silent one
does not.

**Trade-offs**

What the disclosure clause gives up is the size of the shortfall. The condition asks whether
a shortfall is blocking "unless the issue, plan, or required checks make that shortfall
blocking," which means a PR that discloses a large gap can still pass as long as the plan
recorded the deferral. `pkg-13`'s own gold note calls the deferral "arguable," and I agree it
is: a maintainer could reasonably hold that PR for covering only half of a two-part parsing
bug. My check accepts it, and I accept the consequence — I would rather read an honest half
than a confident whole.

Nothing changed elsewhere, and here is how I know: the first full run agreed on all 20
packages with every category matched, so no revision was ever applied — no check was
loosened, no canary was needed, and no `--only` re-grade was run. The clause's cost is
visible inside that run rather than behind it: it is what separates `pkg-13` and `pkg-16`,
which pass with gaps they name, from `pkg-10` and `pkg-14`, which fail because their evidence
never exercises the path the issue reports.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.

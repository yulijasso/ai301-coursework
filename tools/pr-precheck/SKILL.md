---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
ready to submit?

A PR package is the implementation on the candidate branch, its draft
PR title and description, its test evidence, and the plan it claims to
implement, read against the issue that plan belongs to. The plan
includes any recorded deviation notes.

Treat the pull request as an argument a maintainer must be able to
judge without the student in the room. The title says what changed and
where, the description explains why the change should be believed, the
diff shows exactly what changed, and the test evidence shows the
observable result.

Do not decide from instinct or general code-review preference. Execute
`procedure.md`, apply the checks and verdict rule in `rubric.md`, and
gather each evidence family according to
`references/evidence-guide.md`.

## The question

Answer one question only:

**Is this PR package ready to submit?**

Judge whether the candidate implementation and the maintainer-facing
PR package are ready to be opened as a pull request for the issue and
plan they claim to implement.

Do not turn this tool into issue selection, reproduction grading, plan
grading, general refactoring advice, or an unrestricted code review.
Grade only the readiness question defined by the rubric.

## Inputs and modes

There are two modes.

**Live mode**

Grade the student's current work from the repository working copy.
Read:

- `plan.md`, including every recorded deviation note;
- the branch diff relative to the repository's default branch;
- the draft PR title;
- the draft PR description;
- the student's test evidence;
- the issue the plan belongs to.

The branch diff is everything the candidate branch changes relative to
the repository's default branch. From the working copy, obtain it with:

`git diff main...HEAD`

Use the three-dot diff. Treat every changed file and hunk shown there
as part of the candidate implementation being submitted.

Gather live issue and repository evidence only where
`references/evidence-guide.md` directs you to look.

For a house-chain student, read the house-chain artifacts supplied for
that workflow in place of student-owned upstream artifacts where the
course setup requires it. Grade what those artifacts contain. Do not
invent missing evidence from unrelated files or assumptions about what
the student probably intended.

**Eval mode**

The supplied bundle is the whole world.

Use only evidence contained in that bundle. Do not fetch GitHub,
inspect another working copy, search for missing repository facts, or
supplement the package with outside evidence.

Run every rubric check and apply the full verdict rule. Eval mode does
not perform a partial review.

## The scope seam (live mode only)

Before gathering live package evidence, read `scope.md` in this skill
directory.

Use its repository boundary and house rules when deciding what live
issue and repository evidence is allowed and how that evidence should
be interpreted.

Refuse to grade a package whose issue or repository falls outside the
configured scope.

If the repository line in `scope.md` still contains an unfilled
placeholder, stop without grading. Tell the student to obtain their
cohort's completed `scope.md` from the instructor. Never guess,
substitute, or infer the intended repository.

In eval mode, ignore `scope.md` entirely. The eval bundle defines the
grading boundary.

## The voice seam (live mode only)

In live mode, read `voice-guide.md`.

Apply it only to maintainer-facing outgoing PR text: the draft PR title
and draft PR description.

If either breaks a voice-guide rule, report the broken rule in the
readable summary and name or quote the rule that was violated.

Do not allow a voice-guide violation to change the verdict by itself.
It affects a check only when `rubric.md` explicitly makes that evidence
part of the check.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read `rubric.md`. It defines the checks that must be graded and the
verdict rule that combines those grades into `accept` or `reject`.

Use `references/evidence-guide.md` as the evidence map. It identifies
where each evidence family lives, including the issue, plan and
deviation notes, branch diff, PR title and description, test evidence,
and repository standards where applicable.

Then execute `procedure.md` exactly as written. The procedure controls
the order of work, how evidence is gathered, how each rubric check is
executed, and how the check grades are assembled into the verdict.

Do not silently invent a missing procedural step. If the procedure
does not say how to perform a step required to grade the package,
report the procedure gap in the readable summary rather than
improvising around it.

If `rubric.md` contains no checks, stop without grading and say that
the skill cannot run without a populated rubric.

If `procedure.md` contains no executable steps, stop without grading
and say that the skill cannot run without a populated procedure.

A rubric and a procedure are both required. Do not guess a verdict
when either is absent.

## Verdict and output

The verdict space is binary:

`accept` means the PR package is ready to submit.

`reject` means hold the PR; it is not ready to submit.

Before the JSON result, you may provide a short readable summary of
the checks, any procedure gaps, and any live-mode voice-guide findings.

Every completed grading response must end with the following fenced
JSON block. It must be valid JSON and must be the final content in the
reply, with nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
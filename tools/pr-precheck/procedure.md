# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the issue first. Record the problem the PR is supposed to
   solve and the expected observable behavior.

2. Read `plan.md` before opening the diff. Record:
   - the files or areas the plan says will change;
   - the intended behavior change;
   - the plan's test plan;
   - any stated boundaries or things the plan says it will not change;
   - every recorded deviation note and its reason.

3. Read the full branch diff next. In live mode, use the three-dot diff
   against the default branch as defined by the frame. Record:
   - every changed file;
   - the meaningful changes in each file;
   - any extra hunks outside the plan's stated scope;
   - any planned change that appears missing;
   - any debug output, dead code, format churn, generated noise, or
     unrelated work.

4. Read the submitted test evidence after the diff. Record:
   - what command or action was run;
   - the visible outcome;
   - the before/after behavior when provided;
   - whether the evidence demonstrates the behavior the issue and plan
     expect;
   - the outcome of any repository checks required by the plan or repo.

5. Read the draft PR title and description after the plan, diff, and
   evidence so their claims can be checked against facts already
   gathered. Record:
   - what the title claims changed and where;
   - what the description claims was implemented;
   - any stated deviation or shortfall;
   - any testing claims;
   - any claims that contradict the diff or test evidence.

6. Read the repository standards and template asks named by the
   evidence guide. Record:
   - required PR template sections;
   - required disclosure sections;
   - contribution or testing requirements relevant to submission;
   - whether the draft PR satisfies each stated ask.

Keep this order so the diff is read against the plan rather than
judged in isolation, and the PR description is checked against the
implementation rather than accepted at face value.

## Evidence gathering

### Plan fidelity

1. From `plan.md`, make a list of the files, behaviors, and boundaries
   the plan names.
2. Add every recorded deviation note to that list as an allowed change
   only when the note clearly says what changed from the plan.
3. From the diff, make a list of every changed file and meaningful
   hunk.
4. Compare the two lists:
   - mark each diff change as planned, covered by a deviation, or
     unaccounted for;
   - mark each planned change as present or missing.
5. From the PR description, record any claim that the implementation
   matches the plan and any deviation the description discloses.
6. Record any contradiction between the description and the actual
   diff.

### Test evidence

1. From the plan, record the behavior the test plan says must be
   demonstrated.
2. From the issue, record the expected observable result when the plan
   depends on issue-side behavior.
3. From the submitted evidence, record the exact visible outcome rather
   than only the student's conclusion.
4. Record whether the evidence demonstrates the planned behavior.
5. Record the outcome of each repository check required by the plan or
   repository standards.
6. If the package only says something like "tests pass" without showing
   an observable result or required check outcome, record that the
   evidence is only a claim.

### Diff quality

1. Use the full diff, not selected hunks.
2. Record any unrelated file changes.
3. Record debug prints, commented-out experiments, dead code,
   accidental formatting churn, generated noise, or other debris.
4. Decide whether those changes materially make the intended fix harder
   to isolate and review.
5. Do not count a meaningful change as debris merely because it was not
   in the original plan; plan scope is graded under `plan-fidelity`.

### Standards and communications

1. From the repo-facts block or live repository instructions, list each
   PR template, disclosure, or submission requirement that applies.
2. Compare the draft title and description against those requirements.
3. Record whether each required section has real content rather than a
   placeholder or omission.
4. Compare the title and description against the diff:
   - verify that the title truthfully identifies the change;
   - verify that the description does not hide or contradict meaningful
     implementation differences.
5. Compare testing claims in the description against the submitted test
   evidence.
6. In live mode, record voice-guide violations separately from rubric
   evidence unless the rubric explicitly uses them.

## Check execution

Run the rubric checks in this order:

1. `plan-fidelity`
2. `test-evidence`
3. `diff-quality`
4. `standards-and-comms`

For each check:

1. Use only the evidence gathered for that check and the pass condition
   written in `rubric.md`.
2. Assign `pass` when the gathered evidence satisfies the pass
   condition.
3. Assign `fail` when the gathered evidence shows the pass condition
   is not satisfied.
4. Assign `unclear` when the check depends on evidence that should be
   present in the package but cannot be verified from the available
   material.
5. Write one evidence line naming the concrete fact or quote that
   decided the grade.

Do not change a grade because another check already failed. Grade every
check independently so the output describes the whole package.

Do not reread the entire package for each check when the evidence was
already gathered during the read-order stage. Reopen a source only when
the recorded evidence is insufficient to apply that check's pass
condition.

When evidence is genuinely absent, do not invent or infer it. Grade the
check `unclear` unless the rubric's pass condition makes that absence
itself a direct failure.

Do not use one check to punish the same fact for a different reason.
For example:
- an extra implementation hunk belongs to `plan-fidelity`;
- that same hunk belongs to `diff-quality` only if it also creates
  reviewability noise;
- missing test proof belongs to `test-evidence`;
- a false testing claim in the description can also matter to
  `standards-and-comms`.

## Verdict assembly

1. Collect the grades for all rubric checks in rubric order.

2. Apply the verdict rule from `rubric.md` exactly:
   - `accept` only if every required check passes;
   - `reject` if any required check fails;
   - treat `unclear` as `fail`;
   - preferred checks, if any are added later, do not change the
     verdict.

3. If the verdict is `reject`, identify the deciding check as the first
   required check in rubric order whose grade is `fail` or `unclear`.

4. If more than one required check fails, keep all failures in the
   output, but use the first failing required check in rubric order as
   the deciding check for the readable summary.

5. Quote or restate the single concrete evidence fact that caused that
   deciding check to fail. Do not replace it with a general statement
   such as "the PR is not ready."

6. If the verdict is `accept`, state that all required checks passed and
   use the per-check evidence lines to show why.

7. Emit the final JSON exactly as required by `SKILL.md`, preserving the
   rubric check names and grades. The JSON block must be valid and must
   be the final content in the reply.

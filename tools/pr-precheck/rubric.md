# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | Read the branch diff against the plan's stated scope, intended changes, and any recorded deviation notes. Also read the draft PR description against the diff for claims about plan fidelity or implementation scope. | Pass if the meaningful changes in the diff are covered by the plan or by recorded deviation notes, and the description does not claim fidelity that the diff contradicts. An honestly documented deviation can still pass. Fail if the diff silently does more or less than the plan, or if the description hides or misstates a meaningful deviation. | required |
| test-evidence | Read the submitted test evidence against the plan's test plan, the issue's expected observable behavior, and any repository checks the plan or repo requires. | Pass if the evidence shows an observable result relevant to the issue and shows the required repository checks were run with visible outcomes. A bare claim such as "tests pass" is not enough. An honestly disclosed shortfall does not automatically fail unless the issue, plan, or required checks make that shortfall blocking. | required |
| diff-quality | Read the full branch diff for unrelated hunks, debug output, dead code, accidental formatting churn, generated noise, or other debris that obscures the intended change. | Pass if the intended change is easy to isolate and review from the diff without unrelated or accidental changes burying it. Fail if meaningful unrelated work or debris materially obscures the fix or forces the reviewer to separate the real change from avoidable noise. | required |
| standards-and-comms | Read the repo-facts block or repository standards, including PR template asks and disclosure requirements, then compare them against the draft PR title and description. Also read the title and description against the diff so their claims can be verified. | Pass if the PR satisfies the repository's stated submission requirements and truthfully communicates what changed and why. Required template or disclosure asks must contain real content rather than being skipped, left as placeholders, or contradicted by the diff. | required |

## Verdict rule

Accept if every required check passes.

Reject if any required check fails.

Treat `unclear` as `fail`: if the package does not provide enough evidence to verify a required check, the pull request is not ready to submit.

Preferred checks, if added later, never change the verdict.
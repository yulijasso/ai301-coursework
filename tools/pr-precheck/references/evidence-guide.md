# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives**

In eval mode:
- Read the plan-context block for the plan's stated scope, intended
  files or areas, boundaries, test plan, and any recorded deviation
  notes.
- Read the candidate PR's unified diff for every changed file and
  meaningful hunk.
- Read the candidate PR description for claims about what was
  implemented, what stayed in scope, and any disclosed deviations.

In live mode:
- Read `plan.md`, including all deviation notes.
- Read the branch diff against the default branch using
  `git diff main...HEAD`.
- Read the draft PR title and description.

**What good looks like**

Every meaningful change in the diff falls inside the plan's stated
scope or is covered by a recorded deviation note, and the PR
description truthfully reflects what the diff actually contains.

Silent drift appears when the diff does more than the plan without a
recorded deviation, does less than the plan without honestly
disclosing the shortfall, or when the description claims fidelity that
the diff contradicts.

## Test evidence (harness category: not-tested)

**Where it lives**

In eval mode:
- Read the plan-context block's test plan.
- Read the reproduction evidence when the package includes it, so the
  expected failing and fixed behavior can be compared.
- Read the candidate PR's test-evidence section for commands, outputs,
  before/after behavior, and repository-check results.
- Read the repo-facts block for any required test, lint, build, or
  other validation commands.

In live mode:
- Read the test plan in `plan.md`.
- Read the student's captured test output or other submitted proof.
- Read any required repository checks named by the repo's contribution
  instructions, PR template, or plan.

**What good looks like**

The evidence shows an observable behavior tied to the issue or plan,
states or makes clear the expected-after result, and shows the outcome
of required repository checks.

A statement such as "tests pass" without observable output, behavior,
or required check results is not decisive evidence.

## Diff quality (harness category: unreviewable)

**Where it lives**

In eval mode:
- Read the candidate PR's unified diff in full.
- Read the commit list when it helps identify unrelated or accidental
  work included in the package.

In live mode:
- Read the full branch diff from `git diff main...HEAD`.
- Read the branch's commits when needed to understand whether unrelated
  work has been carried into the PR.

Look specifically for:
- unrelated file changes;
- debug prints or logging left behind;
- dead code;
- commented-out experiments;
- accidental formatting churn;
- generated or mechanical noise;
- drive-by edits unrelated to the issue.

**What good looks like**

The intended fix is easy to see in the diff, and unrelated or
accidental changes do not materially obscure it.

A diff is unreviewable when debris or unrelated hunks bury the actual
change and force the reviewer to spend time separating the fix from
noise.

## Standards and comms (harness category: standards-wall)

**Where it lives**

In eval mode:
- Read the repo-facts block for PR template sections, contributing
  instructions, repository policies, testing asks, disclosure asks,
  and any explicit maintainer direction.
- Read the candidate PR title and description to see whether those asks
  are actually honored.

In live mode:
- Read the repository's PR template.
- Read `CONTRIBUTING.md` or equivalent contribution instructions.
- Read any stated repository policy relevant to submitting the PR,
  including AI-use disclosure requirements.
- Read maintainer instructions on the issue or thread when the
  evidence guide or rubric makes them relevant.
- Read the draft PR title and description.

**What good looks like**

Every applicable repository ask is addressed with real content: the
required template sections are completed, required disclosures are
present and meaningful, and explicit maintainer directions are not
ignored.

Boilerplate, untouched placeholders, missing required sections, or a
visibly ignored repository ask are standards-wall failures.

Whether the PR description's claims match the diff belongs under
plan fidelity above, not this family.

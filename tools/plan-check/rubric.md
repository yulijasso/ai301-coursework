# Rubric: is this plan ready to post and build from?

All judgments below read the plan and comment against the issue and the
reproduction evidence that plan builds on. Grade the plan, never the
write-up's shape: a six-line plan can be ready and a long sectioned one
can be unbuildable.

## Terms used below

- **Repro evidence** — the artifacts (output excerpts, logs, measured
  numbers) in the reproduction that this plan builds on, as distinct
  from anything the plan asserts about them.
- **The break** — the point the repro evidence localizes the failure to.
- **Diagnosis** — the plan's stated cause: what it says is wrong, not
  where it intends to edit.
- **Expected-after** — the result the plan says the test will produce
  once the change is in, stated concretely enough to check.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `bounded-scope` | The plan's in-scope and not-in-scope statements and the files or areas it names, read against the diagnosis and the issue. | The plan is one bounded change a reviewer could hold the diff to: a reader can say of any given file whether it is in or out. Fails if any of: (a) it changes files or areas the diagnosis does not implicate; (b) it bundles a rename, reformat, refactor, docs pass, or config migration the bug does not require — the "while I'm here" family; (c) it asks for open-ended work with no endpoint ("improve error handling throughout"); (d) the boundary cannot be determined at all — nothing named as in scope and nothing excluded. Two things are explicitly NOT failures: **more than one file is not creep when the diagnosis implicates each one** (a fix plus the test that covers it is one change), and **a plan that deliberately does less than the whole issue and says so is bounded, not incomplete** — a stated deferral is a pass, and only an unstated one is a gap. | required |
| `diagnosis-grounded` | The plan's stated cause, read against what the repro evidence actually shows — the repro-evidence block in eval mode, the student's posted repro comment live. | The stated cause explains the behavior the repro evidence shows, and nothing in that evidence contradicts it. Fails if any of: (a) the cause rests on a condition the repro evidence rules out — a plan blaming a stale cache where the repro says it ran with the cache disabled and the failure persisted; (b) no cause is stated at all, only an intent to fix or a place to edit; (c) the cause is asserted at a layer the repro evidence never reached, so no artifact could confirm or deny it; (d) the planned change acts downstream of where the evidence localizes the break — suppressing the symptom rather than the cause — and the plan does not say why the downstream fix is the right one. A maintainer asking for the narrower fix, or a stated reason the upstream change is out of reach, satisfies (d). Not disqualifying: a one-sentence cause, or a cause the plan marks provisional, when the evidence supports it. | required |
| `executable-by-a-stranger` | The plan's named files or areas, its approach, and its order of work. | A stranger holding the repo could begin the first step without asking the author anything. Fails if any of: (a) no file, function, or area is named; (b) the approach is given only as an outcome ("make it handle empty input", "fix the rounding") with no mechanism for getting there; (c) a step turns on a decision the plan leaves open without saying how or by whom it gets settled; (d) a step depends on something the reader cannot obtain — a private branch, an unshared config. Not disqualifying: no line numbers, no diff, no prose around the steps. Terseness is not the failure; unresolvability is. | required |
| `test-decisive` | The plan's test plan, read against the repro evidence's own steps and artifacts. | The test plan names something someone else could run, and states the expected-after concretely enough to check without the author. Fails if any of: (a) the success condition is not observable — "see if it works", "verify behavior is correct", "make sure nothing breaks"; (b) no command, test name, or runnable step is named; (c) no expected-after is stated, or the stated one restates the bug as the desired outcome; (d) the named run does not exercise the trigger the repro evidence used, so passing it would not show this bug fixed. Strongest form, not required: a today/expect pair quoting the repro's own numbers. | required |
| `comment-faithful` | The candidate plan comment, read against three things: the plan it represents, the maintainer and reporter signals in the thread, and the repo-facts block's stated conventions and contribution policy. | The comment promises only what the plan contains and engages what the thread already said. Fails if any of: (a) it promises work the plan does not contain, or gives a delivery date or a guaranteed fix; (b) it ignores a constraint a maintainer already stated in the thread — proposing a new flag where a maintainer asked to keep the current API; (c) it is boilerplate: it would read identically on any other issue, or it asks to be assigned with no cause, change, or proof named; (d) the repo's stated policy asks that AI use be disclosed in issue comments and neither the comment nor the plan discloses the tool and the extent of its help. A policy that is silent, that permits AI without asking for disclosure, or that scopes disclosure to pull requests only, does not trigger (d). Not disqualifying: brevity — three lines naming cause, change, and proof is a pass. | required |
| `risks-named` | The plan's stated risks or unknowns, read against the change it proposes. | The plan names at least one concrete consequence or unknown that follows from this specific change — callers that depended on the old behavior, a case the fix does not cover. Generic hedging ("there may be bugs", "I might need to adjust") does not satisfy it, and a plan resting on a guess it presents as settled fails. | preferred |
| `deviation-recorded` | The plan's deviation note, when the package is a re-run after a build. | Where the build departed from the posted plan, the plan records what changed and why, not only the new approach. Not applicable — and not a fail — on a package graded before any build. | preferred |

## Verdict rule

Accept — ready to post and build from — only if every `required` check
passes. A fail on any one of them is a reject: the plan is held, not
posted.

`unclear` on a required check counts as a fail. A plan whose cause,
boundary, executability, test, or comment I cannot verify from the
package itself is not a plan a maintainer can say yes to, and not one
I should start building from.

`preferred` checks never change the verdict. Report their grades; they
say how much stronger a plan is than the minimum it had to clear.

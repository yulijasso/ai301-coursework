# Procedure: how this skill grades a plan package

Follow these steps as written. Where a step does not cover the case in
front of you, say so in the summary rather than inventing a step.

## Read order

Read the whole package before grading anything. The order matters
because three of the five checks read the plan *against* something
else, and whichever you read first becomes the story you measure the
other against. The repro evidence is the baseline, so it goes first.

1. **Repro evidence.** Read it before the plan. Record two things: the
   trigger it used (the exact command, input, or condition), and the
   failure it actually showed (the error text, the number, the
   observable symptom). Record them as the package's own words, not as
   a summary — these get quoted later. Also record where the evidence
   localizes the break, and anything the evidence explicitly rules out
   ("ran with the cache disabled; page 4 still empty"), because a
   ruled-out condition is what `diagnosis-grounded` clause (a) tests.
2. **Issue and thread.** Record what the reporter asked for, and every
   constraint a maintainer stated — an API to keep, a flag not to add,
   a preferred approach. Record each as a quote. These are what
   `comment-faithful` clause (b) is graded against.
3. **Repo facts.** Record the contribution policy and any AI-use
   disclosure requirement, and any stated convention or template the
   repo asks contributors to follow. Do this before reading the
   comment, so the policy is known before the comment is judged.
4. **The plan.** Read it whole, once, before grading. Record: its
   stated cause; the files or areas it names; what it says is in scope
   and what it excludes or defers; its approach; its test plan and
   expected-after; its risks.
5. **The plan comment.** Read it last, against the plan and the thread
   you have already recorded.

## Evidence gathering

For each family, pull the fact from the location named, and record it
as a quotable line. `references/evidence-guide.md` gives the full map;
these are the gathering moves.

- **Diagnosis and grounding.** Take the plan's cause from its own
  diagnosis line, not from its approach — what it says is wrong, not
  where it intends to edit. Set it beside the two lines recorded in
  read-order step 1 (the failure shown, and anything ruled out). If the
  plan names no cause, record "no cause stated" rather than inferring
  one from the approach.
- **Scope.** Take the in-scope and not-in-scope statements and the list
  of files or areas. Then test the boundary: pick one file the plan
  touches and ask whether the recorded diagnosis implicates it. Pick
  one file it does not touch and ask whether a reader could tell it is
  out. If the plan defers part of the issue, record the deferral as
  stated or unstated — that distinction decides the check.
- **Executability.** Take the approach and order of work. Then run the
  stranger test concretely: name the first step, and ask what the
  reader would have to ask the author before starting it. If the answer
  is "nothing", record that; if it is a question, record the question.
- **Test plan.** Take the command or test named and the expected-after.
  Set them beside the trigger recorded in read-order step 1 and check
  they exercise the same thing.
- **Honesty.** Take the stated risks and unknowns. Separate a
  consequence of this change from generic hedging, and record which it
  is. On a re-run after a build, take the deviation note and record
  whether it says what changed *and* why.
- **Comms.** Take the comment and set it beside three recorded things:
  the plan, the maintainer constraints from step 2, and the policy from
  step 3. Record, for each, whether the comment engages it.

## Check execution

1. Grade all five required checks on every package. Do not stop early
   on a fail: the output reports every check, and a package that fails
   two checks is different feedback from one that fails one.
2. Grade in this order, which is also the output order:
   `bounded-scope`, `diagnosis-grounded`, `executable-by-a-stranger`,
   `test-decisive`, `comment-faithful`, then the preferred checks
   `risks-named` and `deviation-recorded`. Fixed order makes two runs
   on the same package comparable line by line.
3. Run each check against the evidence already recorded above. Do not
   re-read the whole package for a check; if the recorded evidence does
   not decide it, go back to that one family's location and nowhere
   else.
4. Apply the rubric's pass condition literally. Where it lists lettered
   clauses, test each clause in turn and stop at the first that holds —
   that clause is the check's reason. Where it names something as
   explicitly not disqualifying, honor that before failing the check.
5. When the evidence a check names is genuinely absent from the
   package, grade `unclear` and say what was missing. `unclear` is not
   for a judgment that is hard; it is for evidence that is not there.
   Never substitute another part of the package for the evidence the
   check names.
6. Grade the plan, not the polish. A check never reads section count,
   length, headings, or formatting.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every `required`
   check passes; any required fail is a reject. `unclear` on a required
   check enters as a fail. Preferred checks are reported and never
   counted.
2. Name the deciding check. On a reject, it is the first required check
   that failed in the fixed order above; on an accept, there is none,
   and the summary says so.
3. Quote the submission's own lines in every evidence field. One line
   each, in the package's words rather than a paraphrase:
   - A **pass** quotes the thing that satisfied the condition —
     `"one change, limits stated"`, `"expected-after stated"`.
   - A **fail** quotes both sides, so the contradiction is visible
     without opening the package: the plan's claim and the evidence
     that defeats it, e.g. `plan: "the cache returns a stale page
     total" / repro: "ran with the cache disabled; page 4 still
     empty"`.
   - An **unclear** names what was absent, not what was hard.
4. Emit the summary (a line per check, plus voice-guide notes in live
   mode), then the fenced JSON block from SKILL.md, and nothing after
   it. The same grades must always produce the same verdict.

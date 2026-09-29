# Evidence guide: where evidence lives in a plan package

The rubric names what to decide and `procedure.md` names when to gather
it; this file says where each family lives and what good looks like
when you find it.

**The package's six surfaces.** In an eval bundle: `## Issue` (title,
body, labels, opener), `## Thread highlights` (reporter and maintainer
comments, carrying the constraints a plan has to respect), `## Repo
facts` (the repo line, stated conventions and templates, and the
contribution policy including any AI-use requirement), `## Repro
evidence` (the artifacts the plan builds on), `## Candidate plan`, and
`## Candidate plan comment`. In live mode: the issue page and its
thread, `CONTRIBUTING.md` in the repo root or `.github/` plus any
`AI_POLICY.md` it links, the student's own posted repro comment from
week 2, and the draft `plan.md` and draft comment as the candidate side.

Read the repro evidence before the plan. It is the baseline the
diagnosis has to survive, and reading the plan first makes its story
feel like the evidence.

## Diagnosis and grounding

**Where it lives.** The plan's diagnosis line — the one saying what is
wrong, distinct from the approach line saying where it will edit. The
behavior it must explain lives in the repro evidence's artifacts: the
error text, the measured number, the observed symptom, and any
condition the reproduction explicitly removed or held fixed.

**What good looks like.** The stated cause accounts for the behavior
the artifacts actually show, and no line of the evidence contradicts
it. "Floor-divide plus one makes a ghost page" is grounded when the
repro shows 4 pages where 3 were expected for 6 items at size 2: the
mechanism named produces exactly the number shown. The failure to watch
for is a cause resting on a condition the reproduction ruled out — a
plan blaming a stale cache when the repro says it ran with the cache
disabled and the page was still empty. That is not a weak diagnosis; it
is one the package's own evidence already answered. The second failure
is quieter: a diagnosis that is fine but whose change acts downstream
of the break, painting over the symptom where the evidence points
further up the chain. Walking upstream stage by stage from where the
repro fails is how you tell which one you are holding.

## Scope

**Where it lives.** The plan's in-scope statement, its not-in-scope or
deferral line, and the list of files or areas it names. Read against
the diagnosis (which files does the stated cause actually implicate?)
and the issue (how much did it ask for?).

**What good looks like.** A reader can take any file in the repo and
say whether it is in or out. Two files is bounded when the diagnosis
implicates both — a fix plus the test that covers it is one change, not
two. What sinks a plan is the "while I'm here" family: a rename, a
config migration, a docs pass, a reformat that the bug does not
require. Maintainers reject those even when the code is good, because
the boundary is what a reviewer holds the diff to. The case that looks
like a failure and is not: a plan that deliberately solves less than
the whole issue and says which part it is deferring. Stating the
deferral is what makes it bounded; only an unstated one is a gap.

## Executability

**Where it lives.** The plan's named files, functions, or areas, its
approach, and its order of work.

**What good looks like.** A stranger holding the repo could begin the
first step without asking the author anything. "Ceil-divide; drop the
+1, in `pager.py`" is executable: the file is named and the mechanism
is given. "Make the pagination handle the edge case" is not — it names
an outcome and leaves the reader to invent the mechanism. Terseness is
not the problem; four lines with no prose can be perfectly executable.
The failures are the unresolvable ones: no file or area named at all, a
step depending on a decision the plan leaves open without saying who
settles it, or a step reaching for something the reader cannot obtain.
Line numbers and a draft diff strengthen a plan and are never required.

## Test plan

**Where it lives.** The plan's test-plan part, read against the repro
evidence's steps and artifacts — the same command, the same input, the
same number.

**What good looks like.** Something someone else can run, and a stated
expected-after they can check without the author.
`run demo --items 6 --size 2 / today 4 pages / expect 3 pages` is
decisive: the command is runnable, the before is the repro's own
number, and the after is a number that is either produced or not. "See
if it works", "verify behavior is correct", "make sure nothing breaks"
are not test plans — nobody but the author can score them. Watch also
for a test that runs something real but not the reported thing: a suite
invocation with no named test, or a run that exercises a different
input than the trigger the repro used, so passing it would not show
this bug fixed. Writing the expected output down before touching code
is what makes the test decisive rather than a retrospective story.

## Honesty

**Where it lives.** The plan's risks or unknowns, and — on a package
re-graded after building — its deviation note.

**What good looks like.** At least one named consequence that follows
from this particular change: callers that counted the ghost page, a
case the fix deliberately does not cover, a version where the behavior
may differ. Generic hedging is the tell that nothing was actually
weighed — "there may be bugs", "I might need to adjust as I go" — and
so is its opposite, a plan asserting an outcome it cannot know ("this
will fix it, no side effects") with nothing behind the claim. A plan
that rests on a guess and presents it as settled is the failure this
family exists to catch. For deviations, an honest note says what
changed *and* why; a note recording only the new approach leaves the
reader unable to tell a discovery from a drift.

## Comms

**Where it lives.** The candidate plan comment, read against three
things: the plan it represents, the maintainer and reporter signals in
the thread highlights (or the live thread), and the repo-facts
contribution policy, conventions, and templates.

**What good looks like.** The comment says what was found, what will be
done, and how it will be proved — and each of those is already in the
plan behind it. It engages what the maintainer already said: if a
maintainer asked to keep the current API and add no new flags, a
thread-aware comment says the fix stays inside the current API, and a
comment proposing a new flag has ignored the room. Boilerplate is the
other tell — a comment that would read identically on any other issue,
or "Hi, I can fix this, please assign me", which promises everything
and contains nothing. Brevity is not a failure: three lines naming
cause, change, and proof is a complete comment. On AI policy, read what
the policy covers before judging the comment. Silent — no stated policy
— needs no disclosure. Permissive, or scoped to pull requests only,
needs none either when the package is an issue comment. A policy asking
that AI use be disclosed in comments needs the tool and the extent of
its help named, and no strength of plan substitutes for it.

# Contribution: timeline_inspector's context-retrieval section is always empty - nothing writes context_retrieval episodes

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Yuliana Jasso
**GitHub Username:** yulijasso
**Issue:** https://github.com/smaramwbc/statewave/issues/485
**Pull Request:** not opened yet

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: built issue-scout and fixed what my first real scan broke**

2026-10-11: I turned my Unit 1 issue-select skill into issue-scout and pointed its search
strategy at retrieval and RAG work, with one TypeScript-only query to leave room for surprises.
My first scan graded five issues and accepted all five, but none of them were about RAG,
because the TypeScript query kept returning brand-new issues with zero comments and those took
every slot. Two of the accepted repos had been created that same day with no stars and no
releases, and my repo-in-use check still passed them, since all it needed was a few recent
commits. I fixed the rubric so a repo without a recent release also needs at least 10 stars,
and changed the ranking so each query takes turns filling the top five. On the second scan my
RAG queries got four of the five slots, the new rule rejected two more tiny repos, and the
patched rubric still scores 20/20 on the Unit 1 eval.

**Unit 6: the voice-guard stopped my claim once, and the repo memory dropped the AGENTS.md import**

2026-10-18: The voice-guard stopped my first claim for statewave#485 because it promised a
timeline ("I'm aiming to have it up within the next week"), which breaks my own rule against
posting a date or ETA. I removed that sentence, and the revised claim passed. I posted it from
the browser, which the guard can't watch, so I ran the guard by hand on the exact text first;
both the stop and the pass are in `guard-log.md`.

For the repo memory, I wrote a 51-line `CLAUDE.local.md` using statewave's CONTRIBUTING.md and
one scoped look at the files my issue touches. One change from the template: I removed the
`@AGENTS.md` line, because this repo's AGENTS.md isn't contributor guidance. It's an
auto-generated note telling AI tools to use a Statewave server I don't have set up. The scoped
look also warned that my fix could accidentally save retrieval logs as memories, and I
confirmed that while reproducing the bug.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

On 2026-10-18 I ran a fresh scan with my scout. Out of 306 issues, it graded the top five and
accepted two: a page of interview questions to write, and a small Makefile task. Neither was
the kind of retrieval code I wanted to work on, so I kept going down the list and graded five
more. That's where I found statewave#485. Statewave is a memory system for AI agents, and this
demo shows several agents sharing one memory. Its timeline tool has a section meant to show
what each agent retrieved before acting, but that section is always empty, because nothing in
the code ever records a retrieval. My scout accepted it, with every required check passing.

I chose it because it's a real bug I can see happen and then see fixed, the issue already
suggests a fix, and it sits right in the retrieval side of an AI memory system, which is
what I want to get better at. I'm hoping to learn how a system like this turns what agents
write into memories and hands the right ones back when an agent asks.

My scout didn't handle this search perfectly. It only grades five issues, and #485 wasn't one
of them, so I had to go past its limit to find the best fit. It also checked the wrong repo:
the issue is filed in the main `statewave` repo, where the maintainer responds quickly, but the
code lives in a separate repo where four PRs from other contributors are still waiting for
review. I only noticed that after I had claimed it, so I'm expecting the review to take a while.
I wrote both problems down in `scan-notes.md`. Next time, I'd have the scout check the repo
where the code actually lives, and grade more than five issues when the first five don't
include much real code work.

**Claim comment:** https://github.com/smaramwbc/statewave/issues/485#issuecomment-6248332834 (posted 2026-10-18)

**Toolkit**

- Tool: issue-scout in live scan mode with my iteration-2 strategy and rubric, then the same
  rubric on five more candidates from further down the same ranking.
- What it produced: scan 3 in `tools/issue-scout/scan-output.md`. Six of ten graded issues
  were accepted. #485 passed every required check, with `maintainer-responsive` failing (the
  only replies in the sample came from other contributors).
- Difficulties: the top-five limit hid #485; the tracker repo and the code repo differ, so the
  responsiveness sample read the wrong repo; Q3 returned nothing again.
- What changed: logged as scan-notes entries 8 to 11, not patched yet. Scan 3 ran on the
  rubric from before the 2026-10-18 scope patch (`scope-fits-newcomer` became
  `scope-feasible`); the patched rubric scores 19/20 in `rubric-regression-run.txt`.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

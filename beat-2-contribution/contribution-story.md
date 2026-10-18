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

2026-10-18: My first claim draft for statewave#485 ended with "I'm aiming to have it up within
the next week", and the guard stopped it on my own never-post rule: "A date, an ETA, or a
guarantee that a fix will land." I cut the sentence, rewrote the claim to point at the lines I
had read, and the final wording passed (both checks are in `guard-log.md`). I posted from the
browser, so the hook never saw the post itself; the manual pass on that exact text is the
guarded check. For the repo memory I wrote a 51-line `CLAUDE.local.md` for
statewave-multi-agent-shared-context from statewave's CONTRIBUTING.md (the example repo has
none) and one scoped orientation run. I deleted the template's `@AGENTS.md` import, because
this repo's AGENTS.md is auto-generated instructions to call a Statewave MCP server I don't
have, not contributor conventions. The orientation also flagged that a retrieval episode could
get compiled into memory, which I confirmed during reproduction and recorded in the file.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I ran a fresh scan on 2026-10-18 with the round-robin strategy from Unit 5. The four queries
returned 306 issues, the filters cut that to 108, and the top five went Q1, Q2, Q4, Q1, Q2. The
scout accepted only two of them, a docs Q&A page and a Makefile task, and the 10-star floor
rejected the other three. Neither accepted issue was the retrieval code I said I wanted, so I
went further down the Q1 and Q2 rankings and graded five more. That found
smaramwbc/statewave#485, which the scout accepted with every required check passing: the
"context retrieval" section of a multi-agent memory demo is always empty because nothing ever
writes the episodes it reads. I picked it over the other accepted issues because it is a real
bug with a clear before and after, the issue suggests a fix, and it sits in the retrieval path
of an agent memory runtime, which is close to the RAG work I want to learn. I hope to learn how
Statewave compiles episodes into memories and serves them back as context.

The scout's weak spots were real. The five-candidate limit hid the best fit, since #485 was
never in the top five. It also graded the wrong repo: #485 is filed in `statewave`, where an
outsider's PR was merged in a day, but the code lives in `statewave-multi-agent-shared-context`,
where four outsider PRs opened between Oct 5 and Oct 17 have no maintainer review yet. I only
saw that after claiming, so I'm going in expecting a slow review. Both are logged in
`scan-notes.md` (entries 8 and 10). The fix I'd make is to sample responsiveness in the repo
that holds the named files, and to grade past five when the top five has fewer than two code
tasks.

**Claim comment:** https://github.com/smaramwbc/statewave/issues/485#issuecomment-6248332834 (posted 2026-10-18)

**Toolkit**

- Tool: issue-scout in live scan mode with my iteration-2 strategy and rubric, then the same
  rubric on five more candidates from further down the same ranking.
- What it produced: scan 3 in `tools/issue-scout/scan-output.md`. Six of ten graded issues
  were accepted. #485 passed every required check, with `maintainer-responsive` failing (the
  only replies in the sample came from other contributors).
- Difficulties: the top-five limit hid #485; the tracker repo and the code repo differ, so the
  responsiveness sample read the wrong repo; Q3 returned nothing again.
- What changed: logged as scan-notes entries 8 to 11. Not patched yet, so the Unit 1
  regression run still matches the committed rubric.

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

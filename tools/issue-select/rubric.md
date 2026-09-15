# Rubric: is this a good first issue?

All date thresholds are measured against the bundle's capture date in eval
mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-alive` | The repo line (`archived:`) and the "last 5 default-branch commits" list in the repo-facts block; on github.com, the archived banner and the commit list on the repo front page. | `archived: no` AND the newest commit in that list is dated within 90 days of the capture date. Commits authored by a bot count: a bot merging a human's pull request is maintainer activity. | required |
| `repo-in-use` | The "latest release" and "last 5 default-branch commits" lines in the repo-facts block; on github.com, the Releases box and the commit list. | The latest release is dated within 12 months of the capture date, OR — when no release is published, or the latest one is older than that — at least 3 of the last 5 default-branch commits are dated within 90 days of the capture date. Ongoing shipping substitutes for tagged releases; a repo with neither is not in use. | required |
| `scope-fits-newcomer` | The issue title, body, labels, opener's `author_association`, open date, the comment thread, and the `linked PRs:` line. | Passes unless ANY of these four disqualifiers holds: (1) **umbrella** — the body lists other issue numbers or sub-items meant to be split into separate pull requests, or asks for open-ended incremental work with no endpoint ("PRs welcome big and small", "megaissue", "add X across the codebase"). A multi-part change with a stated endpoint, confined to one area and deliverable in one pull request, is NOT an umbrella. (2) **unendorsed feature** — the issue requests a new feature or product change (not a bug fix or a docs fix) AND no maintainer has endorsed the requested behavior: the opener is not OWNER/MEMBER/COLLABORATOR, no maintainer comment approves it, and it carries no maintainer-applied `good first issue` / `help wanted` label. (3) **stalled history** — the issue has been open more than 24 months AND either at least 2 linked PRs are closed-unmerged, or 3 or more distinct people claimed it in the thread and nothing was merged. (4) **support request** — the issue asks how to use the software rather than asking for a change. A terse body, a bare acceptance-criteria checklist, or a bug report without reproduction steps is not a disqualifier on its own: grade the size of the work asked for, not the polish of the writeup. | required |
| `unclaimed` | The `this issue: assignees:` and `linked PRs:` lines in the repo-facts block, plus every claim in the comment thread ("I'll take this", "can I work on this", "@bot claim"); on github.com, the Assignees and Development boxes and the thread. | No assignee is set, AND no linked PR (including one from a fork) is in the `open` state, AND no claim comment in the thread is dated within 180 days of the capture date. Closed or merged linked PRs are abandoned or superseded attempts, not claims; a claim older than 180 days with no open PR behind it is stale and does not block, especially when a maintainer has since invited takers. | required |
| `ai-policy-allows` | The "contribution policy" line in the repo-facts block; on github.com, `CONTRIBUTING.md` in the root or `.github/`, the docs it links out to, any `AI_POLICY.md`, and PR-template disclosure checkboxes. | The policy does not ban AI-assisted contributions. An outright refusal ("we do not accept AI-generated code or documentation") fails. Conditions — disclose, personally understand, test, human-review before submitting — pass; they are terms to follow. Silence passes. | required |
| `maintainer-responsive` | The "maintainer first-response sample" in the repo-facts block. | At least one issue in the sample got a first owner/member/collaborator comment within 14 days. | preferred |
| `newcomer-signposted` | The issue's labels and body. | The issue carries a `good first issue`, `help wanted`, or `documentation` label, OR the body names the files, functions, or acceptance criteria to work against. | preferred |

## Verdict rule

Accept only if every `required` check passes; a fail on any one of them
rejects the issue. `unclear` on a required check counts as a fail — a
first issue whose liveness, scope, claim state, or contribution policy I
cannot verify is not one I should take.

`preferred` checks never change the verdict. Report their grades, and use
them to rank the issues that were accepted: among accepted candidates,
prefer the one that passes more preferred checks.

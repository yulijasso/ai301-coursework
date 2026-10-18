# Scan notes: where the wild surprised my scout

One entry for each moment of friction: what happened, which file it points at (strategy or
rubric), and what I did about it. The full read-outs are in `scan-output.md`.

## 2026-10-11: scan 1

**1. The TypeScript query took all five slots.** *(strategy: ranking)*
- **What happened:** filter 5 ordered every survivor by `commentsCount` ascending, then by
  `updatedAt` descending. Q4 is my TypeScript net with no topic word, and it returns hundreds
  of issues opened hours earlier with 0 comments. So all five graded candidates came from Q4.
  None of the RAG queries my fit profile is built around (Q1–Q3) was graded.
- **Changed:** filters 5–6 now rank within each query, give a bonus to issues several queries
  hit, and fill the top 5 round-robin (Q1, Q2, Q3, Q4, then Q1 again).
- **Result:** in scan 2, the RAG queries held 4 of the 5 slots.

**2. `repo-in-use` passed repos created that same day.** *(rubric)*
- **What happened:** codercops/discord-bot and jeganxthan/aether were both created on
  2026-10-11. Each had 0 stars and no release. They passed on the commits-only path ("3 of the
  last 5 commits within 90 days"). That proves the author was busy, not that anyone uses the
  software. The Unit 1 snapshots never contained a brand-new repo, so the gap stayed hidden.
- **Changed:** with no recent release, a repo now also needs at least 10 stars.
- **Result:** I regression-tested with Unit 1's harness and it scored 20/20, the same as
  before. In scan 2, the patch rejected langchengit/leavy (1 star) and aniruddhaadak80/skills
  (2 stars).

**3. Q4 filters by repository language, not the work.** *(strategy: queries)*
- **What happened:** `--language typescript` matches the repo's main language. It surfaced Rust
  tasks (atlastodo/atlas-todo#50, jeganxthan/aether#1) in repos GitHub labels TypeScript.
- **Not changed:** the result fields don't carry the issue's language, so no free filter can
  fix this. I'm accepting it as the cost of a broad net that only gets one slot now.

## 2026-10-11: scan 2

**4. The rubric's ranking put the best fit last.** *(rubric: verdict rule)*
- **What happened:** accepted issues are ranked by how many preferred checks they pass.
  psssnikhil/ai-engineering-hub#32 is the closest fit to my profile in either scan (HNSW,
  hybrid search, RRF). It ranked third, because `maintainer-responsive` was `unclear`: the repo
  had no outsider issues to sample. An empty sample is treated as if the check had failed.
- **To change:** count only preferred *fails* against an issue, not `unclear` grades. Not
  patched yet.

**5. `scope-fits-newcomer` passes non-code work.** *(rubric)*
- **What happened:** Lyellr88/marm-memory#282 asks for a recorded and edited demo video. It
  clears every scope disqualifier, because the rubric never says a first contribution should
  be a change to the repository's code or docs.
- **To change:** decide whether that's a rule I want. If it is, it belongs in
  `scope-fits-newcomer` as a fifth disqualifier. Not patched yet.

**6. Q1's topic word is too broad.** *(strategy: queries)*
- **What happened:** "retrieval" matched a video task in a retrieval tool (#282), because the
  word appears in the repo's description, not in the work.
- **To change:** try `--match title`, as Q3 does, or a narrower phrase like "RAG" or "hybrid
  search". Not changed yet.

**7. Q3 returned nothing usable.** *(strategy: queries)*
- **What happened:** all 9 `help wanted` issues with "vector search" in the title were
  assigned, quiet for more than 90 days, or in a repo another query had already taken.
- **To change:** swap `help wanted` for `good first issue`, or widen the phrase. Not changed
  yet.

## 2026-10-18: scan 3 (claim day)

**8. The top five hid the best fit.** *(strategy: how many to grade)*
- **What happened:** the round-robin top five held one code task in a used repo
  (readprism#199). Going further down Q1 and Q2 found production-rag-assistant#147 and
  statewave#485, both real retrieval bugs. #485 is the issue I claimed.
- **To change:** grade more than five when the top five has fewer than two code tasks, or
  rank `good first issue` bugs above docs and content tasks. Not changed yet.

**9. The 10-star floor sank a real code bug.** *(rubric: repo-in-use)*
- **What happened:** HarmonAIze#54 (embedding-projection bug, 6 stars, no release) was
  rejected only by the floor I added on 2026-10-11. The rule worked as written.
- **Not changed:** one case isn't enough to move the threshold.

**10. The issue tracker and the code live in different repos.** *(rubric: maintainer-responsive)*
- **What happened:** #485 is filed in `statewave`, but the code is in
  `statewave-multi-agent-shared-context`. The scout sampled the tracker repo, where an outsider's
  PR was merged in a day. In the code repo, four outsider PRs (Oct 5 to 17) have no maintainer
  review yet. I found this only after claiming.
- **To change:** when an issue names files that aren't in its repo, sample the repo that holds
  them. Not patched yet.

**11. Two old frictions held.** Q3 returned no survivors again (#7), and every accepted issue
tied on `maintainer-responsive` because of empty samples (#4).

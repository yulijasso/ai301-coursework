# issue-scout scan: 2026-10-11

Live-mode scan, using the four queries in `search-strategy.md` and the checks in `rubric.md`.

**Funnel:**
- Q1–Q4 returned 306 unique issues.
- Filter 1 (no assignees) left 254.
- Filter 2 (updated in the last 90 days) left 186.
- Filter 3 (15 comments or fewer) left 185.
- Filter 4 (one issue per repo) left 106.
- Filter 5 (fewest comments first, then most recently updated) gave the top 5 graded below.

## Accepted, best fit first

None of the five has enough outsider issues to judge `maintainer-responsive`, so all score
the same on preferred checks. They are ordered by the fit profile in `scope.md`.

1. **[TabularisDB/tabularis#999](https://github.com/TabularisDB/tabularis/issues/999)**:
   Ctrl+Tab switches tabs in most-recently-used order.
   *Found by Q4. Ranked on 0 comments, updated 2026-10-11.*
   - **Fit:** the best one. TypeScript and React in a SQL database client with 5.2k stars,
     released 2026-10-08.
   - **Issue:** opened by a collaborator, names the files and functions to change, and has
     acceptance criteria.
   - **AI policy:** an `AGENTS.md` (instructions for AI coding agents) is present, and nothing
     bans AI.
2. **[userfypp/plan-measure#256](https://github.com/userfypp/plan-measure/issues/256)**:
   add tests for edge cases in the takeoff summary.
   *Found by Q4. Ranked on 0 comments.*
   - **Fit:** a small TypeScript task with only tests to write.
   - **Issue:** opened by the owner, labelled `help wanted`. The body is terse.
   - **AI policy:** CONTRIBUTING welcomes AI-assisted PRs if you understand and test them.
3. **[codercops/discord-bot#5](https://github.com/codercops/discord-bot/issues/5)**:
   add a favicon to the leaderboard page.
   *Found by Q4. Ranked on 0 comments.*
   - **Fit:** TypeScript, with a very detailed issue.
   - **AI policy:** allowed, with disclosure in the PR.
   - **Etiquette:** CONTRIBUTING says to comment and *wait until you're assigned*, and to work
     on one issue at a time.
4. **[atlastodo/atlas-todo#50](https://github.com/atlastodo/atlas-todo/issues/50)**:
   make the server's listen address configurable.
   *Found by Q4. Ranked on 0 comments.*
   - **Fit:** bounded, but the work is in **Rust and Nix**, which aren't in the profile.
5. **[jeganxthan/aether#1](https://github.com/jeganxthan/aether/issues/1)**:
   remove an unused command.
   *Found by Q4. Ranked on 0 comments.*
   - **Fit:** very easy, but it's **Rust and Tauri** work.
   - **Repo:** created 2026-10-11, with 0 stars.

## Rejected

None.

## Friction (candidates for `scan-notes.md`)

- **The ranking hides the RAG queries.** Ordering by fewest comments, newest first, rewards
  issues opened in the last few hours, and Q4's broad TypeScript search supplies hundreds of
  them. Q1–Q3 never reach the top five, so none of the five matches the profile's stated
  interest in RAG. To fix the strategy, cap the results taken from each query, or rank results
  that match more than one query higher.
- **`repo-in-use` passes repos that are a day old.** codercops/discord-bot and jeganxthan/aether
  were both created on 2026-10-11. Their recent commits satisfy "3 of the last 5 within 90
  days", so the rubric can't tell a new solo repo from one people actually use. A minimum repo
  age, or a stars or usage signal, would close this gap.
- **Q4 filters by the repository's language, not the issue's.** It surfaced Rust tasks (#4, #5)
  in repos GitHub labels TypeScript.

No issue has been commented on or claimed. Per `scope.md`, claim on the issue itself once you
commit to one.

```json
[
  {"item": "https://github.com/TabularisDB/tabularis/issues/999", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11 (fix(mysql)... #966)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "latest release v0.27.0 on 2026-10-08"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One feature with named files and acceptance criteria; opener is COLLABORATOR with maintainer-applied 'good first issue'"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR (only a cross-reference from an unrelated issue)"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "No AI ban in CONTRIBUTING.md; AGENTS.md/CLAUDE.md present"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "Only outsider issue in sample (#977) is under a day old"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; body names resolveNextTabId, EditorProvider.tsx, Editor.tsx"}
  ], "verdict": "accept"},
  {"item": "https://github.com/userfypp/plan-measure/issues/256", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11 (docs: update audit follow-ups #282)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "latest release v2.10.0 on 2026-10-11"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Bounded: tests for three named buildTakeoffSummary edge cases; opener is OWNER"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING: 'AI-assisted pull requests are welcome under the same rules as any other'"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No outsider-opened issues in the last 40 to sample"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' and 'help wanted' labels; names buildTakeoffSummary"}
  ], "verdict": "accept"},
  {"item": "https://github.com/codercops/discord-bot/issues/5", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "No release; 5 of last 5 commits dated 2026-10-11"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One favicon plus CSP change with files and acceptance criteria; opener is MEMBER"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING: 'You can use AI tools... Say so in the PR' (conditions, not a ban)"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No outsider-opened issues to sample; repo created 2026-10-11"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; names src/page.ts and src/index.ts"}
  ], "verdict": "accept"},
  {"item": "https://github.com/atlastodo/atlas-todo/issues/50", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-10 (Release v0.1.9 #37)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "latest release v0.1.9 on 2026-10-10"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One BIND_ADDR setting across named files; carries a maintainer-applied 'good first issue' label"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "No AI ban in CONTRIBUTING.md; AGENTS.md present"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "Sampled issues #46-#50 are minutes old; 14 days not yet elapsed"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; names main.rs, config.rs, .env.example, nix/server-module.nix"}
  ], "verdict": "accept"},
  {"item": "https://github.com/jeganxthan/aether/issues/1", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11 (added the readME)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "No release; 5 of last 5 commits dated 2026-10-02 to 2026-10-11"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Delete one function and its registration, with a checklist; opener is OWNER"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING.md is silent on AI"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No outsider-opened issues; repo created 2026-10-11"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; names window.rs:80 and lib.rs:93"}
  ], "verdict": "accept"}
]
```

---

# Scan 2 (iteration 2): 2026-10-11

**What changed since scan 1:**
- **Ranking (`search-strategy.md`):** filters 5–6 now rank within each query, give a bonus to
  issues matched by several queries, and fill the top 5 round-robin (Q1, Q2, Q3, Q4, then Q1
  again).
- **Rubric:** `repo-in-use` is patched. With no recent release, a repo now also needs at least
  10 stars.

**Funnel:**
- Q1–Q4 returned 306 unique issues.
- Filter 1 left 253, filter 2 left 185, filter 3 left 184, and filter 4 left 107.
- Survivors per query: Q1 51, Q2 39, Q3 0, Q4 18.
- Q3 had no survivors, so its turns passed to the next query.
- The top 5 slots went Q1, Q2, Q4, Q1, Q2.

**What the iteration fixed:** the RAG queries now hold four of the five slots, against none in
scan 1. The patched `repo-in-use` rejected two low-star, commits-only repos in a real scan.

## Accepted

The rubric ranks accepted issues by how many preferred checks they pass, and fit by profile
breaks ties.

1. **[Lyellr88/marm-memory#282](https://github.com/Lyellr88/marm-memory/issues/282)**:
   record and edit a MARM Console demo video. Preferred: 2/2.
   *Found by Q1 ("retrieval"). Got Q1's second turn: 0 comments, updated 2026-10-10.*
   - **Repo:** a memory-retrieval and knowledge-graph tool with 419 stars and a release today.
     The repo fits the profile.
   - **Task:** video editing, not code, so it's a weak fit for learning RAG.
2. **[RitualDev-Lab/DevShelf#6](https://github.com/RitualDev-Lab/DevShelf/issues/6)**:
   add LocalAI to the directory. Preferred: 2/2.
   *Found by Q2 ("embeddings"). Got Q2's first turn: 0 comments, updated 2026-10-11.*
   - **Task:** one JSON entry. Bounded, but trivial, and it isn't RAG work.
3. **[psssnikhil/ai-engineering-hub#32](https://github.com/psssnikhil/ai-engineering-hub/issues/32)**:
   write a Q&A bank on vector databases, indexing and hybrid search. Preferred: 1/2.
   *Found by Q1 and Q2. Got Q1's first turn: matched 2 queries, 0 comments.*
   - **Fit:** the best one in either scan. The content covers HNSW, IVF-PQ, hybrid search, RRF,
     and dense versus sparse retrieval: exactly the profile's learning goal.
   - **Task:** documentation, not code.
   - **Ranking:** last, only because the owner has no outsider issues to sample for
     `maintainer-responsive`.

## Rejected

- **[langchengit/leavy#4](https://github.com/langchengit/leavy/issues/4)**: sunk by
  `repo-in-use`. The repo was created 2026-10-11, has 1 star, and no release; the patch caught
  it.
- **[aniruddhaadak80/skills#261](https://github.com/aniruddhaadak80/skills/issues/261)**: sunk
  by `repo-in-use`. It has 2 stars and no release, and its commits are mostly a bot updating
  the contributors wall.

## Friction (for `scan-notes.md`)

- **Ranking accepted issues by preferred-check count put the best fit last.** #32's only
  weakness is an `unclear` on `maintainer-responsive`, because the sample was empty. An empty
  sample counts against an issue as if it had failed.
- **`scope-fits-newcomer` passes non-code work.** A video-editing task (#282) clears every
  disqualifier. Whether a first contribution should be code is a rule the rubric doesn't
  state.
- **Q1's topic word is too broad.** "retrieval" matches a demo-video issue in a retrieval tool.
- **Q3 returned nothing usable.** All 9 "vector search" `help wanted` issues were assigned,
  older than 90 days, or in repos already taken.

```json
[
  {"item": "https://github.com/Lyellr88/marm-memory/issues/282", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11 (chore(release): prepare v2.60.0)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "latest release v2.60.0 on 2026-10-11"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One demo video from a supplied demo pack; opener is OWNER; no disqualifier applies"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments; cross-references are issues in other repos, not PRs"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING: 'AI coding tools... are welcome'; owner remains responsible (conditions)"},
    {"name": "maintainer-responsive", "grade": "pass", "evidence": "Outsider issue #273 opened 2026-09-28, maintainer reply 2026-10-03"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' and 'help wanted' labels; names marm-console/assets/demo-pack/"}
  ], "verdict": "accept"},
  {"item": "https://github.com/RitualDev-Lab/DevShelf/issues/6", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11 (fix(seo)...)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "latest release v1.0.0 on 2026-09-11"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Add one JSON entry to shelf/ai-tools.json; opener is COLLABORATOR"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING.md is silent on AI"},
    {"name": "maintainer-responsive", "grade": "pass", "evidence": "Outsider issue #70 opened 2026-10-10, maintainer reply 2026-10-11"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; names shelf/ai-tools.json and the validate commands"}
  ], "verdict": "accept"},
  {"item": "https://github.com/psssnikhil/ai-engineering-hub/issues/32", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-08-23 (Merge pull request #38)"},
    {"name": "repo-in-use", "grade": "pass", "evidence": "No release; 5 of last 5 commits within 90 days (2026-08-09 to 08-23) and 18 stars"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One new doc (docs/interview-prep/questions-vector-search.md) with a stated endpoint of 15+ Q&As; opener is OWNER"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "AGENTS.md present; PR template has an 'AI Agent Pre-Flight Checklist' (conditions, not a ban)"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No outsider-opened issues in the last 40 to sample"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' and 'documentation' labels; names the target file and required topics"}
  ], "verdict": "accept"},
  {"item": "https://github.com/langchengit/leavy/issues/4", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-10-11"},
    {"name": "repo-in-use", "grade": "fail", "evidence": "No release; commits recent but only 1 star (repo created 2026-10-11)"},
    {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Jest setup plus named format.ts test cases; opener is OWNER"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "No AI ban; AGENTS.md present"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No outsider-opened issues; repo created 2026-10-11"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' label; names src/lib/format.ts"}
  ], "verdict": "reject"},
  {"item": "https://github.com/aniruddhaadak80/skills/issues/261", "checks": [
    {"name": "repo-alive", "grade": "pass", "evidence": "archived=false; newest commit 2026-09-29"},
    {"name": "repo-in-use", "grade": "fail", "evidence": "No release; commits recent but only 2 stars"},
    {"name": "scope-fits-newcomer", "grade": "unclear", "evidence": "New feature opened by cline-cloud[bot] (NONE); no maintainer comment; cannot tell whether labels were maintainer-applied"},
    {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, 0 comments, no linked PR"},
    {"name": "ai-policy-allows", "grade": "pass", "evidence": "CONTRIBUTING.md is silent on AI"},
    {"name": "maintainer-responsive", "grade": "unclear", "evidence": "Sampled outsider issues #290-#293 opened 2026-10-10; 14 days not yet elapsed"},
    {"name": "newcomer-signposted", "grade": "pass", "evidence": "'good first issue' and 'help wanted' labels"}
  ], "verdict": "reject"}
]
```

---

# Scan 3 (claim day): 2026-10-18 (live mode, iteration-2 strategy and rubric)

Funnel: Q1–Q4 returned 306 unique issues. f1 (no assignee) 262, f2 (≤90 days) 196, f3 (≤15 comments) 195, f4 (one per repo) 108.
Survivors per query: Q1 52, Q2 41, Q3 0, Q4 16. Q3's turn passed on. Slots: Q1, Q2, Q4, Q1, Q2.

## Accepted (fit order)
1. psssnikhil/ai-engineering-hub#32 — Q&A bank: vector DBs, indexing, hybrid search (Q1+Q2, 2 hits, 0 comments). Preferred 1/2.
2. mohitmishra786/readprism#199 — add `make eval` / `make retrieval-eval`; eval scripts read-only by default (Q1, 0 comments, updated 2026-10-18). Preferred 1/2.

## Rejected
- mintzocloud-coder/sutra#19 — repo-in-use: 1 star, no release, repo created 2026-10-17.
- tobioffice/NbkristQik#43 — repo-in-use: 1 star, latest release 2025-08-06 (>12 months).
- drnicholasbrink/HarmonAIze#54 — repo-in-use: 6 stars, no release.

## Friction
- Q3 ("vector search", help wanted) returned zero survivors again (scan-notes #7 still open).
- #32 and #199 tie at 1/2 preferred because maintainer-responsive is unclear on empty samples (scan-notes #4 still open).
- HarmonAIze#54 is a real code bug touching embedding projections, sunk only by the 10-star floor.

```json
[
 {"item":"https://github.com/psssnikhil/ai-engineering-hub/issues/32","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"archived=false; newest commit 2026-08-23 (Merge PR #38), 56 days ago"},
  {"name":"repo-in-use","grade":"pass","evidence":"No release; 5 of last 5 commits within 90 days (2026-08-09..08-23) and 18 stars"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"One doc file docs/interview-prep/questions-vector-search.md with 15 listed Q&As; opener OWNER"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no linked or cross-referenced PR"},
  {"name":"ai-policy-allows","grade":"pass","evidence":".github/CONTRIBUTING.md silent on AI; AGENTS.md and CLAUDE.md present"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"No outsider-opened issues among the last 60 to sample"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"'good first issue' and 'documentation' labels; names target file path"}],"verdict":"accept"},
 {"item":"https://github.com/mohitmishra786/readprism/issues/199","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"archived=false; newest commit 2026-10-17 (Record the v0.1.0 release)"},
  {"name":"repo-in-use","grade":"pass","evidence":"latest release v0.1.0 on 2026-10-17"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Two Makefile targets plus a --write flag, effort:S, with acceptance criteria; opener OWNER; part of epic #83 but itself one PR"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments; cross-refs are issues (#83, an external issue-finder), not PRs"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"CONTRIBUTING.md silent on AI"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"No outsider-opened issues among the last 60 to sample"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"'good first issue' label; names Makefile, scripts/rank_eval.py, docs/eval/ranking.md"}],"verdict":"accept"},
 {"item":"https://github.com/mintzocloud-coder/sutra/issues/19","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-18"},
  {"name":"repo-in-use","grade":"fail","evidence":"No release; 1 star (repo created 2026-10-17)"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Migration + ingest script + kNN helper with acceptance; opener OWNER"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no PR"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"Not checked further; verdict already decided"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"Repo one day old"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"'good first issue'; names services/ai/scripts/"}],"verdict":"reject"},
 {"item":"https://github.com/tobioffice/NbkristQik/issues/43","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-18"},
  {"name":"repo-in-use","grade":"fail","evidence":"Latest release 2025-08-06 (>12 months); commits recent but 1 star"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"One package.json entry + CI pin; opener OWNER"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no PR"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"AGENTS.md present"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"Not sampled"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"'good first issue'; acceptance criteria"}],"verdict":"reject"},
 {"item":"https://github.com/drnicholasbrink/HarmonAIze/issues/54","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-16"},
  {"name":"repo-in-use","grade":"fail","evidence":"No release; 5 of 5 commits recent but 6 stars"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Bug in core/views.py:1307 palette zip plus perf notes; opener OWNER"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments; cross-ref #64 is an issue"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"No CONTRIBUTING/AI policy file found (silence)"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"Not sampled"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"'good first issue'; names core/views.py:1307"}],"verdict":"reject"}
]
```

---

# Extension: slots past the top 5 (same scan, same queries, 2026-10-18)

Went further down the Q1/Q2/Q4 rankings, pre-screened ~33 survivors on stars/release, and graded the five strongest RAG code candidates.

## Accepted
1. aieng-abdullah/production-rag-assistant#147 — abstain_retrieval_empty metric can never be non-zero (Q1). Preferred 1/2.
2. smaramwbc/statewave#485 — context_retrieval episodes never written, inspector section always empty (Q1). Preferred 1/2.
3. friday-memory/friday#1 — local Ollama embeddings provider (Q2). Preferred 1/2.
4. Aryan-Pardeshi/DeepResearch_AI#25 — metadata_validator: validate or rename (Q1). Preferred 1/2.

## Rejected
- mtrnix/metronix-memory#429 — unclaimed: open PR #549 "Closes #429" by iamcipherdev (2026-10-15).

```json
[
 {"item":"https://github.com/aieng-abdullah/production-rag-assistant/issues/147","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"archived=false; newest commit 2026-10-12 (Qdrant keep-alive #153)"},
  {"name":"repo-in-use","grade":"pass","evidence":"No release; 5 of last 5 commits 2026-10-10..12 and 71 stars"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Bug opened by OWNER; option (a) remove metric is small, acceptance criteria stated"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments; only xref is unrelated closed PR #139"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"CONTRIBUTING.md silent on AI; AGENTS.md present"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"No outsider-opened issues in last 50"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"good first issue + help wanted; names eval/retrieval_precision.py:137"}],"verdict":"accept"},
 {"item":"https://github.com/smaramwbc/statewave/issues/485","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-16"},
  {"name":"repo-in-use","grade":"pass","evidence":"latest release 2026-08-30; 283 stars"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Bug fix (not a feature) in one example module with suggested fix; maintainer-applied good first issue"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no xrefs"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"AGENTS.md: 'orientation for humans and AI coding agents'"},
  {"name":"maintainer-responsive","grade":"fail","evidence":"Sampled outsider issues #500/#502 got replies only from CONTRIBUTORs"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"names timeline_inspector.py, statewave_agents/context.py"}],"verdict":"accept"},
 {"item":"https://github.com/friday-memory/friday/issues/1","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-04"},
  {"name":"repo-in-use","grade":"pass","evidence":"latest release 2026-10-04"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"Feature endorsed: opener is MEMBER; one provider + test + README"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no xrefs"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"CONTRIBUTING silent; AGENTS.md present"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"No outsider-opened issues in sample"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"good first issue + help wanted; acceptance criteria"}],"verdict":"accept"},
 {"item":"https://github.com/Aryan-Pardeshi/DeepResearch_AI/issues/25","checks":[
  {"name":"repo-alive","grade":"pass","evidence":"newest commit 2026-10-17"},
  {"name":"repo-in-use","grade":"pass","evidence":"No release; 5 of 5 commits 2026-10-17 and 68 stars"},
  {"name":"scope-fits-newcomer","grade":"pass","evidence":"OWNER-opened; rename option is one bounded PR"},
  {"name":"unclaimed","grade":"pass","evidence":"No assignee, 0 comments, no xrefs"},
  {"name":"ai-policy-allows","grade":"pass","evidence":"CONTRIBUTING has no AI ban (conditions: don't overclaim, tests offline)"},
  {"name":"maintainer-responsive","grade":"unclear","evidence":"Only outsider issue #41 (2026-10-05) has no reply yet, 13 days in"},
  {"name":"newcomer-signposted","grade":"pass","evidence":"good first issue; names retrieval.py, frontend/app.js"}],"verdict":"accept"},
 {"item":"https://github.com/mtrnix/metronix-memory/issues/429","checks":[
  {"name":"unclaimed","grade":"fail","evidence":"Open PR #549 'Closes #429' by iamcipherdev, 2026-10-15"}],"verdict":"reject"}
]
```

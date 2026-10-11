# Search strategy: where your scout looks, and why

My fit profile in `scope.md` has three sentences that say where I should be
looking. Each query below names the one it came from; if I cannot trace a
query to a sentence, it is somebody else's query and it does not belong here.

## Queries

```bash
# Q1 - profile sentence 3: "especially interested in strengthening my knowledge of
# retrieval-augmented generation (RAG), including hybrid retrieval, more advanced
# retrieval strategies, and different RAG architectures"
# The subject-matter query: retrieval work in the language I write most.
gh search issues "retrieval" --label "good first issue" --language python --state open \
  --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url

# Q2 - profile sentence 2: "generative AI and retrieval tools, including Voyage AI,
# ChromaDB, embeddings, pgvector, and Pinecone"
# The tools I have actually used. No --language here on purpose: the vector-store
# clients I know are split across Python and TypeScript, and filtering by one
# language would hide half of them.
gh search issues "embeddings" --label "good first issue" --state open \
  --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url

# Q3 - profile sentence 3 again, aimed at the thing itself rather than the topic
# word. --match title keeps out the thousands of bodies that mention RAG in passing.
gh search issues "vector search" --match title --label "help wanted" --state open \
  --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url

# Q4 - profile sentence 1: "Python, C++, C#, JavaScript, TypeScript, and SQL"
# A language-only net with no topic word, so the scan is not locked to RAG. This is
# the query that can surprise me, which sentence 4 of my profile says I want.
gh search issues --label "good first issue" --language typescript --state open \
  --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url
```

## Ranking filters

Combine all four result sets, dedupe by `url`, then apply these in order. Every
condition reads a field the search results already carry — nothing here needs the
issue page opened. Anything that would belongs in `rubric.md`.

1. **Drop any result with a non-empty `assignees`.** Out here a claim counts:
   an assignee is a stranger who got there first.
2. **Drop any result whose `updatedAt` is more than 90 days old.** A quiet thread
   is usually a quiet repo, and my rubric's `repo-alive` check would reject it
   anyway — cheaper to drop it here for free than to pay $0.20 to learn it.
3. **Drop any result with `commentsCount` above 15.** A long thread before any
   work starts means an unsettled discussion, not a bounded first task.
4. **Keep at most one issue per `repository`** — the highest-ranked one. Five
   candidates from one repo is one candidate with four spares.
5. **Order the survivors within each query** by how many of my queries returned
   the issue (more first: an issue two of my interests both hit is the best
   fit signal I have for free), then `commentsCount` ascending (quiet, unclaimed
   work first), then `updatedAt` descending (most recently touched first).
6. **Fill the top 5 round-robin by query, in profile order: Q1, Q2, Q3, Q4,
   then Q1 again.** Each turn takes that query's best survivor not already
   taken. If a query has no survivors left, its turn passes to the next query.
   This gives the RAG queries (Q1–Q3) four of the five slots and the
   language-only net (Q4) one.

Filters 5 and 6 are the ordering. Without an ordering the scout would grade
whatever the searches happened to return first, and the five graded candidates
would stop being mine.

**Why filter 6 exists (iteration 2, 2026-10-11).** In the first scan, filter 5
was one ordering across all four queries: `commentsCount` ascending, then
`updatedAt` descending. Q4 (TypeScript, no topic word) returns hundreds of
issues opened hours earlier with 0 comments, so all five slots went to Q4 and
none of the RAG queries my profile is built around was graded. Ranking within
each query, and taking turns between queries, keeps Q4 as the one surprise slot
my profile asks for without letting it crowd out the rest.

## How many to grade

Grade the top **5** ranked results per scan.

Five at about $0.20 each keeps a scan near $1, which is cheap enough to iterate
the queries several times. I need one good issue, not ten, and if five accepts
never appear the fix is the strategy above, not a bigger number.

<!-- TEMPLATE INSTRUCTIONS (kept for reference)

Replace this file with your unit-3 plan: the same `plan.md` your
plan-check run graded.

Keep the deviations heading below, and fill it before you submit. It is
graded on being answered, not on there being deviations to report.

-->

# Plan — issue #68: `ZeroDivisionError` on an empty keyword index

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68
Author: yulijasso · Repo at `f89c06f` · Reproduction posted in the issue thread

## 1. Diagnosis

`KeywordSearcher.index()` builds the BM25 index unconditionally. At
`rag/retriever/keyword_search.py:24-25` it tokenizes the corpus and
constructs `BM25Okapi(tokenized_corpus)` with no check on whether
`chunks` is empty. `rank_bm25`'s `BM25._initialize` then computes
`self.avgdl = num_doc / self.corpus_size`, and with an empty corpus
`corpus_size` is 0, so the constructor raises `ZeroDivisionError`.

The exception is raised inside `index()`, before `search()` is ever
called. `search()` already handles the empty case correctly — at
`keyword_search.py:38-40` it returns `[]` when `self.bm25` or
`self.chunks` is falsy — so `index()` is the only place an empty corpus
becomes an exception. My reproduction in the thread shows the traceback
terminating in `_initialize`, and a control run with one chunk
completing normally in the same session and interpreter.

## 2. Scope

**In scope.** The empty-corpus case in `KeywordSearcher.index()`, and
the `xfail` marker on the test that covers it.

**Not in scope.** `search()`'s existing early return, which is already
correct and which this fix deliberately reuses rather than duplicating.
`rank_bm25` itself — the division is upstream behavior and I am not
proposing a change there. The dense and hybrid retrieval paths. The
other seeded bugs in this repo (#60, #69), which are separate issues.

## 3. Files

- `rag/retriever/keyword_search.py` — the guard.
- `tests/unit/test_keyword_search.py` — remove the `xfail` marker on
  `TestKeywordSearcher::test_empty_index`.

Both files are implicated by the diagnosis: the second is the test that
already describes this bug and is marked `strict=True`, so it must
change in the same commit as the fix.

## 4. Approach

In `index()`, return early when `chunks` is empty, before constructing
`BM25Okapi`:

- Keep `self.chunks = chunks` (line 23) so the recorded corpus stays
  consistent with what was passed in.
- Set `self.bm25 = None`, which clears any index built by a previous
  call, then log `keyword_index_empty` and return. The module already
  names the empty case with its own event rather than reusing the normal
  one — `search()` logs `keyword_search_empty_index` at line 39 instead
  of `keyword_search_complete` with `results_count=0`, and
  `rag/evaluator/relevance_scorer.py:21-23` does the same with
  `relevance_score_empty_chunks`. This follows that convention.
- Add nothing to `search()`. With `self.bm25` as `None`, the existing
  guard at line 38 returns `[]` on the next search, which is the
  behavior the issue asks for. This is why the fix is one guard rather
  than a second code path.

Then remove the `@pytest.mark.xfail(strict=True, reason="issue #68
(manifest H-01): ...")` decorator at `tests/unit/test_keyword_search.py:134-137`.
Per the note in `CONTRIBUTING.md` about seeded bugs, the marker has to
go: with the guard in place `test_empty_index` passes, and a strict
xfail that passes fails the run as `XPASS(strict)`.

## 5. Test plan

The failing case, re-run from my posted reproduction:

```
run     python -c "from rag.retriever.keyword_search import KeywordSearcher; \
                   s = KeywordSearcher(); s.index([]); print(s.search('python', top_k=10))"
today   ZeroDivisionError: division by zero  (from rank_bm25._initialize)
expect  []
```

The control case from the same reproduction, which must not change:

```
run     python -c "from rag.retriever.keyword_search import KeywordSearcher; \
                   s = KeywordSearcher(); s.index([{'id': 1, 'text': 'python programming'}]); \
                   print(s.search('python', top_k=10))"
today   [{'id': 1, 'text': 'python programming', 'bm25_score': -0.2746530721670274}]
expect  unchanged
```

Then the repo's own gates:

```
run     make check && make test-unit
expect  test_empty_index passes on its own (not XPASS), no other test changes state
```

## 6. Risks

- **Stale index state.** Calling `index([])` after a successful index
  leaves `self.chunks` empty; setting `self.bm25 = None` is what keeps
  the two fields consistent. `search()` would return `[]` either way
  today, because its guard also tests `not self.chunks` — so this is
  belt-and-braces rather than load-bearing. It matters for any caller
  that reads `searcher.bm25` directly, and it means the fix does not
  depend on that second clause staying in `search()`.
- **A new log event.** The guard emits `keyword_index_empty`, an event
  name that does not exist in the module yet, so anything consuming
  these logs sees a new key. I judged this the smaller risk: reusing
  `keyword_index_built` with `chunk_count=0` would report a build that
  did not happen, and would break the convention `search()` and
  `relevance_scorer.py` already follow of naming the empty case
  separately.
- **The xfail removal is load-bearing.** Once the marker is gone the
  test fails loudly if the guard is wrong, which is the behavior I want.
  If the guard were incomplete, `make test-unit` fails rather than
  silently passing.

## Deviations

The code change held to the plan. The guard in `index()` keeps
`self.chunks = chunks`, sets `self.bm25 = None`, logs
`keyword_index_empty`, and returns before `BM25Okapi` is constructed.
`search()` is unchanged, and the only other edit is removing the `xfail`
marker from `test_empty_index`. No other files changed.

One part of the test plan did not go as written: `make check` does not
pass. ruff and black pass, but mypy stops with a syntax error inside
numpy's installed type stubs (`numpy/__init__.pyi:737: Type statement is
only supported in Python 3.12 and greater`). The repo pins mypy to
Python 3.11, and numpy 2.5.3's stubs use syntax that needs 3.12. It
fails the same way on unmodified `f89c06f`, so my change did not cause
it, and it stops before mypy reaches any repo code. To type-check the
change anyway I ran mypy with `--python-version 3.12`, which reported no
issues in 76 source files. I left the mypy configuration alone because
it is outside this issue's scope.

The rest of the test plan held. `index([])` now returns and the
following `search()` returns `[]`. The one-chunk control gives the same
result and the same `bm25_score` (`-0.2746530721670274`) as in my
reproduction. `make test-unit` reports 376 passed and 52 xfailed, with
`test_empty_index` passing on its own rather than as an XPASS. As an
extra check I ran that test with the marker removed but without the
guard, and it failed with the same `ZeroDivisionError`, so the test does
cover this bug rather than passing for an unrelated reason.

Two smaller notes from the build. My first attempt logged
`keyword_index_built` with `chunk_count=0` — the option this plan
rejects — and I changed it to `keyword_index_empty` before anything was
committed, so the committed change matches what I posted. Separately,
the dev dependencies had to be installed into `.venv` before `make
check` and `make test-unit` would run; that is environment setup rather
than a change to the plan.

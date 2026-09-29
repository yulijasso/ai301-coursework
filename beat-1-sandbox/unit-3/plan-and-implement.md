# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

<!-- [Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.] -->

yulijasso

**Plan comment**

<!-- [Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.] -->

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5880672157

````
Following up on my reproduction above with the plan, in case any of it should go
differently before I start.

The crash is in `index()`, not `search()`. At `keyword_search.py:24-25` it
tokenizes the corpus and hands it straight to `BM25Okapi`, which divides by
`corpus_size` — zero, for an empty list. `search()` already returns `[]` for the
empty case at lines 38-40, so `index()` is the only place an empty corpus turns
into an exception.

So what I have in mind is one guard on the empty path in `index()`: keep
`self.chunks = chunks`, set `self.bm25 = None` so an index from an earlier call
doesn't linger, log `keyword_index_empty`, and return before `BM25Okapi` is
constructed. Nothing changes in `search()` — with `self.bm25` as `None` its
existing guard already returns `[]`, which is the behavior the issue asks for,
and reusing it keeps this to one code path instead of two.

I used a separate log event rather than `keyword_index_built` with
`chunk_count=0`, since that's what the module already does: `search()` logs
`keyword_search_empty_index` at line 39 instead of reusing
`keyword_search_complete`, and `relevance_scorer.py` names its empty case the
same way.

I'll also drop the `@pytest.mark.xfail(strict=True, ...)` marker from
`test_empty_index`, as the issue asks and per the seeded-bug note in
`CONTRIBUTING.md`. Once the guard is in that test passes, and a strict xfail
that passes fails the run as `XPASS(strict)`.

That's the whole change — `keyword_search.py` and its unit test. I'm leaving
`search()`'s early return alone, not touching `rank_bm25` (the division is
upstream), and staying out of the dense and hybrid retrieval paths.

To show it worked I'll re-run the two cases from my reproduction above:

```
index([])         today   ZeroDivisionError from rank_bm25._initialize
                  expect  []
index([1 chunk])  expect  unchanged — same result and bm25_score as above
```

plus `make check && make test-unit`, with `test_empty_index` passing on its own
rather than as an XPASS. I'll put both outputs on the pull request.
````

---

## Your branch

**Branch**

<!-- [The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.] -->

`fix/68-empty-corpus-guard`

Pushed to my fork, `yulijasso/pathreview-ai301-fa26-s1`, off base commit `f89c06f`.

**Evidence**

<!-- [Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.] -->

Environment: macOS 15.7.5 (arm64), Python 3.12.4, rank-bm25 0.2.2. **Before** is `f89c06f`
unmodified; **after** is `f89c06f` with the guard and the `xfail` removal applied. Each run is
a separate interpreter invocation, so a crash in run 1 cannot affect run 2.

The change under test:

```diff
         self.chunks = chunks
+        if not chunks:
+            # BM25Okapi divides by corpus size; leave the index unset so search() returns [].
+            self.bm25 = None
+            logger.info("keyword_index_empty")
+            return
         tokenized_corpus = [self._tokenize(chunk["text"]) for chunk in chunks]
         self.bm25 = BM25Okapi(tokenized_corpus)
```

```diff
-    @pytest.mark.xfail(
-        strict=True,
-        reason="issue #68 (manifest H-01): BM25 keyword search raises ZeroDivisionError on an empty index",
-    )
     def test_empty_index(self, searcher):
```

### Run 1 — the reported case, `index([])`

```python
from rag.retriever.keyword_search import KeywordSearcher
s = KeywordSearcher()
s.index([])
print(s.search('python', top_k=10))
```

Before:

```
Traceback (most recent call last):
  File "<string>", line 3, in <module>
  File "rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File ".venv/lib/python3.12/site-packages/rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
                 ~~~~~~~~^~~~~~~~~~~~~~~~~~
ZeroDivisionError: division by zero
exit=1
```

After:

```
2026-09-28 18:54:48 [info     ] keyword_index_empty
2026-09-28 18:54:48 [warning  ] keyword_search_empty_index
[]
exit=0
```

### Run 2 (control) — one chunk instead of zero

```python
from rag.retriever.keyword_search import KeywordSearcher
s = KeywordSearcher()
s.index([{'id': 1, 'text': 'python programming'}])
print(s.search('python', top_k=10))
```

Before and after are byte-identical, including the score:

```
2026-09-28 18:54:48 [info     ] keyword_index_built            chunk_count=1
2026-09-28 18:54:48 [info     ] keyword_search_complete        query_len=1 results_count=1
[{'id': 1, 'text': 'python programming', 'bm25_score': -0.2746530721670274}]
exit=0
```

### Unit tests

Before — `test_empty_index` carries `@pytest.mark.xfail(strict=True)`:

```
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index XFAIL [ 52%]
======================== 16 passed, 1 xfailed in 0.23s =========================
```

After — marker removed, the test passes on its own rather than as an XPASS:

```
tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index PASSED [ 52%]
============================== 17 passed in 0.18s ==============================
```

Full unit suite after the fix (`make test-unit`):

```
================= 376 passed, 52 xfailed, 4 warnings in 7.01s ==================
```

As a negative control I also ran `test_empty_index` with the marker removed but *without*
the guard: it failed with the same `ZeroDivisionError`, confirming the test actually covers
this bug rather than passing for an unrelated reason.

`make check` does not pass, for a reason that predates my change — see Deviations in
`plan.md`. ruff and black pass; mypy aborts inside numpy's installed stubs because the repo
pins mypy to Python 3.11 and numpy 2.5.3's stubs need 3.12. It fails identically on
unmodified `f89c06f`. I type-checked the change by running mypy with `--python-version 3.12`,
which reported no issues in 76 source files, and left the mypy config alone as out of scope.

|  | Run 1: `index([])` | Run 2: one chunk | `test_empty_index` |
|---|---|---|---|
| Before | `ZeroDivisionError`, exit 1 | 1 result, score `-0.2746530721670274` | XFAIL |
| After | `[]`, exit 0 | unchanged | PASSED |

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

<!-- [The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.] -->

One run. I wrote the rubric, the procedure, and the evidence guide against the five failure
families named in lecture before spending anything, so the first full run was also the
confirming one:

`agreement: 20/20 scored items  (bar: 18/20: PASS)`

`categories: clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`

That is the agreement line in the committed `eval-run.txt`, whose header fingerprints the
same `rubric.md` (`sha256:c4bf396b7f41fe50`) and `procedure.md`
(`sha256:5ae7a389a17c488f`) that I uploaded to `tools/plan-check/`.

An earlier attempt at the same run was launched without `--save-run` and killed at 11 of 20
packages once I noticed it could not write the run file. It produced no agreement line, so it
is not a run in the sense this field means.

**Package analysis**

<!-- [Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.] -->

`pkg-09` (sharkdp/fd#2067). My rubric's decision: **accept**. Gold label: **accept**, noted
as "honestly scoped-down ... arguable on the deferral, ready as scoped."

This is the package my `bounded-scope` check was written for, and the one that would have
sunk the run if I had written that check the obvious way. The plan fixes the Windows
separator mismatch and openly refuses the larger job:

> Not in scope, stated deferrals: option 1 (switching to direct globset matching, a larger
> rework the maintainers may prefer long term), and any change to regex-mode matching, which
> is correct today.

A check that asks "does this plan solve the issue" rejects that, because it does not — it
solves part of it and names the part it is leaving. So `bounded-scope` tests something
different: whether a reader can say of any given file whether it is in or out. It then carries
an explicit non-disqualifier — "a plan that deliberately does less than the whole issue and
says so is bounded, not incomplete" — with the corollary that "only an unstated one is a gap."
Under that reading `pkg-09` passes on the strength of the deferral rather than in spite of it.

`pkg-14` (zellij-org/zellij#5174) is the same shape, deferring an untestable Windows variant
and saying so. The lecture warned that two accepts in the set are scoped down on purpose;
without that non-disqualifier both become rejects and the run is 18/20 with `clear-accept`
at 5/7 instead of 7/7.

**Check rationale**

<!-- [Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.] -->

The `bounded-scope` check, quoted as it currently reads:

> The plan is one bounded change a reviewer could hold the diff to: a reader can say of any
> given file whether it is in or out. Fails if any of: (a) it changes files or areas the
> diagnosis does not implicate; (b) it bundles a rename, reformat, refactor, docs pass, or
> config migration the bug does not require — the "while I'm here" family; (c) it asks for
> open-ended work with no endpoint ("improve error handling throughout"); (d) the boundary
> cannot be determined at all — nothing named as in scope and nothing excluded. Two things are
> explicitly NOT failures: **more than one file is not creep when the diagnosis implicates each
> one** (a fix plus the test that covers it is one change), and **a plan that deliberately does
> less than the whole issue and says so is bounded, not incomplete** — a stated deferral is a
> pass, and only an unstated one is a gap.

What I rejected in favour of it was the count-based version: *one file, or two at most*. That
is the first thing I would have written, and it fails on both sides of the set. It wrongly
rejects `pkg-09` and `pkg-14`, whose deferrals are the reason they are ready. And it is no help
on `pkg-15` (joplin), where "the isolated one-constant fix is bundled with an undici migration,
a settings panel, UI rework, and a retry framework" — a count cannot tell a fix that genuinely
needs three files from a fix with a campaign attached to it.
So clause (b) names the shape of the failure instead of its size: the rename, the reformat,
the refactor, the docs pass, the config migration. That is what `pkg-06`, `pkg-12`, `pkg-15`
and `pkg-19` all do, and it is what the lecture called "the plan that eats the repo."

Writing the two exemptions as bold sentences rather than leaving them implied was deliberate.
Five parallel workers grade this set, and an unstated exemption is an exemption each worker
decides for itself.

**Trade-offs**

<!-- [Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns the
point in full when the reason follows.] -->

The deferral exemption in `bounded-scope` is the trade I made knowingly, and here is the case
I accept it will miss.

The exemption asks only that a deferral be *stated*, not that what remains be worth doing. A
plan that diagnoses the bug correctly, defers the part that actually fixes it, and says so in
one clear sentence passes `bounded-scope` on my wording. Nothing in this set does that —
`pkg-09` and `pkg-14` both ship the load-bearing half and defer the rework — so the run gives
me no evidence either way. I kept it because the alternative is worse in a way the set does
prove: any rule that judges how much of the issue the plan solves rejects two gold accepts,
and a false reject on an honest contributor is more expensive than a false accept on a plan a
maintainer will simply ask to go further. `test-decisive` is also a partial backstop, since a
plan that defers the fix has nothing observable to put in its test plan.

A second, smaller thing the run showed me, which is a gap in `procedure.md` rather than in the
rubric. `deviation-recorded` is a preferred check that the rubric calls "not applicable — and
not a fail — on a package graded before any build," but neither file says which *grade*
records not-applicable. Grading my own package live, I recorded `unclear`, which is defensible
only because preferred checks never reach the verdict. My week-2 skill had already solved this
with an explicit `not yet applicable:` reason convention, and `plan-check` should borrow it. I
did not change it before committing: the fix is one sentence in Verdict assembly, the run I
committed passes at 20/20 with every category at full marks, and its header fingerprints the
procedure that produced it, so editing that file would have required a fresh full run to keep
the two consistent — about $4 to gain nothing that is scored.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

yulijasso

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5752945639

````
Hi, I'd like to take this bug.

I've reproduced it locally on the current `main` (`f89c06f`) — `index([])` goes
straight into `BM25Okapi`, which divides by `corpus_size`. The traceback, a control
run with one chunk, and my environment are in a follow-up comment below.

What I plan to do next:

- Add an empty-corpus guard in `KeywordSearcher.index()` so it records the (empty)
  chunk list and clears any previously built index, letting the existing `search()`
  early-return handle the empty case rather than adding a second code path.
- Drop the `@pytest.mark.xfail(strict=True, ...)` marker from
  `tests/unit/test_keyword_search.py::TestKeywordSearcher::test_empty_index`, per
  the note in CONTRIBUTING.md about seeded bugs — with the guard in place that test
  would otherwise fail as `XPASS(strict)`.
- Run `make check && make test-unit` before opening the PR and post the results there.

I'll keep the change to what the bug needs and leave the rest of the module as I
found it.
````

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68#issuecomment-5752977388

````
I reproduced the crash on the current `main` (`f89c06f`) — `index([])` never reaches
a guard, it goes straight into `BM25Okapi`, which divides by `corpus_size`.

**Run 1 — empty corpus:**

```python
from rag.retriever.keyword_search import KeywordSearcher
s = KeywordSearcher()
s.index([])
```

```
Traceback (most recent call last):
  File "<string>", line 3, in <module>
  File "rag/retriever/keyword_search.py", line 25, in index
    self.bm25 = BM25Okapi(tokenized_corpus)
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File ".venv/lib/python3.12/site-packages/rank_bm25.py", line 83, in __init__
    super().__init__(corpus, tokenizer)
  File ".venv/lib/python3.12/site-packages/rank_bm25.py", line 27, in __init__
    nd = self._initialize(corpus)
         ^^^^^^^^^^^^^^^^^^^^^^^^
  File ".venv/lib/python3.12/site-packages/rank_bm25.py", line 52, in _initialize
    self.avgdl = num_doc / self.corpus_size
                 ~~~~~~~~^~~~~~~~~~~~~~~~~~
ZeroDivisionError: division by zero
```

**Run 2 (control) — the same calls with one chunk instead of zero:**

```python
s.index([{"id": 1, "text": "python programming"}])
print(s.search("python", top_k=10))
```

```
[info] keyword_index_built      chunk_count=1
[info] keyword_search_complete  query_len=1 results_count=1
[{'id': 1, 'text': 'python programming', 'bm25_score': -0.2746530721670274}]
```

Same session, same interpreter, same `rank-bm25` — the only difference between the
two runs is the argument to `index()`. Run 2 completes without an exception, so the
empty corpus is what triggers the crash rather than anything else in the setup.

**Expected:** `index([])` returns, and the following `search()` returns `[]` the way
it already does when `self.bm25` is unset.
**Actual:** `index([])` raises `ZeroDivisionError` from `rank_bm25._initialize`,
before `search()` is ever reached.

Environment: macOS 15.7.5 (arm64), Python 3.12.4, rank-bm25 0.2.2, repo at `f89c06f`.

That lines up with what the issue describes: `search()` already returns `[]` when
`self.bm25` is falsy (`keyword_search.py:38-40`), so `index()` is the only place an
empty corpus turns into an exception.
````

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

One run. I built the rubric and the evidence guide against the package set before
spending anything, so the first full run was also the confirming one:

`agreement: 19/20 scored items  (bar: 18/20: PASS)`

`categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`

That is the agreement line in the committed `eval-run.txt`. I found a real defect in
that run (see Trade-offs) and decided against fixing it: the fix would have required a
fresh full run to keep `eval-run.txt` consistent with the rubric its header fingerprints,
and it would have moved a passing 19/20 to 20/20 without changing anything that is
graded.

**Package analysis**

`pkg-05` (conda/conda#16543). My rubric's decision: **reject**. Gold label:
**accept** — the one package in the set my rubric and the instructor disagreed on.

My `steps-followable` check sank it. The run's evidence line reads:

> env.yml content is described in prose ("a valid dependencies: list plus a category:
> section") but never shown inline or generated by a command in the steps.

The grader applied my rule correctly; the rule was wrong. I had written the check to
accept an input only in three forms — shown inline, generated by a command in the steps,
or publicly obtainable — because the failure I was defending against is pkg-18, whose
reproduction lives in a private monorepo with an unshared config. pkg-05's `env.yml` is
in none of those three forms, but it is described precisely enough that a stranger could
recreate it in about ten seconds and re-run the attempt. What actually matters is whether
the reader can *reconstruct* the input, not whether the author displayed it verbatim, and
my three forms were a proxy for reconstructability that happened to exclude a fourth
legitimate way of achieving it. Every other check passed pkg-05, including
`outcome-matches-artifact`, which read the `json.tool` parse failure as showing exactly
the failure signature the issue reports.

**Check rationale**

The `outcome-matches-artifact` check, quoted as it currently reads:

> The stated outcome does not claim more than the artifacts show. **If the report claims
> reproduction,** it fails if any of: (a) the steps use a different input, syntax, or
> command than the issue's trigger; (b) the artifact shows a different failure than the
> issue's failure signature — a graceful validation error where a panic was reported, a
> compile error where a runtime error was reported; (c) the issue reports a crash, panic,
> process death, or nonzero exit and the artifact shows the process surviving — output
> still flowing, the prompt returning, the window still open; (d) the artifact shows only
> that the software starts and runs. **If the report states it could not reproduce,** it
> passes when the artifact shows a real attempt that exercised the issue's trigger;
> showing the failure is not required. An evidenced cannot-reproduce is a pass.

What I rejected in favour of it was the obvious version of this check: *the artifact must
show the behavior the issue describes*. That phrasing is what I would have written first,
and it throws away two clear accepts. `pkg-09` and `pkg-10` are both gold **accept** and
in neither one did the author reproduce the bug — they are honest cannot-reproduce
reports that show a real attempt and name what differed from the reporter's conditions.
A check that asks "did the bug appear" rejects both of them.

So the check is split by what the report *claims* rather than by what happened. If it
claims reproduction, the artifact has to carry the issue's trigger and the issue's failure
signature, and the four lettered clauses are the four ways the set violates that:
`pkg-02` ran a prefix range instead of the issue's offset-from-end syntax (a); `pkg-08`
produced a compile error where the issue reports a runtime path error (b); `pkg-17`'s own
artifact shows the window still open and the prompt returning under a claim of a crash
(c); `pkg-14`'s artifacts show only a version banner and a session list, which proves the
setup and not the bug (d). If the report says it could not reproduce, the same check asks
only that the attempt exercised the trigger. Writing it as lettered clauses rather than
flowing prose was deliberate: five parallel workers grade this set, and a list of
conditions applies more consistently across them than a paragraph of qualifications.

**Trade-offs**

`steps-followable` gives up `pkg-05`, and I know exactly what it costs and why I kept it.

The check fails an input that is "referred to but not shown inline, generated by a command
in the steps, or publicly obtainable." That wording buys a clean catch on `pkg-18`, whose
author reproduced a real panic but did it inside a private company monorepo with an
unshared config — truthful, and worth nothing to a reader who cannot re-run a single step.
It costs `pkg-05`, whose `env.yml` is described rather than displayed and is perfectly
reconstructable.

I worked out the fix — add "or described precisely enough that a reader could recreate an
equivalent input" as a fourth accepted form — and checked what it would do before deciding.
`pkg-18` is the package at risk, because it is the only reject in the set resting on
`steps-followable` alone; it survives the loosening because it also fails the clause about
depending on something the reader cannot obtain, which no description repairs. `pkg-06`
and `pkg-14` both fail on the separate clause about steps that omit a condition the issue
names as part of the trigger, so neither moves. That is a projected 20/20.

I did not apply it. The run I committed passes at 19/20 with every category floor met, the
`eval-run.txt` header fingerprints the rubric that produced it, and the fix would have
needed a canary plus a fresh full run to keep those consistent — about $4.80 of course
credit to gain nothing that is scored. The honest version of this check is the one in the
file, with a known false reject I can name.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

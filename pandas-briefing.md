# pandas briefing (prepared for the upcoming pandas-based project and first upstream contribution)

## Confirmed organization login
**pandas-dev** — verified via GitHub organization search (top result; https://github.com/pandas-dev). All findings below use this confirmed login.

## Discussion takeaway
Note: the main `pandas-dev/pandas` repository has GitHub Discussions turned off (its discussion list returns zero entries), so this briefing uses the pandas organization's discussion forum in `pandas-dev/pandas-stubs` (the official public type stubs for pandas).

Chosen discussion: **pandas-dev/pandas-stubs discussion #308 — "How do I parameterize the index data type of a Series?"** (https://github.com/pandas-dev/pandas-stubs/discussions/308), which is its most recently active discussion (last updated 2026-09-28).

What the comments actually say:
- One maintainer explains that for `s = pd.Series([1,3,4], index=pd.date_range("1/1/2022", "1/3/2022"), dtype=float)`, the stubs track the Series as `Series[float]` — pandas-stubs does **not** currently track the type of the supporting index. He also warns that `s: pd.Series[float] = pd.Series([1,2,3])` will type-check but fail at runtime, because pandas does not use generic types on `Series` at runtime.
- A second comment confirms that `pd.Series` is generic over exactly **one** parameter (the value dtype); the index type is not part of the public generic signature, so there is no `Series[Float, DatetimeIndex]`-style syntax. Practical options given: (1) define a type alias like `EditFloatSeries = pd.Series[float]` with a comment documenting the index intent — the recommended approach; (2) drop to `numpy.typing` with an explicit Datetime64 array if the index dtype must be machine-checked, at the cost of losing pandas' API; (3) follow/weigh in on upstream pandas-stubs roadmap issues about index typing, since the single generic parameter is a known limitation.
- Takeaway for our project: type-annotate pandas Series by value dtype only, and document index expectations in comments or type aliases rather than expecting the type checker to verify them.

## Main CI workflow and a recent run
- Workflow: **Unit Tests** (workflow ID 54497638, file `.github/workflows/unit-tests.yml`), which runs the test suite on pushes and pull requests to `main` and `3.0.x`. It builds pandas with Pixi and runs pytest across a matrix (Python 3.11–3.14 on ubuntu-24.04 and arm, plus special jobs: Downstream Compat, Minimum Versions, Freethreading, Without PyArrow, Locale: it_IT / zh_CN, future-config variants, NumPy Nightly, PyArrow Nightly), with MySQL, Postgres, and moto service containers.
- Recent run (reported exactly as returned):
  - **ID: 39629266225**
  - **Name: Unit Tests**
  - **Status: queued**
  - (Run #45288, event `pull_request`, branch `auto-backport-of-pr-71434-on-3.1.x`, display title "Backport PR #71434 on branch 3.1.x (CI: Update pixi to 0.82.1)", created 2026-10-21T15:50:11Z; https://github.com/pandas-dev/pandas/actions/runs/39629266225)

## Starred repositories check
The starred list contains 6 repositories — all NLP/ML projects, and **none of them are pandas or pandas-related**:
1. OpenBMB/AgentCPM — infrastructure for training/evaluating LLM agents (Python)
2. PaddlePaddle/ERNIE — official repo for ERNIE 4.5 and ERNIEKit (Python)
3. FudanNLP/fastNLP — modular NLP framework (Python)
4. maplezzz/NTU_ML2017_Hung-yi-Lee_HW — NTU ML2017 course homework (Jupyter Notebook)
5. fighting41love/funNLP — large Chinese/English NLP corpus and tool collection (Python)
6. 996icu/996.ICU — protest/statement repo (star-counting)

So we are not yet tracking pandas-dev/pandas; worth starring before the project starts.

## Review practice status
Review practice is complete: the practice pull request (with a line-level comment-only review catching the deliberate "recieve" typo) is at https://github.com/mcpmark-eval-liuhezi/review-practice/pull/1

---
*Note: this briefing was saved as a repository file (pandas-briefing.md) rather than a gist because the API token in use is not permitted to create gists.*

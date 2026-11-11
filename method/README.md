# Method

This folder tells how the configs were read, scored and checked. It is for readers who want to know where a score
comes from, or who want to check one. This page gives the purpose of each method document and a reading order.

## Contents

- [Reading order](#reading-order)
- [Scoring](#scoring)
- [Checking the scores](#checking-the-scores)
- [Census](#census)
- [Libraries](#libraries)
- [Scope](#scope)
- [Notes on this public edition](#notes-on-this-public-edition)

## Reading order

To understand how the scores were made, read these documents in this order:

1. [RUBRIC.md](RUBRIC.md): what a review contains, and what each score means.
2. [FORMAT.md](FORMAT.md): how a score is written down and checked.
3. [pilot.md](pilot.md): how the rubric anchors were calibrated before the corpus was scored.
4. [cross-check.md](cross-check.md): how the finished scores were checked.
5. [CENSUS.md](CENSUS.md): how the census evidence behind application breadth (B) was collected.
6. [EXCLUDED.md](EXCLUDED.md): which repos are not scored, and why.

For the libraries, read [LIBRARY-RUBRIC.md](LIBRARY-RUBRIC.md) and then [library-pilot.md](library-pilot.md). The
two review documents ([CATEGORIES-REVIEW.md](CATEGORIES-REVIEW.md) and
[LIBRARY-RUBRIC-REVIEW.md](LIBRARY-RUBRIC-REVIEW.md)) tell why the rubrics have their current form. Read them last.

## Scoring

| document | purpose |
|---|---|
| [RUBRIC.md](RUBRIC.md) | the per-config review rubric. It covers the page structure, the ten categories with their anchors, the calibration rulings and the shortlists. |
| [FORMAT.md](FORMAT.md) | the machine-checked accounting format for scores, including the settings-leak and breadth arithmetic. |
| [CATEGORIES-REVIEW.md](CATEGORIES-REVIEW.md) | the challenge to an earlier seven-category draft, which led to the current categories. |

## Checking the scores

| document | purpose |
|---|---|
| [pilot.md](pilot.md) | before the corpus was scored, two independent reviewers scored seven calibration configs blind. The anchors were tightened where they disagreed. |
| [cross-check.md](cross-check.md) | after scoring, a blind second reading of a random sample of public configs. |

## Census

| document | purpose |
|---|---|
| [CENSUS.md](CENSUS.md) | the census contract. It defines what counts as adopting a piece of software, how machine roles are decided, and how counts are formed. |

## Libraries

| document | purpose |
|---|---|
| [LIBRARY-RUBRIC.md](LIBRARY-RUBRIC.md) | the rubric for aspect namespace libraries. |
| [LIBRARY-RUBRIC-REVIEW.md](LIBRARY-RUBRIC-REVIEW.md) | the challenge to the first library rubric draft. |
| [library-pilot.md](library-pilot.md) | two blind readings of the three libraries, reconciled. |

## Scope

| document | purpose |
|---|---|
| [EXCLUDED.md](EXCLUDED.md) | repos left out of the corpus totals, and why. |

## Notes on this public edition

- Every citation is a `path:line` in the upstream repository at the reviewed revision.
- The method documents mention working files such as `extract/<id>.json`, `census/records/` and `manifest.tsv`.
  Those files hold mechanical facts and evidence records, and are not part of this edition.
- Citations, file paths, evidence strings and software names are quoted exactly as they appear upstream. This
  includes third-party tools, such as AI coding agents that some configs install.
- The only change to quoted code is in the reference config. There, the names of two private repositories are
  written as "a private repository".
- Placeholders such as `<host>` are set in code so they render as text.
- Findings that locate committed credential material are replaced with "a committed credential (reported
  privately; not located here)". The scoring effect of the finding is kept.
- Configs whose source is no longer public stay in aggregate counts. They have no page, row or citation here.

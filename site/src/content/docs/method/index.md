---
title: "Method"
---

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

1. [RUBRIC.md](/method/rubric/): what a review contains, and what each score means.
2. [FORMAT.md](/method/format/): how a score is written down and checked.
3. [pilot.md](/method/pilot/): how the rubric anchors were calibrated before the corpus was scored.
4. [cross-check.md](/method/cross-check/): how the finished scores were checked.
5. [CENSUS.md](/method/census/): how the census evidence behind application breadth (B) was collected.
6. [EXCLUDED.md](/method/excluded/): which repos are not scored, and why.

For the libraries, read [LIBRARY-RUBRIC.md](/method/library-rubric/) and then [library-pilot.md](/method/library-pilot/). The
two review documents ([CATEGORIES-REVIEW.md](/method/categories-review/) and
[LIBRARY-RUBRIC-REVIEW.md](/method/library-rubric-review/)) tell why the rubrics have their current form. Read them last.

## Scoring

| document | purpose |
|---|---|
| [RUBRIC.md](/method/rubric/) | the per-config review rubric. It covers the page structure, the ten categories with their anchors, the calibration rulings and the shortlists. |
| [FORMAT.md](/method/format/) | the machine-checked accounting format for scores, including the settings-leak and breadth arithmetic. |
| [CATEGORIES-REVIEW.md](/method/categories-review/) | the challenge to an earlier seven-category draft, which led to the current categories. |

## Checking the scores

| document | purpose |
|---|---|
| [pilot.md](/method/pilot/) | before the corpus was scored, two independent reviewers scored seven calibration configs blind. The anchors were tightened where they disagreed. |
| [cross-check.md](/method/cross-check/) | after scoring, a blind second reading of a random sample of public configs. |

## Census

| document | purpose |
|---|---|
| [CENSUS.md](/method/census/) | the census contract. It defines what counts as adopting a piece of software, how machine roles are decided, and how counts are formed. |

## Libraries

| document | purpose |
|---|---|
| [LIBRARY-RUBRIC.md](/method/library-rubric/) | the rubric for aspect namespace libraries. |
| [LIBRARY-RUBRIC-REVIEW.md](/method/library-rubric-review/) | the challenge to the first library rubric draft. |
| [library-pilot.md](/method/library-pilot/) | two blind readings of the three libraries, reconciled. |

## Scope

| document | purpose |
|---|---|
| [EXCLUDED.md](/method/excluded/) | repos left out of the corpus totals, and why. |

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

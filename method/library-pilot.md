# Library pilot

This page records the library pilot: two blind readings of the three aspect namespace libraries, reconciled. It is
for readers who want to know how far the library scores depend on the reader, and what both readers found.

## Contents

- [How the libraries were read](#how-the-libraries-were-read)
- [Agreement](#agreement)
- [Findings](#findings)

## How the libraries were read

Two independent reviewers scored the three aspect namespace libraries blind, under the library rubric
([LIBRARY-RUBRIC.md](LIBRARY-RUBRIC.md)).

- The categories are E, N, K, Q, C, U and T.
- Q counts twice, so the total is out of 80.
- Q scores of 8 and 9 are provisional, because no standard resource protocol has been settled yet to measure against.

Each category cell is reader A / reader B.

| library | reader A | reader B | E | N | K | Q | C | U | T |
|---|---|---|---|---|---|---|---|---|---|
| [adanoelle__garden-shell](../libraries/adanoelle__garden-shell.md) | 41 | 41 | 6/5 | 8/9 | 4/5 | 5/5 | 6/5 | 4/3 | 3/4 |
| [crocuda__crocuda.nixos](../libraries/crocuda__crocuda.nixos.md) | 26 | 29 | 4/5 | 2/3 | 3/4 | 4/4 | 3/3 | 3/2 | 3/4 |
| [crocuda__normal.nixos](../libraries/crocuda__normal.nixos.md) | 23 | 26 | 4/3 | 2/2 | 4/4 | 3/5 | 3/2 | 2/3 | 2/2 |

## Agreement

20 of 21 category pairs are within one point, and none differs by more than two. Both readers rank the libraries in
the same order: garden-shell, then crocuda, then normal.

The one pair two points apart is normal Q (3 against 5). Because Q is weighted, it accounts for 4 of the 3-point gap
in normal's totals. Both readers note that Q has no settled protocol to measure against, so it stays provisional. The
other anchors are judged calibrated.

## Findings

**Both readers agree that no library is ready for consumers as published.**

- Garden-shell's isolation and its small contract for mutable state make it the strongest prior art for a community
  library.
- The crocuda repos offer breadth: about 38 and 36 units with real service lifecycles.
- But in the crocuda repos, `flakeModules.default` pulls in the whole tree. Both READMEs advertise a
  `nixosModules.default` that doesn't exist.

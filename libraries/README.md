# Aspect namespace libraries

This page indexes the three namespace libraries in the audit. It is for readers who want to reuse den aspects from
another repo, or who want to know how these repos were scored. It defines a namespace library, summarises the three
libraries, and tells how library scoring differs from config scoring.

## Contents

- [What a namespace library is](#what-a-namespace-library-is)
- [The three libraries](#the-three-libraries)
- [How library scoring differs from config scoring](#how-library-scoring-differs-from-config-scoring)

## What a namespace library is

A namespace library is a repo that exports a den aspect namespace for others to import. It runs no machines of its
own. These repos are audited on a separate track ([rubric](../method/LIBRARY-RUBRIC.md),
[pilot](../method/library-pilot.md)). They do not enter the config ranking or census totals.

## The three libraries

Each row gives one library, the namespace it exports, what it offers, the two blind reader totals out of 80, and
the upstream repo.

| library | namespace | what it offers | reader A / reader B, out of 80 | upstream |
|---|---|---|---|---|
| [adanoelle/garden-shell](adanoelle/garden-shell.md) | `garden` | an aspect and package library, a pure namespace provider | 41 / 41 | [adanoelle/garden-shell](https://github.com/adanoelle/garden-shell) |
| [crocuda/crocuda.nixos](crocuda/crocuda.nixos.md) | `crocuda` | hardened NixOS server modules, with dotfiles kept in their native formats and Nix as glue | 26 / 29 | [crocuda/crocuda.nixos](https://github.com/crocuda/crocuda.nixos) |
| [crocuda/normal.nixos](crocuda/normal.nixos.md) | `normal` | the same author's opinionated desktop modules | 23 / 26 | [crocuda/normal.nixos](https://github.com/crocuda/normal.nixos) |

Both readers agree that no library is ready for consumers as published. The [library pilot](../method/library-pilot.md)
gives the findings.

## How library scoring differs from config scoring

The library rubric asks the questions that a library consumer asks. For example: can a consumer import the library
and know what they get?

| | config | namespace library |
|---|---|---|
| rubric | [RUBRIC.md](../method/RUBRIC.md) | [LIBRARY-RUBRIC.md](../method/LIBRARY-RUBRIC.md) |
| categories | D, I, S, R, P, L, V, O, B, X | E export contract, N namespace hygiene, K parametrization, Q standard-resource use, C consumer docs and examples, U unit inventory, T dependency surface |
| total | 2D + I + S + R + P + L + O + B + ½V + ½X, out of 100 | Q counts twice, out of 80 |
| breadth | scored as B | not scored; published as a per-unit inventory with unit kinds |
| readings published | one review per config | both blind readings, unedited apart from redactions |
| ranked | yes, in the config ranking | no |
| in census totals | yes | no |

Q scores of 8 and 9 are provisional, because no standard resource protocol has been settled yet to measure against.

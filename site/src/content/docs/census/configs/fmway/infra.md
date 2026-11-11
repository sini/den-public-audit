---
title: "fmway/infra: census notes"
---

[Config page](/configs/fmway/infra/) · upstream [fmway/infra](https://github.com/fmway/infra) · [Census summary](/census/summary/)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `ad5b83625ade`.

A Clan-oriented infrastructure configuration imports a garden-provided Clan flake module; its Den host map is explicitly for debug ([`flake.nix:10`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/flake.nix#L10)).

## 2. Software selected and traces

Two local Clan machine entries are known. Because the external adapter owns conventional machine-file imports, local contributions are retained as ambiguous rather than counted as fully traced selections.


## 3. Defined, disabled and ambiguous alternatives

Opc1 has substantive Fish initialization and explicit Fish account-shell choices; Starship is enable-only. No live local definition for the other required families was found, but external adapter contributions remain unresolved and those families are not asserted absent.

- **fish** (ambiguous, conditional, configured): The conventional machine file enables Fish and supplies interactive theme initialization. The root external Clan adapter receives clan.directory and inventory, but its file-import chain is outside reviewed source. Evidence: [`machines/opc1/configuration.nix:15`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/machines/opc1/configuration.nix#L15), [`machines/opc1/configuration.nix:16`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/machines/opc1/configuration.nix#L16), [`flake.nix:6`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/flake.nix#L6), [`modules/clan/default.nix:10`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L10), [`modules/clan/default.nix:23`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L23).
- **fish** (ambiguous, conditional, default): This machine file explicitly assigns Fish to user/root; reachability remains conditional on the external adapter importing conventional machine files. Evidence: [`machines/opc1/configuration.nix:35`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/machines/opc1/configuration.nix#L35), [`machines/opc1/configuration.nix:36`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/machines/opc1/configuration.nix#L36), [`flake.nix:6`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/flake.nix#L6), [`modules/clan/default.nix:10`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L10), [`modules/clan/default.nix:23`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L23).
- **starship** (ambiguous, conditional, configured): The same conventional machine file bare-enables Starship; external adapter selection is not locally established. Evidence: [`machines/opc1/configuration.nix:3`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/machines/opc1/configuration.nix#L3), [`flake.nix:6`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/flake.nix#L6), [`modules/clan/default.nix:10`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L10), [`modules/clan/default.nix:23`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L23).

## 4. Machine roles and limits

Opc1 online tag is documented as server ([`modules/clan/default.nix:19`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L19), [`modules/clan/default.nix:23`](https://github.com/fmway/infra/blob/ad5b83625aded5e8679a87c706734edce341da7f/modules/clan/default.nix#L23)). T480 local tag permits laptop or PC and is not narrowed by its name alone. No architecture is inferred from the separate x86 debug map.

Known local Clan inventory is two machines; external imported adapter may extend inventory or assign platform details, so completeness is not established.

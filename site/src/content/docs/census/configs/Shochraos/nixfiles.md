---
title: "Shochraos/nixfiles: census notes"
---

[Config page](/configs/shochraos/nixfiles/) · upstream [Shochraos/nixfiles](https://github.com/Shochraos/nixfiles) · [Census summary](/census/summary/)

Revision `4d7c55187377`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Four explicit host entries split into two graphical machines and two headless DNS/proxy hosts ([modules/flake/den.nix:81](https://github.com/Shochraos/nixfiles/blob/4d7c551873771cfd65ed440b8f97f3401f504551/modules/flake/den.nix#L81); [README.md:5](https://github.com/Shochraos/nixfiles/blob/4d7c551873771cfd65ed440b8f97f3401f504551/README.md#L5)).

## Software selected and host/user traces

Graphical includes Hyprland/editor/duxshell, whereas base includes shell ([modules/flake/den.nix:18](https://github.com/Shochraos/nixfiles/blob/4d7c551873771cfd65ed440b8f97f3401f504551/modules/flake/den.nix#L18)). System Hyprland and default session are explicit; HM to-users delivery is verified against the exact pinned implementation. Exact pinned dependency verified statically: https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/aspects/fx/aspect/provide.nix, lines21–27 directly dispatch to-users/to-hosts as include effects. Local flake.lock binds this revision. Missing mutual-provider is not a blocker; it is an inert compatibility shim in these pins.

## Defined, disabled and ambiguous alternatives

Provider-only uncertainties were resolved against the exact locked Den implementation. Explicit to-users contributions above are selected where the complete local host/profile/user/HM-class chain is cited. Direct host homeManager content still requires a separate projection route; this conclusion does not infer one.

## Machine roles and remaining unknowns

README supplies explicit desktop/laptop/headless-service purposes. Inventory complete for four declared hosts; no runtime/evaluation claim.

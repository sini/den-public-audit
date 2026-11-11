---
title: "jcranney/nix-configuration: census notes"
---

[Config page](/configs/jcranney/nix-configuration/) · upstream [jcranney/nix-configuration](https://github.com/jcranney/nix-configuration) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: 12376d630e3e; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Actual source declares Agnes, Burter and Recoome (their modules/hosts files:3), with additional abdu on Agnes at [modules/hosts/agnes.nix:4](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L4). README inventory includes stale extra hosts/users; those descriptions are not additional live declarations.

## Software selected and host/user traces

All actual jcranney contexts receive HM via [modules/defaults.nix:14](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L14) and substantive Zsh via [modules/jcranney.nix:63](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L63). OS login default is explicitly selected at [modules/jcranney.nix:4](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L4). Burter and Recoome include graphical at host level and separately provide it to jcranney, enabling OS Niri and installing HM VSCode ([modules/graphical.nix:4](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L4)/78).

## Defined, disabled and ambiguous alternatives

Niri is enable-only; graphical also adds SDDM, which is not a Plasma desktop or explicit Niri default. Plasma enable is merely commented at [modules/graphical.nix:7](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L7). VSCode installation is not editor configuration. Actual configured/default editor is Vim ([modules/jcranney.nix:32](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L32)/51/73), outside the required families; it is not Neovim. Agnes Node-RED Bash service PATH dependency ([modules/hosts/agnes.nix:87](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L87)) is not an interactive Bash choice. Abdu has no local software aspect, so no jcranney settings are silently copied to it.

## Machine roles and remaining limits

README roles match the three actual declarations: Agnes home server, Burter laptop, Recoome desktop ([README.md:31](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L31)/34/35). Ruth/Jeice and shared bambi/etna accounts appear in docs only, excluded from actual target/user inventory. These are account contexts, not counted humans; static selection does not guarantee module evaluation or runtime use.

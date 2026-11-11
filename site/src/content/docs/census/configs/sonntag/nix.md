---
title: "sonntag/nix: census notes"
---

[Config page](/configs/sonntag/nix/) · upstream [sonntag/nix](https://github.com/sonntag/nix) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: 816947c6a270; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

One Darwin host plus three real standalone HM outputs coexist with exported Linux profiles ([modules/hosts.nix:8](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/hosts.nix#L8); [modules/flake/homes.nix:23](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/flake/homes.nix#L23)). Huginn delegates infrastructure to a consuming flake; it is not a local managed host ([modules/hosts/huginn/default.nix:2](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/hosts/huginn/default.nix#L2)).

## Software selected and host/user traces

All declared justin contexts resolve the same aspect. Fish functions, Helix, tmux, Zellij and Starship modules merge directly onto it, with actual imported TOML/KDL themes inspected ([modules/shell/helix.nix:2](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/shell/helix.nix#L2); [modules/shell/starship/default.nix:7](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/shell/starship/default.nix#L7)). Aerospace applies through den.default.darwin ([modules/services/aerospace/default.nix:2](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/services/aerospace/default.nix#L2)).

## Defined, disabled and ambiguous alternatives

The nvim pin is backed by selected package installation and explicit EDITOR, but unread external package internals are not configured-editor evidence ([modules/shell/nvim.nix:8](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/shell/nvim.nix#L8)). Zed is a cask only. Hyprland has genuine OS/HM definitions but no local selecting target ([modules/services/hyprland/default.nix:4](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/services/hyprland/default.nix#L4)). Commented Fish auto-tmux is not active startup ([modules/shell/fish/fish.nix:67](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/shell/fish/fish.nix#L67)).

## Machine roles and remaining limits

Wrath has explicit darwin role; physical chassis is unspecified in inspected source. Homes remain contexts, never additional machines. Fish login default is explicit on wrath, not inferred for standalone HM outputs ([modules/users/justin/default.nix:7](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/users/justin/default.nix#L7)). Nixible Bash task executables are operational dependencies, not interactive Bash adoption.

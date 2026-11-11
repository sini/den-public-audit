# sonntag__nix: census notes

[Config page](../../configs/sonntag__nix.md) · upstream [sonntag/nix](https://github.com/sonntag/nix) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 816947c6a270; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

One Darwin host plus three real standalone HM outputs coexist with exported Linux profiles (modules/hosts.nix:8; modules/flake/homes.nix:23). Huginn delegates infrastructure to a consuming flake; it is not a local managed host (modules/hosts/huginn/default.nix:2).

## Software selected and host/user traces

All declared justin contexts resolve the same aspect. Fish functions, Helix, tmux, Zellij and Starship modules merge directly onto it, with actual imported TOML/KDL themes inspected (modules/shell/helix.nix:2; modules/shell/starship/default.nix:7). Aerospace applies through den.default.darwin (modules/services/aerospace/default.nix:2).

## Defined, disabled and ambiguous alternatives

The nvim pin is backed by selected package installation and explicit EDITOR, but unread external package internals are not configured-editor evidence (modules/shell/nvim.nix:8). Zed is a cask only. Hyprland has genuine OS/HM definitions but no local selecting target (modules/services/hyprland/default.nix:4). Commented Fish auto-tmux is not active startup (modules/shell/fish/fish.nix:67).

## Machine roles and remaining limits

Wrath has explicit darwin role; physical chassis is unspecified in inspected source. Homes remain contexts, never additional machines. Fish login default is explicit on wrath, not inferred for standalone HM outputs (modules/users/justin/default.nix:7). Nixible Bash task executables are operational dependencies, not interactive Bash adoption.

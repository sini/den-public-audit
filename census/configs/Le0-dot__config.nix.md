# Le0-dot__config.nix: census notes

[Config page](../../configs/Le0-dot__config.nix.md) · upstream [Le0-dot/config.nix](https://github.com/Le0-dot/config.nix) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `4171c4b9f1f2`.

Two NixOS servers and one systemManager Linux desktop environment use different class routes (`modules/infra.nix:2`).

## 2. Software selected and traces

The custom makeHomeEnv bridge explicitly supports systemManager and forwards each user into home-manager.users (`modules/home-manager.nix:10`, `modules/home-manager.nix:24`). Omega has a Home Manager user, while the servers have class user contexts only.

- **zsh / zsh** (configured, home-linux, enabled): The named user selects terminal, supplying substantive Zsh completion/plugins and initialization settings; user-shell is also requested, but its custom-OS login mutation is not established. Evidence: `modules/aspects/terminal/default.nix:27`, `modules/aspects/terminal/default.nix:43`, `modules/infra.nix:33`, `modules/home-manager.nix:10`, `modules/home-manager.nix:23`, `modules/home-manager.nix:32`, `modules/aspects/users/lev.koliadich.nix:6`.
- **starship / starship** (configured, home-linux, enabled): The same selected terminal aspect enables Starship and supplies prompt-format settings. Evidence: `modules/aspects/terminal/default.nix:51`, `modules/aspects/terminal/default.nix:54`, `modules/infra.nix:33`, `modules/home-manager.nix:10`, `modules/home-manager.nix:23`, `modules/home-manager.nix:32`, `modules/aspects/users/lev.koliadich.nix:6`.
- **hyprland / hyprland** (configured, home-linux, enabled): The omega-qualified user aspect selects desktop; the enabled HM compositor consumes tracked native Lua monitor, window and binding settings. Evidence: `modules/aspects/desktop/default.nix:64`, `modules/aspects/desktop/hyprland.lua:5`, `modules/aspects/desktop/hyprland.lua:63`, `modules/infra.nix:33`, `modules/home-manager.nix:10`, `modules/home-manager.nix:23`, `modules/home-manager.nix:32`, `modules/aspects/users/lev.koliadich.nix:6`, `modules/aspects/users/lev.koliadich.nix:17`, `modules/aspects/users/lev.koliadich.nix:19`.
- **neovim / neovim** (configured, home-linux, enabled): The host-qualified user includes the parameterized editor, enabling Neovim and aliases; settings link to an external home checkout, whose native body is not available here. Evidence: `modules/aspects/terminal/neovim.nix:11`, `modules/aspects/terminal/neovim.nix:24`, `modules/infra.nix:33`, `modules/home-manager.nix:10`, `modules/home-manager.nix:23`, `modules/home-manager.nix:32`, `modules/aspects/users/lev.koliadich.nix:6`, `modules/aspects/users/lev.koliadich.nix:22`.
- **neovim / neovim** (default, home-linux, enabled): The selected editor explicitly sets the home EDITOR to the Neovim executable. Evidence: `modules/aspects/terminal/neovim.nix:21`, `modules/infra.nix:33`, `modules/home-manager.nix:10`, `modules/home-manager.nix:23`, `modules/home-manager.nix:32`, `modules/aspects/users/lev.koliadich.nix:6`, `modules/aspects/users/lev.koliadich.nix:22`.
- **neovim / neovim** (installed, nixos, enabled): Nu directly installs Neovim in systemPackages; no editor settings or default are established for its ci context. Evidence: `modules/aspects/hosts/nu.nix:177`, `modules/infra.nix:3`.

## 3. Defined, disabled and ambiguous alternatives

Omega supplies substantive Hyprland Lua and Zsh/Starship settings. Its Neovim native configuration is an out-of-store checkout prerequisite. A user-shell zsh request alone is not treated as a verified login change for the custom systemManager class; the custom account policy defaults account management off (`modules/policies/define-user.nix:7`). No Emacs adoption follows from Zsh emacs keymap.


## 4. Machine roles and limits

Nu and tau select the named server aspect (`modules/aspects/hosts/nu.nix:6`, `modules/aspects/hosts/tau.nix:6`). Omega physical form is unknown: monitor eDP settings are generic native WM configuration, not hardware inventory.

Complete three-host inventory. Nested quadlet/OCI container entities are service instances, not additional managed OS hosts (`modules/infra.nix:6`, `modules/infra.nix:28`).

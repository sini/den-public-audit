# drupol: census notes

[Config page](../../configs/drupol.md) · upstream [drupol/infra](https://github.com/drupol/infra) · [Census summary](../summary.md)

Rev b8cf59f140f5.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-file den config. Each topic is one `den.aspects.<name>` split across many files (e.g. `base` in about 25 files). Ten hosts, each declared in `modules/hosts/<name>/default.nix` with a `den.hosts.<sys>.<name>.users.<user> = {}` line. `_to_migrate/` is skipped by import-tree.

## 2. Software selected and traces
Two selection styles coexist. Apollo, nixos, rpi4 and x1c list aspects in the host aspect `includes` (HM parts reach `pol` through `den.batteries.host-aspects`, `users/pol/default.nix:22`). The other six hosts use `provides.to-users.includes` (also pushing `root` and `user` as user aspects).
- zellij: in `base` (`base/console/console.nix:4`), so every host.
- fish and starship: only the `shell` aspect, which only four hosts include (apollo, nixos, rpi4, x1c); fish is the NixOS default user shell there (`shell/fish.nix:36-37`). The six to-users hosts have no fish, though zellij is configured with fish integration; so bash is their login shell and is not configured.
- vscode and zed (plus gram, antigravity): `dev` aspect, eight hosts.
- KDE Plasma 6 + SDDM: `desktop` aspect (`desktop/environment/default.nix:60-67`), eight hosts; plasma-manager config.
- Default editor is micro (`base/editors/micro.nix:5`), not an IDE.

## 3. Defined / alternatives
No neovim, helix, emacs, tmux, nushell, bash config, sway/hyprland/niri, gnome (only keyring), aerospace or yabai. The private input `infra-private` is guarded at `users/pol/default.nix:28`, so unseen private modules could add more (unresolved, not claimed).

## 4. Roles
Roles come from SMBIOS chassis types in each committed `facter.json` (inferred): x13, x260, x280, x1c, elitebook820 laptops; imac, xeonixos desktops; apollo desktop plus server workload; nixos desktop-chassis headless AI/service host (server inferred); rpi4 headless sensor node (server inferred, weak). No vm or wsl.

# andrewix: census notes

[Config page](../../configs/andrewix.md) · upstream [hoanhxlyn/andrewix](https://github.com/hoanhxlyn/andrewix) · [Census summary](../summary.md)

Rev bd9927ece041.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Selected software and traces](#2-selected-software-and-traces)
- [3. Defined / alternative](#3-defined--alternative)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-parts + import-tree den config. Aspects live in the exported `core` namespace (`modules/namespace.nix:7`), referenced as `<core.x>`. Six hosts are plain data built by a local `mkHost` (`modules/hosts.nix:6-163`); one profile user `andrew` (`modules/_settings.nix:17`) lands on all of them via `mk-host.nix:129`.

## 2. Selected software and traces
Selection chain: `den.hosts."x86_64-linux" = hosts` (`hosts.nix:163`) -> `den.aspects.<host>.provides.to-users.includes` picks `<wsl>`, `<homelab>` or `<workstation>` from facts (`hosts.nix:170-181`) -> `mutual-provider` in `den.default` (`defaults.nix:30`) delivers it to user andrew -> variant lists core aspects (`devices/*.nix`).
- fish: login-shell default through `core.shell` -> `<den/batteries/user-shell> host.defaults.shell` (`shell/default.nix:4`, `_settings.nix:14`); all six hosts.
- neovim: via the nix-wrapper-modules neovim wrapper (`editor/_nwm/wrapper.nix`) with native `config/nvim` lua; all six hosts (workstation, homelab and wsl all include core.editor).
- niri: workstation hosts only (vivo14, msi-gf63, home-pc); `host.wm` defaults to niri.
- Peers: herdr multiplexer (conditional on `terminal.mux`, default herdr), oh-my-posh prompt (no starship).

## 3. Defined / alternative
hyprland (`host.wm` switch, nobody sets it), GNOME/GDM (`core.desktop.de.gnome`, never included), nvf/vscode/cursor (commented out of `core.editor`). `sway.nix` only holds swaylock/swayidle. No tmux, zellij, zsh, bash config, nushell, starship, emacs, helix, zed, KDE, aerospace, yabai.

## 4. Roles
Explicit: vivo14 and msi-gf63 laptop + desktop(workstation); home-pc desktop; asus-rog-gl552vx laptop + server (is-homelab); home-wsl, work-wsl wsl. The homelab laptop includes no desktop aspects despite a comment about niri (`hosts.nix:40`). No inferred roles.

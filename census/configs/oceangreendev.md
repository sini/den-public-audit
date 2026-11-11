# oceangreendev: census notes

[Config page](../../configs/oceangreendev.md) · upstream [OceangreenDev/nix-config](https://github.com/OceangreenDev/nix-config) · [Census summary](../summary.md)

Record: records/oceangreendev.json

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / ambiguous / surprising](#3-defined--ambiguous--surprising)
- [4. Machine roles](#4-machine-roles)

## 1. Project and revision
Dendritic config derived from Doc-Steve's design, den from denful/den (flake.lock rev 8f1a594). Directory names carry platform suffixes (`kde__Nn`, `neovim__n`, `macbook__D`). Hosts: `po3-600` (x86_64 NixOS desktop; users OceanGreenDev and po3-600-admin), `crosswork` (WSL) and `work-macbook` (aarch64-darwin), declared in modules/hosts/*/den.nix.

## 2. Software selected and traces
- **How selection works**: import-tree loads everything (flake.nix); suffixes are not enforced. Hosts include aspects and attach apps to the user through policies of the form `{ user, ... }: den.lib.policy.include {...}` (po3-600/den.nix:32-52; users/oceangreendev/nixos.nix:33-51; homemanager.nix:15-49; macbook users file:22-57). The user-filtered policies only fire for user OceanGreenDev.
- **KDE Plasma 6 (po3-600)**: `<kde>` in nixos.nix:14 -> `services.desktopManager.plasma6.enable` and the Plasma login manager (kde__Nn/default.nix:61-70).
- **zsh**: `user-shell-adv "zsh"` (po3-600/den.nix:40; macbook den.nix:16) sets the login shell and enables zsh at OS and Home level (zsh.nix:14-28), mode default.
- **starship, neovim**: both in `system/types/cli` (system-cli.nix:26,29), included by po3-600 and by work-macbook; neovim sets `defaultEditor = true`.
- **vscode**: `<vscode>` in the user policies of po3-600 (homemanager.nix:37) and the macbook (users file:36).

## 3. Defined / ambiguous / surprising
- **crosswork (WSL)** gets no cli software: its only route is the `systemType = "wsl"` chain in `_system-types.nix`, which import-tree never loads (leading `_`; locked import-tree d321337 default.nix:58 drops paths containing "/_"; nothing imports it). neovim and starship for crosswork are `defined`. The same inert option applies to po3-600 (den.nix:12), which includes the type aspects explicitly (den.nix:25-28).
- **bash** is defined (shell/bash.nix:5) but never included. **hyprland** is an empty stub (hyprland.nix:5).
- crosswork's `wsl/vscode` aspect only provides nix-ld for the Windows VS Code Remote server (wsl-vscode.nix:48), not the editor.
- The macbook includes `neovim__n` and `vscode__nd` modules despite the suffix naming, showing the convention is not enforced.
- No tmux, zellij, fish, nushell, helix, emacs, zed, niri/sway/gnome, aerospace or yabai.

## 4. Machine roles
po3-600 desktop (systemType desktop), crosswork wsl (wsl.enable), work-macbook darwin and laptop (entry named MacBook). The extra admin user on po3-600 has no configured software.

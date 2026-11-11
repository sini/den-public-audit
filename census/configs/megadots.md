# megadots: census notes

[Config page](../../configs/megadots.md) · upstream [tomwrw/megadots](https://github.com/tomwrw/megadots) · [Census summary](../summary.md)

Rev 09aae5c6af50.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-parts + import-tree, den aspects as `den.aspects.<name>` (no namespace). Two hosts, `endgame` and `flatmate`, declared as a block in `modules/den/hosts.nix:47-72`, each with `users.tomwrw = {}`. Role aspects (`base`, `workstation`, `dev`, `gaming`) compose feature aspects.

## 2. Software selected and traces
- zsh: `den.batteries.user-shell "zsh"` plus `shell.zsh` in the user aspect (`users/tomwrw/tomwrw.nix:26,38`); the zsh file deliberately omits `enable` because the battery turns it on (`apps/zsh.nix:37`). starship lives in that same provide (`zsh.nix:51`).
- neovim via nvf (`apps/neovim.nix:87-93`), `defaultEditor = true` -> default editor.
- GNOME + GDM: both hosts include `den.aspects.gnome` directly (`endgame/default.nix:13`, `flatmate/default.nix:12`).
- vscodium: `dev` role -> `provides.to-users` (`roles/dev.nix:15-19`). Same hook also installs claude-code and code-cursor for the user, even though the user aspect does not list them.

## 3. Defined / alternatives
COSMIC (`apps`-level `desktop/cosmic.nix`) is fully defined, never included. No fish, nushell, tmux, zellij, helix, emacs, zed, KDE, niri, hyprland, sway, aerospace, yabai.

## 4. Roles
Both hosts include the repo-defined `workstation` role -> explicit desktop. flatmate also laptop (inferred from the Surface Pro nixos-hardware profile and battery-saving suspend fix). endgame has gaming role and an LTO znver4 kernel; no laptop evidence.


Pinned Home Manager integration spot-check: Integration QC: exact pinned Home Manager 095fef2f265c3c0da4fe315efba8f8a04495ab34 provides programs.vscodium via https://raw.githubusercontent.com/nix-community/home-manager/095fef2f265c3c0da4fe315efba8f8a04495ab34/modules/programs/vscodium.nix lines3-8/14-20; its vscode/mkVscodeModule.nix declares modulePath options at310-311 and gates configuration on cfg.enable at353. Actual extension/user-settings bodies were inspected, not inferred from file length. Substantive settings: `modules/aspects/apps/vscodium.nix:79`, `modules/aspects/apps/vscodium.nix:80`.

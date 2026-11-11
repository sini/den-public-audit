# tomwrw/megadots: census notes

[Config page](../../../configs/tomwrw/megadots.md) · upstream [tomwrw/megadots](https://github.com/tomwrw/megadots) · [Census summary](../../summary.md)

Rev 09aae5c6af50.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-parts + import-tree, den aspects as `den.aspects.<name>` (no namespace). Two hosts, `endgame` and `flatmate`, declared as a block in [`modules/den/hosts.nix:47-72`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/hosts.nix#L47-L72), each with `users.tomwrw = {}`. Role aspects (`base`, `workstation`, `dev`, `gaming`) compose feature aspects.

## 2. Software selected and traces
- zsh: `den.batteries.user-shell "zsh"` plus `shell.zsh` in the user aspect ([`users/tomwrw/tomwrw.nix:26,38`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/users/tomwrw/tomwrw.nix#L26)); the zsh file deliberately omits `enable` because the battery turns it on ([`apps/zsh.nix:37`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/zsh.nix#L37)). starship lives in that same provide ([`zsh.nix:51`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/zsh.nix#L51)).
- neovim via nvf ([`apps/neovim.nix:87-93`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/neovim.nix#L87-L93)), `defaultEditor = true` -> default editor.
- GNOME + GDM: both hosts include `den.aspects.gnome` directly ([`endgame/default.nix:13`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/hosts/endgame/default.nix#L13), [`flatmate/default.nix:12`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/hosts/flatmate/default.nix#L12)).
- vscodium: `dev` role -> `provides.to-users` ([`roles/dev.nix:15-19`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/roles/dev.nix#L15-L19)). Same hook also installs claude-code and code-cursor for the user, even though the user aspect does not list them.

## 3. Defined / alternatives
COSMIC (`apps`-level `desktop/cosmic.nix`) is fully defined, never included. No fish, nushell, tmux, zellij, helix, emacs, zed, KDE, niri, hyprland, sway, aerospace, yabai.

## 4. Roles
Both hosts include the repo-defined `workstation` role -> explicit desktop. flatmate also laptop (inferred from the Surface Pro nixos-hardware profile and battery-saving suspend fix). endgame has gaming role and an LTO znver4 kernel; no laptop evidence.


Pinned Home Manager integration spot-check: Integration QC: exact pinned Home Manager 095fef2f265c3c0da4fe315efba8f8a04495ab34 provides programs.vscodium via https://raw.githubusercontent.com/nix-community/home-manager/095fef2f265c3c0da4fe315efba8f8a04495ab34/modules/programs/vscodium.nix lines3-8/14-20; its vscode/mkVscodeModule.nix declares modulePath options at310-311 and gates configuration on cfg.enable at353. Actual extension/user-settings bodies were inspected, not inferred from file length. Substantive settings: [`modules/aspects/apps/vscodium.nix:79`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/vscodium.nix#L79), [`modules/aspects/apps/vscodium.nix:80`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/vscodium.nix#L80).

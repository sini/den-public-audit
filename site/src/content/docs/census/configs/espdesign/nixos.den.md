---
title: "espdesign/nixos.den: census notes"
---

[Config page](/configs/espdesign/nixosden/) · upstream [espdesign/nixos.den](https://github.com/espdesign/nixos.den) · [Census summary](/census/summary/)

Rev f52aed42f511.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
Plain flake (`evalModules` over import-tree), den via `inputs.den.flakeModule`. One file per feature under `modules/`, host aspects under `modules/hosts/`, all four hosts and their users declared in [`modules/den.nix:18-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L18-L30).

## 2. Software selected and traces
Each host aspect uses `provides.to-users.includes = [...]` (e.g. [`hinekora.nix:15-27`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hosts/hinekora.nix#L15-L27)) so that selected aspects (`cli`, `dev`, `gui-core`, ...) contribute to every user of that host, and `mutual-provider` is set on the user schema ([`den.nix:16`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L16)).
- `cli` (all four hosts): programs.zsh (login shell via `user-shell "zsh"` in both user aspects), starship, neovim with a native init.lua (`EDITOR=nvim`, [`cli.nix:77`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/cli.nix#L77)).
- GNOME: host `includes` on abberath, hinekora, kitava.
- vscodium: `dev` aspect, hinekora and kitava only. valako, the server, still gets zsh/starship/neovim since cli is selected for it.
Surprise: user jake exists only on abberath yet gets the same cli stack as espdesign, because `to-users` fans out per host, not per user.

## 3. Defined / alternatives
ghostty and firefox are in gui-core (terminal/browser, not tracked). No fish, nushell, tmux, zellij, helix, emacs, zed, KDE, niri, hyprland, sway, aerospace, yabai.

## 4. Roles
abberath desktop (explicit comment), kitava desktop (explicit comment), hinekora laptop (inferred from the framework nixos-hardware module and comment), valako server (explicit via hardened-server aspect). The source contains a committed credential (reported privately; not located here).


Pinned Home Manager integration spot-check: Integration QC: exact pinned Home Manager 2c0c1f01521469cf0271180c453c79782d53c2f6 provides programs.vscodium via https://raw.githubusercontent.com/nix-community/home-manager/2c0c1f01521469cf0271180c453c79782d53c2f6/modules/programs/vscodium.nix lines3-8/14-20; its vscode/mkVscodeModule.nix declares modulePath options at310-311 and gates configuration on cfg.enable at353. Actual extension/user-settings bodies were inspected, not inferred from file length. Substantive settings: [`modules/dev.nix:60`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/dev.nix#L60), [`modules/dev.nix:77`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/dev.nix#L77).

---
title: "zakuciael/nixpedition: census notes"
---

[Config page](/configs/zakuciael/nixpedition/) · upstream [zakuciael/nixpedition](https://github.com/zakuciael/nixpedition) · [Census summary](/census/summary/)

Rev b45ae683a1b2.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-file generated flake pinned to vic/den v0.17.0 ([`nix/den.nix:15`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L15)); hosts are clan machines ([`nix/den.nix:20-29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20-L29) sets `intoAttr = [ "clan" "machines" host.name ]`). Namespaces `hardware`, `services`, `virtualisation`. Two hosts: `esquie`, `francois`; users zakuciael (both) and wittano (francois).

## 2. Software selected and traces
Almost no user software. The only shell/editor selections: `user-shell "fish"` for zakuciael ([`users/zakuciael.nix:10`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/users/zakuciael.nix#L10)), `user-shell "bash"` for wittano ([`users/wittano.nix:10`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/users/wittano.nix#L10)), and neovim as a system package + `vim` alias from `den.default` ([`modules/defaults/config.nix:84,139`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/config.nix#L84)). Those user aspects are matched to users by name through `den.hosts.*.users` (`machines/*/default.nix`). Fish is enabled only; nothing configures it.

## 3. Defined / alternatives
`dev` shells embed fish completions for tofu (`services/terranix/global/devshell.nix`) but that is a dev shell, not a managed user. No tmux, zellij, zsh, nushell, starship, helix, vscode, emacs, zed, any WM/DE.

## 4. Roles
francois: server (inferred from services) and vm (inferred from facter kvm). esquie: desktop (inferred from facter chassis Desktop), but no session software. Not stated by source anywhere explicitly.

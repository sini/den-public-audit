# voidlily__dotfiles: census notes

[Config page](../../configs/voidlily__dotfiles.md) · upstream [voidlily/dotfiles](https://github.com/voidlily/dotfiles) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `ef20abb997bd`.

Only Homu is a declared host at this revision; Darwin support lives in reusable aspect bodies (`modules/hosts/homu/homu.nix:4`, `modules/darwin/common.nix:6`).

## 2. Software selected and traces

Homu selects minimal, shell-full and desktop. Explicit host-aspects/mutual-provider route user contributions; Lily selects Zsh login (`modules/den.nix:26`, `modules/hosts/users.nix:8`).

- **kde / plasma6** (configured, nixos, enabled): Homu selects desktop→KDE, bare-enabling Plasma6 and its login manager. Evidence: `modules/desktop/kde.nix:13`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/hosts/homu/homu.nix:14`, `modules/desktop.nix:18`.
- **zsh / zsh** (configured, home-linux, enabled): Selected minimal profile enables substantive Zsh Antidote plugins, aliases and init functions; explicit host-aspects routes HM settings. Evidence: `modules/shell/zsh.nix:17`, `modules/shell/zsh.nix:19`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/hosts/homu/homu.nix:10`, `modules/minimal.nix:17`.
- **zsh / zsh** (default, nixos, enabled): Lily explicitly selects user-shell zsh. Evidence: `modules/hosts/users.nix:8`, `modules/hosts/homu/homu.nix:5`.
- **starship / starship** (configured, home-linux, enabled): Selected minimal enables Starship with substantive Solarized prompt palette and JJ integration. Evidence: `modules/shell/starship.nix:10`, `modules/shell/starship.nix:12`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/minimal.nix:15`.
- **emacs / nix-doom-emacs-unstraightened** (configured, home-linux, enabled): Selected shell-full includes enabled Doom Emacs, consuming tracked Doom module selections and native configuration. Evidence: `modules/emacs.nix:65`, `modules/emacs.nix:68`, `doom.d/init.el:17`, `doom.d/config.el:33`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/hosts/homu/homu.nix:11`, `modules/shell-full.nix:7`, `modules/emacs.nix:15`.
- **other_editor / vim** (configured, home-linux, enabled): Selected minimal writes the tracked substantive vimrc and installs Vim at OS scope. Evidence: `modules/minimal.nix:37`, `vimrc:20`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/hosts/homu/homu.nix:10`.
- **other_editor / vim** (default, home-linux, enabled): Selected Zsh session variables explicitly choose EDITOR=vim, not Emacs. Evidence: `modules/shell/zsh.nix:11`, `modules/den.nix:22`, `modules/den.nix:26`, `modules/den.nix:30`, `modules/hosts/homu/homu.nix:9`, `modules/minimal.nix:17`.

## 3. Defined, disabled and ambiguous alternatives

Doom Emacs is configured, while Vim remains explicit EDITOR. Zellij appears only as a commented future include (`modules/shell-full.nix:23`), not an enabled module. Darwin Emacs-plus/Zsh definitions do not establish Darwin deployment.

- **zsh** (defined, enabled, configured): A live darwinCommon aspect enables OS Zsh but no declared Darwin host selects it. Evidence: `modules/darwin/common.nix:39`.
- **emacs** (defined, enabled, installed): darwinCommon installs Emacs-plus but is not selected by a declared Darwin target. Evidence: `modules/darwin/common.nix:12`.

## 4. Machine roles and limits

Homu selects named desktop profile. VM mount/libvirt host capabilities do not make it a VM. No additional Darwin machine is manufactured from platform support or comments.

Complete one-host literal inventory. Reusable Darwin aspects and emulated build systems add no hosts.

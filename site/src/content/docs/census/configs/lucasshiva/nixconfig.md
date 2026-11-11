---
title: "lucasshiva/nixconfig: census notes"
---

[Config page](/configs/lucasshiva/nixconfig/) · upstream [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig) · [Census summary](/census/summary/)

Record: records/lucasshiva.json

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / disabled / ambiguous](#3-defined--disabled--ambiguous)
- [4. Machine roles](#4-machine-roles)

## 1. Project and revision
Exported `shiv` aspect namespace ([modules/den/namespace.nix:3](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/namespace.nix#L3)) with feature files under modules/features. One user `lucas`, one NixOS host `void` ([modules/hosts/void/void.nix:7](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L7)) and one standalone home `lucas@astra` ([modules/hosts/astra.nix:7](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L7)) for the same machine on CachyOS ([README.md:27-28](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/README.md#L27-L28)). Inventory complete.

## 2. Software selected and traces
- **Shells (bash, zsh, nushell, fish)**: user aspect `lucas` includes `shell` ([lucas.nix:14](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/users/lucas.nix#L14)) whose bundle lists all four ([shell/default.nix:6-9](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/shell/default.nix#L6-L9)); each enables its HM program. zsh is `default` on void because `user-shell "zsh"` ([lucas.nix:16](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/users/lucas.nix#L16)) sets the NixOS login shell; but `bash` execs fish in interactive sessions ([bash.nix:6-11](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/shell/bash.nix#L6-L11)) and kitty is set to the fish package ([void.nix:65](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L65)), so fish is what terminals actually run. On astra the same four are configured with no login-shell control.
- **starship**: [lucas.nix:15](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/users/lucas.nix#L15) -> HM `programs.starship` with bash/zsh/fish/nushell integration.
- **niri**: `desktop.niri` is in both [void.nix:34](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L34) and [astra.nix:39](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L39) ([niri.nix:25-33](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L25-L33)): system-wide pkgs.niri plus HM `programs.niri.enable` ([niri.nix:181](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L181)) with a noctalia shell. Login on void is the noctalia greeter; [niri.nix:60](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L60) force-disables the Plasma login manager.
- **kde (void only)**: `desktop.kde` ([void.nix:33](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L33), also via [niri.nix:27](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L27)) -> `services.desktopManager.plasma6.enable` ([kde.nix:8](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/kde.nix#L8)).
- **zed**: `apps.zed` on both ([void.nix:40](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L40), [astra.nix:25](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L25)), `defaultEditor = true` ([zed.nix:8](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/zed.nix#L8)) -> mode default.
- **neovim**: package in void's homeManager block ([void.nix:72](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L72)), installed only.

## 3. Defined / disabled / ambiguous
- **vscode disabled**: void includes apps.vscode ([void.nix:41](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L41)) but the module sets `programs.vscode.enable = false` ([vscode.nix:5](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/vscode.nix#L5)).
- **gnome** and **COSMIC** are defined ([gnome.nix:8-9](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/gnome.nix#L8-L9), [cosmic.nix:29-32](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/cosmic.nix#L29-L32)) but no host includes them.
- dms.nix is a niri shell alternative also unused (noctalia is the one included).
- No emacs, helix, tmux, zellij, hyprland, sway, aerospace, yabai.

## 4. Machine roles
void: desktop, explicit ([README.md:22](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/README.md#L22),27). astra is the same hardware ([README.md:28](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/README.md#L28)) as a standalone home and is a home-kind target, not a machine. Surprise: the Linux login shell is zsh while the interactive shell is fish.

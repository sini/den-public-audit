# lucasshiva: census notes

[Config page](../../configs/lucasshiva.md) · upstream [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig) · [Census summary](../summary.md)

Record: records/lucasshiva.json

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / disabled / ambiguous](#3-defined--disabled--ambiguous)
- [4. Machine roles](#4-machine-roles)

## 1. Project and revision
Exported `shiv` aspect namespace (modules/den/namespace.nix:3) with feature files under modules/features. One user `lucas`, one NixOS host `void` (modules/hosts/void/void.nix:7) and one standalone home `lucas@astra` (modules/hosts/astra.nix:7) for the same machine on CachyOS (README.md:27-28). Inventory complete.

## 2. Software selected and traces
- **Shells (bash, zsh, nushell, fish)**: user aspect `lucas` includes `shell` (lucas.nix:14) whose bundle lists all four (shell/default.nix:6-9); each enables its HM program. zsh is `default` on void because `user-shell "zsh"` (lucas.nix:16) sets the NixOS login shell; but `bash` execs fish in interactive sessions (bash.nix:6-11) and kitty is set to the fish package (void.nix:65), so fish is what terminals actually run. On astra the same four are configured with no login-shell control.
- **starship**: lucas.nix:15 -> HM `programs.starship` with bash/zsh/fish/nushell integration.
- **niri**: `desktop.niri` is in both void.nix:34 and astra.nix:39 (niri.nix:25-33): system-wide pkgs.niri plus HM `programs.niri.enable` (niri.nix:181) with a noctalia shell. Login on void is the noctalia greeter; niri.nix:60 force-disables the Plasma login manager.
- **kde (void only)**: `desktop.kde` (void.nix:33, also via niri.nix:27) -> `services.desktopManager.plasma6.enable` (kde.nix:8).
- **zed**: `apps.zed` on both (void.nix:40, astra.nix:25), `defaultEditor = true` (zed.nix:8) -> mode default.
- **neovim**: package in void's homeManager block (void.nix:72), installed only.

## 3. Defined / disabled / ambiguous
- **vscode disabled**: void includes apps.vscode (void.nix:41) but the module sets `programs.vscode.enable = false` (vscode.nix:5).
- **gnome** and **COSMIC** are defined (gnome.nix:8-9, cosmic.nix:29-32) but no host includes them.
- dms.nix is a niri shell alternative also unused (noctalia is the one included).
- No emacs, helix, tmux, zellij, hyprland, sway, aerospace, yabai.

## 4. Machine roles
void: desktop, explicit (README.md:22,27). astra is the same hardware (README.md:28) as a standalone home and is a home-kind target, not a machine. Surprise: the Linux login shell is zsh while the interactive shell is fish.

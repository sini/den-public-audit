# quasigod-xyz-nixconfig: census notes

[Config page](../../configs/quasigod-xyz-nixconfig.md) · upstream [quasigod.xyz/nixconfig](https://tangled.org/quasigod.xyz/nixconfig) · [Census summary](../summary.md)

Rev 570018d633c7.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
import-tree den config with exported `styx` namespace. Two hosts (hades desktop, zagreus Framework laptop) and one user aspect `quasi` (`modules/quasi.nix:3`). The review notes both hosts fail to evaluate on current inputs; this census reads source only.

## 2. Software selected and traces
Selection is entirely in the user aspect `quasi` (`quasi.nix:4-37`), applied to both hosts because each declares `users.quasi`. Host aspects add only roles (`desktop` on hades, `laptop` on zagreus) and gaming variants.
- helix (default editor via EDITOR/VISUAL), emacs (daemon), niri (+ noctalia), fish, bash, starship (through `shell/full`), nushell.
- Shell arrangement is unusual: login shell is dash (`apps/nushell.nix:9`) and its rc file execs nu (`nushell.nix:15-20`), so nushell is the effective interactive shell while fish and bash remain configured but secondary.
- zellij and herdr arrive only as packages inside `dev._.ai` (`ai.nix:21-22`), reached from `styx/dev` (`quasi.nix:21`); no multiplexer config. Not counted as configured.

## 3. Defined / alternatives
COSMIC (`modules/cosmic.nix`) is fully defined and unreferenced. wezterm and ghostty are terminals. No tmux, neovim, vscode, zed, KDE, GNOME session (only dconf color-scheme), hyprland, sway.

## 4. Roles
hades desktop (explicit, `styx.desktop`), zagreus laptop (explicit, `styx.laptop`; its role also pulls the workstation bundle, recorded as desktop too). No servers or VMs; microvm host support only (`modules/microvm.nix`).

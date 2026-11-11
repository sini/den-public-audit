# henriquekirchheck__nixos-flake: census notes

[Config page](../../configs/henriquekirchheck__nixos-flake.md) · upstream [henriquekirchheck/nixos-flake](https://github.com/henriquekirchheck/nixos-flake) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `f9b5451633a4`.

Typed per-host settings feed aspects selected by Lina and Maria. Both literal hosts are x86 Linux NixOS (`modules/hosts/artemis/config.nix:3`, `modules/hosts/athena/config.nix:3`).

## 2. Software selected and traces

Dendritic root and host-aspects wire named inventory/aspects (`modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`). Lina selects Niri, Fish, Starship, Neovim and Zed; Maria selects Plasma only on Athena. Niri collector merges actual emitter lists into settings (`modules/aspects/apps/window-managers/niri.nix:247`); Zed collector does likewise (`modules/aspects/apps/development/editors/zed.nix:237`).

- **fish / fish** (configured, home-linux, enabled): Lina explicitly includes this aspect on both declared Home Manager contexts. Fish has greeting/plugins settings. Evidence: `modules/aspects/apps/sh/shells/fish.nix:13`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`, `modules/users/lina/config.nix:55`.
- **starship / starship** (configured, home-linux, enabled): Lina explicitly includes this aspect on both declared Home Manager contexts. Prompt format and module settings are supplied. Evidence: `modules/aspects/apps/sh/utils/starship.nix:4`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`, `modules/users/lina/config.nix:59`.
- **neovim / neovim** (configured, home-linux, enabled): Lina explicitly includes this aspect on both declared Home Manager contexts. The current native editor contribution only enables Neovim; the NVF input is not selected as a frontend. Evidence: `modules/aspects/apps/development/editors/neovim.nix:20`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`, `modules/users/lina/config.nix:66`.
- **zed / zed** (configured, home-linux, enabled): Lina explicitly includes this aspect on both declared Home Manager contexts. Zed supplies substantive settings, keymaps and an extension/settings collector. Evidence: `modules/aspects/apps/development/editors/zed.nix:33`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`, `modules/users/lina/config.nix:67`.
- **niri / niri** (configured, home-linux, enabled): Lina explicitly includes this aspect on both declared Home Manager contexts. Niri supplies substantive layout/input settings plus collected rules and binds; peripheral values come from each host settings. Evidence: `modules/aspects/apps/window-managers/niri.nix:164`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`, `modules/users/lina/config.nix:51`.
- **fish / fish** (default, nixos, enabled): Lina explicitly requests user-shell fish; Maria has no corresponding choice. Evidence: `modules/users/lina/config.nix:6`, `modules/inputs/den.nix:9`, `modules/inputs/den.nix:15`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/users/lina/config.nix:4`.
- **bash / bash** (configured, home-linux, enabled): The global default selects Bash with substantive history/completion settings for every declared HM user context; Maria exists only on Athena. Evidence: `modules/aspects/apps/sh/shells/bash.nix:9`, `modules/aspects/apps/sh/shells/bash.nix:3`, `modules/hosts/artemis/config.nix:7`, `modules/hosts/athena/config.nix:8`, `modules/hosts/athena/config.nix:9`.
- **kde / kde** (configured, nixos, enabled): Maria selects Plasma6 with package exclusions; its OS contribution provides the family laptop desktop alongside Lina Niri. Evidence: `modules/aspects/apps/window-managers/plasma.nix:6`, `modules/aspects/apps/window-managers/plasma.nix:7`, `modules/hosts/athena/config.nix:9`, `modules/users/maria/config.nix:25`.

## 3. Defined, disabled and ambiguous alternatives

Zsh and Emacs remain live defined alternatives. Commented Emacs selection is not adoption. Neovim is enable-only; the NVF pin supplies no NVF config. Bash default applies to all three user contexts. Niri GNOME portal use does not establish GNOME desktop.

- **emacs** (defined, enabled, configured): The Emacs aspect supplies a daemon/client package setup, but Lina selection is commented and Maria never includes it. Evidence: `modules/aspects/apps/development/editors/emacs.nix:35`.
- **zsh** (defined, enabled, configured): A substantial Zsh aspect exists but is absent from both user include lists. Evidence: `modules/aspects/apps/sh/shells/zsh.nix:16`.

## 4. Machine roles and limits

Athena is explicitly a shared family laptop; Artemis explicitly also serves as server. The family accounts are configured contexts, not a census of unique humans.

Complete two-host inventory with Lina on both and Maria on Athena. No standalone homes or configured package outputs are declared.

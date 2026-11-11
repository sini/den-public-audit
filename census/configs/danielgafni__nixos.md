# danielgafni__nixos: census notes

[Config page](../../configs/danielgafni__nixos.md) · upstream [danielgafni/nixos](https://github.com/danielgafni/nixos) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 26f03bc416ad; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three declared OS hosts and four standalone homes, explicitly separated by modules/den.nix:101/114. Embedded HM is disabled (den.nix:21/98). MacBook deliberately has no OS users (den.nix:107); dan@MacBook remains an independent home context.

## Software selected and host/user traces

Standalone home aspects explicitly choose dan-linux, underdel-linux or dan-darwin (modules/den.nix:116-120). Each selects shared shell/CLI: substantive Zsh/Starship and enable-only Zellij. Dan alone selects Nixvim/Zed/Helix/Cursor (modules/aspects/users/dan.nix:15-18). Linux homes select shared-hm-linux→Hyprland (modules/aspects/features/shared-hm.nix:13); Darwin dan selects AeroSpace at modules/aspects/users/darwin/dan.nix:9. Den home context injects exact hostData/userData at den.nix:89/90.

## Defined, disabled and ambiguous alternatives

These are home-linux/home-darwin contributions, not HM hosted by NixOS: no host class leakage was assumed. NixOS hosts independently select nixos-system, which enables Hyprland/Zsh and sets greetd Hyprland default plus login Zsh (modules/aspects/features/nixos/system.nix:69/171/278/281). UnderDel shell still says EDITOR=nvim although it does not select Neovim; this is recorded only as preference, not editor configuration. Cursor package is optional named editor; Ghostty enableFishIntegration is not Fish adoption. Native Helix settings were read at modules/aspects/features/editors/helix-config.toml:3.

## Machine roles and remaining limits

Framnix explicitly uses Framework laptop hardware (modules/aspects/hosts/framnix.nix:26/39); MacBook name and Darwin architecture establish laptop/Darwin. DanPC chassis is left unknown. Home targets do not add physical machines; repeated dan accounts are contexts, not distinct people. Static class/data dispatch and settings reachability were read without evaluation/runtime tests.

---
title: "hmajid2301/nixicle: census notes"
---

[Config page](/configs/hmajid2301/nixicle/) · upstream [hmajid2301/nixicle](https://github.com/hmajid2301/nixicle) · [Census summary](/census/summary/)

Revision `ca0d927add73`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six managed host roots (five x86_64 plus RPi) and three standalone Linux homes are declared in [modules/hosts.nix:198](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/hosts.nix#L198) and [modules/hosts.nix:244](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/hosts.nix#L244). The Dell identity is haseebmajid, while framework/desktop homes use haseeb; neither proves distinct humans.

## Software selected and host/user traces

Hosted HM class default is explicit ([modules/defaults.nix:44](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/defaults.nix#L44)). Framework/desktop/VM named providers select desktopProfile, and Dell identity directly selects it; profile then composes common/development/Niri. Exact Den bf2504f9f2e8621fee091335132ab3ae698cf808 provider source https://raw.githubusercontent.com/denful/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/aspects/fx/aspect/provide.nix was read: upstream47-50 matches host/user and includes results. This is built-in delivery, not an assumed missing mutual-provider shim.

## Defined, disabled and ambiguous alternatives

Fish native initialization, locally wrapped Neovim Lua, rich Zellij and Niri are selected by desktop contexts. Desktop profile alone adds Helix ([hosts/desktop/default.nix:15](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/hosts/desktop/default.nix#L15)). VPS uses its own targeted Fish/prompt/history and package-only tmux/Neovim list ([modules/hosts.nix:184](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/hosts.nix#L184); [modules/hosts.nix:188](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/hosts.nix#L188)). Native server-admin account defaults to nixos and Fish, distinct from Den haseeb. NAS rich host Fish HM has no explicit projection consumer, while direct user-shell still enables bare HM Fish. Zsh and rich tmux are unselected alternatives; shell integration comments/plugins are not extra shell adoption.

## Machine roles and remaining unknowns

Framework explicitly isLaptop=true; VM has qemuGuest, desktop uses named desktop inventory/profile, NAS/VPS/RPi select server profiles. Standalone homes can describe existing hardware and never inflate host count. Native nixos account is established by enabled server-admin option, not guessed from tty-autologin comments. Other package outputs and ISO tree are not exhaustively inventoried.

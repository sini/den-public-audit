---
title: "Occhima/nix-conf: census notes"
---

[Config page](/configs/occhima/nix-conf/) · upstream [Occhima/nix-conf](https://github.com/Occhima/nix-conf) · [Census summary](/census/summary/)

Revision `201ebbb67074`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six host targets include four user-bearing NixOS configurations, a Voyager installer builder, and a custom nixOnDroid phone. Two standalone homes include phone-home, which is also imported into the Droid host ([modules/den/aspects/hosts/phone/phone.nix:14](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/aspects/hosts/phone/phone.nix#L14)). They are not additional physical machine claims.

## Software selected and host/user traces

Local hm/name adapter directly imports `flake.modules.homeManager.<name>` ([modules/den/namespaces.nix:13](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/namespaces.nix#L13)). Occhima directly selects home, local Nixvim package, shell and Doom ([modules/den/aspects/users/occhima.nix:43](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/aspects/users/occhima.nix#L43)). Phone-home independently selects only home/Nixvim/shell. Graphical host policy requires host.hasAspect graphical; workstation hosts establish this locally, and the unqualified standalone home receives null host, which passes the same guard. Exact bf2504f9 home.nix:60–89 was read at https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/entities/home.nix ; an unqualified home receives null host, satisfying the explicit desktop guard. This resolves the standalone Hyprland ambiguity.

## Defined, disabled and ambiguous alternatives

Nixvim is locally configured via merged flake modules ([modules/flake/nixvim/opts.nix:23](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/flake/nixvim/opts.nix#L23)), then installed as the local nvim package by HM. Doom supplies native config and daemon defaultEditor ([modules/home-manager/editor/emacs/daemon.nix:21](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/home-manager/editor/emacs/daemon.nix#L21)); Zsh account default coexists with configured Zellij and actual Starship TOML. Niri, Nushell and VSCodium are live unselected alternatives, not adoption inferred from theme hooks. Hyprland HM is directly selected on the three graphical workstation targets. Exact pinned built-in to-hosts dispatch also imports display-hyprland into the three graphical host OS configurations; its native module enables Hyprland and supplies greetd environment choice.

## Machine roles and remaining unknowns

Source explicitly identifies aerodynamic laptop, beyond/steammachine gaming desktops and crescendoll WSL. Voyager explicitly is not a real machine ([modules/den/aspects/hosts/voyager/voyager.nix:1](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/aspects/hosts/voyager/voyager.nix#L1)). Phone has custom Droid class, no forced laptop/desktop role. Per-system Nixvim outputs use an external systems input ([modules/flake/systems.nix:5](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/flake/systems.nix#L5)), so package system inventory remains unresolved rather than inventing package target keys.

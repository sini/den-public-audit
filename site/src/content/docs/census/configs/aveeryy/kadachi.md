---
title: "aveeryy/kadachi: census notes"
---

[Config page](/configs/aveeryy/kadachi/) · upstream [aveeryy/kadachi](https://github.com/aveeryy/kadachi) · [Census summary](/census/summary/)

Revision `ba03c6ede780`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six x86_64 NixOS hosts are declared under hosts/*/system.nix. Custom namespaces separate host compositions, reusable user features and machine-role features ([dendritic.nix:28](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/dendritic.nix#L28)).

## Software selected and host/user traces

Schema host/user aspects are explicitly remapped into the hosts namespace ([defaults/misc.nix:14](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/defaults/misc.nix#L14); [defaults/misc.nix:18](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/defaults/misc.nix#L18)), with HM class17, host-aspects26 and mutual-provider27. Each user tree selects kasane/base-user -> Zsh. The same user trees directly select Hyprland for malfestio/mizuki/totsugeki, so their host/user display guards are traceable without guessing a default provider.

## Defined, disabled and ambiguous alternatives

Zsh is the OS defaultUserShell with substantive home init ([aspects/kasane/zsh.nix:12](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/kasane/zsh.nix#L12); [aspects/kasane/zsh.nix:20](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/kasane/zsh.nix#L20)). Starship has a real add_newline setting ([aspects/kasane/zsh.nix:51](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/kasane/zsh.nix#L51)). Global kadachi-nvim is an external package selection plus explicit EDITOR=nvim ([defaults/nvim.nix:12](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/defaults/nvim.nix#L12); [defaults/nvim.nix:15](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/defaults/nvim.nix#L15)); its external native configuration is not claimed as inspected. Malfestio explicitly sets the Jovian desktopSession to hyprland-uwsm ([hosts/malfestio/system.nix:50](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/hosts/malfestio/system.nix#L50)). Generic uwsm start default on other hosts does not name a compositor, so no extra Hyprland default is inferred.

## Machine roles and remaining unknowns

greatyamada/hatsune/nightcord explicitly select server; mizuki/totsugeki explicitly select desktop roles. Malfestio is a Steam Deck ([hosts/malfestio/system.nix:29](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/hosts/malfestio/system.nix#L29)), a handheld without a dedicated census role; it is not forced to laptop. Unselected WSL feature is not a WSL target. Private secrets and external Neovim package remain dependencies; unrelated per-system packages are not exhaustively inventoried.

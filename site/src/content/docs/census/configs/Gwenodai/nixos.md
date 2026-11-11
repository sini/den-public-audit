---
title: "Gwenodai/nixos: census notes"
---

[Config page](/configs/gwenodai/nixos/) · upstream [Gwenodai/nixos](https://github.com/Gwenodai/nixos) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: ab05d3c6e156; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three explicit x86_64 NixOS targets, with hardware facts and per-user named providers. Inventory is declared in each `modules/hosts/<name>/main.nix:11` and hardware.nix:6. HM user classes are explicit in [modules/schema/defaults.nix:23](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/schema/defaults.nix#L23).

## Software selected and host/user traces

All hosts select system-type.basic directly or through desktop-gaming inheritance ([modules/system-types/system-types.nix:39](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/system-types/system-types.nix#L39)/63); basic includes Zsh/Bash/Starship at24/25/27. Each selected user includes host-aspects ([modules/users/gwen/gwen.nix:5](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/users/gwen/gwen.nix#L5); [modules/users/stacy/stacy.nix:5](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/users/stacy/stacy.nix#L5)), making those HM bodies active. Gwen-t1 and stacy-pc named user providers select environment.niri and vscode.config; ymir provider is empty ([modules/hosts/ymir/main.nix:41](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/hosts/ymir/main.nix#L41)).

## Defined, disabled and ambiguous alternatives

Exact locked Den [provider implementation](https://raw.githubusercontent.com/vic/den/3932adfe8ef02d322168aa5b07d9371d8ec1664d/nix/lib/aspects/fx/aspect/provide.nix) matches named providers to host/user scopes (lines47-50); mutual-provider is already built-in at this pin. The [user-shell battery](https://raw.githubusercontent.com/vic/den/3932adfe8ef02d322168aa5b07d9371d8ec1664d/modules/aspects/batteries/user-shell.nix) assigns Zsh login shell (line20). Niri HM activation was checked against the [pinned niri-flake](https://raw.githubusercontent.com/cmm/niri-flake/0d251ae03aa211fb241b1958e06f250c51980a96/flake.nix): OS module injects config module at518-520; config writes KDL when finalConfig is nonnull at430-434. Thus absent HM enable is not an unresolved guard here. VSCode MIME defaults are explicit; GNOME utilities/portals and KDE Connect are not full desktops.

## Machine roles and remaining limits

All roles are explicit hardware.platform values at each hardware.nix:8: gwen-t1/stacy-pc desktop, ymir server. No additional homes or package targets were declared. Ymir root filesystem is a temporary stub ([modules/hosts/ymir/configuration/filesystem/filesystem.nix:5](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/hosts/ymir/configuration/filesystem/filesystem.nix#L5)), so reachability does not establish a successfully booted machine. User names denote configured contexts only.

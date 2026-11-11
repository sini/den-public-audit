---
title: "DJ-Laser/nixos: census notes"
---

[Config page](/configs/dj-laser/nixos/) · upstream [DJ-Laser/nixos](https://github.com/DJ-Laser/nixos) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: 27e216e2f9d3; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

A two-host NixOS desktop configuration and explicit standalone home, rooted in [flake.nix:5](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/flake.nix#L5) import-tree. Hosts declare the same dj_laser HM-enabled user ([modules/hosts/laser-book/configuration.nix:11](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/laser-book/configuration.nix#L11); [modules/hosts/nix-desktop/configuration.nix:11](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L11)); [modules/users/dj_laser.nix:5](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L5) adds the standalone home.

## Software selected and host/user traces

The shared user aspect directly includes scrolling-wm and vscode ([modules/users/dj_laser.nix:13](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L13)/14), so all three contexts reach actual HM Niri bindings/layout and VSCode FHS settings. These are substantial application settings, not input-pin adoption. Bash is enabled by the selected user-shell battery at [modules/users/dj_laser.nix:10](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L10), with explicit login default only on host user contexts.

## Defined, disabled and ambiguous alternatives

The exact locked Den battery [user-shell.nix](https://raw.githubusercontent.com/vic/den/37eb88ce28a9e42d5b367b967a9097030ff4f665/modules/aspects/batteries/user-shell.nix) enables HM shell (line31) and assigns OS user shell (line20). This establishes activation, but local Bash configuration remains enable-only. Greetd remembers the user session ([modules/system/greeter.nix:14](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/system/greeter.nix#L14)), which does not prove Niri is the default. The selected default editor is Vim ([modules/system/system-cli.nix:38](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/system/system-cli.nix#L38)), outside required editor families.

## Machine roles and remaining limits

Nix-desktop is explicitly named desktop ([modules/hosts/nix-desktop/configuration.nix:9](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L9)); laser-book laptop is inferred from its Framework hardware selection ([modules/system/framework.nix:20](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/system/framework.nix#L20)). The standalone home is no additional machine, and repeated dj_laser contexts are not distinct humans. Static selection does not prove activation success.

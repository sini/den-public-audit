---
title: "scoiatael/dotfiles: census notes"
---

[Config page](/configs/scoiatael/dotfiles/) · upstream [scoiatael/dotfiles](https://github.com/scoiatael/dotfiles) · [Census summary](/census/summary/)

Revision `b1b3cc10eef1`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Five host roots plus a standalone LsAir home are declared; the home does not represent an extra Mac. Source exposes legacy module paths through a dotfiles battery ([modules/den.nix:38](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/den.nix#L38)); exposure alone is not selection.

## Software selected and host/user traces

Identity lukaszczaplinski directly includes Neovim and imports Zsh/tmux ([modules/aspects/lukaszczaplinski.nix:12](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lukaszczaplinski.nix#L12); [modules/aspects/lukaszczaplinski.nix:18](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lukaszczaplinski.nix#L18)). Host named providers add Doom/Fish/Niri/Zellij. Exact locked Den631b034cf8d607b8b6f4b68c2f93fc2b3be64cce was read at https://raw.githubusercontent.com/denful/den/631b034cf8d607b8b6f4b68c2f93fc2b3be64cce/nix/lib/aspects/fx/aspect/provide.nix ; upstream47-50 matches host/user identities and includes provider results. HM classes are local [modules/den.nix:19](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/den.nix#L19). This supports named delivery without assuming current Den.

## Defined, disabled and ambiguous alternatives

Both Macs import actual AeroSpace TOML; old Yabai is unselected. Linux Framework/tabletop receive Niri, while Framework also directly enables Plasma ([modules/aspects/lsframework.nix:307](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lsframework.nix#L307)) and tabletop directly enables Budgie ([modules/aspects/tabletop-nixos.nix:91](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/tabletop-nixos.nix#L91)). Multiple desktops are availability, not a chosen default. Doom provider sets EDITOR on Macs ([modules/aspects/doomemacs.nix:76](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/doomemacs.nix#L76)); Linux provider selects Neovim editor command ([modules/aspects/lsframework.nix:24](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lsframework.nix#L24)). Legacy Helix/VSCodium/Sway definitions are retained but unselected. Server CLI installs Fish/Helix only.

## Machine roles and remaining unknowns

Framework explicit desktop hardware ([modules/aspects/lsframework.nix:43](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lsframework.nix#L43)) also runs inferred server workloads. sd-161581 coherently hosts services, supporting inferred server. Other physical forms remain unknown despite Mac names and graphical configuration. Native service accounts are not human counts. Package outputs and legacy optional peer configurations are not exhaustively inventoried; mutable Doom/native configs remain activation prerequisites.

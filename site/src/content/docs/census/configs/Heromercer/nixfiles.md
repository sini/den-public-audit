---
title: "Heromercer/nixfiles: census notes"
---

[Config page](/configs/heromercer/nixfiles/) · upstream [Heromercer/nixfiles](https://github.com/Heromercer/nixfiles) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: 72d86dd2774f; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three NixOS hosts with alec user contexts declared at [modules/hosts/hosts.nix:3](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/hosts/hosts.nix#L3). The private mercer namespace ([modules/den.nix:12](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/den.nix#L12)) separates reusable roles/features from actual entity aspects. No standalone homes are declared.

## Software selected and host/user traces

HM is explicitly enabled for users at [modules/den.nix:17](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/den.nix#L17). Schema-level includes make Fish and Doom Emacs common to all three ([modules/core/fish.nix:6](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/core/fish.nix#L6); [modules/core/emacs/default.nix:7](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/core/emacs/default.nix#L7)). Host to-users providers select Niri on firelink/majula and the server role on tower; server includes NVF at [modules/hosts/systems.nix:42](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/hosts/systems.nix#L42). Login Fish selection is explicit at [modules/user/user.nix:7](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/user/user.nix#L7), and global EDITOR=emacs at [modules/defaults.nix:22](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/defaults.nix#L22).

## Defined, disabled and ambiguous alternatives

Starship is a substantive but unselected namespace definition ([modules/features/starship.nix:2](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/features/starship.nix#L2)); installing Tide in [modules/core/fish.nix:35](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/core/fish.nix#L35) is not proof of prompt activation. Hyprland is unselected and explicitly disabled ([modules/features/hyprland/default.nix:14](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/features/hyprland/default.nix#L14)). Niri HM configuration was checked against [locked niri-flake](https://raw.githubusercontent.com/sodiboo/niri-flake/9ee3e13b60643448228353097880521658b2fe0e/flake.nix): homeModules.niri imports config at548-549, whose KDL output is guarded only by finalConfig!=null at442-445. The [locked Den shell battery](https://raw.githubusercontent.com/vic/den/0f7675b0b789eabe1a62f8a31b5323a7ad3ca5c4/modules/aspects/batteries/user-shell.nix) assigns login shell at20 and enables HM shell at32.

## Machine roles and remaining limits

Roles are explicit selected desktop/laptop/server profiles at [modules/hosts/firelink/firlink.nix:13](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/hosts/firelink/firlink.nix#L13), [modules/hosts/majula/majula.nix:13](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/hosts/majula/majula.nix#L13) and [modules/hosts/tower/tower.nix:8](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/hosts/tower/tower.nix#L8). Tower runs server role plus GUI-capable common Emacs because that user schema is unconditional; no server/editor exclusion was invented. Runtime success and actual users are outside this static census.

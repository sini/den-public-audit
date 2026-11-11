---
title: "AnonymousRand/nix_config: census notes"
---

[Config page](/configs/anonymousrand/nix_config/) · upstream [AnonymousRand/nix_config](https://github.com/AnonymousRand/nix_config) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: 583567f25d10; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

A custom two-axis profile/syst configuration, imported through [outputs.nix:1](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/outputs.nix#L1). The single NixOS machine snow-rainbow and two standalone homes are explicitly declared in [modules/systs/snow-rainbow/default.nix:8](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/snow-rainbow/default.nix#L8)/27 and [modules/systs/work-vm/default.nix:8](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/work-vm/default.nix#L8).

## Software selected and host/user traces

User schema selects profiles.meow at [modules/profiles/internal/entities_from_aspects.nix:15](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/internal/entities_from_aspects.nix#L15); home schema does so independently at [modules/systs/internal/entities_from_aspects.nix:41](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/internal/entities_from_aspects.nix#L41). Profile includes Bash/Fish/Niri at [modules/profiles/meow/default.nix:13](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/meow/default.nix#L13)/19/20. All three targets receive active substantial HM shell settings and native Niri assets. Syst context policies at [modules/systs/internal/ctx_from_entities.nix:17](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/internal/ctx_from_entities.nix#L17)/24 resolve graphics guards using each named syst.

## Defined, disabled and ambiguous alternatives

Both shell modules enable their corresponding settings: Bash aliases/history/init at [modules/profiles/meow/features/terminal/bash.nix:5](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/meow/features/terminal/bash.nix#L5) and Fish native initialization at [modules/profiles/meow/features/terminal/fish/fish.nix:9](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/meow/features/terminal/fish/fish.nix#L9). Neither establishes an OS login default. The Neovim placeholder modules/features/editors/_neovim.nix is empty, so it is not a live editor definition; Vim is the actual editor selected at [modules/profiles/meow/default.nix:24](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/meow/default.nix#L24). Work-vm graphics.supported=true ([modules/systs/work-vm/settings/syst_settings/capabilities/graphics.nix:4](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/work-vm/settings/syst_settings/capabilities/graphics.nix#L4)) wins over the nearby descriptive comment about not installing a WM.

## Machine roles and remaining limits

Snow-rainbow is explicitly a desktop ([modules/systs/snow-rainbow/README.md:3](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/systs/snow-rainbow/README.md#L3)). Work-vm is only a home target, so its name does not create a VM host count. The home and integrated user contexts are recorded separately, not as distinct people. Static settings reachability does not prove successful module evaluation or running sessions.

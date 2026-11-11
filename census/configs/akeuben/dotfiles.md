# akeuben/dotfiles: census notes

[Config page](../../../configs/akeuben/dotfiles.md) · upstream [akeuben/dotfiles](https://github.com/akeuben/dotfiles) · [Census summary](../../summary.md)

Revision `48183786da04`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Four NixOS hosts share core tooling, split between HTPC Bigscreen and desktop/development profiles ([modules/host/ds9/default.nix:7](https://github.com/akeuben/dotfiles/blob/48183786da040379d88ad2f23dbdc796de4093dc/modules/host/ds9/default.nix#L7); [modules/host/enterprise/default.nix:9](https://github.com/akeuben/dotfiles/blob/48183786da040379d88ad2f23dbdc796de4093dc/modules/host/enterprise/default.nix#L9)).

## Software selected and host/user traces

Named host aspects explicitly select core; wrapped Neovim/Tmux packages carry native configs ([modules/feature/core.nix:9](https://github.com/akeuben/dotfiles/blob/48183786da040379d88ad2f23dbdc796de4093dc/modules/feature/core.nix#L9); [modules/config/tmux/default.nix:17](https://github.com/akeuben/dotfiles/blob/48183786da040379d88ad2f23dbdc796de4093dc/modules/config/tmux/default.nix#L17)). HTPC selection explicitly sets default Bigscreen session, whereas desktop Hyprland is only enabled, not proven default. Exact pinned dependency verified statically: https://raw.githubusercontent.com/vic/den/f88d635baecb9f9a82e8b78002cfd28e940c187b/nix/lib/aspects/fx/aspect/provide.nix, lines21–27 directly dispatch to-users/to-hosts as include effects. Local flake.lock binds this revision. Missing mutual-provider is not a blocker; it is an inert compatibility shim in these pins.

## Defined, disabled and ambiguous alternatives

Provider-only uncertainties were resolved against the exact locked Den implementation. Explicit to-users contributions above are selected where the complete local host/profile/user/HM-class chain is cited. Direct host homeManager content still requires a separate projection route; this conclusion does not infer one.

## Machine roles and remaining unknowns

Avery/htpc are configured account contexts, not distinct humans. Named desktop role is explicit for voyager/enterprise; HTPC role is not forced into an unsupported physical chassis label. All four host entries enumerated; standalone perSystem wrapper package outputs have inherited systems and are not fully inventoried.

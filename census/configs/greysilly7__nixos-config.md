# greysilly7__nixos-config: census notes

[Config page](../../configs/greysilly7__nixos-config.md) · upstream [greysilly7/nixos-config](https://github.com/greysilly7/nixos-config) · [Census summary](../summary.md)

Record: evidence JSON. Revision: `955ea2336310`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Four host targets include one Darwin MacBook, a gaming laptop and two service/VM systems (modules/hosts/hosts.nix:2). Users explicitly include a Time Machine backup account tm, which is not labeled a human (modules/users/tm/tm.nix:7).

## Software selected and host/user traces

Host presets/providers → basic → shell → explicit child enumeration configures Bash/Zsh/Starship for the declared HM contexts (modules/system/system-presets/system-type/system-type.nix:14; modules/programs/shell/!includes.nix:9). mutual-provider is global (modules/core/defaults.nix:6). Gaming laptop explicitly selects Niri; its preset both includes the actual enable aspect and sets defaultSession (modules/hosts/gaminglaptop/default.nix:15; modules/system/system-presets/desktop-type/desktop-type.nix:16). MacBook selects Aerospace at modules/hosts/Scotts-MacBook-Pro/default.nix:7.

## Defined, disabled and ambiguous alternatives

Two server providers install Neovim; MacBook provider installs VSCodium, and its Homebrew list installs Helix (modules/hosts/greyserver/default.nix:33; modules/hosts/ultra-channel-7747/default.nix:25; modules/hosts/Scotts-MacBook-Pro/default.nix:18; modules/hosts/Scotts-MacBook-Pro/default.nix:74). Generic Zed/Helix leaf definitions are not proof the generic editors bundle is selected. Zsh is configured, but the actual user-shell expression chooses Bash despite a stale zsh comment (modules/users/users.nix:7, modules/users/users.nix:8). GNOME portal backend names in modules/window-managers/niri/config.nix:38 do not enable the GNOME desktop.

## Machine roles and remaining limits

Roles follow clearly named inventory entries and selected desktop presets. VM role is explicit for greyserver and ultra-channel from guest comments (modules/hosts/greyserver/default.nix:60; modules/hosts/ultra-channel-7747/default.nix:71); ultra-channel server role is separately inferred from proxy workload. MacBook name supports explicit laptop role and its system gives darwin. Niri class forwarding has an options guard (modules/window-managers/niri/class.nix:23); selected NixOS enable/default rows do not depend on pretending that every HM forwarding context was evaluated. Static provider reachability does not certify private secret availability or successful evaluation.

# closure-labs/foundation: census notes

[Config page](../../../configs/closure-labs/foundation.md) · upstream [closure-labs/foundation](https://github.com/closure-labs/foundation) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: 0715d5823b45; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

A reusable Home Manager product that also instantiates a real root home: [modules/flake/exports/_outputs.nix:6](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/flake/exports/_outputs.nix#L6)/14 calls mkHomeConfiguration on profile.json and exports finite. Actual schema3 profile is generic x86 Linux/Bluefin with empty roles, packages and capabilities ([profile.json:3](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/profile.json#L3)/5/13-18). Template/example profiles are not managed targets.

## Software selected and host/user traces

Constructor normalizes profile, declares den.homes finite and selects feature roots ([modules/home/construction/_module.nix:11](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/home/construction/_module.nix#L11)/29/54). Root home/base depends on home/shell ([modules/home/base/_feature.nix:34](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/home/base/_feature.nix#L34)), so Zsh is enabled; Bluefin adds substantive host-Fzf initialization ([modules/hosts/os/bluefin/_home.nix:30](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/hosts/os/bluefin/_home.nix#L30)). Common essentials capability adds Neovim despite empty packages: home/base metadata:5→selection:10→essentials schema3 deps:13→application module home.packages:19.

## Defined, disabled and ambiguous alternatives

Raw Neovim is installation-only; VSCodium is live but unselected optional app ([modules/apps/vscodium/_feature.nix:5](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/apps/vscodium/_feature.nix#L5)). Devops has real native Zsh/conditional Starship definition, but no selected root role/capability reaches it. Base Bluefin ownership assumptions and GNOME portal correction are not evidence that Foundation configures GNOME desktop itself. Stock shell preference and generic home path are not OS default-shell or physical-role evidence.

## Machine roles and remaining limits

Only a standalone home is instantiated; there is no declared OS host. Generic formFactor gives no defensible laptop/desktop/server role. Root customize.nix and modules/local.nix were read and add no requested software. Product utility packages and generated consumer template are not independently configured editor targets. Static feature trace establishes reachability, not a successfully activated Bluefin session.

# vodfsh/nixos-config: census notes

[Config page](../../../configs/vodfsh/nixos-config.md) · upstream [vodfsh/nixos-config](https://github.com/vodfsh/nixos-config) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: a0ff916b0b31; static source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three NixOS targets plus a separate standalone home key are explicit ([modules/entities.nix:6](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6), [modules/entities.nix:7](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L7)). Profiles and common aspects hold shared OS/HM behavior; native VM runner refers to the declared test-vm output ([modules/hosts/test-vm.nix:36](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L36)).

## Software selected and host/user traces

Every host includes common, profiles._, kitty and zsh ([modules/hosts/home/home.nix:7](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/home/home.nix#L7); [modules/hosts/nautilus/nautilus.nix:14](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/nautilus/nautilus.nix#L14); [modules/hosts/test-vm.nix:11](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L11)). The profiles child group includes workstation/development, enabling/defaulting Plasma and installing Neovim/VSCodium/Zellij. Actual HM projection is explicit via user host-aspects, not a blanket assumption ([modules/users/vodfsh.nix:11](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L11)). Zsh/Starship settings are substantive ([modules/aspects/zsh.nix:30](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L30), [modules/aspects/zsh.nix:96](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L96)). Exact immutable upstream source: https://raw.githubusercontent.com/denful/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/entities/home.nix (name parsing/host-user binding lines57-62, osConfig lines106-114, aspect fallback lines169-172). Projection source: https://raw.githubusercontent.com/denful/den/bf2504f9f2e8621fee091335132ab3ae698cf808/modules/aspects/batteries/host-aspects.nix (spawn request lines22-23). Local lock anchor is [flake.lock:40](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/flake.lock#L40).

## Defined, disabled and ambiguous alternatives

Editor/multiplexer package rows are installation only ([modules/aspects/profiles/development.nix:60](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/development.nix#L60)); EDITOR=nvim is a separate real OS default ([modules/aspects/common/system.nix:56](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/common/system.nix#L56)). Plasma enable and default-session settings do not imply an authored Plasma customization beyond those choices. Standalone vodfsh@home selection was resolved against the exact pinned Den implementation: it binds to declared host home/user vodfsh and supplies osConfig, so selected host-aspects projects the profile into its HM output.

## Machine roles and remaining limits

Workstation profile gives desktop purpose; nautilus explicitly imports laptop hardware ([modules/hosts/nautilus/nautilus.nix:36](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/nautilus/nautilus.nix#L36)), while test-vm is a real declared VM/runner. Hypervisor software on home/nautilus does not make them VM guests. Three hosts and one home are separate counting units. The standalone home selection is also proven from the exact locked Den source; its OS host binding does not add a physical machine. Unix usernames are configured contexts, not humans.

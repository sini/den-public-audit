# icebluerabbit/nixos: census notes

[Config page](../../../configs/icebluerabbit/nixos.md) · upstream [icebluerabbit/nixos](https://github.com/icebluerabbit/nixos) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: 21a704b338c3; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three actual hosts are explicit in [modules/inventory.nix:6](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/inventory.nix#L6)/52/79; network homelab at88 is a distinct network entity, not a fourth machine. NixOS installation images are emitted as package outputs by [modules/iso/iso.nix:118](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/iso/iso.nix#L118), recorded separately. HM class is explicit at [modules/defaults.nix:89](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/defaults.nix#L89).

## Software selected and host/user traces

All zms contexts directly select configured Zsh, Tmux, Nixvim and Oh My Posh via [modules/users/zms.nix:24](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/users/zms.nix#L24)/26/29/32. Desktop user additionally includes Niri/Zed ([modules/inventory.nix:14](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/inventory.nix#L14)/25), with actual settings read. Server explicitly selects hosted code-server container ([modules/hosts/server/host.nix:80](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/hosts/server/host.nix#L80)), whose real enable/settings chain reaches [modules/containers/code-server.nix:100](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/containers/code-server.nix#L100) and host-specific settings file.

## Defined, disabled and ambiguous alternatives

Nixvim has substantial active options, but LSP inclusion spells jsut at [modules/cli/neovim/lsp/lsp.nix:9](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/cli/neovim/lsp/lsp.nix#L9); this known static blocker is not unknown selection. The prompt is Oh My Posh, not Starship. [Exact pinned Niri source](https://raw.githubusercontent.com/sodiboo/niri-flake/68414146fbe13d8fce7748cf2f4e9e46e4834e2e/flake.nix) injects config at529-530 and emits KDL from nonnull finalConfig at442-445, resolving HM activation without an explicit enable. Server VSCode variant is code-server: hosted nested-container association, not a GUI/editor declaration for parent zms. Container Bash is installation-only; container Zsh has real enable/init/default wiring ([modules/containers/code-server.nix:80](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/containers/code-server.nix#L80)/81/95).

## Machine roles and remaining limits

Desktop/server/laptop purposes are explicit profile comments; laptop is MacBook Pro Darwin ([modules/hosts/laptop/host.nix:1](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/hosts/laptop/host.nix#L1)). NixOS containers do not add declared hosts or VM roles. ISO VM-detection branch is installation logic, not evidence of virtualized managed hosts. Names are configured account contexts, not humans; static settings reachability does not prove evaluation/runtime success.

Class verification: [modules/inventory.nix:78](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/inventory.nix#L78) declares aarch64-darwin, with pin at [flake.lock:250](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/flake.lock#L250). [Exact pinned Den host schema](https://raw.githubusercontent.com/vic/den/2040b61346a7215fd7b7f51d4a457544b6e597d0/nix/lib/entities/host.nix) line 66 derives class=darwin from that suffix. No local class override exists. HM contribution platforms remain home-darwin, while the OS default-shell contribution remains darwin; target deployment is therefore darwin.

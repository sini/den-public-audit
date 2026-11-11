# nazarewk-iac/nix-configs: census notes

[Config page](../../../configs/nazarewk-iac/nix-configs.md) · upstream [nazarewk-iac/nix-configs](https://github.com/nazarewk-iac/nix-configs) · [Census summary](../../summary.md)

Revision `a1a10f5c8272`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Mixed legacy fleet and exported Den aspect library. Legacy host metadata drives the principal NixOS/Darwin outputs ([flake.nix:293](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/flake.nix#L293)); the real Den output is a deliberately minimal parallel orr ([hosts-den/orr/default.nix:23](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/hosts-den/orr/default.nix#L23)). Den check entities are explicitly test artifacts ([modules/den/flake-module.nix:85](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/flake-module.nix#L85)), excluded from fleet adoption.

## Software selected and host/user traces

Legacy baseline → headless base → program switches is the common route, with explicit Home Manager sharedModules forwarding. Fish, Zsh and Zellij have substantive native configuration; tmux and Bash are separately installation-only. Helix is the non-minimal terminal editor default. Workstation hosts choose Sway; obler/pryll choose Plasma. Multiple available shells are not all login defaults.

## Defined, disabled and ambiguous alternatives

Native Vim is not Neovim; VS Code language servers, NWG JSON Hyprland widgets, and Emacs-style Zsh bindings are not editor/compositor adoption. Exported Den counterparts and synthetic check homes do not increase adoption counts. [data/slots/den-users.nix:23](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/data/slots/den-users.nix#L23) explicitly says its accounts are not yet imported.

## Machine roles and remaining unknowns

Fourteen metadata-backed legacy hosts plus one parallel Den host are explicit. Profile-derived desktop means author workload, not a chassis deduction. Dell Latitude is separately a documented laptop. Inventory is incomplete for dynamically generated package/install-image outputs and optional feature-generated guests; those are not fabricated as additional physical machines.

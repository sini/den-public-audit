# closure-labs__mish: census notes

[Config page](../../configs/closure-labs__mish.md) · upstream [closure-labs/mish](https://github.com/closure-labs/mish) · [Census summary](../summary.md)

Record: evidence JSON. Revision: `6587ee6dbb2f`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Mish is an offline event-coordination appliance, not a desktop dotfile template. flake.nix:21 enters nix/default.nix:7, which imports Den, its outputs and the composition. Inventory contains four host output variants at nix/den/hosts.nix:7.

## Software selected and host/user traces

Each real coordinator host selects modes.coordinator plus an architecture provider (nix/den/hosts.nix:27, nix/den/hosts.nix:35, nix/den/hosts.nix:39). Coordinator includes control, event defaults and local HTTPS (nix/den/aspects.nix:64); control enables the native product module at nix/den/aspects.nix:25. The installer selects only package plus upstream installation ISO machinery (nix/den/aspects.nix:76). None of these authored bodies selects one of the19 requested desktop/editor/multiplexer/shell/prompt families.

## Defined, disabled and ambiguous alternatives

No authored live family configuration or explicit family package selection was found in this inspected composition. That does not label inherited installer/base-system Bash or external modules as absent at runtime; an upstream default shell is not an explicit authored default. Framework-looking options under modules/nixos/mish/den.nix are product compatibility metadata, not a shell/editor configuration.

## Machine roles and remaining limits

The three coordinator targets receive an inferred server role from their event-control/HTTPS workload (nix/den/aspects.nix:25, nix/den/aspects.nix:64). The installer is a separate declared output but has no physical-form role. The mini-PC imports qemu-vm support and configures a VM variant (hosts/mish-mini-pc/configuration.nix:5, hosts/mish-mini-pc/configuration.nix:15); this alone is not used to classify the physical host as a VM. ARM board targets remain host outputs, not inferred laptops/desktops. No named Den user or distinct-human count is inferred.

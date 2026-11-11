# closure-labs__maestro: census notes

[Config page](../../configs/closure-labs__maestro.md) · upstream [closure-labs/maestro](https://github.com/closure-labs/maestro) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 6d707f35e29b; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

A single instantiated Maestro NixOS appliance with operator maestro (modules/features/appliance/composition.nix:6/13) and real installer-iso package (modules/features/installer/image.nix:27). This is a product configuration, not a library-only declaration.

## Software selected and host/user traces

Host and user share the aspect name maestro. Actual maestro aspect includes operator (modules/features/appliance/composition.nix:16/20), and explicit user HM class at modules/features/appliance/defaults.nix:9 lets the matching user aspect consume operator.homeManager Bash settings. The Bash body actively enables history/options/aliases/init (modules/features/operator/shell/bash.nix:18/20/60). Operator account shell conditional resolves to bashInteractive because host/settings.nix:18 sets enableExtras=false.

## Defined, disabled and ambiguous alternatives

Zsh and Oh My Posh have real substantial alternative configuration, but their actual cfg.enableExtras guards are false (modules/features/operator/shell/zsh.nix:17; modules/features/operator/shell/extras.nix:43). Package/menu override lists are empty (host/settings.nix:22/23; host/menu.nix:5/6), so no additional requested editor/multiplexer is installed by those hooks. Service shell scripts and devshell tools are not interactive software adoption. Installer body was read; it adds boot/access tooling, no authored requested interactive software settings.

## Machine roles and remaining limits

The appliance is explicitly an XCP-ng guest VM (README.md:11; modules/features/xcp-ng/guest/service.nix:8), and server workload is inferred from Xen Orchestra web appliance function (README.md:5). This is distinct from merely running virtualization tools on a host. Installer package does not add a machine or VM count. Static reachability is not a successful build or deployed clone census.

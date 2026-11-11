## Project and inspected revision

A four-host x86 homelab; named hosts compose shared system services and server workloads ([nixos/hosts/tower/configuration.nix:6](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/hosts/tower/configuration.nix#L6)).

## Software selected and host/user traces

Each production host declares kgb33, whose identity explicitly chooses Fish via user-shell ([nixos/users/kgb33.nix:5](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/users/kgb33.nix#L5)). No editor/multiplexer/desktop definition found in reviewed NixOS source tree.

## Defined, disabled and ambiguous alternatives

Required-family finding is Fish as login/account default, not configured HM dotfiles. Service programs and package build runtime shells are not desktop/editor adoption.

## Machine roles and remaining unknowns

Tower server inferred from coherent services, ophiuchus from observability purpose. ghost/targe purpose remains unknown from reviewed minimal configuration. check-* host entities with intoAttr=[] feed runNixOSTest and are fixtures, not production machine inventory ([nixos/apps/roboshpee.nix:60](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/apps/roboshpee.nix#L60); [nixos/apps/roboshpee.nix:68](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/apps/roboshpee.nix#L68)).

, revision `6ee44f24e022`.

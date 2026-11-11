# andreshungbz/nixconfig: census notes

[Config page](../../../configs/andreshungbz/nixconfig.md) · upstream [andreshungbz/nixconfig](https://github.com/andreshungbz/nixconfig) · [Census summary](../../summary.md)

Revision `bdee3f6ec030`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Two managed hosts and six standalone homes (three identity names across two architectures) are explicitly declared. Homes are configuration variants, not six additional physical machines. Kangaroo VM launcher wraps the same root host output ([modules/vm/vm.nix:19](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/vm/vm.nix#L19)).

## Software selected and host/user traces

Host packet classes are explicitly HM; named packet providers are routed by global mutual-provider ([modules/defaults.nix:7](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/defaults.nix#L7)). The packet identity also merges terminal includes from [modules/homes/packet.nix:13](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/homes/packet.nix#L13), while andreshung/ubuntu directly include the same stack. Terminal selects Fish, Helix, custom Starship and Zellij ([modules/aspects/stacks/terminal.nix:9](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/stacks/terminal.nix#L9)). Kangaroo additionally selects Niri in its packet provider ([modules/hosts/kangaroo/kangaroo.nix:24](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/hosts/kangaroo/kangaroo.nix#L24)).

## Defined, disabled and ambiguous alternatives

Fish is the hosted packet account default ([modules/users/packet.nix:6](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/users/packet.nix#L6)), and Helix explicitly sets EDITOR=hx in every terminal home ([modules/aspects/apps/helix.nix:18](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/apps/helix.nix#L18)). Starship uses real host-dependent color settings, not a bare enable ([modules/aspects/apps/starship/starship.nix:28](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/apps/starship/starship.nix#L28)). Zellij has pane-frame configuration but integrations are commented. Niri has full layout/binding children. VSCode/Zed are installation-only dev-tools packages/casks; Plasma is an unselected live alternative. GNOME utilities and Sway-related names do not establish desktops.

## Machine roles and remaining unknowns

Hyena explicitly documents M1 MacBook Air, supporting laptop plus Darwin roles ([modules/hosts/hyena/hyena.nix:3](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/hosts/hyena/hyena.nix#L3)). Kangaroo explicitly documents gaming desktop ([modules/hosts/kangaroo/kangaroo.nix:8](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/hosts/kangaroo/kangaroo.nix#L8)). Standalone identities do not identify distinct humans or host purpose. Package wrappers and VM variants are not exhaustively inventoried as package outputs.

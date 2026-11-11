# Erastos__nixos-dotfiles: census notes

[Config page](../../configs/Erastos__nixos-dotfiles.md) · upstream [Erastos/nixos-dotfiles](https://github.com/Erastos/nixos-dotfiles) · [Census summary](../summary.md)

Revision `f2336347f41d`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Two NixOS hosts plus two matching standalone-home outputs wrap an existing ordinary module tree (parts/hosts.nix:2; parts/hosts.nix:8).

## Software selected and host/user traces

Embedded netscape aspect directly selects shared HM tree with true-by-default editor/shell options (parts/aspects/netscape.nix:6; modules/home/editors.nix:8). Neo explicitly selects Sway; Trinity Niri. Exact dependency inspected: https://raw.githubusercontent.com/vic/den/2f1ae4aa27e756684d1fb5ebc1d25267727bd305/nix/lib/entities/home.nix:174 chooses registry key and userName, and https://raw.githubusercontent.com/vic/den/2f1ae4aa27e756684d1fb5ebc1d25267727bd305/nix/lib/entities/_types.nix:40–58 composes all present candidates. Root flake.lock pins this revision. Both standalone homes therefore include netscape → shared-hm, resolving the previous ambiguity.

## Defined, disabled and ambiguous alternatives

Both hosted and standalone baseline editor/shell modules are selected. Qualified home aspects add machine-specific Niri/River intent, while this record credits the shared baseline separately. Native Vim is not mistaken for Neovim; Plasma remains an unselected definition.

## Machine roles and remaining unknowns

Hosts have mixed virtualization/desktop capabilities; hypervisor enablement does not make them VM targets. Physical form not inferred from GUI. Two homes do not add physical machines or humans.

# Likivik__spectacle: census notes

[Config page](../../configs/Likivik__spectacle.md) · upstream [Likivik/spectacle](https://github.com/Likivik/spectacle) · [Census summary](../summary.md)

Revision `ce6d767b84e9`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Nine explicit x86_64-linux hosts, including declarative skeleton machines with tmpfs roots. Do not equate all nine with deployed physical computers. Real desktop choices are separate from a capitalized convenience aggregate that no host selects.

## Software selected and host/user traces

Serenity and afterglow use Plasma; spectacle uses GNOME; traversal uses DMS → Niri. Dev selects Bash integrations and installs VSCodium on serenity/traversal. likivik/watcher identity aspects explicitly select Bash account defaults. Pin 65c9fd40e958109f5a352c1a93ae8254bf1ed29f user-shell implementation was already read at immutable https://raw.githubusercontent.com/vic/den/65c9fd40e958109f5a352c1a93ae8254bf1ed29f/modules/aspects/batteries/user-shell.nix ; local flake.lock binds that exact dependency.

## Defined, disabled and ambiguous alternatives

Hyprland bigscreen and rich Zsh are definitions with no real host consumer. VSCodium settings are external sync, so installation-only. Niri has actual native KDL but maid points to a mutable checkout. Required editor/shell families seen only in agent fixture prose or DMS muxType defaults are not adoption.

## Machine roles and remaining unknowns

Desktop/laptop roles come from declaration descriptions. Poweredge server role is inferred from selected server bundle; erebus explicitly says VPS. TV box and monoblock descriptions are retained without forcing physical-role labels. Package installer perSystem output systems are not locally enumerated, hence incomplete inventory; no distinct-human count.

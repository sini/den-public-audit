# adanoelle/fern: census notes

[Config page](../../../configs/adanoelle/fern.md) · upstream [adanoelle/fern](https://github.com/adanoelle/fern) · [Census summary](../../summary.md)

Revision `060cd42a3d02`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

One managed NixOS workstation and one Ubuntu standalone home are live ([modules/hosts.nix:4](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L4); [modules/hosts.nix:12](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L12)). The home explicitly maps the tyo login onto ada. Parked moss is commented at [modules/hosts.nix:34](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L34) and excluded.

## Software selected and host/user traces

Shared ada includes CLI and shell bundles ([modules/user-ada.nix:18](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/user-ada.nix#L18); [modules/user-ada.nix:20](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/user-ada.nix#L20)), which supply Helix, Kakoune, tmux, Fish, Zsh, Nu and Starship settings. Explicit user/home mutual-provider routes exist ([modules/dendritic.nix:15](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/dendritic.nix#L15); [modules/dendritic.nix:21](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/dendritic.nix#L21)). Fern forwards desktop and Niri ([modules/host-fern.nix:26](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/host-fern.nix#L26)); the qualified work provider selects the standalone Niri wrapper ([modules/user-ada-work.nix:669](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/user-ada-work.nix#L669)).

## Defined, disabled and ambiguous alternatives

Helix is explicitly defaultEditor ([modules/cli/helix.nix:9](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/cli/helix.nix#L9)), while Kakoune is configured as an alternative. Fish is the OS account default ([modules/users.nix:30](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/users.nix#L30)), but Zsh and Nu are also substantively configured. Fish uses its own prompt and Starship Fish integration is false ([modules/shells/starship.nix:10](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/shells/starship.nix#L10)). Hyprland is an enabled fallback on fern ([modules/host-fern.nix:86](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/host-fern.nix#L86)); it is deliberately absent from ada-work ([modules/user-ada-work.nix:5](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/user-ada-work.nix#L5)). Niri is listed first in greetd but --remember is present ([modules/desktop/greetd.nix:29](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/desktop/greetd.nix#L29); [modules/desktop/greetd.nix:41](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/desktop/greetd.nix#L41)), so session ordering is not a hard default guarantee.

## Machine roles and remaining unknowns

Fern explicitly selects a graphical workstation role, normalized as desktop ([modules/host-fern.nix:11](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/host-fern.nix#L11)). The standalone target is documented as an Ubuntu work laptop ([modules/hosts.nix:6](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L6)), retained as home rather than inflating declared host counts. Garden-shell and niri modules are external dependencies; local explicit routes and imports establish intended static reachability, not successful evaluation. Package outputs are not exhaustively inventoried.

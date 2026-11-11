# byte-sized-emi__nix-config: census notes

[Config page](../../configs/byte-sized-emi__nix-config.md) · upstream [byte-sized-emi/nix-config](https://github.com/byte-sized-emi/nix-config) · [Census summary](../summary.md)

Revision `8df6aa42d1bb`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Four x86_64 NixOS host roots declare emilia (modules/den.nix:22). Two graphical targets and two explicit server-default targets share direct identity shell configuration.

## Software selected and host/user traces

The emilia aspect directly selects shell and user-shell Zsh (modules/emilia.nix:6; modules/emilia.nix:7). Its host-name guards select graphical for nixlaptop and nixda (modules/emilia.nix:9; modules/emilia.nix:15), so full home Niri/Zed configuration is statically reachable independently of implicit provider behavior. The corresponding hosts also select graphical at system scope. Exact pinned dependency verified statically: https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/aspects/fx/aspect/provide.nix, lines21–27 directly dispatch to-users/to-hosts as include effects. Local flake.lock binds this revision. Missing mutual-provider is not a blocker; it is an inert compatibility shim in these pins.

## Defined, disabled and ambiguous alternatives

Provider-only uncertainties were resolved against the exact locked Den implementation. Explicit to-users contributions above are selected where the complete local host/profile/user/HM-class chain is cited. Direct host homeManager content still requires a separate projection route; this conclusion does not infer one.

## Machine roles and remaining unknowns

nixlaptop is an explicitly named laptop (modules/den.nix:23). nixnest and nixdort select server-default (modules/hosts/nixnest/configuration.nix:10; modules/hosts/nixdort/configuration.nix:6). nixda is graphical but its physical form remains unknown. Inventory covers host roots; unrelated package outputs are not exhaustively expanded and cannot be treated as extra hosts.

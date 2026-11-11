# cfrenette__nixos-config: census notes

[Config page](../../configs/cfrenette__nixos-config.md) · upstream [cfrenette/nixos-config](https://github.com/cfrenette/nixos-config) · [Census summary](../summary.md)

Record: evidence JSON. Revision: `af711691cde3`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Four explicitly declared NixOS targets share one cory user aspect (modules/hosts.nix:7, modules/hosts.nix:10). flake.nix:4 imports the live module tree. The user schema enables HM and mutual-provider at modules/den.nix:10 and modules/den.nix:14.

## Software selected and host/user traces

The complete common path is host inventory → cory aspect → headless → nixvim/Starship (modules/users/cory.nix:9; modules/aspects/tui/headless.nix:4). It applies even to the headless Pi: the interactive-user baseline is independent of GUI selection. Nixvim is an installed external package plus explicit EDITOR default (modules/aspects/tui/nixvim/nixvim.nix:13, modules/aspects/tui/nixvim/nixvim.nix:18), not a claim to have read that external editor configuration. Bash is explicitly selected as login shell by modules/users/cory.nix:7.

## Defined, disabled and ambiguous alternatives

Cosmic is the actual optional desktop peer on frmwrk/solstice (modules/hosts/frmwrk.nix:9, modules/hosts/solstice.nix:9, modules/aspects/desktop/cosmic.nix:5). It is not GNOME, and Starship Bash integration is not itself shell-default evidence. Required-family alternatives not represented by live bodies are recorded as not_found.

## Machine roles and remaining limits

frmwrk explicitly selects laptop; laptop inherits workstation, giving both laptop and normalized desktop roles (modules/aspects/laptop.nix:4). Solstice selects workstation. WSL is explicit at modules/hosts/wsl.nix:8. The Pi server role is inferred from its headless DNS/proxy workload, not SSH (modules/hosts/pi.nix:3, modules/hosts/pi.nix:10). These are four declared targets and configured cory contexts, not four verified running machines or distinct humans. Private secrets input may prevent evaluation; no successful evaluation is claimed.

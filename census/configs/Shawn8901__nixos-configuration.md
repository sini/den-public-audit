# Shawn8901__nixos-configuration: census notes

[Config page](../../configs/Shawn8901__nixos-configuration.md) · upstream [Shawn8901/nixos-configuration](https://github.com/Shawn8901/nixos-configuration) · [Census summary](../summary.md)

Revision `890a465d7eb3`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Seven NixOS hosts declare shawn: six x86_64 and one aarch64 watchtower (modules/den.nix:38). cfg namespace separates shared shell, desktop and server aspects from host provider compositions.

## Software selected and host/user traces

Shawn directly selects cfg.shell (modules/aspects/users/shawn.nix:10). All user HM classes and mutual-provider are explicit (modules/aspects/defaults.nix:27; modules/aspects/defaults.nix:28). Host to-users providers select cfg.desktop on pointalpha/zenbook and cfg.server elsewhere, so desktop coding home settings are not inferred from merely declaring users.

## Defined, disabled and ambiguous alternatives

Account default Zsh is explicit and has substantive OS initialization (modules/aspects/cfg/shell.nix:4; modules/aspects/cfg/shell.nix:79). Starship lives at OS scope with full settings (modules/aspects/cfg/shell.nix:22). Plasma and VSCode are selected only by the two desktop providers (modules/aspects/cfg/desktop/default.nix:34; modules/aspects/cfg/desktop/coding.nix:65). No Neovim is inferred from Vim packageConfigurable; Bash completion support is not Bash shell configuration.

## Machine roles and remaining unknowns

Five roots explicitly select server profile; pointalpha and zenbook explicitly select the desktop profile. Desktop here is the author role, not proof of chassis: Zenbook model hints at laptop but no unsupported extra role is forced. cfg.server enables qemuGuest generically (modules/aspects/cfg/server.nix:42), so that shared setting alone is not treated as proof all five servers are VMs. Native service/secondary accounts are not distinct humans or additional Den user contexts.

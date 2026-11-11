# Draculestein__nixos-config: census notes

[Config page](../../configs/Draculestein__nixos-config.md) · upstream [Draculestein/nixos-config](https://github.com/Draculestein/nixos-config) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 3514a1d2e512; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Two Den hosts (modules/hosts.nix:7) and independent installer output (modules/installer.nix:4) form the actual inventory. AlbertProP16 uses the default HM user class; heimdall overrides both constructor and user aspect/classes (modules/hosts.nix:14/21/22).

## Software selected and host/user traces

Only AlbertProP16 reaches the broad albertjul user aspect: default HM class is explicit at modules/home-manager.nix:20. That user selects Zsh, NVF and Niri (modules/users/albertjul/default.nix:12/21/24), and code-dev includes VSCode (modules/aspects/cli/code-dev.nix:10). GNOME is independently selected by the host at modules/hosts/AlbertProP16/default.nix:11, so two desktop families coexist without a proven default session.

## Defined, disabled and ambiguous alternatives

Zsh loads inspected native completions via modules/aspects/cli/zsh/default.nix:9; it is also the explicit login shell at modules/users/albertjul/default.nix:35. Bash is enable-only; Starship explicitly integrates the two enabled shells. NVF has meaningful language settings, while Vim aliases are not a default-editor declaration. Niri KDL uses out-of-store ~/.dotfiles links (modules/aspects/desktop/niri/default.nix:168), so correct checkout is a prerequisite. GNOME application packages and Kvantum styling are not KDE Plasma adoption.

## Machine roles and remaining limits

AlbertProP16 explicitly selects laptop hardware (modules/hosts/AlbertProP16/configuration.nix:9). Heimdall server purpose is inferred from coherent headless administration and OPNsense workload (modules/hosts/heimdall/default.nix:20/21); hypervisor workloads do not make it a VM host. Its user classes=[user] prevents the desktop HM settings from becoming verified server adoption. Installer is an authored output, not a fixture; no requested software settings are authored in its native body.

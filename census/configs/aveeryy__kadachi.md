# aveeryy__kadachi: census notes

[Config page](../../configs/aveeryy__kadachi.md) · upstream [aveeryy/kadachi](https://github.com/aveeryy/kadachi) · [Census summary](../summary.md)

Revision `ba03c6ede780`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six x86_64 NixOS hosts are declared under hosts/*/system.nix. Custom namespaces separate host compositions, reusable user features and machine-role features (dendritic.nix:28).

## Software selected and host/user traces

Schema host/user aspects are explicitly remapped into the hosts namespace (defaults/misc.nix:14; defaults/misc.nix:18), with HM class17, host-aspects26 and mutual-provider27. Each user tree selects kasane/base-user -> Zsh. The same user trees directly select Hyprland for malfestio/mizuki/totsugeki, so their host/user display guards are traceable without guessing a default provider.

## Defined, disabled and ambiguous alternatives

Zsh is the OS defaultUserShell with substantive home init (aspects/kasane/zsh.nix:12; aspects/kasane/zsh.nix:20). Starship has a real add_newline setting (aspects/kasane/zsh.nix:51). Global kadachi-nvim is an external package selection plus explicit EDITOR=nvim (defaults/nvim.nix:12; defaults/nvim.nix:15); its external native configuration is not claimed as inspected. Malfestio explicitly sets the Jovian desktopSession to hyprland-uwsm (hosts/malfestio/system.nix:50). Generic uwsm start default on other hosts does not name a compositor, so no extra Hyprland default is inferred.

## Machine roles and remaining unknowns

greatyamada/hatsune/nightcord explicitly select server; mizuki/totsugeki explicitly select desktop roles. Malfestio is a Steam Deck (hosts/malfestio/system.nix:29), a handheld without a dedicated census role; it is not forced to laptop. Unselected WSL feature is not a WSL target. Private secrets and external Neovim package remain dependencies; unrelated per-system packages are not exhaustively inventoried.

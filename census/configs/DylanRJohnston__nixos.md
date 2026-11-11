# DylanRJohnston__nixos: census notes

[Config page](../../configs/DylanRJohnston__nixos.md) · upstream [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos) · [Census summary](../summary.md)

Four Linux/Darwin hosts share an exported arc namespace (flake.nix:28; modules/namespace.nix:27).

# Software selected and host/user traces

Each real host selects base; explicit host-aspects projection gives dylanj the shared Zsh/Starship/Tmux/Vim/Zed home configuration (modules/host-aspects.nix:5; modules/zsh.nix:3). Loki additionally selects interactive→Niri and greetd explicitly starts niri-session (hosts/loki/loki.nix:14; modules/niri.nix:27).

# Defined, disabled and ambiguous alternatives

Zsh is the account shell and Zed the EDITOR default (modules/zsh.nix:17; modules/zsh.nix:58). Vim remains a separate configured editor. Sway is a live unselected alternative (modules/sway.nix:3); Nushell explicitly disabled (modules/nushell.nix:14). GNOME theme/dconf keys do not configure GNOME desktop (modules/darkmode.nix:8).

# Machine roles and remaining unknowns

Darwin class explicit for asgard/odin; physical form unknown. Loki interactive/gaming workload and external monitor do not establish laptop versus desktop; physical form remains unknown (modules/niri.nix:46). Mimir server inferred from coherent media/home-automation/monitoring selections (hosts/mimir/mimir.nix:21). Four account contexts do not establish four humans.

 · revision `505097f4d0fd`.

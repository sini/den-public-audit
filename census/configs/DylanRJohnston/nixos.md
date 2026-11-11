# DylanRJohnston/nixos: census notes

[Config page](../../../configs/DylanRJohnston/nixos.md) · upstream [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos) · [Census summary](../../summary.md)

Four Linux/Darwin hosts share an exported arc namespace ([flake.nix:28](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/flake.nix#L28); [modules/namespace.nix:27](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/namespace.nix#L27)).

# Software selected and host/user traces

Each real host selects base; explicit host-aspects projection gives dylanj the shared Zsh/Starship/Tmux/Vim/Zed home configuration ([modules/host-aspects.nix:5](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/host-aspects.nix#L5); [modules/zsh.nix:3](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/zsh.nix#L3)). Loki additionally selects interactive→Niri and greetd explicitly starts niri-session ([hosts/loki/loki.nix:14](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/hosts/loki/loki.nix#L14); [modules/niri.nix:27](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/niri.nix#L27)).

# Defined, disabled and ambiguous alternatives

Zsh is the account shell and Zed the EDITOR default ([modules/zsh.nix:17](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/zsh.nix#L17); [modules/zsh.nix:58](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/zsh.nix#L58)). Vim remains a separate configured editor. Sway is a live unselected alternative ([modules/sway.nix:3](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/sway.nix#L3)); Nushell explicitly disabled ([modules/nushell.nix:14](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/nushell.nix#L14)). GNOME theme/dconf keys do not configure GNOME desktop ([modules/darkmode.nix:8](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/darkmode.nix#L8)).

# Machine roles and remaining unknowns

Darwin class explicit for asgard/odin; physical form unknown. Loki interactive/gaming workload and external monitor do not establish laptop versus desktop; physical form remains unknown ([modules/niri.nix:46](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/niri.nix#L46)). Mimir server inferred from coherent media/home-automation/monitoring selections ([hosts/mimir/mimir.nix:21](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/hosts/mimir/mimir.nix#L21)). Four account contexts do not establish four humans.

 · revision `505097f4d0fd`.

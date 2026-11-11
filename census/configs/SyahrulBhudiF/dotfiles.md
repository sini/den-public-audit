# SyahrulBhudiF/dotfiles: census notes

[Config page](../../../configs/SyahrulBhudiF/dotfiles.md) · upstream [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles) · [Census summary](../../summary.md)

A single generic-Linux standalone HM home explicitly imports identity/config/Git/terminal fragments ([flake.nix:40](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/flake.nix#L40); [modules/den.nix:5](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/den.nix#L5)).

# Software selected and host/user traces

The ryuko home maps to ryuko aspect; all explicitly imported fragments contribute to its HM class ([modules/home.nix:3](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/home.nix#L3); [modules/config.nix:3](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/config.nix#L3)).

# Defined, disabled and ambiguous alternatives

Native Neovim and Nushell files are deployed as live-checkout symlinks, and Zsh/Starship are explicitly enabled ([modules/config.nix:18](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/config.nix#L18); [modules/config.nix:22](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/config.nix#L22); [modules/home.nix:159](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/home.nix#L159)). Git chooses nvim as its editor ([modules/git.nix:100](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/git.nix#L100)). No login shell or WM adoption inferred from external non-Nix dotfiles.

# Machine roles and remaining unknowns

No host target, chassis or server role is declared. The home is one configured account context, not a counted physical machine. Missing Starship TOML has a guarded fallback ([modules/home.nix:27](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/home.nix#L27)).

 · revision `ba537827987e`.

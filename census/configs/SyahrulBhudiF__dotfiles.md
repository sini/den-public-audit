# SyahrulBhudiF__dotfiles: census notes

[Config page](../../configs/SyahrulBhudiF__dotfiles.md) · upstream [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles) · [Census summary](../summary.md)

A single generic-Linux standalone HM home explicitly imports identity/config/Git/terminal fragments (flake.nix:40; modules/den.nix:5).

# Software selected and host/user traces

The ryuko home maps to ryuko aspect; all explicitly imported fragments contribute to its HM class (modules/home.nix:3; modules/config.nix:3).

# Defined, disabled and ambiguous alternatives

Native Neovim and Nushell files are deployed as live-checkout symlinks, and Zsh/Starship are explicitly enabled (modules/config.nix:18; modules/config.nix:22; modules/home.nix:159). Git chooses nvim as its editor (modules/git.nix:100). No login shell or WM adoption inferred from external non-Nix dotfiles.

# Machine roles and remaining unknowns

No host target, chassis or server role is declared. The home is one configured account context, not a counted physical machine. Missing Starship TOML has a guarded fallback (modules/home.nix:27).

 · revision `ba537827987e`.

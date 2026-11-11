# JoonasKajava__nvf-config: census notes

[Config page](../../configs/JoonasKajava__nvf-config.md) · upstream [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config) · [Census summary](../summary.md)

Den drives an actual standalone NVF editor package, without host/home inventory (modules/den.nix:24).

# Software selected and host/user traces

The default package explicitly selects den.aspects.nvf and forwards its vim fragments through NVF typed option merging (modules/nvf-integration.nix:15; modules/nvf-integration.nix:41).

# Defined, disabled and ambiguous alternatives

Only required-family adoption established is configured Neovim via NVF. Zellij navigation and VSCode language-server names are dependencies/plugins, not the corresponding applications (modules/config/editor/zellij-nav.nix:7; modules/config/languages/json.nix:15).

# Machine roles and remaining unknowns

Package targets do not count as machines or humans. Exact perSystem expansion is unknown from local declarations; no implicit Linux/Darwin system list invented.

 · revision `9674a20a5632`.

---
title: "JoonasKajava/nvf-config: census notes"
---

[Config page](/configs/joonaskajava/nvf-config/) · upstream [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config) · [Census summary](/census/summary/)

Den drives an actual standalone NVF editor package, without host/home inventory ([modules/den.nix:24](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)).

# Software selected and host/user traces

The default package explicitly selects den.aspects.nvf and forwards its vim fragments through NVF typed option merging ([modules/nvf-integration.nix:15](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L15); [modules/nvf-integration.nix:41](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L41)).

# Defined, disabled and ambiguous alternatives

Only required-family adoption established is configured Neovim via NVF. Zellij navigation and VSCode language-server names are dependencies/plugins, not the corresponding applications ([modules/config/editor/zellij-nav.nix:7](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/editor/zellij-nav.nix#L7); [modules/config/languages/json.nix:15](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/json.nix#L15)).

# Machine roles and remaining unknowns

Package targets do not count as machines or humans. Exact perSystem expansion is unknown from local declarations; no implicit Linux/Darwin system list invented.

 · revision `9674a20a5632`.

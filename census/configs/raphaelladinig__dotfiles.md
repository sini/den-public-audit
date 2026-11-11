# raphaelladinig__dotfiles: census notes

[Config page](../../configs/raphaelladinig__dotfiles.md) · upstream [raphaelladinig/dotfiles](https://github.com/raphaelladinig/dotfiles) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `f29658d31d04`.

One ARM Darwin target uses explicit aspect overrides for the host and user (`modules/hosts/default.nix:4`).

## 2. Software selected and traces

The user directly selects Fish and the modular raw Neovim bundle. Core links native settings and dynamic module loader; feature flags use hasAspect gating, and selected LSP explicitly defaults its own flag true (`modules/defaults.nix:20`, `modules/apps/neovim/lsp.nix:14`).

- **fish / fish** (configured, home-darwin, enabled): Explicit user aspect selects Fish; the HM contribution installs the shell, writes native config and aliases, and generates session-variable translation. Evidence: `modules/apps/fish/default.nix:24`, `modules/apps/fish/config/config.fish:6`, `modules/hosts/default.nix:4`, `modules/hosts/default.nix:5`, `modules/defaults.nix:43`, `modules/users/raphaelladinig.nix:4`, `modules/users/raphaelladinig.nix:15`.
- **fish / fish** (default, darwin, enabled): Selected Fish sets OS shell and enables programs.fish; host activation condition resolves true and explicitly updates the existing account UserShell with dscl. Evidence: `modules/apps/fish/default.nix:12`, `modules/apps/fish/default.nix:13`, `modules/hosts/caelum.nix:21`, `modules/hosts/default.nix:4`, `modules/hosts/default.nix:5`, `modules/defaults.nix:43`, `modules/users/raphaelladinig.nix:4`, `modules/users/raphaelladinig.nix:15`.
- **neovim / raw/modular Lua** (configured, home-darwin, enabled): User selects the Neovim bundle, whose core enables editor and reads tracked native Lua. Subfeatures use effective flags gated by user.hasAspect; selected LSP sets its default flag true, rather than every declared option automatically enabling. Evidence: `modules/apps/neovim/default.nix:77`, `modules/apps/neovim/default.nix:80`, `modules/apps/neovim/init.lua:15`, `modules/apps/neovim/settings.lua:25`, `modules/hosts/default.nix:4`, `modules/hosts/default.nix:5`, `modules/defaults.nix:43`, `modules/users/raphaelladinig.nix:4`, `modules/users/raphaelladinig.nix:14`, `modules/apps/neovim/default.nix:4`.
- **neovim / neovim** (default, home-darwin, enabled): Selected core explicitly sets defaultEditor=true. Evidence: `modules/apps/neovim/default.nix:79`, `modules/hosts/default.nix:4`, `modules/hosts/default.nix:5`, `modules/defaults.nix:43`, `modules/users/raphaelladinig.nix:4`, `modules/users/raphaelladinig.nix:14`.

## 3. Defined, disabled and ambiguous alternatives

Fish is explicitly reconciled as login shell for an existing macOS account; enablement alone is not the basis. Neovim is explicit editor default with substantive native settings. Cmux has terminal application appearance settings; tabs alone do not make it a counted multiplexer.


## 4. Machine roles and limits

Darwin is explicit; no physical laptop/desktop role is inferred from apps or name. Templates are exportable examples, not managed hosts.

Complete single-host inventory. Application-preference modules and templates do not add standalone homes or configured required-family editor package outputs.

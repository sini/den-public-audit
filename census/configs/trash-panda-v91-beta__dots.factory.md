# trash-panda-v91-beta__dots.factory: census notes

[Config page](../../configs/trash-panda-v91-beta__dots.factory.md) · upstream [trash-panda-v91-beta/dots.factory](https://github.com/trash-panda-v91-beta/dots.factory) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `04ed87289164`.

One ARM Darwin MacBook uses capability bundles and explicit mutual host/user providers.

## 2. Software selected and traces

User selects development→terminal/Nixvim and desktop→AeroSpace. PMB provider is static and mutual-provider is explicit (`modules/defaults.nix:15`, `modules/hosts/pmb.nix:23`); account shell assignment is therefore distinct from Nushell enablement.

- **nushell / nushell** (configured, home-darwin, enabled): Selected development bundle includes terminal, supplying substantive Nushell settings, aliases, environment and login path setup. Evidence: `modules/aspects/tool/terminal.nix:97`, `modules/aspects/tool/terminal.nix:99`, `modules/den.nix:5`, `modules/den.nix:7`, `modules/users/trash-panda-v91-beta.nix:25`, `modules/aspects/bundle/dev.nix:7`.
- **nushell / nushell** (default, darwin, enabled): Explicit mutual-provider routes the PMB user provider; it assigns users.users account shell=pkgs.nushell. Evidence: `modules/hosts/pmb.nix:27`, `modules/den.nix:5`, `modules/defaults.nix:15`, `modules/hosts/pmb.nix:23`.
- **starship / starship** (configured, home-darwin, enabled): Terminal enables Starship with substantive prompt format, symbols and module settings. Evidence: `modules/aspects/tool/terminal.nix:217`, `modules/aspects/tool/terminal.nix:240`, `modules/den.nix:5`, `modules/den.nix:7`, `modules/users/trash-panda-v91-beta.nix:25`, `modules/aspects/bundle/dev.nix:7`.
- **other_multiplexer / herdr** (configured, home-darwin, enabled): Terminal configures Herdr keys/workspaces and explicit terminal.default_shell Nushell; this is not tmux/Zellij. Evidence: `modules/aspects/tool/terminal.nix:129`, `modules/aspects/tool/terminal.nix:133`, `modules/den.nix:5`, `modules/den.nix:7`, `modules/users/trash-panda-v91-beta.nix:25`, `modules/aspects/bundle/dev.nix:7`.
- **neovim / nixvim** (configured, home-darwin, enabled): Development bundle explicitly selects Nixvim; its enabled module supplies substantive options/diagnostics and self-registering plugin sub-aspects. Evidence: `modules/aspects/tool/nixvim/default.nix:24`, `modules/aspects/tool/nixvim/default.nix:92`, `modules/den.nix:5`, `modules/den.nix:7`, `modules/users/trash-panda-v91-beta.nix:25`, `modules/aspects/bundle/dev.nix:7`, `modules/aspects/bundle/dev.nix:8`.
- **neovim / nixvim** (default, home-darwin, enabled): Selected Nixvim sets defaultEditor=true and terminal HM environment explicitly sets EDITOR=nvim. Evidence: `modules/aspects/tool/nixvim/default.nix:26`, `modules/aspects/tool/terminal.nix:519`, `modules/den.nix:5`, `modules/den.nix:7`, `modules/users/trash-panda-v91-beta.nix:25`, `modules/aspects/bundle/dev.nix:7`, `modules/aspects/bundle/dev.nix:8`.
- **aerospace / aerospace** (configured, home-darwin, enabled): Selected desktop bundle includes substantive AeroSpace workspace/binding/window routing, with PMB overrides consumed through mutual-provider. Evidence: `modules/aspects/tool/window-manager.nix:33`, `modules/aspects/tool/window-manager.nix:43`, `modules/den.nix:5`, `modules/users/trash-panda-v91-beta.nix:28`, `modules/aspects/bundle/desktop.nix:7`.

## 3. Defined, disabled and ambiguous alternatives

Nushell account default, Nixvim editor default, Starship and Herdr are substantive selected configuration. Ghostty Fish/Zsh/Bash integration toggles do not configure those shell applications. Kubernetes homelab CLI bundle does not create remote managed machine inventory.


## 4. Machine roles and limits

MacBook is explicit laptop/Darwin; desktop role records selected workstation bundle. No server role follows merely from homelab administration tools.

Complete one-host literal inventory; external inputs/npins supply packages but local selections and settings are traced. No standalone home or configured editor package output is separately declared.

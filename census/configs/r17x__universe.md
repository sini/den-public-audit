# r17x__universe: census notes

[Config page](../../configs/r17x__universe.md) · upstream [r17x/universe](https://github.com/r17x/universe) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `f8bc64a503b4`.

A typed r17 profile generates two hosts, with eR17x inheriting eR17 system facts (`nix/den/schema/profile.nix:56`).

## 2. Software selected and traces

The schema projects users.${profileName}=profile.user and merges generated hosts (`nix/den/schema/profile.nix:93`, `nix/den/schema/profile.nix:116`). eR17 selects shell/desktop/terminal/editor; eR17x includes eR17. Default host-aspects makes the HM pieces reachable.

- **fish / fish** (configured, home-darwin, enabled): Profile-derived host eR17 selects machine→shell/terminal/desktop, with eR17x including eR17. Explicit child includes and host-aspects route substantive settings to the corresponding OS/home class. Evidence: `nix/den/aspects/shell.nix:318`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`.
- **starship / starship** (configured, home-darwin, enabled): Profile-derived host eR17 selects machine→shell/terminal/desktop, with eR17x including eR17. Explicit child includes and host-aspects route substantive settings to the corresponding OS/home class. Evidence: `nix/den/aspects/shell.nix:162`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`.
- **tmux / tmux** (configured, home-darwin, enabled): Profile-derived host eR17 selects machine→shell/terminal/desktop, with eR17x including eR17. Explicit child includes and host-aspects route substantive settings to the corresponding OS/home class. Evidence: `nix/den/aspects/terminal.nix:265`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`.
- **aerospace / aerospace** (configured, darwin, enabled): Profile-derived host eR17 selects machine→shell/terminal/desktop, with eR17x including eR17. Explicit child includes and host-aspects route substantive settings to the corresponding OS/home class. Evidence: `nix/den/aspects/desktop.nix:76`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`.
- **fish / fish** (default, darwin, enabled): The profile shell value is fish, consumed by the default user-shell battery. Evidence: `r17.nix:6`, `nix/den/default.nix:85`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`.
- **neovim / nixvim** (configured, home-linux, enabled): Machine selects editor; custom nixvim class resolves host aspects into per-host configured Nixvim packages, which the HM editor contribution installs by networking.hostName. Evidence: `nix/den/aspects/editor/default.nix:4`, `nix/nvim.nix/config/globals.nix:6`, `nix/nvim.nix/default.nix:65`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`, `nix/den/aspects/machine.nix:14`, `nix/nvim.nix/default.nix:70`.
- **neovim / nixvim** (default, home-darwin, enabled): The editor contribution explicitly chooses its per-host Nixvim executable as EDITOR. Evidence: `nix/den/aspects/editor/default.nix:29`, `r17.nix:3`, `nix/den/schema/profile.nix:116`, `nix/den/aspects/machine.nix:4`, `nix/den/aspects/machine.nix:69`, `nix/den/default.nix:77`, `nix/den/aspects/machine.nix:14`.
- **neovim / nixvim** (configured, package, enabled): Each explicit perSystem packages.nvim key aliases the configured eR17 package; the implementation system remains eR17.system, not necessarily the output-key system. Evidence: `nix/den/aspects/editor/default.nix:4`, `nix/nvim.nix/config/globals.nix:6`, `nix/nvim.nix/default.nix:78`, `nix/nvim.nix/default.nix:70`.
- **neovim / nixvim** (configured, package, enabled): Each explicit perSystem packages.nvim key aliases the configured eR17 package; the implementation system remains eR17.system, not necessarily the output-key system. Evidence: `nix/den/aspects/editor/default.nix:4`, `nix/nvim.nix/config/globals.nix:6`, `nix/nvim.nix/default.nix:78`, `nix/nvim.nix/default.nix:70`.
- **neovim / nixvim** (configured, package, enabled): Each explicit perSystem packages.nvim key aliases the configured eR17 package; the implementation system remains eR17.system, not necessarily the output-key system. Evidence: `nix/den/aspects/editor/default.nix:4`, `nix/nvim.nix/config/globals.nix:6`, `nix/nvim.nix/default.nix:78`, `nix/nvim.nix/default.nix:70`.

## 3. Defined, disabled and ambiguous alternatives

Fish/Starship/tmux and AeroSpace have substantive settings. Nixvim uses a custom class and per-host resolver; a separate perSystem nvim output aliases eR17. The Universe CLI is written in Nushell, but a script interpreter is not configured personal shell adoption. Bash prompt integrations and runtime shell-script dependencies likewise do not establish Bash setup.


## 4. Machine roles and limits

Both declared hosts resolve ARM Darwin. eR17x builder systems are guest build capabilities, not extra physical hosts. Tests with igloo/tux are fixtures. No laptop/desktop role is inferred from GUI services.

Complete two-host helper-built profile inventory and three explicitly exposed configured editor output keys. Linux package keys alias the Darwin eR17 implementation and are not a claim of Linux editor build success.

# oxce5__chimera: census notes

[Config page](../../configs/oxce5__chimera.md) · upstream [oxce5/chimera](https://github.com/oxce5/chimera) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `cc96a65abd5d`.

Two literal x86 Linux hosts connect to explicit host/user roles in one assignment module (`modules/assignments.nix:114`).

## 2. Software selected and traces

Oxce5→workstation-user→desktop-base and NVF full; Rei→pentest-user→desktop-base and NVF minimal. Both default to Fish. Mutual-provider is explicit in user schema (`modules/den.nix:9`).

- **niri / niri** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive display/input/layout settings derived from this host displays. Evidence: `modules/desktops/niri/default.nix:74`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:54`.
- **fish / fish** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/programs/fish.nix:13`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:57`.
- **bash / bash** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/shell.nix:14`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:50`.
- **starship / starship** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/shell.nix:19`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:50`.
- **fish / fish** (default, nixos, enabled): Desktop-base explicitly selects user-shell fish. Evidence: `modules/assignments.nix:51`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`.
- **neovim / nvf/full** (configured, home-linux, enabled): The user role selects NVF full; both profiles include the enabled base with substantial core options, keymaps and autocmds. Evidence: `modules/programs/neovim/default.nix:7`, `modules/programs/neovim/default.nix:11`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:85`, `modules/programs/neovim/profiles.nix:7`.
- **neovim / nvf/full** (default, home-linux, enabled): The selected common NVF base explicitly sets defaultEditor=true. Evidence: `modules/programs/neovim/default.nix:9`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:85`.
- **other_multiplexer / herdr** (configured, home-linux, enabled): The user role selects Herdr base, which imports its HM module and enables it. VM-specific plugin settings arrive through a separate explicitly mutual provider. Evidence: `modules/programs/herdr/herdr.nix:9`, `modules/users/oxce5.nix:4`, `modules/assignments.nix:137`, `modules/assignments.nix:64`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:84`.
- **niri / niri** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive display/input/layout settings derived from this host displays. Evidence: `modules/desktops/niri/default.nix:74`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:54`.
- **fish / fish** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/programs/fish.nix:13`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:57`.
- **bash / bash** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/shell.nix:14`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:50`.
- **starship / starship** (configured, home-linux, enabled): The selected user role includes desktop-base, which directly selects this contribution with substantive shell/prompt settings. Evidence: `modules/shell.nix:19`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:50`.
- **fish / fish** (default, nixos, enabled): Desktop-base explicitly selects user-shell fish. Evidence: `modules/assignments.nix:51`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`.
- **neovim / nvf/minimal** (configured, home-linux, enabled): The user role selects NVF minimal; both profiles include the enabled base with substantial core options, keymaps and autocmds. Evidence: `modules/programs/neovim/default.nix:7`, `modules/programs/neovim/default.nix:11`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:106`, `modules/programs/neovim/profiles.nix:7`.
- **neovim / nvf/minimal** (default, home-linux, enabled): The selected common NVF base explicitly sets defaultEditor=true. Evidence: `modules/programs/neovim/default.nix:9`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:106`.
- **other_multiplexer / herdr** (configured, home-linux, enabled): The user role selects Herdr base, which imports its HM module and enables it. VM-specific plugin settings arrive through a separate explicitly mutual provider. Evidence: `modules/programs/herdr/herdr.nix:9`, `modules/users/rei.nix:4`, `modules/assignments.nix:144`, `modules/assignments.nix:98`, `modules/den.nix:9`, `modules/den.nix:10`, `modules/assignments.nix:105`.
- **niri / niri** (default, nixos, enabled): Machina-mori greetd default_session explicitly launches niri-session as rei. Evidence: `modules/hosts/machina-mori/default.nix:26`, `modules/users/rei.nix:4`.

## 3. Defined, disabled and ambiguous alternatives

The full/minimal distinction changes editor extras, not family counts. Niri settings consume each concrete host display inventory. Herdr is retained as optional multiplexer; no tmux/Zellij inference follows from editor split bindings. Nushell integration false is not a Nushell config.


## 4. Machine roles and limits

Overlord explicitly selects laptop, which includes workstation. Machina-mori explicitly selects VM and guest, also including workstation. Desktop denotes the source workstation role; it does not assert a VM has physical desktop chassis.

Complete literal two-host inventory. No configured standalone editor package output is declared; NVF is an HM contribution.

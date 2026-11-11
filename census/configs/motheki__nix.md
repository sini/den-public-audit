# motheki__nix: census notes

[Config page](../../configs/motheki__nix.md) · upstream [motheki/nix](https://github.com/motheki/nix) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `e75e72ed08cc`.

One ARM Darwin MacBook Pro uses shared identity and host-qualified workload composition.

## 2. Software selected and traces

The host-qualified Motheki aspect selects workstation and editor-full (`modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`). Editor-navigation and every language group include core, so substantial Nixvim configuration is statically selected.

- **zsh / zsh** (configured, home-darwin, enabled): Host-qualified user aspect explicitly selects workstation→shell. Actual keymap/history/greeting or edit-mode settings supplement enablement; login remains Zsh. Evidence: `modules/aspects/features/shell.nix:33`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`.
- **fish / fish** (configured, home-darwin, enabled): Host-qualified user aspect explicitly selects workstation→shell. Actual keymap/history/greeting or edit-mode settings supplement enablement; login remains Zsh. Evidence: `modules/aspects/features/shell.nix:47`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`.
- **nushell / nushell** (configured, home-darwin, enabled): Host-qualified user aspect explicitly selects workstation→shell. Actual keymap/history/greeting or edit-mode settings supplement enablement; login remains Zsh. Evidence: `modules/aspects/features/shell.nix:52`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`.
- **bash / bash** (configured, home-darwin, enabled): Host-qualified user aspect explicitly selects workstation→shell. This is bare enablement/integration without substantive application settings. Evidence: `modules/aspects/features/shell.nix:29`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`.
- **starship / starship** (configured, home-darwin, enabled): Host-qualified user aspect explicitly selects workstation→shell. This is bare enablement/integration without substantive application settings. Evidence: `modules/aspects/features/shell.nix:12`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`.
- **zsh / zsh** (default, darwin, enabled): Shared named user explicitly selects user-shell zsh. Evidence: `modules/aspects/users/motheki.nix:5`, `modules/inventory/hosts.nix:4`.
- **neovim / nixvim** (configured, home-darwin, enabled): Workstation editor-navigation includes editor-core; editor-full adds the four explicitly selected language groups. Nixvim has substantive options, LSPs, plugin settings and colorscheme. Evidence: `modules/aspects/features/editor-core.nix:5`, `modules/aspects/features/editor-core.nix:54`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`, `modules/aspects/profiles/workstation.nix:14`, `modules/aspects/features/editor-navigation.nix:3`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:8`, `modules/aspects/features/editor-languages.nix:5`.
- **neovim / nixvim** (default, home-darwin, enabled): Selected editor-core explicitly sets defaultEditor=true. Evidence: `modules/aspects/features/editor-core.nix:10`, `modules/inventory/hosts.nix:4`, `modules/defaults.nix:36`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:11`, `modules/aspects/features/editor-navigation.nix:3`.
- **other_multiplexer / tuios** (installed, home-darwin, enabled): The selected utilities profile installs Tuios without local multiplexer settings. Evidence: `modules/aspects/features/utilities.nix:9`, `modules/inventory/hosts.nix:4`, `modules/aspects/users/motheki@mothekis-macbook-pro.nix:7`, `modules/aspects/profiles/workstation.nix:12`.

## 3. Defined, disabled and ambiguous alternatives

Zsh is explicit login default. Fish/Nushell are configured alternatives; Bash/Starship are enable-only. Optional editor-extras is not selected by editor-full; input pins do not supply extra editor families. Tuios is installed-only.


## 4. Machine roles and limits

Darwin inventory is explicit; MacBook/M1 Pro supports inferred laptop. Desktop role means selected workstation profile, not a conflicting chassis claim. Linux-builder remains an opt-in comment, not another host.

Complete one-host literal inventory; reusable module exports do not add managed targets or standalone configured editor packages.

# Steven-S1020__Nixos-Configuration: census notes

[Config page](../../configs/Steven-S1020__Nixos-Configuration.md) · upstream [Steven-S1020/Nixos-Configuration](https://github.com/Steven-S1020/Nixos-Configuration) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `89fd086f61a5`.

Two declared NixOS hosts have a steven Home Manager context. The README also mentions Vigil, but it is not declared in the live Den inventory (`README.md:32`).

## 2. Software selected and traces

The named user directly selects CLI; both host providers select graphical features. Exact locked Den helper inspection confirms built-in cross-entity provider consumption, so these traces are verified despite no explicit mutual-provider include. Pinned-helper verification: `flake.lock:77` pins Den `e8e8de1e32646456cfc613f152175a7a548508ec`. Static read of [provide.nix](https://raw.githubusercontent.com/vic/den/e8e8de1e32646456cfc613f152175a7a548508ec/nix/lib/aspects/fx/aspect/provide.nix) (SHA-256 `e147fa13e3e4492dcd431c9dd218074464b783bfd590780f641182b5c032e332`), mkCrossPolicy and emitAspectPolicies, proves built-in to-users/to-hosts/named-provider consumption without an explicit mutual-provider battery. Its compatibility shim is inert. No Nix evaluation was performed.

- **bash / bash** (configured, home-linux, enabled): The named user includes CLI, which selects the enabled Bash configuration with prompt initialization. Evidence: `modules/programs/configs/bash.nix:5`, `modules/programs/configs/bash.nix:7`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `modules/defaults.nix:31`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:4`.
- **zsh / zsh** (configured, home-linux, enabled): CLI selects the enabled Zsh aspect with keymap, aliases and interactive configuration. Evidence: `modules/programs/configs/zsh.nix:5`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `modules/defaults.nix:31`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:4`.
- **starship / starship** (configured, home-linux, enabled): CLI selects Starship with a substantial format/settings body. Evidence: `modules/programs/configs/starship.nix:5`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `modules/defaults.nix:31`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:4`.
- **neovim / neovim** (configured, home-linux, enabled): CLI selects a Home Manager link to the tracked native Neovim tree; init imports globals, options, diagnostics, keymaps and plugin setup. Deployment assumes the checkout exists at /etc/nixos. Evidence: `modules/programs/configs/neovim.nix:43`, `modules/programs/configs/_neovim/init.lua:3`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `modules/defaults.nix:31`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:4`.
- **neovim / neovim** (configured, nixos, enabled): Pinned Den registers and consumes cross-entity providers automatically; the named user selects CLI→Neovim, whose NixOS class enables Neovim with aliases/runtime settings. OS-class content is retained in the enclosing host. Evidence: `modules/programs/configs/neovim.nix:9`, `modules/programs/configs/neovim.nix:13`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `modules/defaults.nix:31`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:4`, `flake.lock:77`.
- **hyprland / hyprland** (configured, home-linux, enabled): Pinned Den registers and consumes cross-entity providers automatically; both host to-users providers select Hyprland with substantive tracked Lua settings. Evidence: `modules/desktop/hyprland.nix:8`, `modules/desktop/hyprland.nix:19`, `modules/desktop/_hypr/init.lua:76`, `modules/hosts/azami/azami.nix:9`, `modules/hosts/deimos/deimos.nix:9`, `flake.lock:77`.
- **neovim / neovim** (default, nixos, enabled): Selected CLI Neovim body explicitly sets defaultEditor=true and EDITOR=nvim. Evidence: `modules/programs/configs/neovim.nix:13`, `modules/users/steven.nix:9`, `modules/programs/cli.nix:11`, `flake.lock:77`.
- **zsh / zsh** (default, nixos, enabled): The named user explicitly selects user-shell zsh; locked helper assigns the OS account shell and enables shell at OS/HM level. Evidence: `modules/users/steven.nix:6`, `modules/hosts/azami/azami.nix:6`, `modules/hosts/deimos/deimos.nix:6`, `flake.lock:77`.

## 3. Defined, disabled and ambiguous alternatives

Hyprland has substantial tracked Lua; current editor uses native Lua rather than the README NVF reference. Language-server names containing vscode are not editor adoption. Native config deployment assumes /etc/nixos checkout exists.


## 4. Machine roles and limits

README explicitly labels Azami Laptop and Deimos Desktop (`README.md:30`, `README.md:31`). Their roles can be recorded independently of whether the current graphical provider wiring succeeds.

Complete live two-host Den inventory. README-only Vigil is excluded; no standalone home or configured editor package output is declared.

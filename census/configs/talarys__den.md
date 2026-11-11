# talarys__den: census notes

[Config page](../../configs/talarys__den.md) · upstream [talarys/den](https://github.com/talarys/den) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `469df2c2de88`.

Two NixOS hosts and a standalone home share the talarys user feature aspect (`modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`). Angle references are resolved by den __findFile (`modules/den.nix:5`).

## 2. Software selected and traces

Argos includes Plasma plus desktop applications; Void is WSL with a minimal host include list. Both host users and the standalone home match talarys and select fish, Nushell, Starship and the CLI/development package sets. Global host-aspects establishes HM reachability for Argos host application/xdg contributions (`modules/defaults.nix:69`).

- **kde / Plasma 6** (configured, nixos, enabled): Argos explicitly includes desktop/kde, whose NixOS body enables Plasma 6; the WSL host does not include it. Evidence: `modules/desktop/kde.nix:7`, `modules/hosts/argos.nix:55`.
- **vscode / vscode** (installed, home-linux, enabled): Argos includes apps/apps; host-aspects carries its HM package list to talarys. VS Code has package selection here, not a settings module. Evidence: `modules/apps/apps.nix:14`, `modules/hosts/argos.nix:59`, `modules/defaults.nix:69`.
- **vscode / vscode** (default, home-linux, enabled): Argos additionally selects system/xdg, explicitly assigning home EDITOR/GIT_EDITOR and text MIME defaults to code. Evidence: `modules/system/xdg.nix:8`, `modules/system/xdg.nix:20`, `modules/hosts/argos.nix:51`, `modules/defaults.nix:69`.
- **neovim / external talarys/neovim package** (installed, home-linux, enabled): Every talarys user/home selects shell/dev, which installs neovim. Host overlays replace the package from an external flake; that external editor implementation was not inspected, so configuration is not inferred from its pin. Evidence: `modules/shell/dev.nix:7`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:16`.
- **neovim / neovim** (default, nixos, enabled): Selected talarys user aspect includes shell/env, whose NixOS contribution sets system EDITOR/VISUAL=nvim. This OS-level default is distinct from Argos HM code defaults; it does not apply to the standalone home NixOS class. Evidence: `modules/shell/env.nix:5`, `modules/users/talarys.nix:21`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`.
- **fish / fish** (configured, home-linux, enabled): All talarys contexts select shell/fish and its enabled HM configuration. This does not make fish the OS login shell. Evidence: `modules/shell/fish.nix:7`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:18`.
- **nushell / nushell** (configured, home-linux, enabled): All talarys contexts also select enabled/configured Nushell, with actual extraConfig and aliases. Evidence: `modules/shell/nushell.nix:5`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:19`.
- **nushell / nushell** (default, nixos, enabled): The named user aspect explicitly sets users.users.talarys.shell to Nushell in NixOS. The standalone HM target has no such OS login-shell mutation. Evidence: `modules/users/talarys.nix:32`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:8`.
- **tmux / tmux** (installed, home-linux, enabled): The selected CLI package list installs tmux without tmux settings or an automatic/default multiplexer session. Evidence: `modules/shell/cli.nix:17`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:15`.
- **zellij / zellij** (installed, home-linux, enabled): The same CLI list installs Zellij; no Zellij settings are supplied in this contribution. Evidence: `modules/shell/cli.nix:15`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:15`.
- **starship / starship** (configured, home-linux, enabled): Selected shell/utils enables Starship and integrations for both configured fish and Nushell. Evidence: `modules/shell/utils.nix:6`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:14`.
- **other_multiplexer / herdr** (installed, home-linux, enabled): The author labels herdr a multiplexer and installs it in the same CLI list; it is an optional peer, not exhaustive peer coverage. Evidence: `modules/shell/cli.nix:16`, `modules/users/talarys.nix:9`, `modules/defaults.nix:9`, `modules/hosts/argos.nix:7`, `modules/hosts/void.nix:7`, `modules/users/talarys.nix:6`, `modules/users/talarys.nix:15`.

## 3. Defined, disabled and ambiguous alternatives

Niri and Hyprland exist as enabled definitions but are not verified selections; Argos Niri reference is commented (`modules/hosts/argos.nix:56`). Neovim, tmux, Zellij and herdr package selection is installation-only; no native configuration is inferred from package names or external pins. Fish and Nushell are both configured, but only Nushell is explicitly assigned as the OS login shell. OS EDITOR=nvim and Argos HM EDITOR=code occur at different scopes and are retained separately, not collapsed into one universal default.

- **niri** (defined, enabled, configured): Live Niri aspect enables the compositor, but Argos selection is commented and Void selects only overlays/ssh; no target inclusion was established. Evidence: `modules/desktop/niri.nix:20`.
- **hyprland** (defined, enabled, configured): Live Hyprland aspect has an explicit enable and DMS configuration, but no concrete host selects it in the reviewed inventory. Evidence: `modules/desktop/hyprland.nix:39`.

## 4. Machine roles and limits

Void has explicit WSL role; no physical role is inferred from its name. Argos is graphical but GUI enablement alone is insufficient to label physical desktop versus laptop. The standalone home is not another machine. The external Neovim flake and secret/password validity are outside the source-only conclusion.

Inventory complete: argos and void x86_64-linux host entities plus talarys x86_64-linux standalone home. All user contexts use talarys; no inference of unique people. The NixOS-only shell/env contribution is not credited to standalone HM.

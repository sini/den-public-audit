# EzT32__nixos: census notes

[Config page](../../configs/EzT32__nixos.md) · upstream [EzT32/nixos](https://github.com/EzT32/nixos) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `aa287213a56e`.

Two NixOS hosts share a default aspect list; the ezt user uses Home Manager (`modules/den.nix:11`).

## 2. Software selected and traces

The root default includes both the common software and host-aspects (`modules/hosts/defaults.nix:15`); no optional profile guard controls the shared editor/WM choices.

- **bash / bash** (configured, home-linux, enabled): Both targets inherit the default bash aspect, enabling Home Manager Bash; this is an enable plus helper includes, not evidence of login selection. Evidence: `modules/cli/bash.nix:9`, `modules/cli/bash.nix:10`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:19`.
- **neovim / external nvim-config package** (installed, home-linux, enabled): The nvim aspect installs the external input package for host.system; its native settings are outside this source. Evidence: `modules/dev/nvim.nix:8`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:28`.
- **neovim / neovim** (default, home-linux, enabled): The same default sets Home Manager EDITOR=nvim, independently of package implementation details. Evidence: `modules/hosts/defaults.nix:12`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:28`.
- **vscode / vscode** (configured, home-linux, enabled): Both targets select substantive VS Code settings, extensions and the Python FHS package. Evidence: `modules/dev/vscode.nix:33`, `modules/dev/vscode.nix:41`, `modules/dev/vscode.nix:69`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:30`.
- **hyprland / hyprland** (configured, home-linux, enabled): Default includes select enabled Home Manager Hyprland with input/window settings and keybinding aspects. Evidence: `modules/gui/hyprland/hyprland.nix:26`, `modules/gui/hyprland/hyprland.nix:33`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:35`.
- **hyprland / hyprland** (configured, nixos, enabled): The same selected aspect enables the NixOS compositor with UWSM. SDDM enablement does not establish a default user session. Evidence: `modules/gui/hyprland/hyprland.nix:72`, `modules/den.nix:11`, `modules/den.nix:14`, `modules/hosts/defaults.nix:15`, `modules/hosts/defaults.nix:16`, `modules/hosts/defaults.nix:35`.

## 3. Defined, disabled and ambiguous alternatives

Neovim is an external package installation plus explicit EDITOR default, not locally reviewed native editor configuration. Bash is enabled without an explicit login assignment. GNOME keyring in SDDM is not a GNOME desktop (`modules/services/sddm.nix:17`). No live local contributions for the remaining required families were found.


## 4. Machine roles and limits

The inventory explicitly names desktop and laptop (`modules/den.nix:15`, `modules/den.nix:16`); laptop also imports ThinkPad hardware (`modules/hosts/laptop/configuration.nix:9`). No default graphical session is inferred from SDDM.

Complete literal two-host inventory; no standalone homes or configured package outputs are declared.

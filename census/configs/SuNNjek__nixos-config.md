# SuNNjek__nixos-config: census notes

[Config page](../../configs/SuNNjek__nixos-config.md) · upstream [SuNNjek/nixos-config](https://github.com/SuNNjek/nixos-config) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `f40297e9d045`.

Two NixOS hosts share the robin Home Manager user, desktop tooling and development profile (`modules/hosts.nix:4`).

## 2. Software selected and traces

User classes, mutual-provider and host-aspects are explicitly enabled (`modules/defaults.nix:7`, `modules/defaults.nix:15`). Both hosts directly select Niri and its dux provider; the latter forces the greeter compositor name to niri (`modules/aspects/niri/dux.nix:9`).

- **niri / niri** (configured, nixos, enabled): Both host aspects explicitly select Niri; the NixOS contribution enables the compositor. Evidence: `modules/aspects/niri/niri.nix:12`, `modules/hosts.nix:4`, `modules/defaults.nix:8`, `modules/defaults.nix:9`, `modules/defaults.nix:15`, `modules/robin-pc.nix:15`, `modules/robin-thinkpad.nix:20`.
- **niri / niri** (configured, home-linux, enabled): Mutual-provider and host-aspects connect the selected host Niri aspect to robin; its custom HM module consumes structured KDL configuration under cfg.enable=true. Evidence: `modules/aspects/niri/niri.nix:26`, `modules/aspects/niri/_hm.nix:39`, `modules/aspects/niri/_hm.nix:55`, `modules/hosts.nix:4`, `modules/defaults.nix:8`, `modules/defaults.nix:9`, `modules/defaults.nix:15`, `modules/robin-pc.nix:15`, `modules/robin-thinkpad.nix:20`.
- **vscode / vscode** (configured, home-linux, enabled): Both hosts select development, which bare-enables Home Manager VS Code; no substantive editor settings are supplied here. Evidence: `modules/aspects/development.nix:65`, `modules/hosts.nix:4`, `modules/defaults.nix:8`, `modules/defaults.nix:9`, `modules/defaults.nix:15`, `modules/robin-pc.nix:15`, `modules/robin-thinkpad.nix:20`, `modules/robin-pc.nix:23`, `modules/robin-thinkpad.nix:25`.
- **zsh / zsh** (configured, home-linux, enabled): The named robin user supplies enabled Zsh with suggestions, highlighting and keymap settings. Evidence: `modules/users/robin.nix:35`, `modules/hosts.nix:8`, `modules/hosts.nix:14`, `modules/defaults.nix:8`.
- **zsh / zsh** (default, nixos, enabled): Robin explicitly selects the user-shell zsh battery, choosing its login shell. Evidence: `modules/users/robin.nix:10`, `modules/hosts.nix:8`, `modules/hosts.nix:14`.
- **starship / starship** (configured, home-linux, enabled): Robin bare-enables Starship; this establishes configuration enablement but no custom prompt settings. Evidence: `modules/users/robin.nix:33`, `modules/hosts.nix:8`, `modules/hosts.nix:14`, `modules/defaults.nix:8`.
- **other_editor / vim** (default, nixos, enabled): The unconditional NixOS default enables vim-full and explicitly chooses it as default editor; it is not Neovim. Evidence: `modules/defaults.nix:55`, `modules/defaults.nix:58`, `modules/hosts.nix:4`, `modules/defaults.nix:21`.

## 3. Defined, disabled and ambiguous alternatives

Niri has substantive KDL settings; VS Code and Starship are enable-only. Vim-full is explicitly the system default editor, not Neovim. The generic Dux greeter fallback is Hyprland (`modules/aspects/dux.nix:51`), but both selected niri.dux aspects override it. This does not prove the default user session, so no default WM row is claimed.

- **hyprland** (defined, enabled, configured): A live enabled Hyprland aspect has substantial settings/bindings, but neither host selects that aspect. Dux has separate Hyprland source settings; those alone do not enable the compositor. Evidence: `modules/aspects/hyprland/hyprland.nix:20`, `modules/aspects/hyprland/hyprland.nix:40`.

## 4. Machine roles and limits

Both hosts select the named desktop profile, recorded as explicit configured desktop role. ThinkPad additionally has inferred laptop hardware from its T480s import and laptop display profile (`modules/robin-thinkpad.nix:22`, `modules/robin-thinkpad.nix:32`). No VM role follows from KVM modules.

Complete literal two-host inventory; root VM helper outputs are deployment helpers, not additional declared host machines.

# ivokun__kebun: census notes

[Config page](../../configs/ivokun__kebun.md) · upstream [ivokun/kebun](https://github.com/ivokun/kebun) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `1038ddc22989`.

Two explicit x86 NixOS workstation targets migrate legacy plain modules into Den aspects (`modules/aspects.nix:218`).

## 2. Software selected and traces

The shared host list imports core/desktop/dev; the named ivokun user directly imports legacy HM modules and supplies username/system/inputs explicitly (`modules/users.nix:60`, `modules/users.nix:85`). No forwarding inference is needed for those direct HM imports.

- **neovim / LazyVim** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive native LazyVim configuration and wrapper tools. Evidence: `home/features/editors.nix:42`, `home/nvim/init.lua:2`, `home/nvim/lua/config/lazy.lua:17`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **tmux / tmux** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive bindings, plugins and explicit persistence timer/services. Evidence: `home/features/editors.nix:131`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **helix / helix** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive theme, keymaps and editor settings; defaultEditor is false. Evidence: `home/features/helix.nix:6`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **zsh / zsh** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive aliases, functions and environment initialization; login default remains Fish. Evidence: `home/features/shell.nix:8`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **fish / fish** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive abbreviations, functions and environment initialization. Evidence: `home/features/fish.nix:7`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **starship / starship** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive palette and prompt format. Evidence: `home/features/starship.nix:8`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **hyprland / hyprland** (configured, home-linux, enabled): The ivokun user directly imports this legacy Home Manager module on both hosts; it supplies substantive Lua entry, window/input rules and bindings; laptop-only fragments use host capability values. Evidence: `home/features/hyprland.nix:93`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **neovim / neovim** (default, home-linux, enabled): The imported editor module explicitly sets Neovim defaultEditor=true; Helix explicitly leaves it false. Evidence: `home/features/editors.nix:46`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **fish / fish** (default, nixos, enabled): The selected named user aspect explicitly assigns its OS account shell to pkgs.fish. Evidence: `modules/users.nix:29`, `modules/users.nix:37`, `flake.nix:7`, `modules/default.nix:9`, `modules/default.nix:10`, `modules/aspects.nix:219`, `modules/aspects.nix:223`, `modules/users.nix:60`.
- **hyprland / hyprland** (default, nixos, enabled): Both hosts select the imported desktop module, which explicitly sets defaultSession=hyprland-uwsm. Evidence: `modules/aspects/desktop.nix:243`, `modules/aspects.nix:15`, `modules/aspects.nix:28`, `modules/aspects.nix:202`, `modules/aspects.nix:211`.
- **zsh / zsh** (configured, nixos, enabled): Both host shared aspect lists bare-enable system Zsh; this does not choose it as login shell. Evidence: `modules/aspects.nix:37`, `modules/aspects.nix:20`, `modules/aspects.nix:202`, `modules/aspects.nix:211`.

## 3. Defined, disabled and ambiguous alternatives

Neovim/LazyVim is the default editor; Helix is an enabled configured alternative, explicitly not default (`home/features/helix.nix:8`). Fish is the explicit account shell; configured Zsh remains available. GNOME utilities, KDE applications and swaybg wallpaper are not full desktops/compositors.


## 4. Machine roles and limits

Source labels Sakura laptop and Ume desktop (`modules/aspects.nix:200`, `modules/aspects.nix:207`). Laptop capability feeds display/lid fragments; Ume is described as pre-install, so selection is static intent, not runtime use.

Complete two-host literal inventory; generated script and application packages are not standalone configured editor outputs.

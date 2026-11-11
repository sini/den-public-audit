# ~theutz/flake: census notes

[Config page](../../../configs/theutz/flake.md) · upstream [~theutz/flake](https://git.sr.ht/~theutz/flake) · [Census summary](../../summary.md)

Rev 3ede31e7a4e9.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / alternatives](#3-defined--alternatives)
- [4. Roles](#4-roles)

## 1. Project and revision
flake-file + import-tree den config with one aspect per file under `modules/aspects/`; two hosts: `kocaeli` (aarch64-darwin, `modules/host/kocaeli/kocaeli.nix`) and `istanbul` (NixOS). One user, `theutz`, with `hjem` and `homeManager` classes on both.

## 2. Software selected and traces
Selection is split three ways: the host `includes` (`<shells>`, `<packages>`, `<gui>`), the user aspect ([`theutz.nix:10-31`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/users/theutz/theutz.nix#L10-31)) and user-qualified includes placed inside feature files (`den.hosts.kocaeli.users.theutz.includes = [ <aerospace> ]`, [`aerospace.nix:444`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/aspects/aerospace.nix#L444)). `den.default` includes `host-aspects` ([`flake/den.nix:20`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/flake/den.nix#L20)).
- Shells: `shells` -> `shells._` (bash, fish, zsh, nushell, starship) and `<tui>` -> tmux and zellij. Login shell is bash (`user-shell "bash"`, [`theutz.nix:12`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/users/theutz/theutz.nix#L12)); nushell is the shell inside tmux, zellij and herdr; fish is a bare `enable`.
- Editor: custom nvf-based neovim package; the `editors.nvf` aspect pushes it to hosts with EDITOR/VISUAL=nvim through `provides.to-hosts` ([`editors/nvf.nix:62-75`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/aspects/editors/nvf.nix#L62-75)). Also a package target `nvf`.
- macOS: aerospace (kocaeli only). OmniWM and rift are defined with their includes commented out.
- Linux: niri and waybar via `gui._` on istanbul, but istanbul also enables GDM + GNOME at host level ([`istanbul.nix:118-119`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/host/istanbul/istanbul.nix#L118-119)), a surprising pair; the default session is therefore not demonstrably niri.

## 3. Defined / alternatives
omniwm, rift (commented-out host includes); `gui.noctalia` excluded ([`gui.nix:17`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/aspects/gui/gui.nix#L17)); sketchybar excluded on kocaeli ([`kocaeli.nix:41`](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/host/kocaeli/kocaeli.nix#L41)). No helix, vscode, emacs, zed, KDE, hyprland, sway, yabai.

## 4. Roles
kocaeli: darwin explicit (no form factor stated). istanbul: laptop inferred from lid-switch settings. Neither is a server or VM.

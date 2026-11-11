# neonvoidx__nix: census notes

[Config page](../../configs/neonvoidx__nix.md) · upstream [neonvoidx/nix](https://github.com/neonvoidx/nix) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `50ad179a5fb4`.

Two NixOS hosts share the neonvoid HM context and explicit global Zsh choice (`modules/den.nix:43`).

## 2. Software selected and traces

The named user selects editor, shells, prompt and Umbriel (`modules/users/neonvoid/neonvoid.nix:21`, `modules/users/neonvoid/neonvoid.nix:41`). Host monitor data drives actual output settings (`modules/desktop/umbriel.nix:121`, `modules/desktop/umbriel.nix:200`).

- **neovim / external nvim-config package** (installed, home-linux, enabled): The named user selects nvim, installing the external configured package for its platform. Its settings are not supplied locally. Evidence: `modules/ide/nvim.nix:6`, `modules/ide/nvim.nix:7`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:21`.
- **neovim / neovim** (default, home-linux, enabled): Selected common explicitly sets EDITOR and VISUAL to nvim. Evidence: `modules/home/common.nix:20`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:52`.
- **zsh / zsh** (configured, home-linux, enabled): The named user selects substantive Zsh history, plugin, completion and alias settings. Evidence: `modules/shell/zsh.nix:20`, `modules/shell/zsh.nix:23`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:28`.
- **zsh / zsh** (default, nixos, enabled): Global default explicitly chooses the user-shell zsh battery for declared users. Evidence: `modules/den.nix:43`, `modules/den.nix:37`, `modules/hosts.nix:53`.
- **bash / bash** (configured, home-linux, enabled): Selected common bare-enables Bash for script/interactive availability, not login selection. Evidence: `modules/home/common.nix:49`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:52`.
- **starship / starship** (configured, home-linux, enabled): Selected Starship sets prompt format and character symbols. Fish integration toggles do not establish Fish configuration/adoption. Evidence: `modules/shell/starship.nix:5`, `modules/shell/starship.nix:9`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:24`.
- **other_wm / umbriel** (configured, home-linux, enabled): The user selects Umbriel, supplying substantive settings and output derivation from each concrete host monitor inventory. Voidframe follows the builtin-monitor branch; void follows its multi-monitor branches. Evidence: `modules/desktop/umbriel.nix:145`, `modules/desktop/umbriel.nix:147`, `modules/desktop/umbriel.nix:200`, `modules/den.nix:18`, `modules/hosts.nix:55`, `modules/hosts.nix:179`, `modules/users/neonvoid/neonvoid.nix:4`, `modules/users/neonvoid/neonvoid.nix:41`.

## 3. Defined, disabled and ambiguous alternatives

Umbriel is retained as other_wm rather than mislabeled Niri or Hyprland. External Neovim package installation and EDITOR/VISUAL defaults are separate from locally reviewed app settings. GNOME keyring and KDE Okular are not full desktop environments; enabling Fish prompt integration does not enable Fish.


## 4. Machine roles and limits

Voidframe explicitly sets isLaptop=true. Void is a gaming/multi-monitor context, but source does not establish chassis sufficiently to infer laptop versus desktop from GUI alone.

Complete literal two-host x86 Linux inventory; no standalone homes or configured package outputs are declared.

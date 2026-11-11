---
title: "auscyber/dotfiles: census notes"
---

[Config page](/configs/auscyber/dotfiles/) · upstream [auscyber/dotfiles](https://github.com/auscyber/dotfiles) · [Census summary](/census/summary/)

Revision `96be028eaba6`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Twelve explicit Den hosts include NixOS/Darwin machines, an iOS device and an ESPHome microcontroller, plus one standalone Linux home and real portable Nixvim package outputs. Mobile/ESP outputs are first-class configuration targets rather than invented NixOS hosts.

## Software selected and host/user traces

Global home-base selects shell and Starship; actual identity providers choose Fish/Nixvim. Mac mini inherits shared ivypierlot configuration despite an empty named provider. The exact pinned Den 0f7675b0b789eabe1a62f8a31b5323a7ad3ca5c4 user-shell and provide implementations were read from immutable raw URLs under https://raw.githubusercontent.com/denful/den/0f7675b0b789eabe1a62f8a31b5323a7ad3ca5c4/ ; user-shell sets OS account shell and HM enable, and provide.nix delivers named providers at user/home scopes. Root flake.lock binds that pin; [patched-inputs.nix:61](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/patched-inputs.nix#L61) applies only lib-gen.patch.

## Defined, disabled and ambiguous alternatives

OS shell baseline installs plain Neovim everywhere, separately from substantial user Nixvim and standalone package. Plasma OS enable is selected, but rich hmLinux settings have no verified forward ([aspects/base/home.nix:17](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/home.nix#L17) comments Linux out). Niri, Hyprland, Yabai, Zed, Emacs and rich Zsh remain available definitions. Paneru is the selected Mac tiler. Aliases and shell-init fragments do not establish otherwise disabled programs.

## Machine roles and remaining unknowns

Documented Chromebook/MacBook/Surface hardware supports laptop roles, WSL has actual module import, cache container explicitly server. GUI/gaming labels do not prove auspc chassis. Ivy person object explicitly links several account names, but this census does not infer human counts from logins. Inventory includes all declared Den roots and nvim package systems; additional dynamic package/apps/container outputs are not completely inventoried.

---
title: "sm-f/nix: census notes"
---

[Config page](/configs/sm-f/nix/) · upstream [sm-f/nix](https://github.com/sm-f/nix) · [Census summary](/census/summary/)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `23820eea5e00`.

One explicit NixOS host uses Hjem for Scott ([`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6)). Shell settings live in the OS class; Neovim native files live in the user Hjem class.

## 2. Software selected and traces

Eris directly selects shells/Niri, while Scott directly selects nvim and Nushell user-shell. Locked Den built-in provider consumption also routes the native Niri Hjem body. Pinned-helper verification: [`flake.lock:24`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/flake.lock#L24) pins Den `bf2504f9f2e8621fee091335132ab3ae698cf808`. Static read of [provide.nix](https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/aspects/fx/aspect/provide.nix) (SHA-256 `4b9b45b3c2720a425df03634f2076d5845c264ac804b59feaf27df28cdb9b553`), mkCrossPolicy and emitAspectPolicies, proves built-in to-users/to-hosts/named-provider consumption without an explicit mutual-provider battery. Its compatibility shim is inert. No Nix evaluation was performed.

- **neovim / raw/nightly** (configured, other-os, enabled): Scott directly selects nvim Hjem class; it installs Neovim and links tracked native Lua from the explicit /home/scott/git/nix checkout. Native files supply options/plugins/keymaps. Evidence: [`modules/nvim.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nvim.nix#L9), [`modules/nvim.nix:31`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nvim.nix#L31), [`nvim/init.lua:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/nvim/init.lua#L3), [`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6), [`modules/den.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L9), [`modules/hosts/eris.nix:4`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L4), [`modules/hosts/eris.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L9).
- **neovim / neovim** (default, nixos, enabled): Selected host shells explicitly sets EDITOR=nvim. Evidence: [`modules/shells.nix:22`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L22), [`modules/hosts/eris.nix:27`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L27).
- **nushell / nushell** (configured, nixos, enabled): The selected host aspect supplies substantial Nushell aliases, config and generated completion/source integration. Evidence: [`modules/shells.nix:135`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L135), [`modules/shells.nix:137`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L137), [`modules/hosts/eris.nix:27`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L27).
- **nushell / nushell** (default, nixos, enabled): Scott explicitly selects user-shell nushell. Evidence: [`modules/hosts/eris.nix:13`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L13), [`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6), [`modules/den.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L9), [`modules/hosts/eris.nix:4`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L4).
- **zsh / zsh** (configured, nixos, enabled): The host aspect configures enabled Zsh with history, aliases and options; this is available alongside Nushell, not the account default. Evidence: [`modules/shells.nix:90`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L90), [`modules/hosts/eris.nix:27`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L27).
- **starship / starship** (configured, nixos, enabled): The host shells aspect supplies substantial Starship format/module settings. Evidence: [`modules/shells.nix:50`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L50), [`modules/shells.nix:54`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L54), [`modules/hosts/eris.nix:27`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L27).
- **niri / niri** (configured, nixos, enabled): Eris selects enabled Niri plus substantive greeter compositor/output settings. This proves configured compositor plumbing, not a default user session. Evidence: [`modules/niri.nix:14`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L14), [`modules/niri.nix:47`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L47), [`modules/hosts/eris.nix:24`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L24).
- **niri / niri** (configured, other-os, enabled): Eris selects Niri; locked Den automatically consumes its to-users Hjem provider. It links tracked native KDL configuration from the explicit checkout path. Settings include appearance/input/bindings/output/window-rule fragments. Evidence: [`modules/niri.nix:83`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L83), [`modules/niri.nix:92`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L92), [`dotfiles/niri/config.kdl:2`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/dotfiles/niri/config.kdl#L2), [`modules/hosts/eris.nix:24`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L24), [`flake.lock:24`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/flake.lock#L24).

## 3. Defined, disabled and ambiguous alternatives

Neovim native init imports tracked options/plugin/keymap modules; checkout path is fixed by utils ([`utils/default.nix:2`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/utils/default.nix#L2)). Zsh is substantively configured alongside account-default Nushell. Bash language server and completion bridges do not establish configured Bash/Fish.


## 4. Machine roles and limits

Laptop inference uses selected battery and lid policy ([`modules/power-management.nix:26`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/power-management.nix#L26), [`modules/power-management.nix:38`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/power-management.nix#L38)). No default user session is inferred from the greeter compositor name.

Complete one-host literal inventory. Hjem user contributions use other-os platform because the schema has no Hjem-specific platform label; target class records NixOS deployment.

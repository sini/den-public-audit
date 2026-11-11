# thomasgoulet__nixnites: census notes

[Config page](../../configs/thomasgoulet__nixnites.md) · upstream [thomasgoulet/nixnites](https://github.com/thomasgoulet/nixnites) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `54d53d7979ed`.

Two Linux hosts use explicit user and HM classes; Oric enables WSL and Yousuke selects graphical software through Thom.

## 2. Software selected and traces

Terminal includes editor and Nushell. Its nested imports explicitly load editor and prompt bodies despite the shallow root regex (`flake.nix:46`, `nix/features/terminal.nix:21`). A separate package builder exports configured Helix across four explicit systems.

- **helix / helix** (configured, home-linux, enabled): Both users select terminal→editor, which explicitly imports its nested settings/language tree. The top-level import regex intentionally excludes nested plain modules; explicit import-tree makes them reachable. Evidence: `nix/features/editor.nix:13`, `nix/features/editor/settings.nix:3`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`, `nix/features/editor.nix:10`.
- **helix / helix** (default, home-linux, enabled): Selected editor explicitly sets EDITOR=hx. Evidence: `nix/features/editor.nix:16`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`.
- **starship / starship** (configured, home-linux, enabled): Terminal explicitly imports nested terminal modules, including substantial Starship prompt settings. Evidence: `nix/features/terminal/starship.nix:4`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`, `nix/features/terminal.nix:21`.
- **nushell / nushell** (default, nixos, enabled): Selected Nushell contributes explicit user.shell=pkgs.nushell in the declared user class; native dotfile path prerequisite is tracked separately. Evidence: `nix/features/nushell.nix:7`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`, `nix/features/terminal.nix:11`.
- **niri / niri** (configured, home-linux, enabled): Only Thom selects headful; it imports nested substantive Niri settings. Thomas WSL does not select headful. Evidence: `nix/features/headful/niri.nix:8`, `nix/hosts/yousuke.nix:8`, `nix/users/thom.nix:9`, `nix/features/headful.nix:55`.
- **other_multiplexer / herdr** (installed, home-linux, enabled): Both selected terminal profiles install Herdr. Mutable dotfile Herdr settings depend on unresolved NH_FLAKE; this row establishes installation only. Evidence: `nix/features/terminal.nix:28`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`.
- **helix / helix** (configured, package, enabled): perSystem exposes Helix with generated substantive settings and language config plus helper PATH. Package assembly removes shell setting; this is independent of host users. Evidence: `nix/features/editor/settings.nix:3`, `nix/packages.nix:50`, `nix/defaults.nix:6`, `nix/packages.nix:21`, `nix/packages.nix:44`.
- **helix / helix** (configured, package, enabled): perSystem exposes Helix with generated substantive settings and language config plus helper PATH. Package assembly removes shell setting; this is independent of host users. Evidence: `nix/features/editor/settings.nix:3`, `nix/packages.nix:50`, `nix/defaults.nix:6`, `nix/packages.nix:21`, `nix/packages.nix:44`.
- **helix / helix** (configured, package, enabled): perSystem exposes Helix with generated substantive settings and language config plus helper PATH. Package assembly removes shell setting; this is independent of host users. Evidence: `nix/features/editor/settings.nix:3`, `nix/packages.nix:50`, `nix/defaults.nix:6`, `nix/packages.nix:21`, `nix/packages.nix:44`.
- **helix / helix** (configured, package, enabled): perSystem exposes Helix with generated substantive settings and language config plus helper PATH. Package assembly removes shell setting; this is independent of host users. Evidence: `nix/features/editor/settings.nix:3`, `nix/packages.nix:50`, `nix/defaults.nix:6`, `nix/packages.nix:21`, `nix/packages.nix:44`.

## 3. Defined, disabled and ambiguous alternatives

Helix and Starship substantive settings are reachable. Nushell login-shell assignment is explicit; its mutable native config reachability remains conditional on NH_FLAKE pointing to a checkout. Herdr installation is verified independently. No full GNOME/KDE desktop follows from applications or portals.

- **nushell** (ambiguous, conditional, configured): Both users select Nushell and dotfiles. Native config/environment generation is substantive, but NH_FLAKE is read from impure environment and must point to a real repository checkout; that source guard cannot be resolved statically here. Evidence: `nix/features/nushell.nix:25`, `nix/features/dotfiles.nix:60`, `nushell/config.nu:79`, `flake.nix:46`, `flake.nix:51`, `nix/hosts/oric.nix:6`, `nix/hosts/yousuke.nix:8`, `nix/users/thomas.nix:13`, `nix/users/thom.nix:13`, `nix/features/terminal.nix:9`, `nix/features/terminal.nix:11`, `nix/users/thomas.nix:8`, `nix/users/thom.nix:8`.

## 4. Machine roles and limits

Oric WSL is explicit. Yousuke laptop inference uses its eDP output and actual battery-policy source, not GUI alone. Package assembly HM context is not another declared home/machine.

Complete two-host literal inventory and four standalone configured Helix package outputs. Impure NH_FLAKE prerequisite affects activation/config reachability, not the known target names.

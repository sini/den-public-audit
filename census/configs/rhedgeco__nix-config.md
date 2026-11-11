# rhedgeco__nix-config: census notes

[Config page](../../configs/rhedgeco__nix-config.md) · upstream [rhedgeco/nix-config](https://github.com/rhedgeco/nix-config) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `fd875038e37f`.

Two explicit NixOS hosts attach per-user include lists directly to Ryan (`modules/hosts/hedgebox.nix:13`, `modules/hosts/jetpack.nix:15`).

## 2. Software selected and traces

The local flake adapter imports all modules. Users choose Glade, Fishy and Zed directly; Glade selects Niri. Default create helper consumes generated Zed settings as writable activation files (`modules/utils/create.nix:56`).

- **niri / niri** (configured, home-linux, enabled): Each user explicitly includes Glade→Niri; the aspect installs the compositor and writes substantive native KDL includes. This common chain does not require host-specific provider consumption. Evidence: `modules/aspects/niri.nix:25`, `modules/aspects/niri.nix:36`, `modules/aspects/_assets/niri/layout.kdl:1`, `flake.nix:2`, `mylib/den.nix:12`, `modules/defaults/den.nix:14`, `modules/hosts/hedgebox.nix:17`, `modules/hosts/jetpack.nix:19`, `modules/hosts/hedgebox.nix:20`, `modules/hosts/jetpack.nix:22`, `modules/aspects/glade.nix:10`.
- **niri / niri** (default, nixos, enabled): Both hosts explicitly invoke autologin ryan niri-session; initial and fallback greeter session commands consume that argument. Evidence: `modules/aspects/autologin.nix:6`, `modules/hosts/hedgebox.nix:8`, `modules/hosts/jetpack.nix:9`.
- **fish / fish** (configured, home-linux, enabled): Both users select Fishy→Fish, supplying greeting and plugins. Evidence: `modules/aspects/fish.nix:12`, `flake.nix:2`, `mylib/den.nix:12`, `modules/defaults/den.nix:14`, `modules/hosts/hedgebox.nix:17`, `modules/hosts/jetpack.nix:19`, `modules/hosts/hedgebox.nix:22`, `modules/hosts/jetpack.nix:24`, `modules/aspects/fishy.nix:5`.
- **fish / fish** (default, nixos, enabled): Fishy explicitly selects user-shell fish; this per-account choice takes precedence over generic defaultUserShell Bash. Evidence: `modules/aspects/fishy.nix:4`, `flake.nix:2`, `mylib/den.nix:12`, `modules/defaults/den.nix:14`, `modules/hosts/hedgebox.nix:17`, `modules/hosts/jetpack.nix:19`, `modules/hosts/hedgebox.nix:22`, `modules/hosts/jetpack.nix:24`.
- **starship / starship** (configured, home-linux, enabled): Fishy selects an explicit Starship init fish source hook; no substantive Starship prompt settings are supplied. Evidence: `modules/aspects/starship.nix:3`, `modules/aspects/starship.nix:5`, `flake.nix:2`, `mylib/den.nix:12`, `modules/defaults/den.nix:14`, `modules/hosts/hedgebox.nix:17`, `modules/hosts/jetpack.nix:19`, `modules/aspects/fishy.nix:6`.
- **zed / zed** (configured, home-linux, enabled): Both users directly select Zed: package, theme and generated writable settings are consumed by the default create activation helper. Host-specific provider settings are not needed to establish this common configuration. Evidence: `modules/aspects/zed.nix:32`, `modules/aspects/zed.nix:37`, `modules/utils/create.nix:55`, `flake.nix:2`, `mylib/den.nix:12`, `modules/defaults/den.nix:14`, `modules/hosts/hedgebox.nix:17`, `modules/hosts/jetpack.nix:19`, `modules/hosts/hedgebox.nix:27`, `modules/hosts/jetpack.nix:33`, `modules/utils/create.nix:3`.
- **bash / bash** (installed, nixos, enabled): Global environment.shells registers Bash. defaultUserShell also names it, but both declared users explicitly select Fish, so no current user Bash login-default claim is made. Evidence: `modules/defaults/shell.nix:4`, `modules/hosts/hedgebox.nix:3`, `modules/hosts/jetpack.nix:3`.

## 3. Defined, disabled and ambiguous alternatives

Starship is initialized by an explicit Fish hook, enable-only for prompt depth. Niri and Zed have substantive common settings even without claiming host-specific provides. GNOME portal/keyring/utilities are not a GNOME desktop. Bash registration/default fallback does not supersede explicit Fish users.


## 4. Machine roles and limits

Jetpack laptop inference cites its host-specific internal laptop screen annotation. Hedgebox physical form is unknown; Niri and monitor settings do not establish desktop chassis. build-vm overrides are not additional inventory hosts.

Complete literal two-host inventory. Local yoink gitlink is an input prerequisite; selected software described here is established by public local bodies, not guessed from yoink.

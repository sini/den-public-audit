# quasi-coherent__nix-config: census notes

[Config page](../../configs/quasi-coherent__nix-config.md) · upstream [quasi-coherent/nix-config](https://github.com/quasi-coherent/nix-config) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `52971feef21f`.

Namespace-based Darwin configuration exposes one host, one standalone home and two configured Emacs package variants on three perSystem architectures.

## 2. Software selected and traces

Daniel explicitly includes our.nix-config and stable-emacs; the bundle includes Zsh, tmux and Starship. Mutual-provider is enabled (`modules/den.nix:33`). Package outputs use their own explicit perSystem composition, not managed machine contexts.

- **zsh / zsh** (configured, home-darwin, enabled): Daniel includes our.nix-config, which directly includes this aspect; it supplies substantial native/settings behavior for host-attached and standalone homes. Evidence: `modules/a/terminal/zsh.nix:6`, `modules/my/configurations.nix:3`, `modules/my/configurations.nix:4`, `modules/my/users.nix:18`, `modules/den.nix:32`, `modules/a/terminal/zsh.nix:88`.
- **tmux / tmux** (configured, home-darwin, enabled): Daniel includes our.nix-config, which directly includes this aspect; it supplies substantial native/settings behavior for host-attached and standalone homes. Evidence: `modules/a/terminal/tmux.nix:46`, `modules/a/terminal/_files/tmux/tmux.common.conf:4`, `modules/my/configurations.nix:3`, `modules/my/configurations.nix:4`, `modules/my/users.nix:18`, `modules/den.nix:32`, `modules/a/terminal/tmux.nix:74`.
- **starship / starship** (configured, home-darwin, enabled): Daniel includes our.nix-config, which directly includes this aspect; it supplies substantial native/settings behavior for host-attached and standalone homes. Evidence: `modules/a/terminal/starship.nix:13`, `modules/my/configurations.nix:3`, `modules/my/configurations.nix:4`, `modules/my/users.nix:18`, `modules/den.nix:32`, `modules/a/terminal/starship.nix:75`.
- **emacs / stableEmacsForMyNeeds** (configured, home-darwin, enabled): Daniel explicitly selects stable-emacs, linking the tracked native Lisp tree and installing the package supplied by self perSystem. Evidence: `modules/a/development/emacs.nix:31`, `modules/a/development/_files/emacs/init.el:33`, `modules/my/configurations.nix:3`, `modules/my/configurations.nix:4`, `modules/my/users.nix:18`, `modules/den.nix:32`, `modules/my/users.nix:19`, `modules/a/development/emacs.nix:52`.
- **emacs / emacs** (default, home-darwin, enabled): The selected Emacs wrapper explicitly sets EDITOR/VISUAL to emacsclient. Evidence: `modules/a/development/emacs.nix:21`, `modules/my/configurations.nix:3`, `modules/my/configurations.nix:4`, `modules/my/users.nix:18`, `modules/den.nix:32`, `modules/my/users.nix:19`.
- **zsh / zsh** (default, darwin, enabled): The host user explicitly selects user-shell zsh; standalone home does not imply control of an OS account. Evidence: `modules/my/users.nix:12`, `modules/my/configurations.nix:4`, `modules/den.nix:33`.
- **emacs / stableEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.
- **emacs / latestEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.
- **emacs / stableEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.
- **emacs / latestEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.
- **emacs / stableEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.
- **emacs / latestEmacsForMyNeeds** (configured, package, enabled): The perSystem package output calls the local emacsWithPackages composition with stable/latest epkgs, supplying substantive editor extension selection. Evidence: `modules/a/development/_emacs/pkgsFor.nix:2`, `nix/systems.nix:6`, `modules/a/development/_emacs/default.nix:12`.

## 3. Defined, disabled and ambiguous alternatives

Stable Emacs is selected for the homes; latest remains an alternate package output. AeroSpace sits under our.disabled but is not an explicit false setting, so it is defined/unselected. Native Emacs Lisp and tmux config are substantive. Nushell syntax packages and Bash word-style choices are not shell adoption.

- **aerospace** (defined, enabled, configured): Substantial AeroSpace settings exist under a.aerospace but only our.disabled includes it; no live root selects that grouping. This is defined/unselected, not an explicit false services.enable setting. Evidence: `modules/a/applications/aerospace.nix:3`.

## 4. Machine roles and limits

Only Hemlock is a declared machine, with Darwin role explicit. The standalone home and six package outputs are separate non-machine units. No physical desktop/laptop role follows from applications or Linux CI systems.

Complete one-host/one-home inventory plus six configured package outputs from two names × three systems. Linux runner systems are package platforms, not NixOS hosts.

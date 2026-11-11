# repparw__nix: census notes

[Config page](../../configs/repparw__nix.md) · upstream [repparw/nix](https://github.com/repparw/nix) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `b2a680435a4e`.

Three literal Linux hosts use explicit per-user aspect overrides; Alpha selects GUI/gaming, while ARM Epsilon and Pi select service-host workflows.

## 2. Software selected and traces

Each user explicitly includes repparw and Fish. Shared repparw includes shell/editors/tmux; global nixvim supplies the external package overlay. Only Alpha directly includes desktop→GUI→Niri.

- **fish / fish** (configured, home-linux, enabled): Every explicit user aspect includes repparw and Fish; the shared repparw bundle selects shell/tmux. Actual plugin, initialization and binding settings make this substantive. Evidence: `modules/aspects/cli/fish.nix:62`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`.
- **bash / bash** (configured, home-linux, enabled): Every explicit user aspect includes repparw and Fish; the shared repparw bundle selects shell/tmux. Actual plugin, initialization and binding settings make this substantive. Evidence: `modules/aspects/cli/shell.nix:134`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`.
- **tmux / tmux** (configured, home-linux, enabled): Every explicit user aspect includes repparw and Fish; the shared repparw bundle selects shell/tmux. Actual plugin, initialization and binding settings make this substantive. Evidence: `modules/aspects/cli/tmux.nix:12`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`.
- **fish / fish** (default, nixos, enabled): Every explicit user selects Fish, whose includes requests user-shell fish; SSH dispatcher Bash arms do not change the account default. Evidence: `modules/aspects/cli/fish.nix:9`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`.
- **neovim / external nixvim-config** (installed, home-linux, enabled): Shared editor installs the external configured Nixvim package, extended with a Stylix exported module. Local source does not provide the underlying editor settings, so this is installation-only. Evidence: `modules/aspects/cli/editors.nix:24`, `modules/aspects/nixvim.nix:27`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`, `modules/aspects/repparw.nix:13`, `modules/defaults.nix:21`.
- **neovim / neovim** (default, home-linux, enabled): Selected editor explicitly sets EDITOR=nvim and VISUAL=$EDITOR. Evidence: `modules/aspects/cli/editors.nix:18`, `modules/entities.nix:8`, `modules/entities.nix:25`, `modules/entities.nix:36`, `modules/defaults.nix:4`, `modules/aspects/repparw.nix:9`, `modules/aspects/repparw.nix:13`.
- **niri / niri** (configured, home-linux, enabled): Alpha user explicitly selects desktop→gui→Niri, supplying substantive input/layout/window bindings; other hosts do not select GUI. The direct user HM chain does not require the to-hosts provider to prove these settings. Evidence: `modules/aspects/gui/niri.nix:119`, `modules/aspects/gui/niri.nix:124`, `modules/entities.nix:10`, `modules/aspects/desktop.nix:9`, `modules/aspects/gui/default.nix:8`.
- **niri / niri** (default, nixos, enabled): Alpha user selects desktop; locked Den built-in cross-provider consumption includes desktop.to-hosts→gui→session in its NixOS class, explicitly choosing defaultSession=niri. Evidence: `modules/aspects/gui/default.nix:30`, `modules/entities.nix:10`, `modules/aspects/desktop.nix:25`, `modules/aspects/desktop.nix:28`, `flake.lock:93`.

## 3. Defined, disabled and ambiguous alternatives

Fish account default coexists with substantive Bash fallback/SSH configuration. External Neovim is installed plus explicit EDITOR default; unseen external settings are not locally credited. Fish pure prompt is not Starship. Both direct HM Niri settings and routed OS default session are statically verified. Pinned-helper verification: `flake.lock:93` pins Den `37eb88ce28a9e42d5b367b967a9097030ff4f665`. Static read of [provide.nix](https://raw.githubusercontent.com/denful/den/37eb88ce28a9e42d5b367b967a9097030ff4f665/nix/lib/aspects/fx/aspect/provide.nix) (SHA-256 `4b9b45b3c2720a425df03634f2076d5845c264ac804b59feaf27df28cdb9b553`), mkCrossPolicy and emitAspectPolicies, proves built-in to-users/to-hosts/named-provider consumption without an explicit mutual-provider battery. Its compatibility shim is inert. No Nix evaluation was performed.


## 4. Machine roles and limits

Alpha explicit desktop plus inferred media server; Epsilon/Pi explicit service-host, with Pi described as deployment controller. Nested service containers and VM tests are not extra declared hosts.

Complete literal three-host inventory; service containers and synthetic VM tests do not add managed host targets.

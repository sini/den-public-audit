# sini__nix-config: census notes

[Config page](../../configs/sini__nix-config.md) · upstream [sini/nix-config](https://github.com/sini/nix-config) · [Census summary](../summary.md)

Record: ../records/sini__nix-config.json. All citations are repo-relative at rev `7e267a559e4a`. Static reading only; nothing was evaluated.

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Selected software and traces](#2-selected-software-and-traces)
- [3. Defined, disabled, ambiguous](#3-defined-disabled-ambiguous)
- [4. Machine roles](#4-machine-roles)

## 1. Project and inspected revision

The flake is import-tree over `modules/`; den hosts live one per file in `modules/den/hosts/`, the aspect library in `modules/den/aspects/`, users in `modules/den/users/`. Eleven den hosts were found (no other `den.hosts` or `den.homes` declaration; the other hits are readers in policies, batteries and diagrams). `generated/`, `diagrams/`, `docs/`, `images/`, `infra/`, `sites/` and `modules/den/aspects/kubernetes` were not used as selection sources.

## 2. Selected software and traces

Hosts include `roles.*`. Users arrive by policy, not by listing: `modules/den/access.nix:6` grants `system-access` and `workstation-access` per environment, `modules/den/policies/fleet.nix:50` intersects that with the union of environment and host gates, and `modules/den/policies/users.nix:106` resolves registry users onto the host. Result (derived by hand from the policy bodies): servers get sini, dvicory, vic, theutz, pol; blade and cortex get sini, vic, shuo, theutz, will; patch and slab get sini. sini's own aspect includes `den.batteries.host-aspects` (`modules/den/users/sini.nix:4`), which projects each host's home arms onto sini; the other users include only `roles.default` (`modules/den/users/vic.nix:4` etc.) plus host-qualified user aspects. The battery was read at den@bf2504f9f2e8: `modules/aspects/batteries/host-aspects.nix:24` spawns the user's classes, the spawn walks the host aspect for `homeManager` (`nix/lib/aspects/fx/resolve.nix:107`), and the user-scope detector in `nix/lib/home-env.nix:133` forwards it into `home-manager.users.<name>`. Every home-arm row cites the HM enable it reaches (e.g. `programs.zellij.enable`, `zellij.nix:254`).

| family | variant | hosts | users | trace |
|---|---|---|---|---|
| neovim | nvf, `EDITOR=nvim` | blade, cortex, uplink-dev, bitstream, patch (5 verified; slab ambiguous) | sini; bitstream also vic | host includes `roles.dev` (`roles/dev.nix:49`) -> `applications/dev/editor/nvf.nix:13,200` |
| tmux | tmux | same 6 | same | `roles/dev.nix:87` -> `mux/tmux.nix:4` |
| zellij | zellij | same 6 | same | `roles/dev.nix:88` -> `mux/zellij/zellij.nix:254` |
| starship | starship | same 6 | same | `roles/dev.nix:62` -> `shell/starship.nix:4` |
| other_multiplexer | herdr (install only) | same 6 | same | `roles/dev.nix:85` -> `mux/herdr.nix:6` |
| vscode | programs.vscode (VSCodium state dirs) | blade, cortex, patch (3) | sini | `roles/dev-gui.nix:6` (blade, cortex), `roles/darwin-workstation.nix:40` (patch) |
| gnome | GNOME via GDM, plus sini's dconf | blade, cortex (2) | system scope; dconf for sini | `roles/workstation.nix:22,23` -> `desktop/gnome.nix:30`, `desktop/gdm.nix:6` |
| aerospace | aerospace (homeDarwin) | patch (1) | sini | `roles/darwin-workstation.nix:29` -> `macos/wm/aerospace.nix:19` |
| zsh | login shell (nixos default); HM config | 9 NixOS hosts (default shell), patch (os arm and HM), slab (login shell) | all resolved users | `roles/default.nix:11,31` -> `core/users/shell.nix:20`, `applications/shell/zsh.nix:26`; slab `hosts/slab.nix:24` and `core/nix-on-droid-base.nix:37` |
| bash | root's login shell only | 9 NixOS hosts | root | `core/users/shell.nix:19` |

Families selected (distinct hosts): zsh 11, neovim 5 (+ slab ambiguous), tmux 6, zellij 6, starship 6, vscode 3, gnome 2, aerospace 1, bash 9 (root only). Per-user variation: only sini, via host-aspects, receives the roles.dev and roles.workstation home arms; vic additionally gets `roles.dev` on bitstream (`modules/den/hosts/bitstream.nix:102`). Surprising combination: `desktop.uwsm` is selected on blade and cortex (`blade.nix:42`, `cortex.nix:81`) although `desktop.hyprland` is commented out beside it, so uwsm has no WM behind it.

## 3. Defined, disabled, ambiguous

- hyprland: `desktop/hyprland.nix:31` enables `programs.hyprland`, but the only host references are comments (`blade.nix:41`, `cortex.nix:80`). Defined, not selected.
- kde: `desktop/kde.nix:4` enables plasma6; nothing includes it. Defined, not selected.
- niri: `desktop/niri/niri.nix:3` is a stub (includes uwsm, empty nixos arm); nothing includes it.
- Not found: yabai, sway (only a portal key at `desktop/xdg-portal.nix:58`), emacs (`defaultKeymap = "emacs"` is zsh), helix (a gitignore pattern), zed, fish and nushell (integration flags in starship, kitty and direnv only), recorded as references.
- Not traced: an `antigravity` VSCodium-family editor aspect included by `roles/dev-gui.nix:5`.
- Ambiguous: neovim (nvf) on slab. slab omits `roles.default`, the only consumer of the `homeManagerModules` quirk (`core/users/home-manager/home-manager.nix:71`), so the nvf HM module appears never imported on droid. The guest hosts' user sets are also not derivable statically (see below).

## 4. Machine roles

| host | system / class | roles | basis |
|---|---|---|---|
| axon-01, axon-02, axon-03 | x86_64 nixos | server (explicit) | `roles.server` at `axon-01.nix:64`, `axon-02.nix:62`, `axon-03.nix:62`; k3s cluster nodes |
| bitstream | x86_64 nixos | server (explicit) | `bitstream.nix:83`; also dev, builder, genie agents |
| uplink | x86_64 nixos | server (explicit) | `uplink.nix:76`; gateway, headscale, kanidm; microvm host for uplink-dev |
| blade | x86_64 nixos | desktop (explicit), laptop (explicit) | `roles.workstation` at `blade.nix:26` (workstation normalised to desktop); `hardware.laptop` at `blade.nix:37` |
| cortex | x86_64 nixos | desktop (explicit) | `roles.workstation` at `cortex.nix:62`; also a remote builder and microvm host, which do not add a server role |
| cortex-cuda | x86_64 nixos guest | vm (explicit), server (inferred) | `microvm.guest.enable` at `cortex-cuda.nix:164`; inference workload (`roles.inference`) with no desktop |
| uplink-dev | x86_64 nixos guest | vm (explicit) | `microvm.guest.enable` at `uplink-dev.nix:82`; dev sandbox, no server role |
| patch | aarch64 darwin | darwin (explicit), desktop (explicit) | `patch.nix:5`, `roles.darwin-workstation` at `patch.nix:17`; laptop vs desktop unknown |
| slab | aarch64-linux, class droid | none | nix-on-droid (`slab.nix:4`); none of the six census roles fits |

Counts: 11 declared host targets; explicit roles: server 5, desktop 3, laptop 1, vm 2, darwin 1; inferred: server 1. `inventory_complete` is true for host enumeration. Remaining unknowns: guest user resolution (cortex-cuda declares no users; both guests have `intoAttr = [ ]` so `env-to-hosts` skips them), the user `classes` value (taken from `users.nix:102` priority, not evaluated), and form factor of patch.

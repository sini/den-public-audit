# moxie0420__dotfiles: census notes

[Config page](../../configs/moxie0420__dotfiles.md) · upstream [moxie0420/dotfiles](https://github.com/moxie0420/dotfiles) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `42df6003db8c`.

Three Linux hosts share madelyn and namespace-based desktop/program/service aspects. The generated flake imports the full modules tree (`flake.nix:141`); defaults and user schema are in `modules/aspects/defaults.nix:36`.

## 2. Software selected and traces

Niri is selected by the laptop/desktop host aspects and explicitly projected to users; Helix follows the named user aspect on all three. Fish login choice is explicit, while Starship settings reach the OS through a to-hosts provider.

- **niri / niri** (configured, home-linux, enabled): Both named host aspects include desktop.niri; reciprocal to-users provider and global mutual-provider deliver its HM module to madelyn. The module enables niri without an unresolved condition. Evidence: `modules/aspects/programs/niri/niri.nix:7`, `modules/aspects/programs/niri/niri.nix:43`, `modules/aspects/hosts/nixOwO/nixOwO.nix:11`, `modules/aspects/hosts/nixUwU/nixUwU.nix:17`, `modules/aspects/defaults.nix:41`, `modules/aspects/programs/niri/niri.nix:47`.
- **niri / niri** (configured, nixos, enabled): The same selected niri aspect imports its NixOS module and explicitly enables the system compositor. Evidence: `modules/aspects/programs/niri/niri.nix:44`, `modules/hosts.nix:29`, `modules/hosts.nix:35`, `modules/aspects/hosts/nixOwO/nixOwO.nix:11`, `modules/aspects/hosts/nixUwU/nixUwU.nix:17`.
- **niri / niri** (default, nixos, enabled): nixUwU includes the greetd aspect; both default_session and initial_session run niri-session for the user-bound session. nixOwO has no verified default-session assignment here. Evidence: `modules/aspects/services/displayManager/greetd.nix:14`, `modules/hosts.nix:35`, `modules/aspects/hosts/nixUwU/nixUwU.nix:40`.
- **helix / helix** (configured, home-linux, enabled): Every inventory host declares madelyn, whose named user aspect includes the configured HM Helix aspect. Evidence: `modules/aspects/programs/helix/helix.nix:15`, `modules/hosts.nix:31`, `modules/hosts.nix:42`, `modules/hosts.nix:49`, `modules/aspects/users/madelyn.nix:18`, `modules/aspects/defaults.nix:79`.
- **helix / helix** (default, home-linux, enabled): The selected HM Helix module explicitly sets defaultEditor; this is stronger than the separate package install. Evidence: `modules/aspects/programs/helix/helix.nix:17`, `modules/aspects/users/madelyn.nix:18`, `modules/aspects/defaults.nix:79`, `modules/hosts.nix:31`, `modules/hosts.nix:42`, `modules/hosts.nix:49`.
- **helix / helix** (installed, nixos, enabled): TheHub host body separately installs plain Helix system-wide; this package-only contribution does not establish system-wide editor configuration. Evidence: `modules/aspects/hosts/theHub/theHub.nix:23`, `modules/hosts.nix:46`.
- **fish / fish** (configured, home-linux, enabled): The user schema includes system.shell, which supplies fish greeting and plugin configuration in HM. Evidence: `modules/aspects/system/shell/shell.nix:19`, `modules/aspects/defaults.nix:72`, `modules/aspects/defaults.nix:79`, `modules/hosts.nix:31`, `modules/hosts.nix:42`, `modules/hosts.nix:49`.
- **fish / fish** (default, nixos, enabled): The automatically matched madelyn aspect explicitly selects den user-shell fish for her OS login shell. Evidence: `modules/aspects/users/madelyn.nix:12`, `modules/hosts.nix:31`, `modules/hosts.nix:42`, `modules/hosts.nix:49`.
- **starship / starship** (configured, nixos, enabled): Madelyn includes programs.starship, whose to-hosts provider is activated through mutual-provider. The enabled settings are NixOS content; the commented to-users provider is not credited. Evidence: `modules/aspects/programs/starship.nix:22`, `modules/aspects/users/madelyn.nix:25`, `modules/aspects/programs/starship.nix:159`, `modules/aspects/defaults.nix:41`, `modules/hosts.nix:31`, `modules/hosts.nix:42`, `modules/hosts.nix:49`.

## 3. Defined, disabled and ambiguous alternatives

No KDE desktop is credited for plasma-login-manager (`modules/aspects/services/displayManager/plasmaLoginManager.nix:4`); a login manager is not Plasma desktop enablement. Swayidle/GTK or GNOME utility packages are not Sway/GNOME sessions. Helix language-server strings mentioning vscode are not a VS Code editor definition (`modules/aspects/programs/helix/helix.nix:51`). Other required families have no live local contribution in the inspected feature/body scope.


## 4. Machine roles and limits

Laptop/desktop/server labels come directly from the inventory; nixUwU additionally receives inferred server role from its selected media/file-service workload. Comments listing web hosts are not targets. The aarch64-linux flake systems entry is not an ARM managed host. These are configured account contexts, not distinct humans; static reachability does not establish successful secret provisioning or runtime sessions.

Inventory complete: exactly nixOwO, nixUwU and theHub; commented web-0..web-3 are omitted (`modules/hosts.nix:52`). No standalone home or independently configured editor package target is declared.

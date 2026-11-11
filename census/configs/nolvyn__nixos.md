# nolvyn__nixos: census notes

[Config page](../../configs/nolvyn__nixos.md) · upstream [nolvyn/nixos](https://github.com/nolvyn/nixos) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `e0fd0f9f0537`.

Two platform-specific hosts opt into a cross-platform workstation profile (`modules/aspects/profiles/workstation.nix:3`).

## 2. Software selected and traces

Both named users select primaryUser, including host-aspects; this supplies host-selected workstation software to the HM contexts (`modules/aspects/user.nix:6`). Linux desktop and Darwin OmniWM selections remain platform-specific.

- **fish / fish** (configured, home-darwin, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive aliases, initialization and plugin settings. Evidence: `modules/aspects/fish.nix:80`, `modules/aspects/hosts/astraeus/astraeus.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/astraeus/astraeus.nix:11`, `modules/aspects/profiles/workstation.nix:18`.
- **vscode / vscode** (configured, home-darwin, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive language settings and extensions, with Linux-only Qt arms resolved by platform. Evidence: `modules/aspects/vscode.nix:27`, `modules/aspects/hosts/astraeus/astraeus.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/astraeus/astraeus.nix:11`, `modules/aspects/profiles/workstation.nix:24`.
- **zed / zed** (configured, home-darwin, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive editor/LSP settings, with Linux-only theme arm. Evidence: `modules/aspects/zed.nix:16`, `modules/aspects/hosts/astraeus/astraeus.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/astraeus/astraeus.nix:11`, `modules/aspects/profiles/workstation.nix:25`.
- **fish / fish** (default, darwin, enabled): The named user explicitly selects user-shell fish; Darwin also has a desired UserShell reconciliation in the selected Fish aspect. Evidence: `modules/aspects/user.nix:29`, `modules/aspects/hosts/astraeus/astraeus.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/astraeus/astraeus.nix:11`.
- **fish / fish** (configured, home-linux, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive aliases, initialization and plugin settings. Evidence: `modules/aspects/fish.nix:80`, `modules/aspects/hosts/weebmachine/weebmachine.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/weebmachine/weebmachine.nix:13`, `modules/aspects/profiles/workstation.nix:18`.
- **vscode / vscode** (configured, home-linux, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive language settings and extensions, with Linux-only Qt arms resolved by platform. Evidence: `modules/aspects/vscode.nix:27`, `modules/aspects/hosts/weebmachine/weebmachine.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/weebmachine/weebmachine.nix:13`, `modules/aspects/profiles/workstation.nix:24`.
- **zed / zed** (configured, home-linux, enabled): Host selects workstation; user host-aspects projects it into this HM context. The aspect supplies substantive editor/LSP settings, with Linux-only theme arm. Evidence: `modules/aspects/zed.nix:16`, `modules/aspects/hosts/weebmachine/weebmachine.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/weebmachine/weebmachine.nix:13`, `modules/aspects/profiles/workstation.nix:25`.
- **fish / fish** (default, nixos, enabled): The named user explicitly selects user-shell fish; Darwin also has a desired UserShell reconciliation in the selected Fish aspect. Evidence: `modules/aspects/user.nix:22`, `modules/aspects/hosts/weebmachine/weebmachine.nix:3`, `modules/setup.nix:43`, `modules/aspects/user.nix:6`, `modules/aspects/hosts/weebmachine/weebmachine.nix:13`.
- **hyprland / hyprland** (configured, home-linux, enabled): Linux desktop selects Hyprland; HM Linux guard resolves true and links tracked native Lua settings through host.flakeDir. Evidence: `modules/aspects/hyprland.nix:36`, `config/hypr/hyprland.lua:12`, `modules/aspects/hosts/weebmachine/weebmachine.nix:12`, `modules/aspects/profiles/linux-desktop.nix:13`, `modules/aspects/user.nix:6`.
- **hyprland / hyprland** (default, nixos, enabled): Selected SDDM explicitly chooses defaultSession=hyprland; greeter compositor KWin is not a Plasma desktop. Evidence: `modules/aspects/sddm.nix:9`, `modules/aspects/hosts/weebmachine/weebmachine.nix:12`, `modules/aspects/profiles/linux-desktop.nix:16`.
- **other_wm / omniwm** (configured, home-darwin, enabled): Astraeus selects OmniWM, enabling it and linking tracked TOML with substantive layout/gesture settings. Its niri layout subsection does not establish Niri adoption. Evidence: `modules/aspects/omniwm.nix:28`, `config/omniwm/settings.toml:56`, `modules/aspects/hosts/astraeus/astraeus.nix:15`, `modules/aspects/user.nix:6`.
- **other_editor / nano** (default, home-unknown, enabled): Selected Fish environment explicitly chooses EDITOR=nano -L in both contexts; this default is not Neovim. Evidence: `modules/aspects/fish.nix:72`, `modules/aspects/profiles/workstation.nix:18`, `modules/aspects/user.nix:6`.

## 3. Defined, disabled and ambiguous alternatives

VS Code/Zed/Fish have substantive settings. Neovim exists only as an unselected installation/desktop-entry aspect; the explicit editor default is Nano. OmniWM native niri layout settings are not a Niri compositor enable. SDDM KWin compositor is not full Plasma desktop adoption.

- **neovim** (defined, enabled, installed): A live Neovim package/desktop-entry aspect exists, but neither workstation nor Linux desktop/user includes select it. Evidence: `modules/aspects/neovim.nix:5`.

## 4. Machine roles and limits

Workstation is normalized to explicit desktop configured role for both hosts, without asserting physical chassis. Astraeus Darwin role follows its inventory platform. External mutable checkout symlinks require the repository to remain at the schema flakeDir path (`modules/schema.nix:10`).

Complete literal two-host inventory; the Linux desktop profile is reusable for homes but no standalone home target is declared.

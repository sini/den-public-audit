# redxtech__nixfiles: census notes

[Config page](../../configs/redxtech__nixfiles.md) · upstream [redxtech/nixfiles](https://github.com/redxtech/nixfiles) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `f0611199ba42`.

Three NixOS machines compose base plus workstation/server roles; all declare gabe (`modules/hosts/bastion/bastion.nix:9`, `modules/hosts/voyager/voyager.nix:4`, `modules/hosts/quasar/quasar.nix:9`). Generated import-tree wiring loads feature definitions (`modules/dendritic.nix:19`).

## 2. Software selected and traces

The shared chain is host→workstation/server→base→cli→editor/multiplexer/fish/prompt. Gabe explicitly includes host-aspects (`modules/users/gabe/gabe.nix:11`), which establishes HM reachability rather than assuming host inclusion alone configures its user. Niri is workstation-only, while Zed, Neovim, tmux and Zellij are all in the common CLI branch.

- **neovim / tu wrapper + HM Neovim** (configured, home-linux, enabled): Workstation/server both include base→cli→editor; gabe includes host-aspects, so its HM body enables raw Neovim and the external self-contained tu wrapper. No hasDisplay guard limits this editor body to workstations. Evidence: `modules/features/base/cli/editor.nix:18`, `modules/features/base/cli/editor.nix:16`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **neovim / tu wrapper** (default, home-linux, enabled): The selected editor body explicitly assigns VISUAL=tu; this is a visual-editor default, not a claim that plain nvim is the shell EDITOR. Evidence: `modules/features/base/cli/editor.nix:11`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **zed / zed** (configured, home-linux, enabled): The same unguarded HM editor body enables Zed and extensions on all three user contexts, including the server. Evidence: `modules/features/base/cli/editor.nix:25`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **tmux / tmux** (configured, home-linux, enabled): Base CLI includes multiplexer; its HM body enables and configures tmux. Evidence: `modules/features/base/cli/multiplexer.nix:5`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **zellij / zellij** (configured, home-linux, enabled): Multiplexer also enables Zellij and provides a native KDL layout; fish auto-integration is explicitly false, not a default-session assignment. Evidence: `modules/features/base/cli/multiplexer.nix:104`, `modules/features/base/cli/multiplexer.nix:126`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **fish / fish** (configured, home-linux, enabled): Base CLI selects the fish-shell aspect; actual functions, abbreviations and plugin configuration are supplied. Login default is counted separately. Evidence: `modules/features/base/cli/fish.nix:22`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **fish / fish** (default, nixos, enabled): Each declared gabe user resolves the named aspect and explicitly selects fish through user-shell. Evidence: `modules/users/gabe/gabe.nix:9`, `modules/hosts/bastion/bastion.nix:10`, `modules/hosts/voyager/voyager.nix:5`, `modules/hosts/quasar/quasar.nix:10`.
- **fish / fish** (default, nixos, enabled): Base also includes root, whose native OS account definition sets root.shell=fish. This system account is not counted as another human or den user entity. Evidence: `modules/users/root/root.nix:8`, `modules/features/base/base.nix:69`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`.
- **starship / starship** (configured, home-linux, enabled): CLI includes prompt, whose HM body enables and customizes Starship. Evidence: `modules/features/base/cli/prompt.nix:5`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.
- **niri / niri** (configured, nixos, enabled): Only the two workstation hosts include window-manager; its NixOS body enables niri. KDE Connect/keyring/portal packages do not establish KDE or GNOME desktop adoption. Evidence: `modules/features/workstation/wm/niri.nix:21`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/features/workstation/workstation.nix:12`.
- **niri / niri** (configured, home-linux, enabled): gabe host-aspects imports the workstation WM body, including monitor/input/bind configuration into HM. Evidence: `modules/features/workstation/wm/niri.nix:56`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/features/workstation/workstation.nix:12`, `modules/users/gabe/gabe.nix:11`.
- **niri / niri** (default, nixos, enabled): Selected greetd session command explicitly runs niri-session via tuigreet. Evidence: `modules/features/workstation/wm/niri.nix:30`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/features/workstation/workstation.nix:12`.
- **other_editor / micro** (installed, home-linux, enabled): The base CLI HM package list installs micro without native editor configuration. Evidence: `modules/features/base/cli/cli.nix:133`, `modules/hosts/bastion/bastion.nix:132`, `modules/hosts/voyager/voyager.nix:93`, `modules/hosts/quasar/quasar.nix:93`, `modules/features/workstation/workstation.nix:8`, `modules/features/server/server.nix:56`, `modules/features/base/base.nix:65`, `modules/features/base/cli/cli.nix:5`, `modules/users/gabe/gabe.nix:11`, `modules/defaults.nix:17`.

## 3. Defined, disabled and ambiguous alternatives

Zed on the server is an actual unguarded enable, not an inference from a package or pin (`modules/features/base/cli/editor.nix:25`). The tu frontend is explicitly enabled, though its external implementation is not audited. The fish helper named hclients invokes hyprctl but contains no Hyprland enable/configuration (`modules/features/base/cli/fish.nix:150`); it is not Hyprland adoption. GNOME keyring/AT-SPI and KDE Connect are components, not desktop sessions. Required families without contributions are recorded not_found.


## 4. Machine roles and limits

README and selected role profiles distinguish the desktop/workstation, laptop/workstation and home server. Root and the server data account have fish settings but are not inferred people. Static enabled definitions are counted even on headless targets when there is no guard; no runtime or build success is claimed.

Inventory complete for the three den host entities and their gabe contexts; no independent standalone home declaration found. Developer-shell/VM helper artifacts are not enumerated as extra physical hosts.

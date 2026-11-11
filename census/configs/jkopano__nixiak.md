# jkopano__nixiak: census notes

[Config page](../../configs/jkopano__nixiak.md) · upstream [jkopano/nixiak](https://github.com/jkopano/nixiak) · [Census summary](../summary.md)

Record: evidence JSON. Revision: `97bf0689bb4d`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Inventory has a Den laptop host and a standalone kuba home (modules/den.nix:11; modules/users/kuba.nix:9), plus two native outputs outside den.hosts: wsl and wsl-bootstrap (modules/wsl.nix:25, modules/wsl.nix:30). These native outputs matter: counting only dotted Den inventory would miss real configured targets.

## Software selected and host/user traces

kuba selects cli/tui/gui; cli explicitly includes Zsh/Nushell/Starship, and tui explicitly includes Helix/Neovim/tmux (modules/users/kuba.nix:12; modules/cli/default.nix:11; modules/tui/default.nix:11). The Neovim frontend is raw HM Neovim with an authored LazyVim tree and mutable link (modules/tui/nvim/default.nix:21, modules/tui/nvim/default.nix:82, modules/tui/nvim/init.lua:2). Host wayland enables both Niri and GNOME, even though its optional GNOME HM include is commented (modules/wayland/default.nix:10, modules/wayland/default.nix:19). WSL directly imports a narrower set of HM functions, so only its explicit Zsh/Starship/tmux imports are followed (hosts/wsl/system.nix:59).

## Defined, disabled and ambiguous alternatives

Fish and Zellij are live definitions but omitted from selected cli/tui includes; they are not adoption (modules/cli/fish.nix:7; modules/tui/zellij/default.nix:10). Plasma is explicitly disabled in a selected NixOS module (modules/wayland/default.nix:20). Standalone GNOME HM customization and i3 remain defined alternatives, while NixOS GNOME is enabled. Zed is installation-only (modules/gui/default.nix:88). Stylix targets named sway/kde/nvf/hyprland merely control theming and do not prove those programs are enabled (modules/stylix.nix:79). Zsh login defaults are explicit independently of its enablement; editor defaults come from base/WSL EDITOR assignments (modules/users/kuba.nix:32; modules/base.nix:55; hosts/wsl/system.nix:7).

## Machine roles and remaining limits

jkopano has an explicit selected isLaptop flag and ThinkPad hardware module (modules/vars.nix:15; modules/hosts/jkopano/default.nix:29). Native wsl and wsl-bootstrap explicitly enable WSL; bootstrap is a separate declared output, not a claimed second physical instance. The kuba home is not a fourth machine. Only declared configured contexts are listed; no humans inferred. WSL direct HM imports and mutable checkout links may require context/assets not proven by static reachability. No host-aspects battery is assumed to project every host HM contribution into the standalone home; selected Niri is recorded at NixOS scope.

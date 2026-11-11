# lorenzorapetti__nix: census notes

[Config page](../../configs/lorenzorapetti__nix.md) · upstream [lorenzorapetti/nix](https://github.com/lorenzorapetti/nix) · [Census summary](../summary.md)

Record: evidence JSON. Revision: e6b3e716d30a; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Four NixOS hosts share lorenzo and base concerns; user schema explicitly enables HM/user classes (modules/den.nix:100). Host variation remains in per-host selected features.

## Software selected and host/user traces

User lorenzo selects shell and opts into host-aspects (modules/users/lorenzo/lorenzo.nix:17, modules/users/lorenzo/lorenzo.nix:23). Thus Fish/Starship/Zellij are selected HM configuration, and Hyprland HM settings reach only the three selecting hosts. Actual Lua input body was inspected (modules/desktop/hyprland/config/input.lua:1).

## Defined, disabled and ambiguous alternatives

Base installs stock Neovim plus an external nvim-nix output; shell sets EDITOR=nvim (modules/base/utils.nix:36, modules/base/utils.nix:42, modules/shell/default.nix:6). These are installation/default claims, not unread external configuration. Zed is genuinely enabled only in selected desktop.coding (modules/desktop/applications/coding.nix:73). GNOME keyring/theming and generated Bash/Zsh completions do not establish those desktop/shell adoptions.

## Machine roles and remaining limits

Hades is explicitly a laptop (modules/hosts/hades/default.nix:40), while selected desktop presets identify Hades/Zagreus desktop roles. nixvm is clearly a named VM target. Nyx server role is inferred from DNS/proxy/cache workloads (modules/hosts/nyx/default.nix:15). Four user contexts are not four humans; external package inputs and private secrets are prerequisites, not proof of runtime success.

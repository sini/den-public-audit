# Spebby/NixOS: census notes

[Config page](../../../configs/Spebby/NixOS.md) · upstream [Spebby/NixOS](https://github.com/Spebby/NixOS) · [Census summary](../../summary.md)

Revision `e6ea71a1af5e`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Five root NixOS targets include a real test configuration and a VPS ISO; test is not silently discarded as a fixture ([modules/hosts/test/configuration.nix:2](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/test/configuration.nix#L2); [modules/hosts/vps/configuration.nix:17](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/vps/configuration.nix#L17)). Four declare thom/max/dummy, with HM classes assigned explicitly ([modules/defaults.nix:20](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/defaults.nix#L20)).

## Software selected and host/user traces

User profiles directly select dev/all or dev/tools, reaching shell and editor definitions ([modules/users/thom.nix:6](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/users/thom.nix#L6); [modules/users/max.nix:6](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/users/max.nix#L6); [modules/users/dummy.nix:9](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/users/dummy.nix#L9); [modules/apps/profiles.nix:49](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/apps/profiles.nix#L49)). Zsh/Starship option defaults resolve true. Desktop OS selection is direct: COSMIC on fio/rosso/test, GNOME on fio/tink. Extra GNOME home projection remains ambiguous without a local host-aspects route.

## Defined, disabled and ambiguous alternatives

External Nixvim and Vim are installed alongside configured Zed ([modules/apps/dev/editors/vim.nix:4](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/apps/dev/editors/vim.nix#L4); [modules/apps/dev/editors/zed.nix:20](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/apps/dev/editors/zed.nix#L20)); max additionally installs VSCode. Thom forces EDITOR=nvim ([modules/users/thom.nix:112](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/users/thom.nix#L112)). Global OS defaultUserShell is Zsh and /bin/sh is Bash ([modules/defaults.nix:213](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/defaults.nix#L213); [modules/defaults.nix:216](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/defaults.nix#L216)). Tink explicitly defaults GNOME; Fio defaults COSMIC ([modules/hosts/tink/configuration.nix:80](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/tink/configuration.nix#L80); [modules/hosts/fio/configuration.nix:92](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/fio/configuration.nix#L92)). KDE/Niri/Hyprland are live unselected alternatives. The host GNOME HM companion is a definition with no established consumer, distinct from verified OS GNOME. No mutual-provider workaround is presumed necessary.

## Machine roles and remaining unknowns

Fio/tink select desktop profiles; rosso selects laptop ([modules/hosts/fio/configuration.nix:25](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/fio/configuration.nix#L25); [modules/hosts/tink/configuration.nix:19](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/tink/configuration.nix#L19); [modules/hosts/rosso/configuration.nix:31](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/rosso/configuration.nix#L31)). VPS explicitly selects QEMU guest ([modules/hosts/vps/configuration.nix:23](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/hosts/vps/configuration.nix#L23)). Test physical role is unknown. Per-system image/package outputs are not exhaustively enumerated. Multiple enabled desktops do not mean multiple default sessions.

# eldios/dotfiles: census notes

[Config page](../../../configs/eldios/dotfiles.md) · upstream [eldios/dotfiles](https://github.com/eldios/dotfiles) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: ce9d9573891e; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three explicit x86 NixOS hosts with eldios at [modules/hosts.nix:4](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/hosts.nix#L4). Root is also explicitly configured by selected base module ([modules/aspects/_base/users.nix:15](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/_base/users.nix#L15)), retained as a user context for its Bash shell, not a human. HM classes are explicit at [modules/den.nix:18](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/den.nix#L18).

## Software selected and host/user traces

Shared eldios user selects CLI and host-aspects ([modules/users/eldios.nix:19](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/users/eldios.nix#L19)/21). That makes actual Zsh/Starship and each host-selected HM feature active. All hosts select substantive Neovim system and LazyVim home bodies at their host aspect:12. Only desktop/laptop select terminals and Hyprland (their aspect files:15/16), so Nu/Tmux/GUI editors do not spill onto mininixos.

## Defined, disabled and ambiguous alternatives

Neovim actual customRC and native Lua bootstrap were inspected ([modules/aspects/neovim.nix:27](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/neovim.nix#L27); [modules/aspects/_neovim/nvim/init.lua:17](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/_neovim/nvim/init.lua#L17)). Zed/VSCode are GUI package-list installations ([modules/aspects/desktop/_desktop-gui/packages_linux_gui.nix:131](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/desktop/_desktop-gui/packages_linux_gui.nix#L131)/215); language-server packages do not configure VSCode. ZELLIJ_AUTO_* environment strings are not Zellij adoption. Native Hyprland settings are unconditional linked files with generated entrypoint ([modules/aspects/desktop/_hyprland/omarchy-shell.nix:341](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/desktop/_hyprland/omarchy-shell.nix#L341)), so no HM enable flag is required. GDM has no explicit compositor default.

## Machine roles and remaining limits

Roles are explicit inventory comments: desktop workstation, laptop, headless storage/services ([modules/hosts.nix:5](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/hosts.nix#L5)/11/16). Mininixos starts an existing HomeAssistant libvirt domain ([modules/hosts/_mininixos/libvirt-vms.nix:23](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/hosts/_mininixos/libvirt-vms.nix#L23)), but does not declare that guest OS as another managed target. Private secrets influence passwords/services ([modules/users/eldios.nix:31](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/users/eldios.nix#L31)), not finite inventory. Static source reachability does not prove evaluation/boot success.

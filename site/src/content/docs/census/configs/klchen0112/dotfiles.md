---
title: "klchen0112/dotfiles: census notes"
---

[Config page](/configs/klchen0112/dotfiles/) · upstream [klchen0112/dotfiles](https://github.com/klchen0112/dotfiles) · [Census summary](/census/summary/)

Revision `d47908159f3e`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Eight managed roots include initIso plus seven other Linux/Darwin targets; one standalone Darwin home is separately declared. config.nix contains a legacy caoanda/Android data attrset but no selected root import was established, so it is not invented as inventory.

## Software selected and host/user traces

Ordinary HM Nu/Starship/utils are direct identity includes ([modules/users/klchen.nix:126](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/users/klchen.nix#L126)). Other apps deliberately use custom class names: roleClass intersects host.roles and user.roles and forwards matching classes into HM ([modules/den.nix:12](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/den.nix#L12)). This proves Emacs-twist on a2700/a99r50/i12400/wsl/Mac, and VSCode/Zsh/Paneru only on the Mac. niri-home is in both a99r50 lists; Niri OS include is explicit ([modules/hosts/a99r50/default.nix:214](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/hosts/a99r50/default.nix#L214)).

## Defined, disabled and ambiguous alternatives

Nu supplies real environment/completion settings, Starship actual TOML, tmux is bare enable with Stylix target wiring. Bare Bash enable resolves only Linux; commented user-shell nu does not make Nu account default. Emacs-twist explicitly sets defaultEditor, but its external config implementation is not claimed inspected. Plain Neovim is installation-only on init/initIso. Fish/Tide, GNOME and AeroSpace definitions remain alternatives; a custom-role identity include without matching host/user role is not adoption. Standalone Mac home lacks user-role intersection context, so custom classes are not promoted there.

## Machine roles and remaining unknowns

WSL is explicit. Sanjiao selected K3s control-plane supports inferred server. Darwin class does not establish a laptop merely from mbp naming; other physical forms remain unknown. Role strings like emacs-twist are software capability routing keys, not machine roles. Host/home roots complete; dynamic package outputs and legacy config data are not exhaustively inventoried.

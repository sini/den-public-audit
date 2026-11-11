---
title: "vitalyavolyn/dotfiles: census notes"
---

[Config page](/configs/vitalyavolyn/dotfiles/) · upstream [vitalyavolyn/dotfiles](https://github.com/vitalyavolyn/dotfiles) · [Census summary](/census/summary/)

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six root hosts span Darwin, laptops and service machines; only configuration.nix files form the imported inventory ([flake.nix:90](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/flake.nix#L90)).

## Software selected and host/user traces

Base profiles reach Zsh and base-home; vitalya explicitly selects host-aspects and Zsh user-shell ([den.nix:23](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/den.nix#L23); [den.nix:24](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/den.nix#L24)). Dev→Zed only applies to applin/celebi/tynamo, GNOME to celebi/tynamo.

## Defined, disabled and ambiguous alternatives

Actual .vimrc is Vim, not TODO-mentioned Neovim ([modules/base-home.nix:42](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/modules/base-home.nix#L42)). Porygon secondary account is native Fish default ([hosts/porygon/configuration.nix:102](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/hosts/porygon/configuration.nix#L102)). oh-my-zsh theme fishy is not Fish configuration ([modules/apps/zsh.nix:37](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/modules/apps/zsh.nix#L37)).

## Machine roles and remaining unknowns

Laptop profiles explicit for celebi/tynamo; QEMU guest explicit for sinistea. Porygon/shinx coherent server workloads visible but no physical form forced. No humans inferred.

 · `4fbe31ccb7bb`.

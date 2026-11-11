## Project and inspected revision

Six root hosts span Darwin, laptops and service machines; only configuration.nix files form the imported inventory (flake.nix:90).

## Software selected and host/user traces

Base profiles reach Zsh and base-home; vitalya explicitly selects host-aspects and Zsh user-shell (den.nix:23; den.nix:24). Dev→Zed only applies to applin/celebi/tynamo, GNOME to celebi/tynamo.

## Defined, disabled and ambiguous alternatives

Actual .vimrc is Vim, not TODO-mentioned Neovim (modules/base-home.nix:42). Porygon secondary account is native Fish default (hosts/porygon/configuration.nix:102). oh-my-zsh theme fishy is not Fish configuration (modules/apps/zsh.nix:37).

## Machine roles and remaining unknowns

Laptop profiles explicit for celebi/tynamo; QEMU guest explicit for sinistea. Porygon/shinx coherent server workloads visible but no physical form forced. No humans inferred.

 · `4fbe31ccb7bb`.

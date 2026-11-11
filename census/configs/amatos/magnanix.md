# amatos/magnanix: census notes

[Config page](../../../configs/amatos/magnanix.md) · upstream [amatos/magnanix](https://github.com/amatos/magnanix) · [Census summary](../../summary.md)

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Six declared Linux/Darwin targets share global base; finite genAttrs creates two nixostron VM variants ([modules/hosts/nixostron.nix:40](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/hosts/nixostron.nix#L40)).

## Software selected and host/user traces

Base selects LazyVim, four shells, Starship and Zellij ([modules/den/base.nix:19](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L19); [modules/den/base.nix:22](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L22)). Both identity aspects explicitly project host-aspects ([modules/users/alberth/alberth.nix:33](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/users/alberth/alberth.nix#L33); [modules/users/ephemeral/ephemeral.nix:17](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/users/ephemeral/ephemeral.nix#L17)). Fortuna selects Hyprland and Zed.

## Defined, disabled and ambiguous alternatives

Zsh is account default despite Fish/Bash/Nu availability ([modules/users/alberth/alberth.nix:106](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/users/alberth/alberth.nix#L106)). Neovim EDITOR and Zed VISUAL intentionally coexist ([modules/packages/neovim.nix:144](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/neovim.nix#L144); [modules/packages/zed/zed.nix:240](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L240)). Niri is an unselected alternative. Magnus also explicitly selects Zed ([`modules/hosts/magnus.nix:89`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/hosts/magnus.nix#L89)); the existing alberth host-aspects route reaches its settings symlink and Darwin `VISUAL=zed --wait` ([`modules/packages/zed/zed.nix:240`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L240), [`modules/packages/zed/zed.nix:243`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L243)).

## Machine roles and remaining unknowns

Fortuna desktop and muninn headless server are explicit; disposable root VM targets retained as genuine outputs, unlike nested test fixtures. No humans inferred from account names.

 · `7675475f0509`.

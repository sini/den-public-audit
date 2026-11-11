## Project and inspected revision

Six declared Linux/Darwin targets share global base; finite genAttrs creates two nixostron VM variants (modules/hosts/nixostron.nix:40).

## Software selected and host/user traces

Base selects LazyVim, four shells, Starship and Zellij (modules/den/base.nix:19; modules/den/base.nix:22). Both identity aspects explicitly project host-aspects (modules/users/alberth/alberth.nix:33; modules/users/ephemeral/ephemeral.nix:17). Fortuna selects Hyprland and Zed.

## Defined, disabled and ambiguous alternatives

Zsh is account default despite Fish/Bash/Nu availability (modules/users/alberth/alberth.nix:106). Neovim EDITOR and Zed VISUAL intentionally coexist (modules/packages/neovim.nix:144; modules/packages/zed/zed.nix:240). Niri is an unselected alternative. Magnus also explicitly selects Zed (`modules/hosts/magnus.nix:89`); the existing alberth host-aspects route reaches its settings symlink and Darwin `VISUAL=zed --wait` (`modules/packages/zed/zed.nix:240`, `modules/packages/zed/zed.nix:243`).

## Machine roles and remaining unknowns

Fortuna desktop and muninn headless server are explicit; disposable root VM targets retained as genuine outputs, unlike nested test fixtures. No humans inferred from account names.

 · `7675475f0509`.

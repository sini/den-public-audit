# cmetz/dotfiles: census notes

[Config page](../../../configs/cmetz/dotfiles.md) · upstream [cmetz/dotfiles](https://github.com/cmetz/dotfiles) · [Census summary](../../summary.md)

Rev 0c38be9224d7.

## Contents

- [1. Project and revision](#1-project-and-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined / not selected](#3-defined--not-selected)
- [4. Roles](#4-roles)

## 1. Project and revision
npins-based den config (`default.nix` shim, flake.nix delegates). Nine hosts in [`modules/hosts.nix:3-12`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/hosts.nix#L3-L12): four with user `loom` (evo-x2, loom-center, powerpi, loombox) and five Proxmox LXC service containers without users. Feature aspects are in the exported `gloom` namespace. The source contains a committed credential (reported privately; not located here).

## 2. Software selected and traces
- `den.aspects.loom.includes = [ gloom.everywhere ]` ([`gloom/everywhere.nix:8`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/gloom/everywhere.nix#L8)). Individual app files add themselves to `gloom.everywhere.includes` (e.g. [`apps/helix.nix:3`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/gloom/apps/helix.nix#L3), [`apps/tmux.nix:3`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/gloom/apps/tmux.nix#L3)), so helix (defaultEditor = true) and tmux reach every host with user loom. A surprising pattern: the aspect inclusion lives in the app file, not the user file.
- bash: `programs.bash` in the loom user aspect ([`users/loom.nix:249`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/users/loom.nix#L249)).
- vscodium and bspwm: `provides.to-users.includes = [ <gloom/desktop> ]` on evo-x2, loom-center and powerpi (`hosts/*.nix:7-9`); `gloom/desktop.nix` includes bspwm, polybar, gtk, vscode. bspwm is X11 via HM `xsession`.
- The user-specific `provides.<host>` blocks in `users/loom.nix` carry the per-host monitor maps and packages (mutual-provider on `den.schema.user`, [`modules/default.nix:3`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/default.nix#L3)).

## 3. Defined / not selected
neovim (`apps/neovim.nix`) is defined; both include lines in the user aspect are commented ([`loom.nix:64,162`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/users/loom.nix#L64)). No GNOME (only gnome-keyring), no starship, no shells other than bash, no zellij.

## 4. Roles
evo-x2, loom-center, powerpi: desktop inferred from gloom/desktop selection and absence of battery config (powerpi is a Raspberry Pi 4). loombox: server inferred (mailcow) and vm explicit (qemuGuest). Five LXC hosts: server inferred, no vm claim (LXC container, not VM). No laptops found.


Pinned Home Manager integration spot-check: Integration QC: exact pinned Home Manager b787c48e2ec57a9d098f5c2721882a3bc1e16f97 provides programs.vscodium via https://raw.githubusercontent.com/nix-community/home-manager/b787c48e2ec57a9d098f5c2721882a3bc1e16f97/modules/programs/vscodium.nix lines3-8/14-20; its vscode/mkVscodeModule.nix declares modulePath options at310-311 and gates configuration on cfg.enable at353. Actual extension/user-settings bodies were inspected, not inferred from file length. Substantive settings: [`modules/gloom/apps/vscode.nix:22`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/gloom/apps/vscode.nix#L22), [`modules/gloom/apps/vscode.nix:68`](https://github.com/cmetz/dotfiles/blob/0c38be9224d7276100c5c835a2eea1c712dec2c9/modules/gloom/apps/vscode.nix#L68).

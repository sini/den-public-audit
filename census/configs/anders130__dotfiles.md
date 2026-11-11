# anders130__dotfiles: census notes

[Config page](../../configs/anders130__dotfiles.md) · upstream [anders130/dotfiles](https://github.com/anders130/dotfiles) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 470c551356c8; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three explicit NixOS hosts imported along with modules at outputs.nix:3. Integrated HM is enabled and host-aspects projection selected at modules/default/homeManager.nix:22/25. A real configured Tmux wrapper package is also exported by modules/shell/tmux.nix:8 and consumed at88.

## Software selected and host/user traces

Global default includes Fish and external NVIX (modules/default/den.nix:15/19). Fish includes shell→Starship; native prompt and shell assets were read. All hosts select dev→project→Tmux (modules/dev/dev.nix:10; modules/dev/project.nix:17). Desktop and workstation select Caelestia→Hyprland; WSL does not, so it receives CLI/editor/multiplexer settings without a fabricated compositor adoption.

## Defined, disabled and ambiguous alternatives

Fish user.shell at modules/shell/fish/default.nix:5 reaches OS through [pinned Den user-to-host routing](https://raw.githubusercontent.com/denful/den/bf2504f9f2e8621fee091335132ab3ae698cf808/modules/aspects/batteries/os-user.nix): built-in global policy lines41-58 routes user-class content independently of user.classes. NVIX is externally configured package installation: local code selects base system package and full HM package (modules/shell/nvix.nix:20/36; modules/dev/dev.nix:14), not local editor settings. Hyprland tty1 default is explicit and guarded by true host ttyAutostart flags (modules/desktop/hyprland/autologin.nix:12/18). No requested families follow from incidental KDE Connect/GTK apps.

## Machine roles and remaining limits

Workstation is explicitly called work laptop at hosts/workstation/default.nix:12; jesse-desktop has explicit desktop name, and WSL enable is explicit at hosts/wsl/default.nix:63. WSL source warns it is no longer used (hosts/wsl/default.nix:16), retained as declared configuration rather than assumed running machine. Hypervisor apps do not add VM roles. Package target does not inflate host counts.

# eugencowie/dotfiles: census notes

[Config page](../../../configs/eugencowie/dotfiles.md) · upstream [eugencowie/dotfiles](https://github.com/eugencowie/dotfiles) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: 64dbfad5d9ca; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three hosts with different user aspects: inspiron-16/nixos, macbook-air-m1/eugen, nzxt-h1/echo. Explicit host declarations occur in their modules/hosts files at30/13/28. All declared users receive HM by [modules/den.nix:28](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/den.nix#L28). No standalone home output is declared.

## Software selected and host/user traces

Each concrete user selects Zsh and Starship; login shell is separately explicit via user-shell zsh at each modules/users file:10. Echo alone includes Zellij, LazyVim and Zed ([modules/users/echo.nix:23](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/users/echo.nix#L23)/35/36). Host NZXT directly includes GNOME at [modules/hosts/nzxt-h1.nix:22](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/hosts/nzxt-h1.nix#L22). These include chains prevent shared definitions from being counted on unrelated Darwin/WSL targets.

## Defined, disabled and ambiguous alternatives

Starship and Zellij are enable-only locally. Zsh adds suggestion/highlighting; Eugen also supplies Homebrew profile initialization ([modules/aspects/env/homebrew.nix:9](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/aspects/env/homebrew.nix#L9)). Zed has substantial font/theme/telemetry and agent configuration; LazyVim enables Copilot extra in an imported module ([modules/aspects/editor/lazyvim.nix:16](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/aspects/editor/lazyvim.nix#L16)), and explicitly makes Neovim default at20. remote.vscode only enables nix-ld ([modules/aspects/remote/vscode.nix:8](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/aspects/remote/vscode.nix#L8)), so it is not VSCode adoption. VSCode base_keymap string in Zed is likewise not installation.

## Machine roles and remaining limits

Darwin and laptop roles follow declared MacBook inventory; WSL is explicit ([modules/hosts/inspiron-16.nix:4](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/hosts/inspiron-16.nix#L4)). NZXT GUI enable alone does not prove desktop physical role, so its chassis remains unknown. User names are different configured accounts, not evidence of distinct humans. Native OS contributions use the project OS class route; no evaluation or boot success was tested.

Class verification: [modules/hosts/macbook-air-m1.nix:13](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/hosts/macbook-air-m1.nix#L13) declares aarch64-darwin, with pin at [flake.lock:163](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/flake.lock#L163). [Exact pinned Den host schema](https://raw.githubusercontent.com/vic/den/bf2504f9f2e8621fee091335132ab3ae698cf808/nix/lib/entities/host.nix) line 65 derives class=darwin from that suffix. No local class override exists. HM contribution platforms remain home-darwin, while the OS default-shell contribution remains darwin; target deployment is therefore darwin.

# Sharparam/nix-config: census notes

[Config page](../../../configs/Sharparam/nix-config.md) · upstream [Sharparam/nix-config](https://github.com/Sharparam/nix-config) · [Census summary](../../summary.md)

Revision `eb5fe2550c15`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Three managed roots include a deliberate disposable VM and one standalone generic-Linux home. All hosted HM classes are explicit ([modules/nix/home-manager.nix:8](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/nix/home-manager.nix#L8)). Sharparam identity composes base, dev and Helix; base fragments merge application settings even though base/module.nix only lists extra application includes.

## Software selected and host/user traces

Identity directly selects all core shell/editor contributions. Explicit mutual-provider ([modules/nix/den.nix:45](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/nix/den.nix#L45)) routes Sif Noctalia-Niri and the Mac disabled Paneru/VSCode choices. No arbitrary host HM projection is assumed. Neovim uses actual NVF settings and HM import ([modules/programs/neovim/module.nix:88](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/programs/neovim/module.nix#L88); [modules/programs/neovim/module.nix:97](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/programs/neovim/module.nix#L97)).

## Defined, disabled and ambiguous alternatives

Zsh is explicit account default; Bash has extra tmux/Zellij functions while Nu is enable-only. Tmux/Zellij both configured, but Zellij autoAttach=false ([modules/base/zellij.nix:3](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/zellij.nix#L3)). NVF supplies EDITOR/VISUAL defaults. Emacs links native Doom config on all identity homes, with Mac cask installation separately visible; the linked Doom directory is absent from the recorded tree and remains an external prerequisite; only local link/environment/alias integration is source-verified. VSCode dev selection is commented and Mac explicitly false ([modules/profiles/dev.nix:22](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/profiles/dev.nix#L22); [modules/hosts/NINETECH-617128/host.nix:69](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/hosts/NINETECH-617128/host.nix#L69)). Paneru is selected but disabled. Fish completion hooks do not themselves establish an enabled Fish shell; a zed alias does not install Zed.

## Machine roles and remaining unknowns

Sif selected ThinkPad X260 supports inferred laptop; Mac is Darwin with unknown physical form. Root nixos target is explicitly used by VM launcher ([modules/hosts/vm.nix:46](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/hosts/vm.nix#L46)), retained as real declared output. Melina home is generic Linux, not another managed host. Package outputs are outside the exhaustive host/home inventory; no distinct humans inferred.

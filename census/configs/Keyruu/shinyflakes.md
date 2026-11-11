# Keyruu/shinyflakes: census notes

[Config page](../../../configs/Keyruu/shinyflakes.md) · upstream [Keyruu/shinyflakes](https://github.com/Keyruu/shinyflakes) · [Census summary](../../summary.md)

Revision `021ee48343db`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Seven Den NixOS roots split five Lucas workstations and two root server contexts; a separate direct nixOnDroid output is also real ([modules/phone.nix:51](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/phone.nix#L51)). HM default applies to users except server root classes=[] ([modules/hosts/mentat/default.nix:7](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/hosts/mentat/default.nix#L7); [modules/hosts/prime/default.nix:6](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/hosts/prime/default.nix#L6)).

## Software selected and host/user traces

Lucas directly selects shell/editor/workstation bundles, with explicit host-aspects ([modules/users/lucas.nix:10](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/users/lucas.nix#L10)) and HM class. Full editor/multiplexer settings are therefore user-selected, not guessed from host inclusion. Workstation->wm selects Umbriel ([modules/aspects/workstation/wm/default.nix:11](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/aspects/workstation/wm/default.nix#L11)), whose commands explicitly force greetd sessions ([modules/aspects/workstation/wm/umbriel/default.nix:34](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/aspects/workstation/wm/umbriel/default.nix#L34)).

## Defined, disabled and ambiguous alternatives

Fish is account default and Starship manually initialized in Fish; Zsh is an additional configured shell. Neovim is locally wrapped native Lua, VSCodium and Zed have real settings, tmux/Zellij/Herdr each have substantive configurations. EDITOR=nvim and text/plain MIME=Zed are different default scopes. Required-family Niri/Hyprland/Sway are not inferred from swaybg, Noctalia or compositor-adjacent helpers. The hx package is a real configured Helix output, distinct from user adoption. Droid Fish is substantive; Droid Starship is enable-only.

## Machine roles and remaining unknowns

Host sources explicitly identify four laptops, muadib desktop, mentat home server and prime server. Phone output has no forced laptop/desktop role. Root servers receive Bash through headless and do not inherit Lucas applications. Submodule/private application trees are dependencies, and other package-directory outputs are not exhaustively inventoried; the finite host inventory is complete.

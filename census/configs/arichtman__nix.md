# arichtman__nix: census notes

[Config page](../../configs/arichtman__nix.md) · upstream [arichtman/nix](https://github.com/arichtman/nix) · [Census summary](../summary.md)

Revision `a33136e4580d`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Root import-tree loads modules (flake.nix:63), including six Linux lab nodes, one Darwin host and two standalone Linux homes. The nested den/ subtree is not the root module import and is not counted as a second fleet.

## Software selected and host/user traces

Personal arichtman identity directly selects myhome (modules/users/arichtman/aspect/aspect.nix:5), then terminal (modules/den/aspects/home/myhome/myhome.nix:9). Darwin explicitly has HM class (modules/hosts.nix:22). Native Helix TOML, Zsh initialization, Starship jj prompt and Zellij bindings are reachable in those homes. Schema user explicitly includes host-aspects and Zsh login-shell selection (modules/den/schema/user/default.nix:9; modules/den/schema/user/default.nix:12).

## Defined, disabled and ambiguous alternatives

Helix is defaultEditor and EDITOR=hx; Alacritty explicitly starts Zellij (modules/den/aspects/home/myhome/terminal.nix:154). Bash has bare enable/completion, not the richer Zsh body. Linux lab nodes install Helix through debugTools (modules/den/aspects/debugTools.nix:18), without inheriting personal HM settings. vscode-langservers-extracted is a language-server package, not VSCode adoption. Host-qualified work/bash-workaround providers exist, but their extra routing is not required for the independently selected shared terminal settings.

## Machine roles and remaining unknowns

The six Linux nodes select Kubernetes master/worker roles, supporting inferred server workloads (modules/hosts/fat-controller/aspect/fat-controller.nix:7; modules/hosts/tweedledee/aspect/tweedledee.nix:7). fat-controller explicitly selects virtualNode (modules/hosts/fat-controller/aspect/fat-controller.nix:5); physicalNode does not distinguish laptop/desktop for the others. Native account nixos is declared by defaultUser; there are no named Den users on those nodes. Homes do not inflate host counts. No evaluation performed; schema migration issues are not resolved by static inventory.

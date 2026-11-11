# clemak27__homelab: census notes

[Config page](../../configs/clemak27__homelab.md) · upstream [clemak27/homelab](https://github.com/clemak27/homelab) · [Census summary](../summary.md)

Record: evidence JSON. Revision: a8bb1c3f0fec; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

A finite three-node NixOS homelab: x86 server and two ARM agents declared at modules/hosts/hosts.nix:2-4. Root import-tree is flake.nix:4; hardware and k3s are namespaces (modules/defaults.nix:6/7), not extra hosts. Flux service deployments are cluster workload definitions, not additional declared OS hosts.

## Software selected and host/user traces

Each declared clemens user resolves the shared aspect, which selects shell (modules/users/clemens.nix:4). Shell includes nvim, pkgs and Zsh (modules/aspects/shell.nix:4-6), and Zsh includes Starship at modules/aspects/shell/zsh.nix:4. All relevant bodies use the OS nixos class, so this trace does not depend on integrated HM activation.

## Defined, disabled and ambiguous alternatives

Zsh history/aliases/options and Starship formatting are substantial actual settings, while raw Neovim is installed-only (modules/aspects/shell/nvim.nix:7). EDITOR/VISUAL nvim and login Zsh are explicit (modules/aspects/shell/nvim.nix:18/19; modules/users/clemens.nix:19). No additional WM/editor/multiplexer family definitions were found in live Nix source; service package metadata and container images are not interactive-software adoptions.

## Machine roles and remaining limits

Hl-server server role is explicit via name and selected k3s.server (modules/hosts/hl-server.nix:11). Agent server function is inferred from selected k3s.agent (each agent file:6), role=agent plus storage service (modules/aspects/k3s/agent.nix:16/33); README.md:5 identifies bare-metal server plus two smaller nodes. No VM role follows from containers. Contexts are not people; no evaluation or service runtime was tested.

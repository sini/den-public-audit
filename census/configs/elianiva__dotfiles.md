# elianiva__dotfiles: census notes

[Config page](../../configs/elianiva__dotfiles.md) · upstream [elianiva/dotfiles](https://github.com/elianiva/dotfiles) · [Census summary](../summary.md)

Record: evidence JSON. Revision: `44d6d212ab1d`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

One declared Darwin host (melon) integrates elianiva HM; three Linux HM outputs have no declared NixOS machine (modules/hosts.nix:20, modules/hosts.nix:25). Linux variants select elianiva plus generic-Linux plumbing through modules/user.nix:44. No Linux home is counted as an additional physical host.

## Software selected and host/user traces

Host user or explicit Linux home aspect → elianiva.includes → nvim/fish/helix/nushell/zellij native-link aspects (modules/user.nix:21, modules/user.nix:25). Actual native entry files were read, including nvim/init.lua:1, nushell/config.nu:27 and helix/config.toml:3. Global package placement is different: Darwin uses environment.systemPackages (modules/aspects/packages.nix:100), Linux uses guarded home.packages (modules/aspects/packages.nix:108). Zed is a selected macOS Homebrew cask, not a configured editor (modules/_lib/casks.nix:3).

## Defined, disabled and ambiguous alternatives

Neovim, Helix, Fish, Nushell, Bash startup files, Zellij and Starship have authored selected configuration. Tmux is installed by the common package list at modules/aspects/packages.nix:50, but legacy/tmux/.tmux.conf is not selected: do not count historical configuration. Fish native config disables its greeting and initializes Starship (fish/config.fish:2, fish/config.fish:4), while no live account-shell declaration makes it the login default. Commented exec-fish in misc/.bashrc:1 is not a default. Git core.editor=nvim is a real editor default (modules/aspects/git.nix:30).

## Machine roles and remaining limits

Only melon receives explicit darwin role; source reviewed here does not identify its physical chassis. Three standalone homes retain full output keys and empty user lists rather than claiming additional hosts or unique people (modules/hosts.nix:26, modules/hosts.nix:31, modules/hosts.nix:36). The native symlink configuration assumes a writable ~/.dotfiles checkout (modules/aspects/fish.nix:7), so reachability is not proof files exist after deployment. No upstream login shell or runtime activation is inferred.

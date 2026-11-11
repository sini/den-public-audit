---
title: "elianiva/dotfiles: census notes"
---

[Config page](/configs/elianiva/dotfiles/) · upstream [elianiva/dotfiles](https://github.com/elianiva/dotfiles) · [Census summary](/census/summary/)

Record: evidence JSON. Revision: `44d6d212ab1d`; static `git show` source review only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

One declared Darwin host (melon) integrates elianiva HM; three Linux HM outputs have no declared NixOS machine ([modules/hosts.nix:20](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L20), [modules/hosts.nix:25](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L25)). Linux variants select elianiva plus generic-Linux plumbing through [modules/user.nix:44](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L44). No Linux home is counted as an additional physical host.

## Software selected and host/user traces

Host user or explicit Linux home aspect → elianiva.includes → nvim/fish/helix/nushell/zellij native-link aspects ([modules/user.nix:21](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L21), [modules/user.nix:25](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L25)). Actual native entry files were read, including [nvim/init.lua:1](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nvim/init.lua#L1), [nushell/config.nu:27](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nushell/config.nu#L27) and [helix/config.toml:3](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/helix/config.toml#L3). Global package placement is different: Darwin uses environment.systemPackages ([modules/aspects/packages.nix:100](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L100)), Linux uses guarded home.packages ([modules/aspects/packages.nix:108](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L108)). Zed is a selected macOS Homebrew cask, not a configured editor ([modules/_lib/casks.nix:3](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/casks.nix#L3)).

## Defined, disabled and ambiguous alternatives

Neovim, Helix, Fish, Nushell, Bash startup files, Zellij and Starship have authored selected configuration. Tmux is installed by the common package list at [modules/aspects/packages.nix:50](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L50), but legacy/tmux/.tmux.conf is not selected: do not count historical configuration. Fish native config disables its greeting and initializes Starship ([fish/config.fish:2](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/fish/config.fish#L2), [fish/config.fish:4](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/fish/config.fish#L4)), while no live account-shell declaration makes it the login default. Commented exec-fish in [misc/.bashrc:1](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/misc/.bashrc#L1) is not a default. Git core.editor=nvim is a real editor default ([modules/aspects/git.nix:30](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/git.nix#L30)).

## Machine roles and remaining limits

Only melon receives explicit darwin role; source reviewed here does not identify its physical chassis. Three standalone homes retain full output keys and empty user lists rather than claiming additional hosts or unique people ([modules/hosts.nix:26](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L26), [modules/hosts.nix:31](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L31), [modules/hosts.nix:36](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L36)). The native symlink configuration assumes a writable ~/.dotfiles checkout ([modules/aspects/fish.nix:7](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/fish.nix#L7)), so reachability is not proof files exist after deployment. No upstream login shell or runtime activation is inferred.

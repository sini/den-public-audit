# derangga/dotfiles: census notes

[Config page](../../../configs/derangga/dotfiles.md) · upstream [derangga/dotfiles](https://github.com/derangga/dotfiles) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: c43c24f8b7f7; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Two helper-built Darwin hosts from finite map maclop→derangga and worklop→sociolla ([den.nix:96-98](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L96-L98)); helper sets concrete user and instantiate args at39/24. HM is explicit at [den.nix:46](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L46); schema user imports modules at93.

## Software selected and host/user traces

Both user contexts receive actual shared Fish, Tmux, Starship preset and Nixvim settings through modules/default.nix. Darwin schema imports configuration at [den.nix:51](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L51); that module enables Fish and deliberately changes each configured username login shell using dscl activation ([darwin/configuration.nix:26-31](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/darwin/configuration.nix#L26-L31)). Root flake exports actual Darwin configurations at [flake.nix:40](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/flake.nix#L40).

## Defined, disabled and ambiguous alternatives

Shared Nixvim defaultEditor is explicit ([modules/nixvim/default.nix:14](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/modules/nixvim/default.nix#L14)); native options were inspected. Zed is only a shared cask ([darwin/homebrew/default.nix:22](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/darwin/homebrew/default.nix#L22)). Derangga alone enables VSCode and imports AeroSpace ([den.nix:127](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L127)/150); sociolla instead imports OmniWM ([den.nix:176](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L176)), whose actual settings and activation copy mechanism were read. Starship powerline.nix is a live unselected alternative; default module selects no-version.nix at20. No Bash adoption follows from AeroSpace exec-on-workspace shell command.

## Machine roles and remaining limits

Both targets are explicitly Darwin. Laptop-like host names are not a sufficient physical-role basis, so chassis remains unknown. Each has exactly one explicit HM user, matching the host-specific extraSpecialArgs wiring noted in [den.nix:59](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L59). Account names are configured contexts, not distinct humans. Activation code was read only; no dscl, Nix evaluation or clone code was executed.

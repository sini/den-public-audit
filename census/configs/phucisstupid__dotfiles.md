# phucisstupid__dotfiles: census notes

[Config page](../../configs/phucisstupid__dotfiles.md) · upstream [phucisstupid/dotfiles](https://github.com/phucisstupid/dotfiles) · [Census summary](../summary.md)

## Contents

- [1. Project and inspected revision](#1-project-and-inspected-revision)
- [2. Software selected and traces](#2-software-selected-and-traces)
- [3. Defined, disabled and ambiguous alternatives](#3-defined-disabled-and-ambiguous-alternatives)
- [4. Machine roles and limits](#4-machine-roles-and-limits)

## 1. Project and inspected revision

Revision `0e80243bb07b`.

One Linux target and one ARM Darwin MacBook share a broad wow user selection (`modules/users/wow.nix:3`).

## 2. Software selected and traces

Wow directly selects Fish, Starship, LazyVim and tmux, so no host-provider inference is needed. AeroSpace is also unconditionally selected in wow, including on Linux.

- **fish / fish** (configured, home-linux, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:39`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:4`.
- **starship / starship** (configured, home-linux, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/shells/prompts.nix:5`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:5`.
- **neovim / lazyvim-nix** (configured, home-linux, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/editors/lazyvim.nix:16`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:8`.
- **tmux / tmux** (configured, home-linux, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/multiplexers.nix:5`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:10`.
- **neovim / lazyvim-nix** (default, home-linux, enabled): Selected LazyVim body explicitly sets Neovim defaultEditor=true. Evidence: `modules/aspects/editors/lazyvim.nix:12`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`.
- **fish / fish** (default, nixos, enabled): Selected shell.fish explicitly includes user-shell fish. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:36`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:4`.
- **fish / fish** (configured, home-darwin, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:39`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:4`.
- **starship / starship** (configured, home-darwin, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/shells/prompts.nix:5`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:5`.
- **neovim / lazyvim-nix** (configured, home-darwin, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/editors/lazyvim.nix:16`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:8`.
- **tmux / tmux** (configured, home-darwin, enabled): The named wow user directly includes this feature on the concrete target, supplying substantive settings/extras/plugins. Evidence: `modules/aspects/multiplexers.nix:5`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:10`.
- **neovim / lazyvim-nix** (default, home-darwin, enabled): Selected LazyVim body explicitly sets Neovim defaultEditor=true. Evidence: `modules/aspects/editors/lazyvim.nix:12`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`.
- **fish / fish** (default, darwin, enabled): Selected shell.fish explicitly includes user-shell fish. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:36`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:4`.
- **aerospace / aerospace** (configured, home-darwin, enabled): Wow explicitly selects AeroSpace with substantive bindings/settings. This Darwin target matches the application platform. Evidence: `modules/aspects/window-managers/aerospace.nix:8`, `modules/hosts/phucs-MacBook-Air/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:7`.

## 3. Defined, disabled and ambiguous alternatives

Darwin AeroSpace selection is verified; Linux state is unknown because the source lacks a platform guard and the app is platform-specific. Zsh/Nushell, NVF/Helix/Zed, Zellij, Niri and Hyprland are live unselected alternatives. LazyVim extras are substantive rather than an input-pin inference.

- **aerospace** (ambiguous, unknown, configured): Wow explicitly selects AeroSpace with substantive bindings/settings. The body has no Darwin guard, so the Linux selection is real but unsupported-target evaluation/state is unknown; do not infer Linux support. Evidence: `modules/aspects/window-managers/aerospace.nix:8`, `modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:41`, `modules/users/wow.nix:3`, `modules/users/wow.nix:7`.
- **zsh** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:20`.
- **nushell** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/shells/zsh-fish-nushell.nix:56`.
- **helix** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/editors/helix.nix:4`.
- **zed** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/editors/zed-editor.nix:4`.
- **neovim** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/editors/nvf.nix:4`.
- **zellij** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/multiplexers.nix:44`.
- **niri** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/window-managers/niri.nix:4`.
- **hyprland** (defined, enabled, configured): Live alternative feature exists but wow include list does not select it. Evidence: `modules/aspects/window-managers/hyprland.nix:11`.

## 4. Machine roles and limits

MacBook Air supports inferred laptop plus explicit Darwin role. Generic linux preset does not establish a desktop chassis. No additional user contexts arise from the nested host wow grouping.

Complete literal two-host inventory; Linux software state can be unsupported even when the declared inventory itself is clear.

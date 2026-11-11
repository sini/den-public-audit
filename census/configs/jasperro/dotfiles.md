# jasperro/dotfiles: census notes

[Config page](../../../configs/jasperro/dotfiles.md) · upstream [jasperro/dotfiles](https://github.com/jasperro/dotfiles) · [Census summary](../../summary.md)

Record: evidence JSON. Revision: 37a402659597; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Nine finite OS hosts with explicit per-user aspect/classes declarations in each `modules/hosts/<name>/<name>.nix`. The modules/homes files define named aspects only: no den.homes or standalone homeConfigurations are declared. Actual integrated HM user contexts total twelve; colin@superlaptop is an available but unselected aspect, excluded from target/user inventory.

## Software selected and host/user traces

Every actual account explicitly selects shared shell directly or through jasperro CLI. HM class is explicit in host user blocks, so Zsh/Nu actual settings activate; Fish is installation-only. Utilities independently enable raw OS Neovim/Zsh on all hosts ([modules/system/utilities.nix:35](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/system/utilities.nix#L35)/40). Only jasperro on doosje/ijsje/tinkpet/tosti selects Niri (their named user aspects:11); Nixvim also applies on tinkpet-wsl. Plasma is independently host-selected on koekie/superlaptop/waffie, with explicit defaultSession at [modules/ui/plasma.nix:27](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/ui/plasma.nix#L27).

## Defined, disabled and ambiguous alternatives

Niri has actual active niri-nix HM settings ([modules/jasperro/ui/niri/default.nix:62](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/jasperro/ui/niri/default.nix#L62)/65); Hyprland and Umbriel are unselected alternatives, not inferred adoption. VSCode user module forces empty settings ([modules/jasperro/editors/vscode/default.nix:11](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/jasperro/editors/vscode/default.nix#L11)), so its actual contribution is enable-only; extensive commented plugin list is not configuration. Wiktorine on koekie/superlaptop installs VSCode directly, distinct from jasperro enable wiring. Shared active Zsh explicitly prefers EDITOR=nvim even users without Nixvim. Native Nu history/completion and Oh My Posh JSON were read; their impurity links depend on source checkout availability ([modules/system/impurity.nix:21](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/system/impurity.nix#L21)).

## Machine roles and remaining limits

Explicit roles: doosje/koekie desktop, superlaptop/waffie laptop, taart home server; named ThinkPad/Yoga hardware supports inferred laptop on tinkpet/tosti and WSL ThinkPad. IJsje is an explicitly declared custom installer ISO host, not a VM inferred from test tooling ([modules/hosts/ijsje/ijsje.nix:9](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/hosts/ijsje/ijsje.nix#L9)). Taart commented LXC/hardware lines are not a VM declaration. Twelve account contexts are not twelve humans; static traces do not prove activation or runtime use.

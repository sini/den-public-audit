# recursivepaws__nix: census notes

[Config page](../../configs/recursivepaws__nix.md) · upstream [recursivepaws/nix](https://github.com/recursivepaws/nix) · [Census summary](../summary.md)

Record: evidence JSON. Revision: c4317eb95fad; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Four Linux hosts have five declared vera/work contexts (modules/hosts/hosts.nix:12); HM is the default user class and mutual-provider is explicit (modules/default/default.nix:11).

## Software selected and host/user traces

The important selection is host.desktop: true by schema default, false only on barkstation (modules/hosts/hosts.nix:8, modules/hosts/hosts.nix:25). Therefore guarded global Niri applies to three hosts/users, not the container host (modules/default/default.nix:21). Neovim/defaultEditor, Zsh and Starship are unconditional defaults and still reach barkstation.

## Defined, disabled and ambiguous alternatives

Only work selects hightouch, installing tmux on hericium/amanita (modules/users/work.nix:9; modules/aspects/hightouch/hightouch.nix:30). Neovim has local native init content and version validation (nvim/init.lua:1). GNOME control-center/keyring/portal support in the Niri aspect does not enable the GNOME desktop (modules/aspects/niri.nix:17, modules/aspects/niri.nix:30); Bash helper dependencies are not interactive-shell adoption.

## Machine roles and remaining limits

Desktop setting is explicit. Battery/touchpad and lid behavior support inferred laptop roles for amanita/ampulex (modules/hosts/amanita.nix:25; modules/hosts/ampulex.nix:35). Barkstation server role is inferred from headless Portainer stacks (modules/hosts/barkstation.nix:104). Configured Unix accounts are not human counts. Mutable/native assets and fetched prompt content remain deployment prerequisites, not a passing-evaluation claim.

Activation clarification: the exact locked Den user-shell battery was read as source text at https://raw.githubusercontent.com/vic/den/6e5e413880e3d1f05713c617b569c2f268c4bd9c/modules/aspects/batteries/user-shell.nix . Its homeManager block explicitly enables programs.${shell} (lines30-31); vera/work both select it (modules/users/vera.nix:6, modules/users/work.nix:6). Thus the HM initContent is active through the selected battery, independently of the OS Zsh enable.

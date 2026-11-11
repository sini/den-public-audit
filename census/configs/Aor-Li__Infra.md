# Aor-Li__Infra: census notes

[Config page](../../configs/Aor-Li__Infra.md) · upstream [Aor-Li/Infra](https://github.com/Aor-Li/Infra) · [Census summary](../summary.md)

Revision `87405e2c8b13`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Five hosts and one standalone Ubuntu cluster home are declared in modules/inventory.nix:14 through modules/inventory.nix:63. Global dev defaults supply a shared terminal/editor baseline; desktop/application trees are explicitly selected per host (modules/aspects/default/default.nix:15).

## Software selected and host/user traces

Global dev -> editor and shell provides LazyVim, Helix, tmux, three shell hooks and native Starship TOML. The aor identity explicitly includes host-aspects (modules/aspects/entity/users/aor/default.nix:8), proving desktop and VSCode home projection. Linux Enten/Kuregumo select desktop -> Niri; Macs explicitly select the Darwin AeroSpace service. Tobimune excludes desktop/app. The standalone philo context gets global dev and explicit Rex, not a desktop.

## Defined, disabled and ambiguous alternatives

EDITOR/VISUAL select nvim-lazy (modules/aspects/trait/dev/editor/editor.nix:13); Helix is a bare enable alternative (modules/aspects/trait/dev/editor/helix/helix.nix:3). Fish is the explicit account shell (modules/aspects/entity/users/aor/default.nix:12); Bash/Zsh are configured alternatives. VSCode supplies actual mutable native settings and extensions; Cursor and Herdr are installation-only. Rex Linux server versus guarded Darwin tunnel behavior is explicit (modules/aspects/trait/dev/shell/multiplexer/rex.nix:77). Niri’s direct enable row is distinguished from the separately defined DMS fragment integration.

## Machine roles and remaining unknowns

Inventory explicitly labels Enten desktop, both Macs laptops, Kuregumo laptop plus virt=vm, and Tobimune server (modules/inventory.nix:17; modules/inventory.nix:25; modules/inventory.nix:33; modules/inventory.nix:42; modules/inventory.nix:44; modules/inventory.nix:52). These are declared roles, not a physical-device census. dgx resource lists belong to hwstat settings, not host inventory. Several OS hardware files are placeholders; static reachability does not establish successful deployment.

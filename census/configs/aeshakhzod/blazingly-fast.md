# aeshakhzod/blazingly-fast: census notes

[Config page](../../../configs/aeshakhzod/blazingly-fast.md) · upstream [aeshakhzod/blazingly-fast](https://github.com/aeshakhzod/blazingly-fast) · [Census summary](../../summary.md)

Revision `2c2fb84d6b39`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Two x86_64 NixOS hosts share shakhzod ([modules/hosts/qoravoy/default.nix:2](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/hosts/qoravoy/default.nix#L2); [modules/hosts/waffle/default.nix:2](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/hosts/waffle/default.nix#L2)). Both select workhorse; qoravoy additionally selects homelab. The vm package wraps qoravoy.system.build.vm ([modules/vm.nix:9](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/vm.nix#L9)), not a separately declared host.

## Software selected and host/user traces

Workhorse directly reaches Plasma at OS scope ([modules/aspects/profiles/workhorse.nix:11](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/aspects/profiles/workhorse.nix#L11)). The identity directly chooses account Zsh ([modules/users/shakhzod.nix:12](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/users/shakhzod.nix#L12)). Rich editor/shell/home Plasma contributions are selected by the host profile, but the only local host-aspects declaration is on schema.host ([modules/defaults.nix:22](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/defaults.nix#L22)), not the user. Their user projection remains ambiguous instead of assuming external Den policy semantics. Exact locked implementation inspected: https://raw.githubusercontent.com/denful/den/65c9fd40e958109f5a352c1a93ae8254bf1ed29f/modules/aspects/batteries/host-aspects.nix:23–24 emits spawn for user.classes; https://raw.githubusercontent.com/denful/den/65c9fd40e958109f5a352c1a93ae8254bf1ed29f/nix/lib/aspects/fx/policy/schema.nix:160–204 dispatches parent-registered policies at matching user children; policy/dispatch.nix:54 checks required arguments. Thus schema.host attachment is sufficient here and all workhorse HM contributions are selected. Local flake.lock binds the pin.

## Defined, disabled and ambiguous alternatives

Workhorse selects Plasma, AstroNvim, ordinary Emacs, Zed, VS Code, Starship and Zsh. Exact dependency analysis resolves the host-aspects placement uncertainty. GNOME, Doom and Lem are explicitly unselected alternatives; comment/input presence does not count.

## Machine roles and remaining unknowns

Two real NixOS hosts with shakhzod account; host declarations and hardware modules support recorded roles. HM projection is established from the exact locked policy implementation, with no evaluation or runtime activation claim.

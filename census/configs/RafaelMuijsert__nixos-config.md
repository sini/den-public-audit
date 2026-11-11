# RafaelMuijsert__nixos-config: census notes

[Config page](../../configs/RafaelMuijsert__nixos-config.md) · upstream [RafaelMuijsert/nixos-config](https://github.com/RafaelMuijsert/nixos-config) · [Census summary](../summary.md)

Revision `c2466a023f20`.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

Five x86_64 NixOS roots declare rafael, including a custom live ISO (modules/hosts/iso/default.nix:11). aorus/elite/iso select the Niri desktop bundle; core hosts application services; infra selects network/SSH only.

## Software selected and host/user traces

Identity explicitly selects user-shell Fish and host-aspects (modules/system/users/rafael/rafael.nix:13; modules/system/users/rafael/rafael.nix:14). The exact Den pin at flake.lock:92 is 65c9fd40e958109f5a352c1a93ae8254bf1ed29f. Its immutable host-aspects source https://raw.githubusercontent.com/denful/den/65c9fd40e958109f5a352c1a93ae8254bf1ed29f/modules/aspects/batteries/host-aspects.nix uses user.classes or homeManager (upstream line24), so HM activation is verified without substituting current Den. Its user-shell source at the same revision enables Fish OS/account/HM contributions (upstream lines19-20,31-32).

## Defined, disabled and ambiguous alternatives

Global Fish aliases/Pure prompt and Helix settings are substantive (modules/defaults/fish.nix:7; modules/defaults/helix.nix:9). Helix defaultEditor is explicit; Niri has substantive HM settings but a bare OS enable. ISO selects Niri yet its tty1 login initializer calls sway (modules/hosts/iso/default.nix:40); no Sway package/enable was found, so this attempted default remains ambiguous. GNOME keyring is not GNOME desktop adoption.

## Machine roles and remaining unknowns

Elite is explicitly an Intel laptop (modules/hosts/elite/hardware.nix:8). Core has an inferred server workload from its application/nginx bundle (modules/hosts/core/default.nix:18; modules/hosts/core/default.nix:24). Other physical forms are unknown. ISO is a declared output, not proof of another physical machine. Static reads do not prove the ISO autostart succeeds.

# aullisia__nixos-config: census notes

[Config page](../../configs/aullisia__nixos-config.md) · upstream [aullisia/nixos-config](https://github.com/aullisia/nixos-config) · [Census summary](../summary.md)

Record: evidence JSON. Revision: 233eb5e4cfaf; static git-show source reading only.

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining limits](#machine-roles-and-remaining-limits)

## Project and inspected revision

Three explicit NixOS hosts each with aul (modules/hosts.nix:10). All user contexts have HM classes (modules/den.nix:41), and the same aul aspect selects desktop and editor software. Test remains a declared configuration despite absent generated hardware file.

## Software selected and host/user traces

Aul directly selects Niri, Zsh, Helix and VSCode (modules/users/aul/aul.nix:8/14/27/29). Actual application bodies enable them, supply substantial configuration and establish activation. Starship lives inside selected Zsh. The global battery explicitly chooses Zsh login shell at modules/den.nix:51; Noctalia greeter explicitly chooses Niri session at modules/greeters/noctalia-greeter.nix:19.

## Defined, disabled and ambiguous alternatives

Plasma is a live substantial OS/HM alternative (modules/desktop/plasma.nix:24/86) but only a commented include in aul at modules/users/aul/aul.nix:6. VSCode is configured beyond installation by supplied argv.json (modules/programs/vscode.nix:10). Swayidle/swaylock and KDE agents are not compositor/desktop adoption. Test Niri settings are selected, but its host map lookups explicitly throw because only b660/auronix keys exist (modules/desktop/niri/_parts/settings.nix:89/94); rows record static enable reachability, not successful evaluation.

## Machine roles and remaining limits

Auronix display is explicitly described as laptop in its host-keyed settings (modules/desktop/niri/_parts/settings.nix:70). Test is explicitly called VM in its host-specific comment (modules/hosts/test/default.nix:54). B660 chassis purpose stays unknown. Test additionally imports absent hosts/test/hardware-configuration.nix (modules/hosts/test/default.nix:32). Finite inventory is still complete; known blockers do not create unknown hidden hosts or distinct humans.

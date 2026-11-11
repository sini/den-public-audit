# jadestar1864__nix-config: census notes

[Config page](../../configs/jadestar1864__nix-config.md) · upstream [jadestar1864/nix-config](https://github.com/jadestar1864/nix-config) · [Census summary](../summary.md)

## Contents

- [Project and inspected revision](#project-and-inspected-revision)
- [Software selected and host/user traces](#software-selected-and-hostuser-traces)
- [Defined, disabled and ambiguous alternatives](#defined-disabled-and-ambiguous-alternatives)
- [Machine roles and remaining unknowns](#machine-roles-and-remaining-unknowns)

## Project and inspected revision

`1e0fcc909f4f`.

## Software selected and host/user traces

Schema explicitly assigns HM and host-aspects/mutual-provider to both admin and jaden accounts (modules/defaults.nix:16). Helix is global; pc/devops and Plasma are selected only by asrock/thinkpadx1. Host checks reference existing outputs, not extra machines (hosts/checks.nix:8).

## Defined, disabled and ambiguous alternatives

Substantive Helix allhosts; pc Starship and devops Tmux/Zsh only workstation/laptop. Plasma OS and HM settings are selected explicitly. VS Code language servers inside Helix are not VS Code editor adoption. README Bash code fences are not Bash setup.

## Machine roles and remaining unknowns

Laptop role explicit; workstation and persistent service roles inferred from selected workloads/profiles. Dokja VM status inferred only from virtual disk cue; roles overlap and do not establish physical chassis or unique humans. Static source only, no success/build/runtime claim.

Pinned helper verification: [user-shell](https://raw.githubusercontent.com/denful/den/2f1ae4aa27e756684d1fb5ebc1d25267727bd305/modules/aspects/batteries/user-shell.nix), lines19-20 and31-32; [host-aspects](https://raw.githubusercontent.com/denful/den/2f1ae4aa27e756684d1fb5ebc1d25267727bd305/modules/aspects/batteries/host-aspects.nix), line24. Lock identity is `flake.lock:45`. These exact immutable sources were read; current Den was not substituted. Substantive Starship source is `modules/assets/gruvbox-rainbow.toml:3`; Zsh plugins/highlighters are in `modules/cli/notify-after-long-running-command.nix:8` and `modules/cli/syntax-highlighting.nix:2`. Helix settings are at `modules/cli/helix.nix:6`.

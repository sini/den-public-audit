---
title: "Reviewed software and machine roles"
---

This page is the census summary. It records which software each config selects, and which machine roles its hosts
have. It is for readers who want adoption counts across the corpus, or the application breadth of one config. Each
table below has a one-line explanation, and the per-config detail is in [configs/](https://github.com/sini/den-public-audit/tree/main/census/configs/).

## Contents

- [What the census measured](#what-the-census-measured)
- [How selection was traced](#how-selection-was-traced)
- [What the tiers mean](#what-the-tiers-mean)
- [Coverage by source](#coverage-by-source)
- [Software selections across reviewed repositories](#software-selections-across-reviewed-repositories)
- [Window managers by deployment platform](#window-managers-by-deployment-platform)
- [Declared host roles](#declared-host-roles)
- [Per-repository application breadth](#per-repository-application-breadth)
- [Files](#files)

## What the census measured

- The census reviewed **108 / 108** included manifest entries.
- Evidence is retained for **120 / 120** manifest entries.
- The findings are static and come from the source. There was no Nix evaluation, activation or runtime observation.
- Counts refer to repositories and declared targets. They do not count unique people or physical machines.
- Aggregate counts are as computed over all 108 included configs. Among them are 3 whose source is no longer public.
  The per-repository rows of these 3 configs are omitted from these tables and the TSVs.

## How selection was traced

A reviewer reads the source and follows a declared target through den selection to a software contribution. The
[census contract](/method/census/) gives the full rules. These limits apply to every count on this page:

- A repo may select several alternatives.
- Ambiguous repository counts can overlap confirmed ones, when different targets resolve differently.
- A negative is limited to the reviewed source scope.
- Homes and packages never inflate machine counts.
- Host associations can include hosted or nested services (such as code-server), not only local desktop apps.
- Known configuration blockers remain in project notes. Verified reachability does not assert a usable build.

## What the tiers mean

Only selection-verified, enabled rows count as adoption. The census retains defined, ambiguous and disabled evidence
separately.

| tier | meaning | counts as adoption |
|---|---|---|
| selection-verified | selected by a traced den selection path | yes, when enabled |
| defined | declared but never selected | no |
| ambiguous | can't be decided statically | no |

Adoption has two modes, and the tables keep them in separate columns:

- **configured/default:** the target configures the software, or selects it as the default.
- **installation-only:** the target installs the package and nothing more.

## Coverage by source

This table gives, for each source, the repos reviewed, the repos in the manifest, and the repos with incomplete
target inventories.

| source | reviewed | manifest | incomplete target inventories (including packages) |
|---|---:|---:|---:|
| local | 10 | 10 | 0 |
| archived | 4 | 4 | 0 |
| public | 93 | 93 | 22 |
| anchor | 1 | 1 | 0 |

## Software selections across reviewed repositories

This table gives, for each software item, the repos in each adoption mode, the ambiguous repos, and the declared
hosts configured.

| item | configured/default repos | installation-only repos | ambiguous repos | declared hosts configured |
|---|---:|---:|---:|---:|
| aerospace | 13 | 0 | 1 | 14 |
| yabai | 0 | 0 | 0 | 0 |
| niri | 43 | 0 | 1 | 75 |
| hyprland | 19 | 0 | 1 | 36 |
| sway | 2 | 0 | 1 | 3 |
| gnome | 10 | 0 | 1 | 16 |
| kde | 20 | 0 | 2 | 43 |
| neovim | 63 | 5 | 2 | 175 |
| vscode | 27 | 9 | 0 | 68 |
| emacs | 10 | 1 | 0 | 26 |
| helix | 23 | 2 | 0 | 62 |
| zed | 23 | 7 | 0 | 58 |
| tmux | 32 | 9 | 0 | 103 |
| zellij | 20 | 5 | 0 | 77 |
| zsh | 58 | 0 | 1 | 198 |
| fish | 50 | 1 | 1 | 160 |
| nushell | 23 | 0 | 1 | 63 |
| bash | 42 | 3 | 0 | 131 |
| starship | 74 | 0 | 3 | 221 |

## Window managers by deployment platform

This table splits the window managers by deployment platform, and counts standalone homes apart from declared hosts.

| deployment | item | configured/default repos | installation-only repos | declared hosts configured | standalone homes configured |
|---|---|---:|---:|---:|---:|
| macos | aerospace | 13 | 0 | 14 | 2 |
| macos | yabai | 0 | 0 | 0 | 0 |
| nixos | niri | 43 | 0 | 75 | 0 |
| nixos | hyprland | 18 | 0 | 35 | 0 |
| nixos | sway | 2 | 0 | 3 | 0 |
| nixos | gnome | 10 | 0 | 16 | 0 |
| nixos | kde | 20 | 0 | 43 | 0 |

Counts by source/platform/mode and target kind are in [repo-counts.tsv](/census/repo-counts.tsv). Use these rows of it:

| question | rows to use in repo-counts.tsv |
|---|---|
| **AeroSpace on macOS** | deployment=macos (Darwin hosts plus standalone Darwin homes, deduplicated by repository) |
| the OS-host axis | deployment=darwin |
| **Niri versus Hyprland on NixOS** | deployment=nixos, platform=all |

The deployment=nixos rows include HM contributions on a declared NixOS host, and keep standalone homes separate. A
generic-Linux HM target is not NixOS.

## Declared host roles

This table gives, for each role, the explicit host targets, the inferred host targets, and the repositories with the
role.

| role | explicit host targets | inferred host targets | repositories with role |
|---|---:|---:|---:|
| server | 55 | 53 | 52 |
| laptop | 70 | 25 | 67 |
| desktop | 86 | 11 | 61 |
| wsl | 16 | 0 | 14 |
| vm | 27 | 2 | 20 |
| darwin | 44 | 0 | 35 |

Read the role counts with these limits:

- Roles overlap. A desktop may serve workloads, and WSL/VM/Darwin describe environment as well as purpose.
- Unknown roles remain in target notes.
- Incomplete target inventories are explicitly reported. They may concern additional package outputs rather than
  missing hosts. Coverage notes distinguish these cases.
- Counts describe observed declared targets, not unseen machines.

## Per-repository application breadth

This table gives, for each published config, the distinct required families selection-verified and enabled, out of
19, and splits them by configuration depth.

- Installation-only families are shown separately.
- Optional peers retain their names.
- This is application coverage, not a quality score or a count of people.
- Unresolved selections are not proof of absence.

| repository | source | selected / 19 | substantive | enable-only | installation-only | optional peers |
|---|---|---:|---:|---:|---:|---|
| [Adda/nixos-config](/census/configs/adda/nixos-config/) | local | 11 | 10 | 1 | 0 | other_editor:clion/pycharm, other_multiplexer:screen |
| [~theutz/flake](/census/configs/theutz/flake/) | local | 11 | 8 | 3 | 0 | — |
| [Aor-Li/Infra](/census/configs/aor-li/infra/) | public | 10 | 8 | 2 | 0 | other_editor:cursor, other_multiplexer:herdr, other_multiplexer:rex |
| [Keyruu/shinyflakes](/census/configs/keyruu/shinyflakes/) | public | 10 | 9 | 1 | 0 | other_multiplexer:herdr, other_wm:umbriel |
| [Sharparam/nix-config](/census/configs/sharparam/nix-config/) | public | 10 | 9 | 1 | 0 | other_editor:vim |
| [mrbandler/nix](/census/configs/mrbandler/nix/) | public | 10 | 9 | 1 | 0 | other_multiplexer:tuios |
| [scoiatael/dotfiles](/census/configs/scoiatael/dotfiles/) | public | 10 | 8 | 1 | 1 | — |
| [KGB33/.dotfiles](/census/configs/kgb33/dotfiles/) | public | 9 | 9 | 0 | 0 | other_editor:vim |
| [amatos/magnanix](/census/configs/amatos/magnanix/) | public | 9 | 9 | 0 | 0 | — |
| [eldios/dotfiles](/census/configs/eldios/dotfiles/) | public | 9 | 6 | 1 | 2 | — |
| [elianiva/dotfiles](/census/configs/elianiva/dotfiles/) | public | 9 | 7 | 0 | 2 | — |
| [greysilly7/nixos-config](/census/configs/greysilly7/nixos-config/) | public | 9 | 2 | 3 | 4 | — |
| [jkopano/nixiak](/census/configs/jkopano/nixiak/) | public | 9 | 5 | 3 | 1 | — |
| [klchen0112/dotfiles](/census/configs/klchen0112/dotfiles/) | public | 9 | 6 | 2 | 1 | other_wm:paneru |
| [lucasshiva/nixconfig](/census/configs/lucasshiva/nixconfig/) | archived | 9 | 6 | 2 | 1 | — |
| [mio-19/config-public](/census/configs/mio-19/config-public/) | public | 9 | 9 | 0 | 0 | — |
| [sini/nix-config](/census/configs/sini/nix-config/) | anchor | 9 | 8 | 1 | 0 | other_multiplexer:herdr |
| [adanoelle/fern](/census/configs/adanoelle/fern/) | public | 8 | 8 | 0 | 0 | other_editor:kakoune |
| [auscyber/dotfiles](/census/configs/auscyber/dotfiles/) | public | 8 | 4 | 2 | 2 | — |
| [danielgafni/nixos](/census/configs/danielgafni/nixos/) | public | 8 | 7 | 1 | 0 | other_editor:cursor |
| [loystonpais/lunar](/census/configs/loystonpais/lunar/) | public | 8 | 5 | 1 | 2 | other_shell:xonsh |
| [nazarewk-iac/nix-configs](/census/configs/nazarewk-iac/nix-configs/) | public | 8 | 6 | 0 | 2 | — |
| [quasigod.xyz/nixconfig](/census/configs/quasigodxyz/nixconfig/) | local | 8 | 7 | 0 | 1 | — |
| [sonntag/nix](/census/configs/sonntag/nix/) | public | 8 | 6 | 1 | 1 | — |
| [talarys/den](/census/configs/talarys/den/) | public | 8 | 3 | 3 | 2 | other_multiplexer:herdr |
| [Draculestein/nixos-config](/census/configs/draculestein/nixos-config/) | public | 7 | 6 | 1 | 0 | — |
| [Spebby/NixOS](/census/configs/spebby/nixos/) | public | 7 | 4 | 2 | 1 | other_editor:vim, other_wm:cosmic |
| [aeshakhzod/blazingly-fast](/census/configs/aeshakhzod/blazingly-fast/) | public | 7 | 7 | 0 | 0 | — |
| [andreshungbz/nixconfig](/census/configs/andreshungbz/nixconfig/) | public | 7 | 5 | 0 | 2 | — |
| [derangga/dotfiles](/census/configs/derangga/dotfiles/) | public | 7 | 5 | 1 | 1 | other_wm:omniwm |
| [henriquekirchheck/nixos-flake](/census/configs/henriquekirchheck/nixos-flake/) | public | 7 | 6 | 1 | 0 | — |
| [hmajid2301/nixicle](/census/configs/hmajid2301/nixicle/) | public | 7 | 6 | 0 | 1 | — |
| [icebluerabbit/nixos](/census/configs/icebluerabbit/nixos/) | public | 7 | 7 | 0 | 0 | other_prompt:oh-my-posh |
| [ivokun/kebun](/census/configs/ivokun/kebun/) | public | 7 | 7 | 0 | 0 | — |
| [jasperro/dotfiles](/census/configs/jasperro/dotfiles/) | public | 7 | 4 | 2 | 1 | other_prompt:oh-my-posh |
| [redxtech/nixfiles](/census/configs/redxtech/nixfiles/) | public | 7 | 7 | 0 | 0 | other_editor:micro |
| [Erastos/nixos-dotfiles](/census/configs/erastos/nixos-dotfiles/) | public | 6 | 3 | 2 | 1 | — |
| [Occhima/nix-conf](/census/configs/occhima/nix-conf/) | public | 6 | 6 | 0 | 0 | — |
| [acrobertson/infra](/census/configs/acrobertson/infra/) | public | 6 | 3 | 3 | 0 | — |
| [akeuben/dotfiles](/census/configs/akeuben/dotfiles/) | public | 6 | 5 | 0 | 1 | — |
| [augustocdias/nixos](/census/configs/augustocdias/nixos/) | public | 6 | 5 | 0 | 1 | other_wm:omniwm |
| [byte-sized-emi/nix-config](/census/configs/byte-sized-emi/nix-config/) | public | 6 | 3 | 1 | 2 | other_editor:kate |
| [drupol/infra](/census/configs/drupol/infra/) | local | 6 | 6 | 0 | 0 | other_editor:gram (Zed fork), antigravity, other_editor:micro |
| [eugencowie/dotfiles](/census/configs/eugencowie/dotfiles/) | public | 6 | 4 | 2 | 0 | — |
| [lorenzorapetti/nix](/census/configs/lorenzorapetti/nix/) | public | 6 | 4 | 2 | 0 | — |
| [motheki/nix](/census/configs/motheki/nix/) | public | 6 | 4 | 2 | 0 | other_multiplexer:tuios |
| [vodfsh/nixos-config](/census/configs/vodfsh/nixos-config/) | public | 6 | 2 | 2 | 2 | — |
| [DylanRJohnston/nixos](/census/configs/dylanrjohnston/nixos/) | public | 5 | 5 | 0 | 0 | other_editor:vim |
| [Gwenodai/nixos](/census/configs/gwenodai/nixos/) | public | 5 | 4 | 1 | 0 | — |
| [Kykero/Nazunix](/census/configs/kykero/nazunix/) | public | 5 | 5 | 0 | 0 | — |
| [Likivik/spectacle](/census/configs/likivik/spectacle/) | public | 5 | 4 | 0 | 1 | — |
| [Steven-S1020/Nixos-Configuration](/census/configs/steven-s1020/nixos-configuration/) | public | 5 | 5 | 0 | 0 | — |
| [anders130/dotfiles](/census/configs/anders130/dotfiles/) | public | 5 | 4 | 1 | 0 | — |
| [arichtman/nix](/census/configs/arichtman/nix/) | public | 5 | 4 | 1 | 0 | — |
| [aullisia/nixos-config](/census/configs/aullisia/nixos-config/) | public | 5 | 5 | 0 | 0 | — |
| [jadestar1864/nix-config](/census/configs/jadestar1864/nix-config/) | public | 5 | 5 | 0 | 0 | — |
| [tomwrw/megadots](/census/configs/tomwrw/megadots/) | local | 5 | 5 | 0 | 0 | — |
| [espdesign/nixos.den](/census/configs/espdesign/nixosden/) | local | 5 | 5 | 0 | 0 | — |
| [oxce5/chimera](/census/configs/oxce5/chimera/) | public | 5 | 5 | 0 | 0 | other_multiplexer:herdr |
| [phucisstupid/dotfiles](/census/configs/phucisstupid/dotfiles/) | public | 5 | 5 | 0 | 0 | — |
| [r17x/universe](/census/configs/r17x/universe/) | public | 5 | 5 | 0 | 0 | — |
| [recursivepaws/nix](/census/configs/recursivepaws/nix/) | public | 5 | 4 | 0 | 1 | — |
| [repparw/nix](/census/configs/repparw/nix/) | public | 5 | 4 | 1 | 0 | — |
| [rhedgeco/nix-config](/census/configs/rhedgeco/nix-config/) | public | 5 | 3 | 1 | 1 | — |
| [sm-f/nix](/census/configs/sm-f/nix/) | public | 5 | 5 | 0 | 0 | — |
| [soriPhoono/homelab](/census/configs/soriphoono/homelab/) | public | 5 | 4 | 1 | 0 | — |
| [EzT32/nixos](/census/configs/ezt32/nixos/) | public | 4 | 2 | 2 | 0 | — |
| [Heromercer/nixfiles](/census/configs/heromercer/nixfiles/) | public | 4 | 4 | 0 | 0 | — |
| [Le0-dot/config.nix](/census/configs/le0-dot/confignix/) | public | 4 | 4 | 0 | 0 | — |
| [Shawn8901/nixos-configuration](/census/configs/shawn8901/nixos-configuration/) | public | 4 | 4 | 0 | 0 | — |
| [Shochraos/nixfiles](/census/configs/shochraos/nixfiles/) | public | 4 | 3 | 1 | 0 | — |
| [SuNNjek/nixos-config](/census/configs/sunnjek/nixos-config/) | public | 4 | 2 | 2 | 0 | other_editor:vim |
| [SyahrulBhudiF/dotfiles](/census/configs/syahrulbhudif/dotfiles/) | public | 4 | 4 | 0 | 0 | — |
| [aveeryy/kadachi](/census/configs/aveeryy/kadachi/) | public | 4 | 3 | 1 | 0 | — |
| [moxie0420/dotfiles](/census/configs/moxie0420/dotfiles/) | public | 4 | 4 | 0 | 0 | — |
| [neonvoidx/nix](/census/configs/neonvoidx/nix/) | public | 4 | 2 | 2 | 0 | other_wm:umbriel |
| [nolvyn/nixos](/census/configs/nolvyn/nixos/) | public | 4 | 4 | 0 | 0 | other_editor:nano, other_wm:omniwm |
| [quasi-coherent/nix-config](/census/configs/quasi-coherent/nix-config/) | public | 4 | 4 | 0 | 0 | — |
| [thomasgoulet/nixnites](/census/configs/thomasgoulet/nixnites/) | public | 4 | 3 | 1 | 0 | other_multiplexer:herdr |
| [trash-panda-v91-beta/dots.factory](/census/configs/trash-panda-v91-beta/dotsfactory/) | public | 4 | 4 | 0 | 0 | other_multiplexer:herdr |
| [vitalyavolyn/dotfiles](/census/configs/vitalyavolyn/dotfiles/) | public | 4 | 4 | 0 | 0 | other_editor:vim |
| [voidlily/dotfiles](/census/configs/voidlily/dotfiles/) | public | 4 | 3 | 1 | 0 | other_editor:vim |
| [AnonymousRand/nix_config](/census/configs/anonymousrand/nix_config/) | public | 3 | 3 | 0 | 0 | — |
| [DJ-Laser/nixos](/census/configs/dj-laser/nixos/) | public | 3 | 2 | 1 | 0 | — |
| [RafaelMuijsert/nixos-config](/census/configs/rafaelmuijsert/nixos-config/) | public | 3 | 3 | 0 | 0 | — |
| [hoanhxlyn/andrewix](/census/configs/hoanhxlyn/andrewix/) | local | 3 | 3 | 0 | 0 | other_prompt:oh-my-posh |
| [cfrenette/nixos-config](/census/configs/cfrenette/nixos-config/) | public | 3 | 1 | 2 | 0 | other_wm:cosmic |
| [clemak27/homelab](/census/configs/clemak27/homelab/) | public | 3 | 2 | 1 | 0 | — |
| [jcranney/nix-configuration](/census/configs/jcranney/nix-configuration/) | public | 3 | 1 | 1 | 1 | — |
| [muhammadtalha-quant/denix](/census/configs/muhammadtalha-quant/denix/) | public | 3 | 3 | 0 | 0 | other_editor:vim |
| [zakuciael/nixpedition](/census/configs/zakuciael/nixpedition/) | local | 3 | 0 | 2 | 1 | — |
| [pdarulewski/dotfiles](/census/configs/pdarulewski/dotfiles/) | public | 3 | 3 | 0 | 0 | other_prompt:oh-my-posh |
| [sk4rd/mikos-den](/census/configs/sk4rd/mikos-den/) | public | 3 | 3 | 0 | 0 | — |
| [closure-labs/foundation](/census/configs/closure-labs/foundation/) | public | 2 | 1 | 0 | 1 | — |
| [jmartindf/dendritic](/census/configs/jmartindf/dendritic/) | public | 2 | 2 | 0 | 0 | other_editor:vim |
| [raphaelladinig/dotfiles](/census/configs/raphaelladinig/dotfiles/) | public | 2 | 2 | 0 | 0 | — |
| [FastTrackStudios/task](/census/configs/fasttrackstudios/task/) | public | 1 | 0 | 0 | 1 | — |
| [JoonasKajava/nvf-config](/census/configs/joonaskajava/nvf-config/) | public | 1 | 1 | 0 | 0 | — |
| [KGB33/homelab](/census/configs/kgb33/homelab/) | public | 1 | 1 | 0 | 0 | — |
| [closure-labs/maestro](/census/configs/closure-labs/maestro/) | public | 1 | 1 | 0 | 0 | — |
| [closure-labs/mish](/census/configs/closure-labs/mish/) | public | 0 | 0 | 0 | 0 | — |
| [fmway/infra](/census/configs/fmway/infra/) | public | 0 | 0 | 0 | 0 | — |
| [nifoc/dotfiles](/census/configs/nifoc/dotfiles/) | public | 0 | 0 | 0 | 0 | — |

## Files

- [Census index](/census/): one line for each file in this folder.
- [Census contract](/method/census/): what counts as adoption and how roles are decided.
- [Per-config census notes](https://github.com/sini/den-public-audit/tree/main/census/configs/): one page per published config.
- TSVs: [software](/census/software.tsv) · [targets](/census/targets.tsv) · [roles](/census/roles.tsv) · [coverage](/census/coverage.tsv) · [breadth](/census/breadth.tsv) · [repo-counts](/census/repo-counts.tsv). Per-repository rows cover published configs only; `repo-counts.tsv` holds the aggregate counts.

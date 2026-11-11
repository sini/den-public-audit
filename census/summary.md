# Reviewed software and machine roles

This page is the census summary. It records which software each config selects, and which machine roles its hosts
have. It is for readers who want adoption counts across the corpus, or the application breadth of one config. Each
table below has a one-line explanation, and the per-config detail is in [configs/](configs/).

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
[census contract](../method/CENSUS.md) gives the full rules. These limits apply to every count on this page:

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

Counts by source/platform/mode and target kind are in [repo-counts.tsv](repo-counts.tsv). Use these rows of it:

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
| [adda-nixos-config](configs/adda-nixos-config.md) | local | 11 | 10 | 1 | 0 | other_editor:clion/pycharm, other_multiplexer:screen |
| [theutz](configs/theutz.md) | local | 11 | 8 | 3 | 0 | — |
| [Aor-Li__Infra](configs/Aor-Li__Infra.md) | public | 10 | 8 | 2 | 0 | other_editor:cursor, other_multiplexer:herdr, other_multiplexer:rex |
| [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md) | public | 10 | 9 | 1 | 0 | other_multiplexer:herdr, other_wm:umbriel |
| [Sharparam__nix-config](configs/Sharparam__nix-config.md) | public | 10 | 9 | 1 | 0 | other_editor:vim |
| [mrbandler__nix](configs/mrbandler__nix.md) | public | 10 | 9 | 1 | 0 | other_multiplexer:tuios |
| [scoiatael__dotfiles](configs/scoiatael__dotfiles.md) | public | 10 | 8 | 1 | 1 | — |
| [KGB33__.dotfiles](configs/KGB33__.dotfiles.md) | public | 9 | 9 | 0 | 0 | other_editor:vim |
| [amatos__magnanix](configs/amatos__magnanix.md) | public | 9 | 9 | 0 | 0 | — |
| [eldios__dotfiles](configs/eldios__dotfiles.md) | public | 9 | 6 | 1 | 2 | — |
| [elianiva__dotfiles](configs/elianiva__dotfiles.md) | public | 9 | 7 | 0 | 2 | — |
| [greysilly7__nixos-config](configs/greysilly7__nixos-config.md) | public | 9 | 2 | 3 | 4 | — |
| [jkopano__nixiak](configs/jkopano__nixiak.md) | public | 9 | 5 | 3 | 1 | — |
| [klchen0112__dotfiles](configs/klchen0112__dotfiles.md) | public | 9 | 6 | 2 | 1 | other_wm:paneru |
| [lucasshiva](configs/lucasshiva.md) | archived | 9 | 6 | 2 | 1 | — |
| [mio-19__config-public](configs/mio-19__config-public.md) | public | 9 | 9 | 0 | 0 | — |
| [sini__nix-config](configs/sini__nix-config.md) | anchor | 9 | 8 | 1 | 0 | other_multiplexer:herdr |
| [adanoelle__fern](configs/adanoelle__fern.md) | public | 8 | 8 | 0 | 0 | other_editor:kakoune |
| [auscyber__dotfiles](configs/auscyber__dotfiles.md) | public | 8 | 4 | 2 | 2 | — |
| [danielgafni__nixos](configs/danielgafni__nixos.md) | public | 8 | 7 | 1 | 0 | other_editor:cursor |
| [loystonpais__lunar](configs/loystonpais__lunar.md) | public | 8 | 5 | 1 | 2 | other_shell:xonsh |
| [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md) | public | 8 | 6 | 0 | 2 | — |
| [quasigod-xyz-nixconfig](configs/quasigod-xyz-nixconfig.md) | local | 8 | 7 | 0 | 1 | — |
| [sonntag__nix](configs/sonntag__nix.md) | public | 8 | 6 | 1 | 1 | — |
| [talarys__den](configs/talarys__den.md) | public | 8 | 3 | 3 | 2 | other_multiplexer:herdr |
| [Draculestein__nixos-config](configs/Draculestein__nixos-config.md) | public | 7 | 6 | 1 | 0 | — |
| [Spebby__NixOS](configs/Spebby__NixOS.md) | public | 7 | 4 | 2 | 1 | other_editor:vim, other_wm:cosmic |
| [aeshakhzod__blazingly-fast](configs/aeshakhzod__blazingly-fast.md) | public | 7 | 7 | 0 | 0 | — |
| [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md) | public | 7 | 5 | 0 | 2 | — |
| [derangga__dotfiles](configs/derangga__dotfiles.md) | public | 7 | 5 | 1 | 1 | other_wm:omniwm |
| [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md) | public | 7 | 6 | 1 | 0 | — |
| [hmajid2301__nixicle](configs/hmajid2301__nixicle.md) | public | 7 | 6 | 0 | 1 | — |
| [icebluerabbit__nixos](configs/icebluerabbit__nixos.md) | public | 7 | 7 | 0 | 0 | other_prompt:oh-my-posh |
| [ivokun__kebun](configs/ivokun__kebun.md) | public | 7 | 7 | 0 | 0 | — |
| [jasperro__dotfiles](configs/jasperro__dotfiles.md) | public | 7 | 4 | 2 | 1 | other_prompt:oh-my-posh |
| [redxtech__nixfiles](configs/redxtech__nixfiles.md) | public | 7 | 7 | 0 | 0 | other_editor:micro |
| [Erastos__nixos-dotfiles](configs/Erastos__nixos-dotfiles.md) | public | 6 | 3 | 2 | 1 | — |
| [Occhima__nix-conf](configs/Occhima__nix-conf.md) | public | 6 | 6 | 0 | 0 | — |
| [acrobertson__infra](configs/acrobertson__infra.md) | public | 6 | 3 | 3 | 0 | — |
| [akeuben__dotfiles](configs/akeuben__dotfiles.md) | public | 6 | 5 | 0 | 1 | — |
| [augustocdias__nixos](configs/augustocdias__nixos.md) | public | 6 | 5 | 0 | 1 | other_wm:omniwm |
| [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md) | public | 6 | 3 | 1 | 2 | other_editor:kate |
| [drupol](configs/drupol.md) | local | 6 | 6 | 0 | 0 | other_editor:gram (Zed fork), antigravity, other_editor:micro |
| [eugencowie__dotfiles](configs/eugencowie__dotfiles.md) | public | 6 | 4 | 2 | 0 | — |
| [lorenzorapetti__nix](configs/lorenzorapetti__nix.md) | public | 6 | 4 | 2 | 0 | — |
| [motheki__nix](configs/motheki__nix.md) | public | 6 | 4 | 2 | 0 | other_multiplexer:tuios |
| [vodfsh__nixos-config](configs/vodfsh__nixos-config.md) | public | 6 | 2 | 2 | 2 | — |
| [DylanRJohnston__nixos](configs/DylanRJohnston__nixos.md) | public | 5 | 5 | 0 | 0 | other_editor:vim |
| [Gwenodai__nixos](configs/Gwenodai__nixos.md) | public | 5 | 4 | 1 | 0 | — |
| [Kykero__Nazunix](configs/Kykero__Nazunix.md) | public | 5 | 5 | 0 | 0 | — |
| [Likivik__spectacle](configs/Likivik__spectacle.md) | public | 5 | 4 | 0 | 1 | — |
| [Steven-S1020__Nixos-Configuration](configs/Steven-S1020__Nixos-Configuration.md) | public | 5 | 5 | 0 | 0 | — |
| [anders130__dotfiles](configs/anders130__dotfiles.md) | public | 5 | 4 | 1 | 0 | — |
| [arichtman__nix](configs/arichtman__nix.md) | public | 5 | 4 | 1 | 0 | — |
| [aullisia__nixos-config](configs/aullisia__nixos-config.md) | public | 5 | 5 | 0 | 0 | — |
| [jadestar1864__nix-config](configs/jadestar1864__nix-config.md) | public | 5 | 5 | 0 | 0 | — |
| [megadots](configs/megadots.md) | local | 5 | 5 | 0 | 0 | — |
| [nixos.den](configs/nixos.den.md) | local | 5 | 5 | 0 | 0 | — |
| [oceangreendev](configs/oceangreendev.md) | archived | 5 | 3 | 2 | 0 | — |
| [oxce5__chimera](configs/oxce5__chimera.md) | public | 5 | 5 | 0 | 0 | other_multiplexer:herdr |
| [phucisstupid__dotfiles](configs/phucisstupid__dotfiles.md) | public | 5 | 5 | 0 | 0 | — |
| [r17x__universe](configs/r17x__universe.md) | public | 5 | 5 | 0 | 0 | — |
| [recursivepaws__nix](configs/recursivepaws__nix.md) | public | 5 | 4 | 0 | 1 | — |
| [repparw__nix](configs/repparw__nix.md) | public | 5 | 4 | 1 | 0 | — |
| [rhedgeco__nix-config](configs/rhedgeco__nix-config.md) | public | 5 | 3 | 1 | 1 | — |
| [sm-f__nix](configs/sm-f__nix.md) | public | 5 | 5 | 0 | 0 | — |
| [soriPhoono__homelab](configs/soriPhoono__homelab.md) | public | 5 | 4 | 1 | 0 | — |
| [EzT32__nixos](configs/EzT32__nixos.md) | public | 4 | 2 | 2 | 0 | — |
| [Heromercer__nixfiles](configs/Heromercer__nixfiles.md) | public | 4 | 4 | 0 | 0 | — |
| [Le0-dot__config.nix](configs/Le0-dot__config.nix.md) | public | 4 | 4 | 0 | 0 | — |
| [Shawn8901__nixos-configuration](configs/Shawn8901__nixos-configuration.md) | public | 4 | 4 | 0 | 0 | — |
| [Shochraos__nixfiles](configs/Shochraos__nixfiles.md) | public | 4 | 3 | 1 | 0 | — |
| [SuNNjek__nixos-config](configs/SuNNjek__nixos-config.md) | public | 4 | 2 | 2 | 0 | other_editor:vim |
| [SyahrulBhudiF__dotfiles](configs/SyahrulBhudiF__dotfiles.md) | public | 4 | 4 | 0 | 0 | — |
| [aveeryy__kadachi](configs/aveeryy__kadachi.md) | public | 4 | 3 | 1 | 0 | — |
| [dotfiles](configs/dotfiles.md) | local | 4 | 4 | 0 | 0 | other_wm:bspwm |
| [moxie0420__dotfiles](configs/moxie0420__dotfiles.md) | public | 4 | 4 | 0 | 0 | — |
| [neonvoidx__nix](configs/neonvoidx__nix.md) | public | 4 | 2 | 2 | 0 | other_wm:umbriel |
| [nolvyn__nixos](configs/nolvyn__nixos.md) | public | 4 | 4 | 0 | 0 | other_editor:nano, other_wm:omniwm |
| [quasi-coherent__nix-config](configs/quasi-coherent__nix-config.md) | public | 4 | 4 | 0 | 0 | — |
| [thomasgoulet__nixnites](configs/thomasgoulet__nixnites.md) | public | 4 | 3 | 1 | 0 | other_multiplexer:herdr |
| [trash-panda-v91-beta__dots.factory](configs/trash-panda-v91-beta__dots.factory.md) | public | 4 | 4 | 0 | 0 | other_multiplexer:herdr |
| [vitalyavolyn__dotfiles](configs/vitalyavolyn__dotfiles.md) | public | 4 | 4 | 0 | 0 | other_editor:vim |
| [voidlily__dotfiles](configs/voidlily__dotfiles.md) | public | 4 | 3 | 1 | 0 | other_editor:vim |
| [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md) | public | 3 | 3 | 0 | 0 | — |
| [DJ-Laser__nixos](configs/DJ-Laser__nixos.md) | public | 3 | 2 | 1 | 0 | — |
| [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md) | public | 3 | 3 | 0 | 0 | — |
| [andrewix](configs/andrewix.md) | local | 3 | 3 | 0 | 0 | other_prompt:oh-my-posh |
| [cfrenette__nixos-config](configs/cfrenette__nixos-config.md) | public | 3 | 1 | 2 | 0 | other_wm:cosmic |
| [clemak27__homelab](configs/clemak27__homelab.md) | public | 3 | 2 | 1 | 0 | — |
| [jcranney__nix-configuration](configs/jcranney__nix-configuration.md) | public | 3 | 1 | 1 | 1 | — |
| [muhammadtalha-quant__denix](configs/muhammadtalha-quant__denix.md) | public | 3 | 3 | 0 | 0 | other_editor:vim |
| [nixpedition](configs/nixpedition.md) | local | 3 | 0 | 2 | 1 | — |
| [pdarulewski__dotfiles](configs/pdarulewski__dotfiles.md) | public | 3 | 3 | 0 | 0 | other_prompt:oh-my-posh |
| [sk4rd__mikos-den](configs/sk4rd__mikos-den.md) | public | 3 | 3 | 0 | 0 | — |
| [closure-labs__foundation](configs/closure-labs__foundation.md) | public | 2 | 1 | 0 | 1 | — |
| [jmartindf__dendritic](configs/jmartindf__dendritic.md) | public | 2 | 2 | 0 | 0 | other_editor:vim |
| [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md) | public | 2 | 2 | 0 | 0 | — |
| [FastTrackStudios__task](configs/FastTrackStudios__task.md) | public | 1 | 0 | 0 | 1 | — |
| [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md) | public | 1 | 1 | 0 | 0 | — |
| [KGB33__homelab](configs/KGB33__homelab.md) | public | 1 | 1 | 0 | 0 | — |
| [closure-labs__maestro](configs/closure-labs__maestro.md) | public | 1 | 1 | 0 | 0 | — |
| [closure-labs__mish](configs/closure-labs__mish.md) | public | 0 | 0 | 0 | 0 | — |
| [fmway__infra](configs/fmway__infra.md) | public | 0 | 0 | 0 | 0 | — |
| [nifoc__dotfiles](configs/nifoc__dotfiles.md) | public | 0 | 0 | 0 | 0 | — |

## Files

- [Census index](README.md): one line for each file in this folder.
- [Census contract](../method/CENSUS.md): what counts as adoption and how roles are decided.
- [Per-config census notes](configs/): one page per published config.
- TSVs: [software](software.tsv) · [targets](targets.tsv) · [roles](roles.tsv) · [coverage](coverage.tsv) · [breadth](breadth.tsv) · [repo-counts](repo-counts.tsv). Per-repository rows cover published configs only; `repo-counts.tsv` holds the aggregate counts.

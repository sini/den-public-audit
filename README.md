# den configuration audit

This is a community survey of public [den](https://github.com/denful/den) configurations. It shows how people lay
out aspects, route data between hosts, handle platforms and operations, and document their setups. It is for den
users who want to find good configs to learn from, and for config authors who want a reading of their own config.
For each config, you get a review page with a score, a scorecard and the cited evidence.

The survey covers 103 published configs and 3 aspect namespace libraries, by 101 authors.

The audit uses each term with one meaning. The [glossary](GLOSSARY.md) defines every term, both den's terms and the
audit's terms.

## Contents

- [How the audit was made](#how-the-audit-was-made)
- [What is in this repository](#what-is-in-this-repository)
- [How the configs were scored](#how-the-configs-were-scored)
- [Shortlists](#shortlists)
- [Top 15](#top-15)
- [Find your config](#find-your-config)
- [Starter picks](#starter-picks)
- [Showcase picks](#showcase-picks)
- [Libraries](#libraries)
- [Census highlights](#census-highlights)
- [How to read a scorecard](#how-to-read-a-scorecard)
- [Caveats](#caveats)
- [Thank you](#thank-you)
- [Corrections and opt-out](#corrections-and-opt-out)
- [License](#license)

## How the audit was made

Everything here comes from static reading. No configuration was evaluated, built or run. Each config was read at one
pinned revision. Every claim cites a `path:line` in that revision.

## What is in this repository

| location | what it contains |
|---|---|
| [GLOSSARY.md](GLOSSARY.md) | the terms that these docs use |
| [RANKING.md](RANKING.md) | the full ranking, the category scores and the shortlists |
| [configs/](configs/README.md) | one review page per config |
| [libraries/](libraries/README.md) | the three aspect namespace libraries, scored on their own track |
| [census/](census/summary.md) | which window managers, editors, shells and machine roles each config selects |
| [synthesis/](synthesis/public-themes.md) | recurring patterns and den friction points |
| [synthesis/library-candidates.md](synthesis/library-candidates.md) | library candidates for a community aspect library |
| [patterns/](patterns/sini-nix-config.md) | a deeper study of the reference config |
| [method/](method/README.md) | the rubric, the census contract and how the scoring was checked |

## How the configs were scored

Each config gets ten category scores from 1 to 10. Each score has written evidence. The categories are:

- structured data flow (D)
- layout and isolation (I)
- settings contracts (S)
- reuse (R)
- platform boundaries (P)
- explanation (L)
- verification (V)
- operations (O)
- application breadth (B)
- integrations (X)

The total is out of 100. Data flow counts twice. Verification and integrations count at half weight.

Two checks calibrated the scores:

1. Before the corpus was scored, two independent reviewers scored a pilot set blind. Where they disagreed by more
   than two points, the anchors were tightened.
2. After scoring, a blind second reading of a random sample checked the finished scores.

The details are in [method/](method/README.md).

## Shortlists

Three shortlists sit beside the score. Each shortlist is judged apart from the total, so a config can be on a
shortlist with a modest total.

| shortlist | what it means |
|---|---|
| showcase | the config demonstrates a mechanism that is worth showing to the den community |
| starter | the config is a good config to learn from |
| library units | the config has self-contained aspects that are nominated for a shared library |

## Top 15

This table gives the 15 highest totals. Ties at the cutoff are included.

| rank | config | author | total | shortlists |
|---:|---|---|---:|---|
| 1 | [sini/nix-config](configs/sini/nix-config.md) | sini | 71.5 | showcase, library units (9) |
| 2 | [Occhima/nix-conf](configs/Occhima/nix-conf.md) | Occhima | 69.0 | starter, library units (1) |
| 3 | [auscyber/dotfiles](configs/auscyber/dotfiles.md) | auscyber | 68.5 | showcase, library units (3) |
| 4 | [tomwrw/megadots](configs/tomwrw/megadots.md) | tomwrw | 67.5 | showcase, library units (4) |
| 5 | [Aor-Li/Infra](configs/Aor-Li/Infra.md) | Aor-Li | 66.5 | showcase, library units (2) |
| 6 | [closure-labs/foundation](configs/closure-labs/foundation.md) | closure-labs | 65.5 | library units (1) |
| 7 | [amatos/magnanix](configs/amatos/magnanix.md) | amatos | 64.0 | starter, library units (1) |
| 8 | [icebluerabbit/nixos](configs/icebluerabbit/nixos.md) | icebluerabbit | 63.0 | library units (1) |
| 8 | [repparw/nix](configs/repparw/nix.md) | repparw | 63.0 | showcase, library units (1) |
| 10 | [r17x/universe](configs/r17x/universe.md) | r17x | 62.5 | showcase, library units (1) |
| 11 | [closure-labs/mish](configs/closure-labs/mish.md) | closure-labs | 61.5 | library units (1) |
| 12 | [soriPhoono/homelab](configs/soriPhoono/homelab.md) | soriPhoono | 61.0 | showcase, library units (2) |
| 13 | [Kykero/Nazunix](configs/Kykero/Nazunix.md) | Kykero | 60.5 | showcase, starter, library units (1) |
| 14 | [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md) | nazarewk-iac | 60.0 | showcase, library units (2) |
| 15 | [Adda/nixos-config](configs/Adda/nixos-config.md) | Adda | 59.5 | library units (4) |
| 15 | [closure-labs/maestro](configs/closure-labs/maestro.md) | closure-labs | 59.5 | library units (2) |
| 15 | [mrbandler/nix](configs/mrbandler/nix.md) | mrbandler | 59.5 | showcase |

`sini/nix-config` is the audit maintainer's own configuration and the rubric's reference anchor. It was scored
under the same rubric as every other config.

## Find your config

The [config index](configs/README.md) lists every published config, grouped by owner, with its total and its
shortlists. Each config page links to the upstream repository at the reviewed revision. The
[full ranking](RANKING.md) lists the same configs in score order, with all ten category scores.

5 more configs were scored and are counted in the totals. They are not listed, because their source is
no longer public.

## Starter picks

These are good configs to learn from. Each one has these properties:

- a short path from the flake entry to a built host;
- few prerequisites;
- clear host and user variation;
- an honest statement of which platforms it supports.

- [Occhima/nix-conf](configs/Occhima/nix-conf.md) by Occhima, 69.0
- [amatos/magnanix](configs/amatos/magnanix.md) by amatos, 64.0
- [Kykero/Nazunix](configs/Kykero/Nazunix.md) by Kykero, 60.5
- [andreshungbz/nixconfig](configs/andreshungbz/nixconfig.md) by andreshungbz, 54.5
- [motheki/nix](configs/motheki/nix.md) by motheki, 52.5
- [lucasshiva/nixconfig](configs/lucasshiva/nixconfig.md) by lucasshiva, 48.0
- [espdesign/nixos.den](configs/espdesign/nixos.den.md) by espdesign, 38.5

## Showcase picks

These configs demonstrate a den mechanism especially well. Examples of such mechanisms are routed data between
hosts, typed settings and den data that drives deployment.

- [sini/nix-config](configs/sini/nix-config.md) by sini, 71.5
- [auscyber/dotfiles](configs/auscyber/dotfiles.md) by auscyber, 68.5
- [tomwrw/megadots](configs/tomwrw/megadots.md) by tomwrw, 67.5
- [Aor-Li/Infra](configs/Aor-Li/Infra.md) by Aor-Li, 66.5
- [repparw/nix](configs/repparw/nix.md) by repparw, 63.0
- [r17x/universe](configs/r17x/universe.md) by r17x, 62.5
- [soriPhoono/homelab](configs/soriPhoono/homelab.md) by soriPhoono, 61.0
- [Kykero/Nazunix](configs/Kykero/Nazunix.md) by Kykero, 60.5
- [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md) by nazarewk-iac, 60.0
- [mrbandler/nix](configs/mrbandler/nix.md) by mrbandler, 59.5
- [lorenzorapetti/nix](configs/lorenzorapetti/nix.md) by lorenzorapetti, 59.0
- [Le0-dot/config.nix](configs/Le0-dot/config.nix.md) by Le0-dot, 57.5
- [henriquekirchheck/nixos-flake](configs/henriquekirchheck/nixos-flake.md) by henriquekirchheck, 57.5
- [neonvoidx/nix](configs/neonvoidx/nix.md) by neonvoidx, 57.5
- [zakuciael/nixpedition](configs/zakuciael/nixpedition.md) by zakuciael, 57.5
- [sk4rd/mikos-den](configs/sk4rd/mikos-den.md) by sk4rd, 57.0
- [Gwenodai/nixos](configs/Gwenodai/nixos.md) by Gwenodai, 56.0
- [Keyruu/shinyflakes](configs/Keyruu/shinyflakes.md) by Keyruu, 55.5
- [greysilly7/nixos-config](configs/greysilly7/nixos-config.md) by greysilly7, 55.5
- [aveeryy/kadachi](configs/aveeryy/kadachi.md) by aveeryy, 54.0
- [byte-sized-emi/nix-config](configs/byte-sized-emi/nix-config.md) by byte-sized-emi, 54.0
- [ivokun/kebun](configs/ivokun/kebun.md) by ivokun, 54.0
- [raphaelladinig/dotfiles](configs/raphaelladinig/dotfiles.md) by raphaelladinig, 53.0
- [anders130/dotfiles](configs/anders130/dotfiles.md) by anders130, 52.5
- [AnonymousRand/nix_config](configs/AnonymousRand/nix_config.md) by AnonymousRand, 52.0
- [RafaelMuijsert/nixos-config](configs/RafaelMuijsert/nixos-config.md) by RafaelMuijsert, 50.5
- [JoonasKajava/nvf-config](configs/JoonasKajava/nvf-config.md) by JoonasKajava, partial 44.5 / 90

## Libraries

These repos are namespace libraries. They are scored on their own track and are not in the ranking.

- [adanoelle/garden-shell](libraries/adanoelle/garden-shell.md) by adanoelle: the `garden` namespace, an aspect and package library, a pure namespace provider
- [crocuda/crocuda.nixos](libraries/crocuda/crocuda.nixos.md) by crocuda: the `crocuda` namespace, hardened NixOS server modules, with dotfiles kept in their native formats and Nix as glue
- [crocuda/normal.nixos](libraries/crocuda/normal.nixos.md) by crocuda: the `normal` namespace, the same author's opinionated desktop modules

## Census highlights

Counts are repositories out of the 108 included configs (configured or default, selection verified in source).

- Window managers on NixOS hosts: niri 43, KDE 20, Hyprland 18, GNOME 10, Sway 2. On macOS, AeroSpace 13.
- Editors: Neovim 63, VS Code 27, Helix 23, Zed 23, Emacs 10.
- Shells: zsh 58, fish 50, bash 42, Nushell 23. The Starship prompt appears in 74; tmux in 32 and Zellij in 20.
- Machine roles: laptops 67, desktops 61, servers 52, macOS machines 35, VMs 20, WSL 14.

The full tables, including per-repository breadth, are in [census/summary.md](census/summary.md).

## How to read a scorecard

Each config page starts with a header. The header gives the upstream repository, the reviewed revision, the author,
the score and the shortlists. The review follows, in the same order on every page:

1. **Shape**: how the repo is organized, and how den is wired in.
2. **Common patterns**: recognizable den idioms, each with a citation.
3. **Novel patterns**: ideas that are not on the common list.
4. **Library candidates**: aspects that are worth generalizing. Each one has a grade: A (drop-in), B (light
   parametrizing) or C (idea only).
5. **den friction**: places where den made something harder than necessary.
6. **Docs and complexity**, then **6a. Defects and scoring notes**: every deduction, each with one primary category.
7. **Template notes**: whether and how to use the config as a starting point.
8. **Scorecard**: one evidence card per category. Each card gives the scope, the pros, the cons, the score and the
   reviewer's confidence.

This table gives the categories and their weights in the total:

| category | what it measures | weight |
|---|---|---:|
| D | structured data flow: quirks, pipes and policies that carry facts between aspects and hosts | ×2 |
| I | layout and isolation of concerns | ×1 |
| S | settings and variation contracts, and how many author-specific constants appear in shared code | ×1 |
| R | reuse contract: how easily another user can adopt an aspect | ×1 |
| P | platform boundaries: NixOS, Darwin, standalone homes and others | ×1 |
| L | explanation and navigation | ×1 |
| V | verification intent: checks, tests and the CI that runs them | ×½ |
| O | operations driven by den data: deployment, secrets, bootstrap, builders | ×1 |
| B | application breadth, from the census and complete reference units | ×1 |
| X | integrations: den drives other module systems, such as terranix, Kubernetes or microvm | ×½ |

A score is a reading of one revision against fixed anchors. It is not a grade of the author. The confidence is high,
medium or low. It tells how sure the reviewer was, for example when part of a config depends on private inputs.

### Walkthrough: one real scorecard

This walkthrough uses one config from the Top 15 and the starter picks:

[Occhima/nix-conf](configs/Occhima/nix-conf.md) by Occhima has rank 2 of 101 ranked configs. Its shortlists are: starter, library units (1).

| category | score | weight | points |
|---|---:|---:|---:|
| D: structured data flow | 6 | ×2 | 12 |
| I: layout and isolation of concerns | 9 | ×1 | 9 |
| S: settings and variation contracts | 6 | ×1 | 6 |
| R: reuse contract | 7 | ×1 | 7 |
| P: platform boundaries | 8 | ×1 | 8 |
| L: explanation and navigation | 8 | ×1 | 8 |
| V: verification intent | 9 | ×½ | 4.5 |
| O: operations driven by den data | 5 | ×1 | 5 |
| B: application breadth | 7 | ×1 | 7 |
| X: integrations with other module systems | 5 | ×½ | 2.5 |
| **total** | | | **69.0** |

To read its page, do these steps:

1. Read the header. Find the total and the ten category scores in one line.
2. Read section 6a. Each defect starts with the category that it costs, and a severity such as "moderate".
3. Read section 8. Find the evidence card for each category. Each pro and each con cites a `path:line`.
4. Find the score and the confidence at the end of each card.
5. Multiply each score by its weight, and add the points. The sum is the total, as the table above shows.

## Caveats

- Scores reflect one revision at one point in time. Your config has probably changed since.
- This is static reading only. Nothing was evaluated, built or activated. A defect here is a reading of the source,
  not an observed failure. A config that reads well is not proven to build.
- Nothing here is a security review, or an endorsement of the security of a config. Where a review found committed
  credential material, the location is not published here. The audit reports it privately instead.
- Category scores compare against written anchors, not against other configs. Small differences in totals are not
  meaningful.

## Thank you

Thank you to every author below for publishing your configuration. Reading real, working configs is the best way to
learn den, and this survey only exists because you chose to share yours.

- [acrobertson](https://github.com/acrobertson): [acrobertson/infra](configs/acrobertson/infra.md)
- [adanoelle](https://github.com/adanoelle): [adanoelle/fern](configs/adanoelle/fern.md), [adanoelle/garden-shell](libraries/adanoelle/garden-shell.md)
- [Adda](https://codeberg.org/Adda): [Adda/nixos-config](configs/Adda/nixos-config.md)
- [aeshakhzod](https://github.com/aeshakhzod): [aeshakhzod/blazingly-fast](configs/aeshakhzod/blazingly-fast.md)
- [akeuben](https://github.com/akeuben): [akeuben/dotfiles](configs/akeuben/dotfiles.md)
- [amatos](https://github.com/amatos): [amatos/magnanix](configs/amatos/magnanix.md)
- [anders130](https://github.com/anders130): [anders130/dotfiles](configs/anders130/dotfiles.md)
- [andreshungbz](https://github.com/andreshungbz): [andreshungbz/nixconfig](configs/andreshungbz/nixconfig.md)
- [AnonymousRand](https://github.com/AnonymousRand): [AnonymousRand/nix_config](configs/AnonymousRand/nix_config.md)
- [Aor-Li](https://github.com/Aor-Li): [Aor-Li/Infra](configs/Aor-Li/Infra.md)
- [arichtman](https://github.com/arichtman): [arichtman/nix](configs/arichtman/nix.md)
- [augustocdias](https://github.com/augustocdias): [augustocdias/nixos](configs/augustocdias/nixos.md)
- [aullisia](https://github.com/aullisia): [aullisia/nixos-config](configs/aullisia/nixos-config.md)
- [auscyber](https://github.com/auscyber): [auscyber/dotfiles](configs/auscyber/dotfiles.md)
- [aveeryy](https://github.com/aveeryy): [aveeryy/kadachi](configs/aveeryy/kadachi.md)
- [byte-sized-emi](https://github.com/byte-sized-emi): [byte-sized-emi/nix-config](configs/byte-sized-emi/nix-config.md)
- [cfrenette](https://github.com/cfrenette): [cfrenette/nixos-config](configs/cfrenette/nixos-config.md)
- [clemak27](https://github.com/clemak27): [clemak27/homelab](configs/clemak27/homelab.md)
- [closure-labs](https://github.com/closure-labs): [closure-labs/foundation](configs/closure-labs/foundation.md), [closure-labs/maestro](configs/closure-labs/maestro.md), [closure-labs/mish](configs/closure-labs/mish.md)
- [crocuda](https://github.com/crocuda): [crocuda/crocuda.nixos](libraries/crocuda/crocuda.nixos.md), [crocuda/normal.nixos](libraries/crocuda/normal.nixos.md)
- [danielgafni](https://github.com/danielgafni): [danielgafni/nixos](configs/danielgafni/nixos.md)
- [derangga](https://github.com/derangga): [derangga/dotfiles](configs/derangga/dotfiles.md)
- [DJ-Laser](https://github.com/DJ-Laser): [DJ-Laser/nixos](configs/DJ-Laser/nixos.md)
- [Draculestein](https://github.com/Draculestein): [Draculestein/nixos-config](configs/Draculestein/nixos-config.md)
- [drupol](https://github.com/drupol): [drupol/infra](configs/drupol/infra.md)
- [DylanRJohnston](https://github.com/DylanRJohnston): [DylanRJohnston/nixos](configs/DylanRJohnston/nixos.md)
- [eldios](https://github.com/eldios): [eldios/dotfiles](configs/eldios/dotfiles.md)
- [elianiva](https://github.com/elianiva): [elianiva/dotfiles](configs/elianiva/dotfiles.md)
- [Erastos](https://github.com/Erastos): [Erastos/nixos-dotfiles](configs/Erastos/nixos-dotfiles.md)
- [espdesign](https://github.com/espdesign): [espdesign/nixos.den](configs/espdesign/nixos.den.md)
- [eugencowie](https://github.com/eugencowie): [eugencowie/dotfiles](configs/eugencowie/dotfiles.md)
- [EzT32](https://github.com/EzT32): [EzT32/nixos](configs/EzT32/nixos.md)
- [FastTrackStudios](https://github.com/FastTrackStudios): [FastTrackStudios/task](configs/FastTrackStudios/task.md)
- [fmway](https://github.com/fmway): [fmway/infra](configs/fmway/infra.md)
- [greysilly7](https://github.com/greysilly7): [greysilly7/nixos-config](configs/greysilly7/nixos-config.md)
- [Gwenodai](https://github.com/Gwenodai): [Gwenodai/nixos](configs/Gwenodai/nixos.md)
- [henriquekirchheck](https://github.com/henriquekirchheck): [henriquekirchheck/nixos-flake](configs/henriquekirchheck/nixos-flake.md)
- [Heromercer](https://github.com/Heromercer): [Heromercer/nixfiles](configs/Heromercer/nixfiles.md)
- [hmajid2301](https://github.com/hmajid2301): [hmajid2301/nixicle](configs/hmajid2301/nixicle.md)
- [hoanhxlyn](https://github.com/hoanhxlyn): [hoanhxlyn/andrewix](configs/hoanhxlyn/andrewix.md)
- [icebluerabbit](https://github.com/icebluerabbit): [icebluerabbit/nixos](configs/icebluerabbit/nixos.md)
- [ivokun](https://github.com/ivokun): [ivokun/kebun](configs/ivokun/kebun.md)
- [jadestar1864](https://github.com/jadestar1864): [jadestar1864/nix-config](configs/jadestar1864/nix-config.md)
- [jasperro](https://github.com/jasperro): [jasperro/dotfiles](configs/jasperro/dotfiles.md)
- [jcranney](https://github.com/jcranney): [jcranney/nix-configuration](configs/jcranney/nix-configuration.md)
- [jkopano](https://github.com/jkopano): [jkopano/nixiak](configs/jkopano/nixiak.md)
- [jmartindf](https://github.com/jmartindf): [jmartindf/dendritic](configs/jmartindf/dendritic.md)
- [JoonasKajava](https://github.com/JoonasKajava): [JoonasKajava/nvf-config](configs/JoonasKajava/nvf-config.md)
- [Keyruu](https://github.com/Keyruu): [Keyruu/shinyflakes](configs/Keyruu/shinyflakes.md)
- [KGB33](https://github.com/KGB33): [KGB33/.dotfiles](configs/KGB33/.dotfiles.md), [KGB33/homelab](configs/KGB33/homelab.md)
- [klchen0112](https://github.com/klchen0112): [klchen0112/dotfiles](configs/klchen0112/dotfiles.md)
- [Kykero](https://github.com/Kykero): [Kykero/Nazunix](configs/Kykero/Nazunix.md)
- [Le0-dot](https://github.com/Le0-dot): [Le0-dot/config.nix](configs/Le0-dot/config.nix.md)
- [Likivik](https://github.com/Likivik): [Likivik/spectacle](configs/Likivik/spectacle.md)
- [lorenzorapetti](https://github.com/lorenzorapetti): [lorenzorapetti/nix](configs/lorenzorapetti/nix.md)
- [loystonpais](https://github.com/loystonpais): [loystonpais/lunar](configs/loystonpais/lunar.md)
- [lucasshiva](https://github.com/lucasshiva): [lucasshiva/nixconfig](configs/lucasshiva/nixconfig.md)
- [mio-19](https://github.com/mio-19): [mio-19/config-public](configs/mio-19/config-public.md)
- [motheki](https://github.com/motheki): [motheki/nix](configs/motheki/nix.md)
- [moxie0420](https://github.com/moxie0420): [moxie0420/dotfiles](configs/moxie0420/dotfiles.md)
- [mrbandler](https://github.com/mrbandler): [mrbandler/nix](configs/mrbandler/nix.md)
- [muhammadtalha-quant](https://github.com/muhammadtalha-quant): [muhammadtalha-quant/denix](configs/muhammadtalha-quant/denix.md)
- [nazarewk-iac](https://github.com/nazarewk-iac): [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md)
- [neonvoidx](https://github.com/neonvoidx): [neonvoidx/nix](configs/neonvoidx/nix.md)
- [nifoc](https://github.com/nifoc): [nifoc/dotfiles](configs/nifoc/dotfiles.md)
- [nolvyn](https://github.com/nolvyn): [nolvyn/nixos](configs/nolvyn/nixos.md)
- [Occhima](https://github.com/Occhima): [Occhima/nix-conf](configs/Occhima/nix-conf.md)
- [oxce5](https://github.com/oxce5): [oxce5/chimera](configs/oxce5/chimera.md)
- [pdarulewski](https://github.com/pdarulewski): [pdarulewski/dotfiles](configs/pdarulewski/dotfiles.md)
- [phucisstupid](https://github.com/phucisstupid): [phucisstupid/dotfiles](configs/phucisstupid/dotfiles.md)
- [quasi-coherent](https://github.com/quasi-coherent): [quasi-coherent/nix-config](configs/quasi-coherent/nix-config.md)
- [quasigod.xyz](https://tangled.org/quasigod.xyz): [quasigod.xyz/nixconfig](configs/quasigod.xyz/nixconfig.md)
- [r17x](https://github.com/r17x): [r17x/universe](configs/r17x/universe.md)
- [RafaelMuijsert](https://github.com/RafaelMuijsert): [RafaelMuijsert/nixos-config](configs/RafaelMuijsert/nixos-config.md)
- [raphaelladinig](https://github.com/raphaelladinig): [raphaelladinig/dotfiles](configs/raphaelladinig/dotfiles.md)
- [recursivepaws](https://github.com/recursivepaws): [recursivepaws/nix](configs/recursivepaws/nix.md)
- [redxtech](https://github.com/redxtech): [redxtech/nixfiles](configs/redxtech/nixfiles.md)
- [repparw](https://github.com/repparw): [repparw/nix](configs/repparw/nix.md)
- [rhedgeco](https://github.com/rhedgeco): [rhedgeco/nix-config](configs/rhedgeco/nix-config.md)
- [scoiatael](https://github.com/scoiatael): [scoiatael/dotfiles](configs/scoiatael/dotfiles.md)
- [Sharparam](https://github.com/Sharparam): [Sharparam/nix-config](configs/Sharparam/nix-config.md)
- [Shawn8901](https://github.com/Shawn8901): [Shawn8901/nixos-configuration](configs/Shawn8901/nixos-configuration.md)
- [Shochraos](https://github.com/Shochraos): [Shochraos/nixfiles](configs/Shochraos/nixfiles.md)
- [sini](https://github.com/sini): [sini/nix-config](configs/sini/nix-config.md)
- [sk4rd](https://github.com/sk4rd): [sk4rd/mikos-den](configs/sk4rd/mikos-den.md)
- [sm-f](https://github.com/sm-f): [sm-f/nix](configs/sm-f/nix.md)
- [sonntag](https://github.com/sonntag): [sonntag/nix](configs/sonntag/nix.md)
- [soriPhoono](https://github.com/soriPhoono): [soriPhoono/homelab](configs/soriPhoono/homelab.md)
- [Spebby](https://github.com/Spebby): [Spebby/NixOS](configs/Spebby/NixOS.md)
- [Steven-S1020](https://github.com/Steven-S1020): [Steven-S1020/Nixos-Configuration](configs/Steven-S1020/Nixos-Configuration.md)
- [SuNNjek](https://github.com/SuNNjek): [SuNNjek/nixos-config](configs/SuNNjek/nixos-config.md)
- [SyahrulBhudiF](https://github.com/SyahrulBhudiF): [SyahrulBhudiF/dotfiles](configs/SyahrulBhudiF/dotfiles.md)
- [talarys](https://github.com/talarys): [talarys/den](configs/talarys/den.md)
- [theutz](https://sr.ht/~theutz): [~theutz/flake](configs/theutz/flake.md)
- [thomasgoulet](https://github.com/thomasgoulet): [thomasgoulet/nixnites](configs/thomasgoulet/nixnites.md)
- [tomwrw](https://github.com/tomwrw): [tomwrw/megadots](configs/tomwrw/megadots.md)
- [trash-panda-v91-beta](https://github.com/trash-panda-v91-beta): [trash-panda-v91-beta/dots.factory](configs/trash-panda-v91-beta/dots.factory.md)
- [vitalyavolyn](https://github.com/vitalyavolyn): [vitalyavolyn/dotfiles](configs/vitalyavolyn/dotfiles.md)
- [vodfsh](https://github.com/vodfsh): [vodfsh/nixos-config](configs/vodfsh/nixos-config.md)
- [voidlily](https://github.com/voidlily): [voidlily/dotfiles](configs/voidlily/dotfiles.md)
- [zakuciael](https://github.com/zakuciael): [zakuciael/nixpedition](configs/zakuciael/nixpedition.md)

## Corrections and opt-out

If a finding is wrong, or you want your config removed from this survey, please open an issue. Name the config and
the finding, and link the source if you can. Removal requests are honoured without question. See
[CONTRIBUTING.md](CONTRIBUTING.md).

## License

The audit text is licensed under [CC BY 4.0](LICENSE). The configurations themselves belong to their authors and keep
their own licenses. Short quotations from them are used here for review.

# den configuration audit

This is a community survey of public [den](https://github.com/denful/den) configurations. It shows how people lay
out aspects, route data between hosts, handle platforms and operations, and document their setups. It is for den
users who want to find good configs to learn from, and for config authors who want a reading of their own config.
For each config, you get a review page with a score, a scorecard and the cited evidence.

The survey covers 105 published configs and 3 aspect namespace libraries, by 103 authors.

The audit uses each term with one meaning. The [glossary](GLOSSARY.md) defines every term, both den's terms and the
audit's terms.

## Contents

- [How the audit was made](#how-the-audit-was-made)
- [What is in this repository](#what-is-in-this-repository)
- [How the configs were scored](#how-the-configs-were-scored)
- [Shortlists](#shortlists)
- [Find your config](#find-your-config)
- [Top 15](#top-15)
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

## Find your config

This table lists every published config, in alphabetical order by author. Totals are out of 100. A "partial" total
means that a category did not apply, so that config is not ranked against the others. The
[list of config pages](configs/README.md) gives the same configs, grouped by letter.

| author | config | upstream | total | shortlists |
|---|---|---|---:|---|
| acrobertson | [acrobertson__infra](configs/acrobertson__infra.md) | [acrobertson/infra](https://github.com/acrobertson/infra) | 46.0 | library units (1) |
| adanoelle | [adanoelle__fern](configs/adanoelle__fern.md) | [adanoelle/fern](https://github.com/adanoelle/fern) | 58.5 | library units (1) |
| Adda | [adda-nixos-config](configs/adda-nixos-config.md) | [Adda/nixos-config](https://codeberg.org/Adda/nixos-config) | 59.5 | library units (4) |
| aeshakhzod | [aeshakhzod__blazingly-fast](configs/aeshakhzod__blazingly-fast.md) | [aeshakhzod/blazingly-fast](https://github.com/aeshakhzod/blazingly-fast) | 41.0 | library units (1) |
| akeuben | [akeuben__dotfiles](configs/akeuben__dotfiles.md) | [akeuben/dotfiles](https://github.com/akeuben/dotfiles) | 48.0 | library units (1) |
| amatos | [amatos__magnanix](configs/amatos__magnanix.md) | [amatos/magnanix](https://github.com/amatos/magnanix) | 64.0 | starter, library units (1) |
| anders130 | [anders130__dotfiles](configs/anders130__dotfiles.md) | [anders130/dotfiles](https://github.com/anders130/dotfiles) | 52.5 | showcase, library units (1) |
| andreshungbz | [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md) | [andreshungbz/nixconfig](https://github.com/andreshungbz/nixconfig) | 54.5 | starter, library units (1) |
| AnonymousRand | [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md) | [AnonymousRand/nix_config](https://github.com/AnonymousRand/nix_config) | 52.0 | showcase, library units (1) |
| Aor-Li | [Aor-Li__Infra](configs/Aor-Li__Infra.md) | [Aor-Li/Infra](https://github.com/Aor-Li/Infra) | 66.5 | showcase, library units (2) |
| arichtman | [arichtman__nix](configs/arichtman__nix.md) | [arichtman/nix](https://github.com/arichtman/nix) | 41.5 | library units (2) |
| augustocdias | [augustocdias__nixos](configs/augustocdias__nixos.md) | [augustocdias/nixos](https://github.com/augustocdias/nixos) | 41.0 | library units (1) |
| aullisia | [aullisia__nixos-config](configs/aullisia__nixos-config.md) | [aullisia/nixos-config](https://github.com/aullisia/nixos-config) | 46.0 | library units (3) |
| auscyber | [auscyber__dotfiles](configs/auscyber__dotfiles.md) | [auscyber/dotfiles](https://github.com/auscyber/dotfiles) | 68.5 | showcase, library units (3) |
| aveeryy | [aveeryy__kadachi](configs/aveeryy__kadachi.md) | [aveeryy/kadachi](https://github.com/aveeryy/kadachi) | 54.0 | showcase, library units (3) |
| byte-sized-emi | [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md) | [byte-sized-emi/nix-config](https://github.com/byte-sized-emi/nix-config) | 54.0 | showcase, library units (1) |
| cfrenette | [cfrenette__nixos-config](configs/cfrenette__nixos-config.md) | [cfrenette/nixos-config](https://github.com/cfrenette/nixos-config) | 42.5 | — |
| clemak27 | [clemak27__homelab](configs/clemak27__homelab.md) | [clemak27/homelab](https://github.com/clemak27/homelab) | 34.5 | library units (1) |
| closure-labs | [closure-labs__foundation](configs/closure-labs__foundation.md) | [closure-labs/foundation](https://github.com/closure-labs/foundation) | 65.5 | library units (1) |
| closure-labs | [closure-labs__maestro](configs/closure-labs__maestro.md) | [closure-labs/maestro](https://github.com/closure-labs/maestro) | 59.5 | library units (2) |
| closure-labs | [closure-labs__mish](configs/closure-labs__mish.md) | [closure-labs/mish](https://github.com/closure-labs/mish) | 61.5 | library units (1) |
| cmetz | [dotfiles](configs/dotfiles.md) | [cmetz/dotfiles](https://github.com/cmetz/dotfiles) | 42.0 | library units (3) |
| danielgafni | [danielgafni__nixos](configs/danielgafni__nixos.md) | [danielgafni/nixos](https://github.com/danielgafni/nixos) | 50.5 | library units (1) |
| derangga | [derangga__dotfiles](configs/derangga__dotfiles.md) | [derangga/dotfiles](https://github.com/derangga/dotfiles) | 46.5 | library units (1) |
| DJ-Laser | [DJ-Laser__nixos](configs/DJ-Laser__nixos.md) | [DJ-Laser/nixos](https://github.com/DJ-Laser/nixos) | 34.0 | library units (1) |
| Draculestein | [Draculestein__nixos-config](configs/Draculestein__nixos-config.md) | [Draculestein/nixos-config](https://github.com/Draculestein/nixos-config) | 47.0 | library units (2) |
| drupol | [drupol](configs/drupol.md) | [drupol/infra](https://github.com/drupol/infra) | 39.0 | library units (2) |
| DylanRJohnston | [DylanRJohnston__nixos](configs/DylanRJohnston__nixos.md) | [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos) | 56.5 | library units (1) |
| eldios | [eldios__dotfiles](configs/eldios__dotfiles.md) | [eldios/dotfiles](https://github.com/eldios/dotfiles) | 51.5 | library units (1) |
| elianiva | [elianiva__dotfiles](configs/elianiva__dotfiles.md) | [elianiva/dotfiles](https://github.com/elianiva/dotfiles) | 45.0 | library units (1) |
| Erastos | [Erastos__nixos-dotfiles](configs/Erastos__nixos-dotfiles.md) | [Erastos/nixos-dotfiles](https://github.com/Erastos/nixos-dotfiles) | 34.0 | library units (1) |
| espdesign | [nixos.den](configs/nixos.den.md) | [espdesign/nixos.den](https://github.com/espdesign/nixos.den) | 38.5 | starter, library units (3) |
| eugencowie | [eugencowie__dotfiles](configs/eugencowie__dotfiles.md) | [eugencowie/dotfiles](https://github.com/eugencowie/dotfiles) | 44.5 | library units (1) |
| EzT32 | [EzT32__nixos](configs/EzT32__nixos.md) | [EzT32/nixos](https://github.com/EzT32/nixos) | 42.0 | — |
| FastTrackStudios | [FastTrackStudios__task](configs/FastTrackStudios__task.md) | [FastTrackStudios/task](https://github.com/FastTrackStudios/task) | partial 51.0 / 90 | library units (1) |
| fmway | [fmway__infra](configs/fmway__infra.md) | [fmway/infra](https://github.com/fmway/infra) | 40.5 | — |
| greysilly7 | [greysilly7__nixos-config](configs/greysilly7__nixos-config.md) | [greysilly7/nixos-config](https://github.com/greysilly7/nixos-config) | 55.5 | showcase, library units (1) |
| Gwenodai | [Gwenodai__nixos](configs/Gwenodai__nixos.md) | [Gwenodai/nixos](https://github.com/Gwenodai/nixos) | 56.0 | showcase, library units (1) |
| henriquekirchheck | [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md) | [henriquekirchheck/nixos-flake](https://github.com/henriquekirchheck/nixos-flake) | 57.5 | showcase, library units (1) |
| Heromercer | [Heromercer__nixfiles](configs/Heromercer__nixfiles.md) | [Heromercer/nixfiles](https://github.com/Heromercer/nixfiles) | 33.0 | library units (3) |
| hmajid2301 | [hmajid2301__nixicle](configs/hmajid2301__nixicle.md) | [hmajid2301/nixicle](https://github.com/hmajid2301/nixicle) | 57.0 | library units (2) |
| hoanhxlyn | [andrewix](configs/andrewix.md) | [hoanhxlyn/andrewix](https://github.com/hoanhxlyn/andrewix) | 54.0 | library units (2) |
| icebluerabbit | [icebluerabbit__nixos](configs/icebluerabbit__nixos.md) | [icebluerabbit/nixos](https://github.com/icebluerabbit/nixos) | 63.0 | library units (1) |
| ivokun | [ivokun__kebun](configs/ivokun__kebun.md) | [ivokun/kebun](https://github.com/ivokun/kebun) | 54.0 | showcase |
| jadestar1864 | [jadestar1864__nix-config](configs/jadestar1864__nix-config.md) | [jadestar1864/nix-config](https://github.com/jadestar1864/nix-config) | 54.5 | library units (1) |
| jasperro | [jasperro__dotfiles](configs/jasperro__dotfiles.md) | [jasperro/dotfiles](https://github.com/jasperro/dotfiles) | 50.5 | library units (1) |
| jcranney | [jcranney__nix-configuration](configs/jcranney__nix-configuration.md) | [jcranney/nix-configuration](https://github.com/jcranney/nix-configuration) | 25.0 | — |
| jkopano | [jkopano__nixiak](configs/jkopano__nixiak.md) | [jkopano/nixiak](https://github.com/jkopano/nixiak) | 47.5 | library units (1) |
| jmartindf | [jmartindf__dendritic](configs/jmartindf__dendritic.md) | [jmartindf/dendritic](https://github.com/jmartindf/dendritic) | 40.5 | library units (1) |
| JoonasKajava | [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md) | [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config) | partial 44.5 / 90 | showcase, library units (1) |
| Keyruu | [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md) | [Keyruu/shinyflakes](https://github.com/Keyruu/shinyflakes) | 55.5 | showcase, library units (1) |
| KGB33 | [KGB33__.dotfiles](configs/KGB33__.dotfiles.md) | [KGB33/.dotfiles](https://github.com/KGB33/.dotfiles) | 48.5 | library units (1) |
| KGB33 | [KGB33__homelab](configs/KGB33__homelab.md) | [KGB33/homelab](https://github.com/KGB33/homelab) | 44.5 | library units (1) |
| klchen0112 | [klchen0112__dotfiles](configs/klchen0112__dotfiles.md) | [klchen0112/dotfiles](https://github.com/klchen0112/dotfiles) | 39.5 | library units (2) |
| Kykero | [Kykero__Nazunix](configs/Kykero__Nazunix.md) | [Kykero/Nazunix](https://github.com/Kykero/Nazunix) | 60.5 | showcase, starter, library units (1) |
| Le0-dot | [Le0-dot__config.nix](configs/Le0-dot__config.nix.md) | [Le0-dot/config.nix](https://github.com/Le0-dot/config.nix) | 57.5 | showcase |
| Likivik | [Likivik__spectacle](configs/Likivik__spectacle.md) | [Likivik/spectacle](https://github.com/Likivik/spectacle) | 43.0 | library units (1) |
| lorenzorapetti | [lorenzorapetti__nix](configs/lorenzorapetti__nix.md) | [lorenzorapetti/nix](https://github.com/lorenzorapetti/nix) | 59.0 | showcase, library units (1) |
| loystonpais | [loystonpais__lunar](configs/loystonpais__lunar.md) | [loystonpais/lunar](https://github.com/loystonpais/lunar) | 51.0 | library units (1) |
| lucasshiva | [lucasshiva](configs/lucasshiva.md) | [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig) | 48.0 | starter, library units (3) |
| mio-19 | [mio-19__config-public](configs/mio-19__config-public.md) | [mio-19/config-public](https://github.com/mio-19/config-public) | 48.5 | — |
| motheki | [motheki__nix](configs/motheki__nix.md) | [motheki/nix](https://github.com/motheki/nix) | 52.5 | starter, library units (1) |
| moxie0420 | [moxie0420__dotfiles](configs/moxie0420__dotfiles.md) | [moxie0420/dotfiles](https://github.com/moxie0420/dotfiles) | 44.5 | library units (1) |
| mrbandler | [mrbandler__nix](configs/mrbandler__nix.md) | [mrbandler/nix](https://github.com/mrbandler/nix) | 59.5 | showcase |
| muhammadtalha-quant | [muhammadtalha-quant__denix](configs/muhammadtalha-quant__denix.md) | [muhammadtalha-quant/denix](https://github.com/muhammadtalha-quant/denix) | 51.5 | library units (1) |
| nazarewk-iac | [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md) | [nazarewk-iac/nix-configs](https://github.com/nazarewk-iac/nix-configs) | 60.0 | showcase, library units (2) |
| neonvoidx | [neonvoidx__nix](configs/neonvoidx__nix.md) | [neonvoidx/nix](https://github.com/neonvoidx/nix) | 57.5 | showcase |
| nifoc | [nifoc__dotfiles](configs/nifoc__dotfiles.md) | [nifoc/dotfiles](https://github.com/nifoc/dotfiles) | 45.5 | — |
| nolvyn | [nolvyn__nixos](configs/nolvyn__nixos.md) | [nolvyn/nixos](https://github.com/nolvyn/nixos) | 52.0 | — |
| Occhima | [Occhima__nix-conf](configs/Occhima__nix-conf.md) | [Occhima/nix-conf](https://github.com/Occhima/nix-conf) | 69.0 | starter, library units (1) |
| OceangreenDev | [oceangreendev](configs/oceangreendev.md) | [OceangreenDev/nix-config](https://github.com/OceangreenDev/nix-config) | 42.0 | library units (5) |
| oxce5 | [oxce5__chimera](configs/oxce5__chimera.md) | [oxce5/chimera](https://github.com/oxce5/chimera) | 47.5 | library units (1) |
| pdarulewski | [pdarulewski__dotfiles](configs/pdarulewski__dotfiles.md) | [pdarulewski/dotfiles](https://github.com/pdarulewski/dotfiles) | 31.0 | library units (1) |
| phucisstupid | [phucisstupid__dotfiles](configs/phucisstupid__dotfiles.md) | [phucisstupid/dotfiles](https://github.com/phucisstupid/dotfiles) | 42.5 | library units (1) |
| quasi-coherent | [quasi-coherent__nix-config](configs/quasi-coherent__nix-config.md) | [quasi-coherent/nix-config](https://github.com/quasi-coherent/nix-config) | 43.5 | — |
| quasigod.xyz | [quasigod-xyz-nixconfig](configs/quasigod-xyz-nixconfig.md) | [quasigod.xyz/nixconfig](https://tangled.org/quasigod.xyz/nixconfig) | 43.0 | library units (3) |
| r17x | [r17x__universe](configs/r17x__universe.md) | [r17x/universe](https://github.com/r17x/universe) | 62.5 | showcase, library units (1) |
| RafaelMuijsert | [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md) | [RafaelMuijsert/nixos-config](https://github.com/RafaelMuijsert/nixos-config) | 50.5 | showcase, library units (1) |
| raphaelladinig | [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md) | [raphaelladinig/dotfiles](https://github.com/raphaelladinig/dotfiles) | 53.0 | showcase, library units (1) |
| recursivepaws | [recursivepaws__nix](configs/recursivepaws__nix.md) | [recursivepaws/nix](https://github.com/recursivepaws/nix) | 46.5 | library units (1) |
| redxtech | [redxtech__nixfiles](configs/redxtech__nixfiles.md) | [redxtech/nixfiles](https://github.com/redxtech/nixfiles) | 51.5 | library units (1) |
| repparw | [repparw__nix](configs/repparw__nix.md) | [repparw/nix](https://github.com/repparw/nix) | 63.0 | showcase, library units (1) |
| rhedgeco | [rhedgeco__nix-config](configs/rhedgeco__nix-config.md) | [rhedgeco/nix-config](https://github.com/rhedgeco/nix-config) | 50.5 | library units (1) |
| scoiatael | [scoiatael__dotfiles](configs/scoiatael__dotfiles.md) | [scoiatael/dotfiles](https://github.com/scoiatael/dotfiles) | 48.0 | library units (3) |
| Sharparam | [Sharparam__nix-config](configs/Sharparam__nix-config.md) | [Sharparam/nix-config](https://github.com/Sharparam/nix-config) | 51.0 | library units (1) |
| Shawn8901 | [Shawn8901__nixos-configuration](configs/Shawn8901__nixos-configuration.md) | [Shawn8901/nixos-configuration](https://github.com/Shawn8901/nixos-configuration) | 44.5 | library units (1) |
| Shochraos | [Shochraos__nixfiles](configs/Shochraos__nixfiles.md) | [Shochraos/nixfiles](https://github.com/Shochraos/nixfiles) | 50.5 | library units (1) |
| sini | [sini__nix-config](configs/sini__nix-config.md) | [sini/nix-config](https://github.com/sini/nix-config) | 71.5 | showcase, library units (9) |
| sk4rd | [sk4rd__mikos-den](configs/sk4rd__mikos-den.md) | [sk4rd/mikos-den](https://github.com/sk4rd/mikos-den) | 57.0 | showcase, library units (1) |
| sm-f | [sm-f__nix](configs/sm-f__nix.md) | [sm-f/nix](https://github.com/sm-f/nix) | 42.5 | library units (1) |
| sonntag | [sonntag__nix](configs/sonntag__nix.md) | [sonntag/nix](https://github.com/sonntag/nix) | 57.0 | library units (2) |
| soriPhoono | [soriPhoono__homelab](configs/soriPhoono__homelab.md) | [soriPhoono/homelab](https://github.com/soriPhoono/homelab) | 61.0 | showcase, library units (2) |
| Spebby | [Spebby__NixOS](configs/Spebby__NixOS.md) | [Spebby/NixOS](https://github.com/Spebby/NixOS) | 48.5 | library units (2) |
| Steven-S1020 | [Steven-S1020__Nixos-Configuration](configs/Steven-S1020__Nixos-Configuration.md) | [Steven-S1020/Nixos-Configuration](https://github.com/Steven-S1020/Nixos-Configuration) | 36.0 | library units (1) |
| SuNNjek | [SuNNjek__nixos-config](configs/SuNNjek__nixos-config.md) | [SuNNjek/nixos-config](https://github.com/SuNNjek/nixos-config) | 50.5 | library units (1) |
| SyahrulBhudiF | [SyahrulBhudiF__dotfiles](configs/SyahrulBhudiF__dotfiles.md) | [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles) | 30.0 | library units (1) |
| talarys | [talarys__den](configs/talarys__den.md) | [talarys/den](https://github.com/talarys/den) | 34.0 | library units (1) |
| theutz | [theutz](configs/theutz.md) | [~theutz/flake](https://git.sr.ht/~theutz/flake) | 53.0 | library units (2) |
| thomasgoulet | [thomasgoulet__nixnites](configs/thomasgoulet__nixnites.md) | [thomasgoulet/nixnites](https://github.com/thomasgoulet/nixnites) | 40.0 | — |
| tomwrw | [megadots](configs/megadots.md) | [tomwrw/megadots](https://github.com/tomwrw/megadots) | 67.5 | showcase, library units (4) |
| trash-panda-v91-beta | [trash-panda-v91-beta__dots.factory](configs/trash-panda-v91-beta__dots.factory.md) | [trash-panda-v91-beta/dots.factory](https://github.com/trash-panda-v91-beta/dots.factory) | 45.0 | — |
| vitalyavolyn | [vitalyavolyn__dotfiles](configs/vitalyavolyn__dotfiles.md) | [vitalyavolyn/dotfiles](https://github.com/vitalyavolyn/dotfiles) | 48.0 | library units (1) |
| vodfsh | [vodfsh__nixos-config](configs/vodfsh__nixos-config.md) | [vodfsh/nixos-config](https://github.com/vodfsh/nixos-config) | 36.0 | — |
| voidlily | [voidlily__dotfiles](configs/voidlily__dotfiles.md) | [voidlily/dotfiles](https://github.com/voidlily/dotfiles) | 47.5 | library units (1) |
| zakuciael | [nixpedition](configs/nixpedition.md) | [zakuciael/nixpedition](https://github.com/zakuciael/nixpedition) | 57.5 | showcase, library units (4) |

3 more configs were scored and are counted in the totals. They are not listed, because their source is
no longer public.

## Top 15

This table gives the 15 highest totals. Ties at the cutoff are included.

| rank | config | author | total | shortlists |
|---:|---|---|---:|---|
| 1 | [sini__nix-config](configs/sini__nix-config.md) | sini | 71.5 | showcase, library units (9) |
| 2 | [Occhima__nix-conf](configs/Occhima__nix-conf.md) | Occhima | 69.0 | starter, library units (1) |
| 3 | [auscyber__dotfiles](configs/auscyber__dotfiles.md) | auscyber | 68.5 | showcase, library units (3) |
| 4 | [megadots](configs/megadots.md) | tomwrw | 67.5 | showcase, library units (4) |
| 5 | [Aor-Li__Infra](configs/Aor-Li__Infra.md) | Aor-Li | 66.5 | showcase, library units (2) |
| 6 | [closure-labs__foundation](configs/closure-labs__foundation.md) | closure-labs | 65.5 | library units (1) |
| 7 | [amatos__magnanix](configs/amatos__magnanix.md) | amatos | 64.0 | starter, library units (1) |
| 8 | [icebluerabbit__nixos](configs/icebluerabbit__nixos.md) | icebluerabbit | 63.0 | library units (1) |
| 8 | [repparw__nix](configs/repparw__nix.md) | repparw | 63.0 | showcase, library units (1) |
| 10 | [r17x__universe](configs/r17x__universe.md) | r17x | 62.5 | showcase, library units (1) |
| 11 | [closure-labs__mish](configs/closure-labs__mish.md) | closure-labs | 61.5 | library units (1) |
| 12 | [soriPhoono__homelab](configs/soriPhoono__homelab.md) | soriPhoono | 61.0 | showcase, library units (2) |
| 13 | [Kykero__Nazunix](configs/Kykero__Nazunix.md) | Kykero | 60.5 | showcase, starter, library units (1) |
| 14 | [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md) | nazarewk-iac | 60.0 | showcase, library units (2) |
| 15 | [adda-nixos-config](configs/adda-nixos-config.md) | Adda | 59.5 | library units (4) |
| 15 | [closure-labs__maestro](configs/closure-labs__maestro.md) | closure-labs | 59.5 | library units (2) |
| 15 | [mrbandler__nix](configs/mrbandler__nix.md) | mrbandler | 59.5 | showcase |

`sini__nix-config` is the audit maintainer's own configuration and the rubric's reference anchor. It was scored
under the same rubric as every other config.

## Starter picks

These are good configs to learn from. Each one has these properties:

- a short path from the flake entry to a built host;
- few prerequisites;
- clear host and user variation;
- an honest statement of which platforms it supports.

- [Occhima__nix-conf](configs/Occhima__nix-conf.md) by Occhima, 69.0
- [amatos__magnanix](configs/amatos__magnanix.md) by amatos, 64.0
- [Kykero__Nazunix](configs/Kykero__Nazunix.md) by Kykero, 60.5
- [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md) by andreshungbz, 54.5
- [motheki__nix](configs/motheki__nix.md) by motheki, 52.5
- [lucasshiva](configs/lucasshiva.md) by lucasshiva, 48.0
- [nixos.den](configs/nixos.den.md) by espdesign, 38.5

## Showcase picks

These configs demonstrate a den mechanism especially well. Examples of such mechanisms are routed data between
hosts, typed settings and den data that drives deployment.

- [sini__nix-config](configs/sini__nix-config.md) by sini, 71.5
- [auscyber__dotfiles](configs/auscyber__dotfiles.md) by auscyber, 68.5
- [megadots](configs/megadots.md) by tomwrw, 67.5
- [Aor-Li__Infra](configs/Aor-Li__Infra.md) by Aor-Li, 66.5
- [repparw__nix](configs/repparw__nix.md) by repparw, 63.0
- [r17x__universe](configs/r17x__universe.md) by r17x, 62.5
- [soriPhoono__homelab](configs/soriPhoono__homelab.md) by soriPhoono, 61.0
- [Kykero__Nazunix](configs/Kykero__Nazunix.md) by Kykero, 60.5
- [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md) by nazarewk-iac, 60.0
- [mrbandler__nix](configs/mrbandler__nix.md) by mrbandler, 59.5
- [lorenzorapetti__nix](configs/lorenzorapetti__nix.md) by lorenzorapetti, 59.0
- [Le0-dot__config.nix](configs/Le0-dot__config.nix.md) by Le0-dot, 57.5
- [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md) by henriquekirchheck, 57.5
- [neonvoidx__nix](configs/neonvoidx__nix.md) by neonvoidx, 57.5
- [nixpedition](configs/nixpedition.md) by zakuciael, 57.5
- [sk4rd__mikos-den](configs/sk4rd__mikos-den.md) by sk4rd, 57.0
- [Gwenodai__nixos](configs/Gwenodai__nixos.md) by Gwenodai, 56.0
- [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md) by Keyruu, 55.5
- [greysilly7__nixos-config](configs/greysilly7__nixos-config.md) by greysilly7, 55.5
- [aveeryy__kadachi](configs/aveeryy__kadachi.md) by aveeryy, 54.0
- [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md) by byte-sized-emi, 54.0
- [ivokun__kebun](configs/ivokun__kebun.md) by ivokun, 54.0
- [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md) by raphaelladinig, 53.0
- [anders130__dotfiles](configs/anders130__dotfiles.md) by anders130, 52.5
- [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md) by AnonymousRand, 52.0
- [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md) by RafaelMuijsert, 50.5
- [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md) by JoonasKajava, partial 44.5 / 90

## Libraries

These repos are namespace libraries. They are scored on their own track and are not in the ranking.

- [adanoelle__garden-shell](libraries/adanoelle__garden-shell.md) by adanoelle: the `garden` namespace, an aspect and package library, a pure namespace provider
- [crocuda__crocuda.nixos](libraries/crocuda__crocuda.nixos.md) by crocuda: the `crocuda` namespace, hardened NixOS server modules, with dotfiles kept in their native formats and Nix as glue
- [crocuda__normal.nixos](libraries/crocuda__normal.nixos.md) by crocuda: the `normal` namespace, the same author's opinionated desktop modules

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

[Occhima__nix-conf](configs/Occhima__nix-conf.md) by Occhima has rank 2 of 103 ranked configs. Its shortlists are: starter, library units (1).

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

- [acrobertson](https://github.com/acrobertson): [acrobertson__infra](configs/acrobertson__infra.md)
- [adanoelle](https://github.com/adanoelle): [adanoelle__fern](configs/adanoelle__fern.md), [adanoelle__garden-shell](libraries/adanoelle__garden-shell.md)
- [Adda](https://codeberg.org/Adda): [adda-nixos-config](configs/adda-nixos-config.md)
- [aeshakhzod](https://github.com/aeshakhzod): [aeshakhzod__blazingly-fast](configs/aeshakhzod__blazingly-fast.md)
- [akeuben](https://github.com/akeuben): [akeuben__dotfiles](configs/akeuben__dotfiles.md)
- [amatos](https://github.com/amatos): [amatos__magnanix](configs/amatos__magnanix.md)
- [anders130](https://github.com/anders130): [anders130__dotfiles](configs/anders130__dotfiles.md)
- [andreshungbz](https://github.com/andreshungbz): [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md)
- [AnonymousRand](https://github.com/AnonymousRand): [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md)
- [Aor-Li](https://github.com/Aor-Li): [Aor-Li__Infra](configs/Aor-Li__Infra.md)
- [arichtman](https://github.com/arichtman): [arichtman__nix](configs/arichtman__nix.md)
- [augustocdias](https://github.com/augustocdias): [augustocdias__nixos](configs/augustocdias__nixos.md)
- [aullisia](https://github.com/aullisia): [aullisia__nixos-config](configs/aullisia__nixos-config.md)
- [auscyber](https://github.com/auscyber): [auscyber__dotfiles](configs/auscyber__dotfiles.md)
- [aveeryy](https://github.com/aveeryy): [aveeryy__kadachi](configs/aveeryy__kadachi.md)
- [byte-sized-emi](https://github.com/byte-sized-emi): [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md)
- [cfrenette](https://github.com/cfrenette): [cfrenette__nixos-config](configs/cfrenette__nixos-config.md)
- [clemak27](https://github.com/clemak27): [clemak27__homelab](configs/clemak27__homelab.md)
- [closure-labs](https://github.com/closure-labs): [closure-labs__foundation](configs/closure-labs__foundation.md), [closure-labs__maestro](configs/closure-labs__maestro.md), [closure-labs__mish](configs/closure-labs__mish.md)
- [cmetz](https://github.com/cmetz): [dotfiles](configs/dotfiles.md)
- [crocuda](https://github.com/crocuda): [crocuda__crocuda.nixos](libraries/crocuda__crocuda.nixos.md), [crocuda__normal.nixos](libraries/crocuda__normal.nixos.md)
- [danielgafni](https://github.com/danielgafni): [danielgafni__nixos](configs/danielgafni__nixos.md)
- [derangga](https://github.com/derangga): [derangga__dotfiles](configs/derangga__dotfiles.md)
- [DJ-Laser](https://github.com/DJ-Laser): [DJ-Laser__nixos](configs/DJ-Laser__nixos.md)
- [Draculestein](https://github.com/Draculestein): [Draculestein__nixos-config](configs/Draculestein__nixos-config.md)
- [drupol](https://github.com/drupol): [drupol](configs/drupol.md)
- [DylanRJohnston](https://github.com/DylanRJohnston): [DylanRJohnston__nixos](configs/DylanRJohnston__nixos.md)
- [eldios](https://github.com/eldios): [eldios__dotfiles](configs/eldios__dotfiles.md)
- [elianiva](https://github.com/elianiva): [elianiva__dotfiles](configs/elianiva__dotfiles.md)
- [Erastos](https://github.com/Erastos): [Erastos__nixos-dotfiles](configs/Erastos__nixos-dotfiles.md)
- [espdesign](https://github.com/espdesign): [nixos.den](configs/nixos.den.md)
- [eugencowie](https://github.com/eugencowie): [eugencowie__dotfiles](configs/eugencowie__dotfiles.md)
- [EzT32](https://github.com/EzT32): [EzT32__nixos](configs/EzT32__nixos.md)
- [FastTrackStudios](https://github.com/FastTrackStudios): [FastTrackStudios__task](configs/FastTrackStudios__task.md)
- [fmway](https://github.com/fmway): [fmway__infra](configs/fmway__infra.md)
- [greysilly7](https://github.com/greysilly7): [greysilly7__nixos-config](configs/greysilly7__nixos-config.md)
- [Gwenodai](https://github.com/Gwenodai): [Gwenodai__nixos](configs/Gwenodai__nixos.md)
- [henriquekirchheck](https://github.com/henriquekirchheck): [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md)
- [Heromercer](https://github.com/Heromercer): [Heromercer__nixfiles](configs/Heromercer__nixfiles.md)
- [hmajid2301](https://github.com/hmajid2301): [hmajid2301__nixicle](configs/hmajid2301__nixicle.md)
- [hoanhxlyn](https://github.com/hoanhxlyn): [andrewix](configs/andrewix.md)
- [icebluerabbit](https://github.com/icebluerabbit): [icebluerabbit__nixos](configs/icebluerabbit__nixos.md)
- [ivokun](https://github.com/ivokun): [ivokun__kebun](configs/ivokun__kebun.md)
- [jadestar1864](https://github.com/jadestar1864): [jadestar1864__nix-config](configs/jadestar1864__nix-config.md)
- [jasperro](https://github.com/jasperro): [jasperro__dotfiles](configs/jasperro__dotfiles.md)
- [jcranney](https://github.com/jcranney): [jcranney__nix-configuration](configs/jcranney__nix-configuration.md)
- [jkopano](https://github.com/jkopano): [jkopano__nixiak](configs/jkopano__nixiak.md)
- [jmartindf](https://github.com/jmartindf): [jmartindf__dendritic](configs/jmartindf__dendritic.md)
- [JoonasKajava](https://github.com/JoonasKajava): [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md)
- [Keyruu](https://github.com/Keyruu): [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md)
- [KGB33](https://github.com/KGB33): [KGB33__.dotfiles](configs/KGB33__.dotfiles.md), [KGB33__homelab](configs/KGB33__homelab.md)
- [klchen0112](https://github.com/klchen0112): [klchen0112__dotfiles](configs/klchen0112__dotfiles.md)
- [Kykero](https://github.com/Kykero): [Kykero__Nazunix](configs/Kykero__Nazunix.md)
- [Le0-dot](https://github.com/Le0-dot): [Le0-dot__config.nix](configs/Le0-dot__config.nix.md)
- [Likivik](https://github.com/Likivik): [Likivik__spectacle](configs/Likivik__spectacle.md)
- [lorenzorapetti](https://github.com/lorenzorapetti): [lorenzorapetti__nix](configs/lorenzorapetti__nix.md)
- [loystonpais](https://github.com/loystonpais): [loystonpais__lunar](configs/loystonpais__lunar.md)
- [lucasshiva](https://github.com/lucasshiva): [lucasshiva](configs/lucasshiva.md)
- [mio-19](https://github.com/mio-19): [mio-19__config-public](configs/mio-19__config-public.md)
- [motheki](https://github.com/motheki): [motheki__nix](configs/motheki__nix.md)
- [moxie0420](https://github.com/moxie0420): [moxie0420__dotfiles](configs/moxie0420__dotfiles.md)
- [mrbandler](https://github.com/mrbandler): [mrbandler__nix](configs/mrbandler__nix.md)
- [muhammadtalha-quant](https://github.com/muhammadtalha-quant): [muhammadtalha-quant__denix](configs/muhammadtalha-quant__denix.md)
- [nazarewk-iac](https://github.com/nazarewk-iac): [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md)
- [neonvoidx](https://github.com/neonvoidx): [neonvoidx__nix](configs/neonvoidx__nix.md)
- [nifoc](https://github.com/nifoc): [nifoc__dotfiles](configs/nifoc__dotfiles.md)
- [nolvyn](https://github.com/nolvyn): [nolvyn__nixos](configs/nolvyn__nixos.md)
- [Occhima](https://github.com/Occhima): [Occhima__nix-conf](configs/Occhima__nix-conf.md)
- [OceangreenDev](https://github.com/OceangreenDev): [oceangreendev](configs/oceangreendev.md)
- [oxce5](https://github.com/oxce5): [oxce5__chimera](configs/oxce5__chimera.md)
- [pdarulewski](https://github.com/pdarulewski): [pdarulewski__dotfiles](configs/pdarulewski__dotfiles.md)
- [phucisstupid](https://github.com/phucisstupid): [phucisstupid__dotfiles](configs/phucisstupid__dotfiles.md)
- [quasi-coherent](https://github.com/quasi-coherent): [quasi-coherent__nix-config](configs/quasi-coherent__nix-config.md)
- [quasigod.xyz](https://tangled.org/quasigod.xyz): [quasigod-xyz-nixconfig](configs/quasigod-xyz-nixconfig.md)
- [r17x](https://github.com/r17x): [r17x__universe](configs/r17x__universe.md)
- [RafaelMuijsert](https://github.com/RafaelMuijsert): [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md)
- [raphaelladinig](https://github.com/raphaelladinig): [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md)
- [recursivepaws](https://github.com/recursivepaws): [recursivepaws__nix](configs/recursivepaws__nix.md)
- [redxtech](https://github.com/redxtech): [redxtech__nixfiles](configs/redxtech__nixfiles.md)
- [repparw](https://github.com/repparw): [repparw__nix](configs/repparw__nix.md)
- [rhedgeco](https://github.com/rhedgeco): [rhedgeco__nix-config](configs/rhedgeco__nix-config.md)
- [scoiatael](https://github.com/scoiatael): [scoiatael__dotfiles](configs/scoiatael__dotfiles.md)
- [Sharparam](https://github.com/Sharparam): [Sharparam__nix-config](configs/Sharparam__nix-config.md)
- [Shawn8901](https://github.com/Shawn8901): [Shawn8901__nixos-configuration](configs/Shawn8901__nixos-configuration.md)
- [Shochraos](https://github.com/Shochraos): [Shochraos__nixfiles](configs/Shochraos__nixfiles.md)
- [sini](https://github.com/sini): [sini__nix-config](configs/sini__nix-config.md)
- [sk4rd](https://github.com/sk4rd): [sk4rd__mikos-den](configs/sk4rd__mikos-den.md)
- [sm-f](https://github.com/sm-f): [sm-f__nix](configs/sm-f__nix.md)
- [sonntag](https://github.com/sonntag): [sonntag__nix](configs/sonntag__nix.md)
- [soriPhoono](https://github.com/soriPhoono): [soriPhoono__homelab](configs/soriPhoono__homelab.md)
- [Spebby](https://github.com/Spebby): [Spebby__NixOS](configs/Spebby__NixOS.md)
- [Steven-S1020](https://github.com/Steven-S1020): [Steven-S1020__Nixos-Configuration](configs/Steven-S1020__Nixos-Configuration.md)
- [SuNNjek](https://github.com/SuNNjek): [SuNNjek__nixos-config](configs/SuNNjek__nixos-config.md)
- [SyahrulBhudiF](https://github.com/SyahrulBhudiF): [SyahrulBhudiF__dotfiles](configs/SyahrulBhudiF__dotfiles.md)
- [talarys](https://github.com/talarys): [talarys__den](configs/talarys__den.md)
- [theutz](https://sr.ht/~theutz): [theutz](configs/theutz.md)
- [thomasgoulet](https://github.com/thomasgoulet): [thomasgoulet__nixnites](configs/thomasgoulet__nixnites.md)
- [tomwrw](https://github.com/tomwrw): [megadots](configs/megadots.md)
- [trash-panda-v91-beta](https://github.com/trash-panda-v91-beta): [trash-panda-v91-beta__dots.factory](configs/trash-panda-v91-beta__dots.factory.md)
- [vitalyavolyn](https://github.com/vitalyavolyn): [vitalyavolyn__dotfiles](configs/vitalyavolyn__dotfiles.md)
- [vodfsh](https://github.com/vodfsh): [vodfsh__nixos-config](configs/vodfsh__nixos-config.md)
- [voidlily](https://github.com/voidlily): [voidlily__dotfiles](configs/voidlily__dotfiles.md)
- [zakuciael](https://github.com/zakuciael): [nixpedition](configs/nixpedition.md)

## Corrections and opt-out

If a finding is wrong, or you want your config removed from this survey, please open an issue. Name the config and
the finding, and link the source if you can. Removal requests are honoured without question. See
[CONTRIBUTING.md](CONTRIBUTING.md).

## License

The audit text is licensed under [CC BY 4.0](LICENSE). The configurations themselves belong to their authors and keep
their own licenses. Short quotations from them are used here for review.

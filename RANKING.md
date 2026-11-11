# Ranking

This page ranks the published configs by their totals, and shows the ten category scores behind each total. It is for readers who want to compare configs, or to find configs that are strong in one category. For the terms on this page, see the [glossary](GLOSSARY.md).

Each category is scored 1-10. The total is out of 100 and uses 2D + I + S + R + P + L + O + B + ½V + ½X. Shortlists are independent judgments, not awards. The anchors for each score are in [method/RUBRIC.md](method/RUBRIC.md). The README shows [how to read a scorecard](README.md#how-to-read-a-scorecard).

3 scored configs are counted but not listed, because their source is no longer public. They are part of the category distributions below and of the census totals.

`sini__nix-config` is the audit maintainer's own configuration and the rubric's reference anchor. It was scored under the same rubric as every other config.

## Contents

- [Full ranking](#full-ranking)
- [Partial vectors](#partial-vectors)
- [Category distributions](#category-distributions)
- [Showcase](#showcase)
- [Starter](#starter)
- [Library units](#library-units)

## Full ranking

The score columns use one letter per category:

| letter | category | weight in the total |
|---|---|---|
| D | structured data flow | ×2 |
| I | layout and isolation of concerns | ×1 |
| S | settings and variation contracts | ×1 |
| R | reuse contract | ×1 |
| P | platform boundaries | ×1 |
| L | explanation and navigation | ×1 |
| V | verification intent | ×½ |
| O | operations driven by den data | ×1 |
| B | application breadth | ×1 |
| X | integrations with other module systems | ×½ |

| rank | config | upstream | total | D | I | S | R | P | L | V | O | B | X | shortlists |
|---:|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| 1 | [sini__nix-config](configs/sini__nix-config.md) | [sini/nix-config](https://github.com/sini/nix-config) | 71.5 | 7 | 9 | 5 | 6 | 7 | 6 | 6 | 9 | 8 | 9 | showcase, library units (9) |
| 2 | [Occhima__nix-conf](configs/Occhima__nix-conf.md) | [Occhima/nix-conf](https://github.com/Occhima/nix-conf) | 69.0 | 6 | 9 | 6 | 7 | 8 | 8 | 9 | 5 | 7 | 5 | starter, library units (1) |
| 3 | [auscyber__dotfiles](configs/auscyber__dotfiles.md) | [auscyber/dotfiles](https://github.com/auscyber/dotfiles) | 68.5 | 7 | 8 | 6 | 7 | 7 | 6 | 7 | 8 | 5 | 8 | showcase, library units (3) |
| 4 | [megadots](configs/megadots.md) | [tomwrw/megadots](https://github.com/tomwrw/megadots) | 67.5 | 8 | 9 | 6 | 7 | 6 | 9 | 5 | 6 | 5 | 2 | showcase, library units (4) |
| 5 | [Aor-Li__Infra](configs/Aor-Li__Infra.md) | [Aor-Li/Infra](https://github.com/Aor-Li/Infra) | 66.5 | 7 | 8 | 5 | 9 | 8 | 8 | 3 | 5 | 7 | 2 | showcase, library units (2) |
| 6 | [closure-labs__foundation](configs/closure-labs__foundation.md) | [closure-labs/foundation](https://github.com/closure-labs/foundation) | 65.5 | 5 | 9 | 7 | 9 | 9 | 9 | 9 | 5 | 2 | 2 | library units (1) |
| 7 | [amatos__magnanix](configs/amatos__magnanix.md) | [amatos/magnanix](https://github.com/amatos/magnanix) | 64.0 | 5 | 8 | 6 | 5 | 9 | 9 | 6 | 6 | 7 | 2 | starter, library units (1) |
| 8 | [icebluerabbit__nixos](configs/icebluerabbit__nixos.md) | [icebluerabbit/nixos](https://github.com/icebluerabbit/nixos) | 63.0 | 5 | 8 | 5 | 7 | 7 | 7 | 5 | 7 | 7 | 5 | library units (1) |
| 8 | [repparw__nix](configs/repparw__nix.md) | [repparw/nix](https://github.com/repparw/nix) | 63.0 | 8 | 7 | 5 | 5 | 5 | 8 | 8 | 8 | 4 | 2 | showcase, library units (1) |
| 10 | [r17x__universe](configs/r17x__universe.md) | [r17x/universe](https://github.com/r17x/universe) | 62.5 | 7 | 9 | 7 | 5 | 5 | 7 | 8 | 6 | 3 | 5 | showcase, library units (1) |
| 11 | [closure-labs__mish](configs/closure-labs__mish.md) | [closure-labs/mish](https://github.com/closure-labs/mish) | 61.5 | 2 | 9 | 9 | 9 | 9 | 9 | 9 | 5 | 2 | 2 | library units (1) |
| 12 | [soriPhoono__homelab](configs/soriPhoono__homelab.md) | [soriPhoono/homelab](https://github.com/soriPhoono/homelab) | 61.0 | 5 | 7 | 6 | 7 | 7 | 7 | 6 | 7 | 6 | 2 | showcase, library units (2) |
| 13 | [Kykero__Nazunix](configs/Kykero__Nazunix.md) | [Kykero/Nazunix](https://github.com/Kykero/Nazunix) | 60.5 | 6 | 8 | 7 | 5 | 5 | 9 | 7 | 5 | 5 | 2 | showcase, starter, library units (1) |
| 14 | [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md) | [nazarewk-iac/nix-configs](https://github.com/nazarewk-iac/nix-configs) | 60.0 | 2 | 9 | 6 | 8 | 9 | 8 | 9 | 2 | 7 | 5 | showcase, library units (2) |
| 15 | [adda-nixos-config](configs/adda-nixos-config.md) | [Adda/nixos-config](https://codeberg.org/Adda/nixos-config) | 59.5 | 7 | 7 | 6 | 6 | 5 | 8 | 3 | 3 | 8 | 2 | library units (4) |
| 15 | [closure-labs__maestro](configs/closure-labs__maestro.md) | [closure-labs/maestro](https://github.com/closure-labs/maestro) | 59.5 | 4 | 6 | 7 | 9 | 7 | 9 | 9 | 6 | 2 | 2 | library units (2) |
| 15 | [mrbandler__nix](configs/mrbandler__nix.md) | [mrbandler/nix](https://github.com/mrbandler/nix) | 59.5 | 5 | 7 | 6 | 5 | 7 | 7 | 5 | 6 | 8 | 2 | showcase |
| 18 | [lorenzorapetti__nix](configs/lorenzorapetti__nix.md) | [lorenzorapetti/nix](https://github.com/lorenzorapetti/nix) | 59.0 | 7 | 6 | 4 | 7 | 5 | 7 | 6 | 7 | 5 | 2 | showcase, library units (1) |
| 19 | [adanoelle__fern](configs/adanoelle__fern.md) | [adanoelle/fern](https://github.com/adanoelle/fern) | 58.5 | 5 | 8 | 5 | 7 | 5 | 8 | 3 | 5 | 8 | 2 | library units (1) |
| 20 | [Le0-dot__config.nix](configs/Le0-dot__config.nix.md) | [Le0-dot/config.nix](https://github.com/Le0-dot/config.nix) | 57.5 | 6 | 7 | 6 | 5 | 7 | 5 | 6 | 7 | 3 | 5 | showcase |
| 20 | [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md) | [henriquekirchheck/nixos-flake](https://github.com/henriquekirchheck/nixos-flake) | 57.5 | 7 | 9 | 7 | 5 | 5 | 2 | 5 | 5 | 7 | 2 | showcase, library units (1) |
| 20 | [neonvoidx__nix](configs/neonvoidx__nix.md) | [neonvoidx/nix](https://github.com/neonvoidx/nix) | 57.5 | 5 | 9 | 5 | 5 | 5 | 8 | 5 | 6 | 6 | 2 | showcase |
| 20 | [nixpedition](configs/nixpedition.md) | [zakuciael/nixpedition](https://github.com/zakuciael/nixpedition) | 57.5 | 7 | 8 | 6 | 5 | 5 | 2 | 6 | 8 | 3 | 7 | showcase, library units (4) |
| 24 | [hmajid2301__nixicle](configs/hmajid2301__nixicle.md) | [hmajid2301/nixicle](https://github.com/hmajid2301/nixicle) | 57.0 | 6 | 6 | 4 | 9 | 6 | 2 | 6 | 7 | 7 | 2 | library units (2) |
| 24 | [sk4rd__mikos-den](configs/sk4rd__mikos-den.md) | [sk4rd/mikos-den](https://github.com/sk4rd/mikos-den) | 57.0 | 7 | 9 | 6 | 5 | 5 | 7 | 4 | 5 | 3 | 2 | showcase, library units (1) |
| 24 | [sonntag__nix](configs/sonntag__nix.md) | [sonntag/nix](https://github.com/sonntag/nix) | 57.0 | 5 | 6 | 5 | 5 | 7 | 8 | 4 | 7 | 6 | 2 | library units (2) |
| 27 | [DylanRJohnston__nixos](configs/DylanRJohnston__nixos.md) | [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos) | 56.5 | 5 | 8 | 5 | 5 | 8 | 5 | 9 | 5 | 5 | 2 | library units (1) |
| 28 | [Gwenodai__nixos](configs/Gwenodai__nixos.md) | [Gwenodai/nixos](https://github.com/Gwenodai/nixos) | 56.0 | 7 | 7 | 6 | 7 | 5 | 2 | 2 | 7 | 6 | 2 | showcase, library units (1) |
| 29 | [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md) | [Keyruu/shinyflakes](https://github.com/Keyruu/shinyflakes) | 55.5 | 7 | 8 | 4 | 5 | 5 | 3 | 5 | 5 | 8 | 2 | showcase, library units (1) |
| 29 | [greysilly7__nixos-config](configs/greysilly7__nixos-config.md) | [greysilly7/nixos-config](https://github.com/greysilly7/nixos-config) | 55.5 | 7 | 5 | 4 | 7 | 7 | 2 | 5 | 7 | 6 | 2 | showcase, library units (1) |
| 31 | [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md) | [andreshungbz/nixconfig](https://github.com/andreshungbz/nixconfig) | 54.5 | 5 | 8 | 5 | 5 | 8 | 5 | 3 | 5 | 6 | 2 | starter, library units (1) |
| 31 | [jadestar1864__nix-config](configs/jadestar1864__nix-config.md) | [jadestar1864/nix-config](https://github.com/jadestar1864/nix-config) | 54.5 | 7 | 5 | 5 | 5 | 6 | 5 | 5 | 5 | 6 | 2 | library units (1) |
| 33 | [andrewix](configs/andrewix.md) | [hoanhxlyn/andrewix](https://github.com/hoanhxlyn/andrewix) | 54.0 | 5 | 8 | 6 | 5 | 6 | 7 | 2 | 5 | 5 | 2 | library units (2) |
| 33 | [aveeryy__kadachi](configs/aveeryy__kadachi.md) | [aveeryy/kadachi](https://github.com/aveeryy/kadachi) | 54.0 | 8 | 8 | 5 | 5 | 4 | 2 | 2 | 7 | 5 | 2 | showcase, library units (3) |
| 33 | [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md) | [byte-sized-emi/nix-config](https://github.com/byte-sized-emi/nix-config) | 54.0 | 7 | 8 | 4 | 7 | 5 | 3 | 2 | 7 | 4 | 2 | showcase, library units (1) |
| 33 | [ivokun__kebun](configs/ivokun__kebun.md) | [ivokun/kebun](https://github.com/ivokun/kebun) | 54.0 | 5 | 7 | 6 | 5 | 5 | 9 | 6 | 3 | 5 | 2 | showcase |
| 37 | [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md) | [raphaelladinig/dotfiles](https://github.com/raphaelladinig/dotfiles) | 53.0 | 5 | 8 | 8 | 6 | 5 | 2 | 8 | 6 | 3 | 2 | showcase, library units (1) |
| 37 | [theutz](configs/theutz.md) | [~theutz/flake](https://git.sr.ht/~theutz/flake) | 53.0 | 7 | 7 | 4 | 5 | 6 | 1 | 2 | 7 | 7 | 2 | library units (2) |
| 39 | [anders130__dotfiles](configs/anders130__dotfiles.md) | [anders130/dotfiles](https://github.com/anders130/dotfiles) | 52.5 | 5 | 6 | 5 | 7 | 5 | 4 | 5 | 7 | 5 | 2 | showcase, library units (1) |
| 39 | [motheki__nix](configs/motheki__nix.md) | [motheki/nix](https://github.com/motheki/nix) | 52.5 | 5 | 8 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 2 | starter, library units (1) |
| 41 | [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md) | [AnonymousRand/nix_config](https://github.com/AnonymousRand/nix_config) | 52.0 | 7 | 8 | 6 | 5 | 5 | 7 | 2 | 2 | 3 | 2 | showcase, library units (1) |
| 41 | [nolvyn__nixos](configs/nolvyn__nixos.md) | [nolvyn/nixos](https://github.com/nolvyn/nixos) | 52.0 | 5 | 8 | 6 | 5 | 7 | 2 | 6 | 5 | 5 | 2 | — |
| 43 | [eldios__dotfiles](configs/eldios__dotfiles.md) | [eldios/dotfiles](https://github.com/eldios/dotfiles) | 51.5 | 5 | 6 | 4 | 5 | 5 | 7 | 5 | 6 | 5 | 2 | library units (1) |
| 43 | [muhammadtalha-quant__denix](configs/muhammadtalha-quant__denix.md) | [muhammadtalha-quant/denix](https://github.com/muhammadtalha-quant/denix) | 51.5 | 5 | 8 | 5 | 5 | 5 | 6 | 5 | 5 | 4 | 2 | library units (1) |
| 43 | [redxtech__nixfiles](configs/redxtech__nixfiles.md) | [redxtech/nixfiles](https://github.com/redxtech/nixfiles) | 51.5 | 5 | 7 | 5 | 5 | 5 | 5 | 5 | 6 | 5 | 2 | library units (1) |
| 46 | [Sharparam__nix-config](configs/Sharparam__nix-config.md) | [Sharparam/nix-config](https://github.com/Sharparam/nix-config) | 51.0 | 6 | 5 | 3 | 5 | 7 | 2 | 4 | 6 | 8 | 2 | library units (1) |
| 46 | [loystonpais__lunar](configs/loystonpais__lunar.md) | [loystonpais/lunar](https://github.com/loystonpais/lunar) | 51.0 | 5 | 7 | 3 | 5 | 5 | 5 | 3 | 6 | 6 | 5 | library units (1) |
| 48 | [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md) | [RafaelMuijsert/nixos-config](https://github.com/RafaelMuijsert/nixos-config) | 50.5 | 6 | 8 | 5 | 5 | 4 | 4 | 3 | 5 | 5 | 2 | showcase, library units (1) |
| 48 | [Shochraos__nixfiles](configs/Shochraos__nixfiles.md) | [Shochraos/nixfiles](https://github.com/Shochraos/nixfiles) | 50.5 | 5 | 7 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 2 | library units (1) |
| 48 | [SuNNjek__nixos-config](configs/SuNNjek__nixos-config.md) | [SuNNjek/nixos-config](https://github.com/SuNNjek/nixos-config) | 50.5 | 6 | 9 | 5 | 5 | 5 | 2 | 5 | 5 | 4 | 2 | library units (1) |
| 48 | [danielgafni__nixos](configs/danielgafni__nixos.md) | [danielgafni/nixos](https://github.com/danielgafni/nixos) | 50.5 | 5 | 5 | 4 | 7 | 7 | 4 | 5 | 5 | 5 | 2 | library units (1) |
| 48 | [jasperro__dotfiles](configs/jasperro__dotfiles.md) | [jasperro/dotfiles](https://github.com/jasperro/dotfiles) | 50.5 | 5 | 5 | 5 | 5 | 7 | 4 | 3 | 6 | 6 | 2 | library units (1) |
| 48 | [rhedgeco__nix-config](configs/rhedgeco__nix-config.md) | [rhedgeco/nix-config](https://github.com/rhedgeco/nix-config) | 50.5 | 6 | 8 | 6 | 5 | 5 | 2 | 5 | 4 | 5 | 2 | library units (1) |
| 54 | [KGB33__.dotfiles](configs/KGB33__.dotfiles.md) | [KGB33/.dotfiles](https://github.com/KGB33/.dotfiles) | 48.5 | 2 | 8 | 5 | 5 | 8 | 2 | 9 | 5 | 6 | 2 | library units (1) |
| 54 | [Spebby__NixOS](configs/Spebby__NixOS.md) | [Spebby/NixOS](https://github.com/Spebby/NixOS) | 48.5 | 5 | 5 | 7 | 5 | 4 | 3 | 5 | 5 | 6 | 2 | library units (2) |
| 54 | [mio-19__config-public](configs/mio-19__config-public.md) | [mio-19/config-public](https://github.com/mio-19/config-public) | 48.5 | 5 | 5 | 6 | 5 | 7 | 3 | 4 | 2 | 6 | 5 | — |
| 57 | [akeuben__dotfiles](configs/akeuben__dotfiles.md) | [akeuben/dotfiles](https://github.com/akeuben/dotfiles) | 48.0 | 5 | 8 | 6 | 5 | 5 | 2 | 2 | 5 | 5 | 2 | library units (1) |
| 57 | [lucasshiva](configs/lucasshiva.md) | [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig) | 48.0 | 4 | 7 | 6 | 6 | 6 | 5 | 2 | 3 | 5 | 2 | starter, library units (3) |
| 57 | [scoiatael__dotfiles](configs/scoiatael__dotfiles.md) | [scoiatael/dotfiles](https://github.com/scoiatael/dotfiles) | 48.0 | 2 | 7 | 4 | 7 | 8 | 2 | 4 | 6 | 7 | 2 | library units (3) |
| 57 | [vitalyavolyn__dotfiles](configs/vitalyavolyn__dotfiles.md) | [vitalyavolyn/dotfiles](https://github.com/vitalyavolyn/dotfiles) | 48.0 | 5 | 8 | 5 | 7 | 8 | 1 | 2 | 2 | 5 | 2 | library units (1) |
| 61 | [jkopano__nixiak](configs/jkopano__nixiak.md) | [jkopano/nixiak](https://github.com/jkopano/nixiak) | 47.5 | 5 | 6 | 4 | 7 | 5 | 5 | 5 | 2 | 5 | 2 | library units (1) |
| 61 | [oxce5__chimera](configs/oxce5__chimera.md) | [oxce5/chimera](https://github.com/oxce5/chimera) | 47.5 | 5 | 8 | 6 | 5 | 5 | 5 | 3 | 2 | 4 | 2 | library units (1) |
| 61 | [voidlily__dotfiles](configs/voidlily__dotfiles.md) | [voidlily/dotfiles](https://github.com/voidlily/dotfiles) | 47.5 | 4 | 8 | 5 | 5 | 6 | 2 | 5 | 5 | 5 | 2 | library units (1) |
| 64 | [Draculestein__nixos-config](configs/Draculestein__nixos-config.md) | [Draculestein/nixos-config](https://github.com/Draculestein/nixos-config) | 47.0 | 5 | 7 | 4 | 5 | 5 | 2 | 4 | 5 | 6 | 2 | library units (2) |
| 65 | [derangga__dotfiles](configs/derangga__dotfiles.md) | [derangga/dotfiles](https://github.com/derangga/dotfiles) | 46.5 | 5 | 5 | 4 | 5 | 5 | 7 | 5 | 2 | 5 | 2 | library units (1) |
| 65 | [recursivepaws__nix](configs/recursivepaws__nix.md) | [recursivepaws/nix](https://github.com/recursivepaws/nix) | 46.5 | 5 | 5 | 3 | 7 | 5 | 2 | 5 | 6 | 5 | 2 | library units (1) |
| 67 | [acrobertson__infra](configs/acrobertson__infra.md) | [acrobertson/infra](https://github.com/acrobertson/infra) | 46.0 | 3 | 5 | 4 | 5 | 9 | 5 | 6 | 5 | 3 | 2 | library units (1) |
| 67 | [aullisia__nixos-config](configs/aullisia__nixos-config.md) | [aullisia/nixos-config](https://github.com/aullisia/nixos-config) | 46.0 | 5 | 6 | 5 | 7 | 3 | 2 | 4 | 5 | 5 | 2 | library units (3) |
| 69 | [nifoc__dotfiles](configs/nifoc__dotfiles.md) | [nifoc/dotfiles](https://github.com/nifoc/dotfiles) | 45.5 | 4 | 7 | 4 | 4 | 7 | 1 | 5 | 7 | 4 | 2 | — |
| 70 | [elianiva__dotfiles](configs/elianiva__dotfiles.md) | [elianiva/dotfiles](https://github.com/elianiva/dotfiles) | 45.0 | 3 | 8 | 5 | 5 | 5 | 7 | 2 | 2 | 5 | 2 | library units (1) |
| 70 | [trash-panda-v91-beta__dots.factory](configs/trash-panda-v91-beta__dots.factory.md) | [trash-panda-v91-beta/dots.factory](https://github.com/trash-panda-v91-beta/dots.factory) | 45.0 | 3 | 7 | 6 | 4 | 5 | 6 | 4 | 4 | 4 | 2 | — |
| 72 | [KGB33__homelab](configs/KGB33__homelab.md) | [KGB33/homelab](https://github.com/KGB33/homelab) | 44.5 | 5 | 6 | 5 | 5 | 5 | 3 | 5 | 5 | 2 | 2 | library units (1) |
| 72 | [Shawn8901__nixos-configuration](configs/Shawn8901__nixos-configuration.md) | [Shawn8901/nixos-configuration](https://github.com/Shawn8901/nixos-configuration) | 44.5 | 5 | 7 | 5 | 5 | 4 | 1 | 5 | 5 | 4 | 2 | library units (1) |
| 72 | [eugencowie__dotfiles](configs/eugencowie__dotfiles.md) | [eugencowie/dotfiles](https://github.com/eugencowie/dotfiles) | 44.5 | 5 | 6 | 5 | 5 | 7 | 3 | 3 | 2 | 4 | 2 | library units (1) |
| 72 | [moxie0420__dotfiles](configs/moxie0420__dotfiles.md) | [moxie0420/dotfiles](https://github.com/moxie0420/dotfiles) | 44.5 | 6 | 8 | 3 | 5 | 4 | 2 | 3 | 2 | 6 | 2 | library units (1) |
| 76 | [quasi-coherent__nix-config](configs/quasi-coherent__nix-config.md) | [quasi-coherent/nix-config](https://github.com/quasi-coherent/nix-config) | 43.5 | 2 | 9 | 6 | 5 | 5 | 1 | 5 | 5 | 5 | 2 | — |
| 77 | [Likivik__spectacle](configs/Likivik__spectacle.md) | [Likivik/spectacle](https://github.com/Likivik/spectacle) | 43.0 | 2 | 6 | 3 | 5 | 5 | 5 | 8 | 6 | 4 | 2 | library units (1) |
| 77 | [quasigod-xyz-nixconfig](configs/quasigod-xyz-nixconfig.md) | [quasigod.xyz/nixconfig](https://tangled.org/quasigod.xyz/nixconfig) | 43.0 | 5 | 7 | 4 | 6 | 5 | 2 | 2 | 2 | 5 | 2 | library units (3) |
| 79 | [cfrenette__nixos-config](configs/cfrenette__nixos-config.md) | [cfrenette/nixos-config](https://github.com/cfrenette/nixos-config) | 42.5 | 5 | 6 | 4 | 5 | 5 | 1 | 3 | 5 | 4 | 2 | — |
| 79 | [phucisstupid__dotfiles](configs/phucisstupid__dotfiles.md) | [phucisstupid/dotfiles](https://github.com/phucisstupid/dotfiles) | 42.5 | 3 | 8 | 4 | 5 | 5 | 3 | 5 | 2 | 6 | 2 | library units (1) |
| 79 | [sm-f__nix](configs/sm-f__nix.md) | [sm-f/nix](https://github.com/sm-f/nix) | 42.5 | 4 | 7 | 4 | 5 | 5 | 3 | 5 | 4 | 3 | 2 | library units (1) |
| 82 | [EzT32__nixos](configs/EzT32__nixos.md) | [EzT32/nixos](https://github.com/EzT32/nixos) | 42.0 | 3 | 9 | 5 | 5 | 4 | 4 | 2 | 2 | 5 | 2 | — |
| 82 | [dotfiles](configs/dotfiles.md) | [cmetz/dotfiles](https://github.com/cmetz/dotfiles) | 42.0 | 5 | 6 | 4 | 5 | 5 | 2 | 2 | 4 | 4 | 2 | library units (3) |
| 82 | [oceangreendev](configs/oceangreendev.md) | [OceangreenDev/nix-config](https://github.com/OceangreenDev/nix-config) | 42.0 | 4 | 5 | 5 | 6 | 5 | 3 | 4 | 3 | 4 | 2 | library units (5) |
| 85 | [arichtman__nix](configs/arichtman__nix.md) | [arichtman/nix](https://github.com/arichtman/nix) | 41.5 | 5 | 6 | 4 | 6 | 4 | 3 | 5 | 2 | 3 | 2 | library units (2) |
| 86 | [aeshakhzod__blazingly-fast](configs/aeshakhzod__blazingly-fast.md) | [aeshakhzod/blazingly-fast](https://github.com/aeshakhzod/blazingly-fast) | 41.0 | 2 | 8 | 5 | 5 | 5 | 1 | 2 | 5 | 6 | 2 | library units (1) |
| 86 | [augustocdias__nixos](configs/augustocdias__nixos.md) | [augustocdias/nixos](https://github.com/augustocdias/nixos) | 41.0 | 2 | 6 | 2 | 5 | 7 | 4 | 2 | 5 | 6 | 2 | library units (1) |
| 88 | [fmway__infra](configs/fmway__infra.md) | [fmway/infra](https://github.com/fmway/infra) | 40.5 | 5 | 7 | 4 | 3 | 5 | 2 | 2 | 4 | 2 | 5 | — |
| 88 | [jmartindf__dendritic](configs/jmartindf__dendritic.md) | [jmartindf/dendritic](https://github.com/jmartindf/dendritic) | 40.5 | 5 | 5 | 4 | 5 | 5 | 2 | 3 | 5 | 2 | 2 | library units (1) |
| 90 | [thomasgoulet__nixnites](configs/thomasgoulet__nixnites.md) | [thomasgoulet/nixnites](https://github.com/thomasgoulet/nixnites) | 40.0 | 3 | 7 | 5 | 5 | 5 | 3 | 2 | 3 | 4 | 2 | — |
| 91 | [klchen0112__dotfiles](configs/klchen0112__dotfiles.md) | [klchen0112/dotfiles](https://github.com/klchen0112/dotfiles) | 39.5 | 2 | 7 | 2 | 5 | 5 | 2 | 3 | 5 | 7 | 2 | library units (2) |
| 92 | [drupol](configs/drupol.md) | [drupol/infra](https://github.com/drupol/infra) | 39.0 | 3 | 6 | 3 | 4 | 5 | 3 | 2 | 4 | 6 | 2 | library units (2) |
| 93 | [nixos.den](configs/nixos.den.md) | [espdesign/nixos.den](https://github.com/espdesign/nixos.den) | 38.5 | 3 | 6 | 3 | 5 | 5 | 4 | 5 | 3 | 3 | 2 | starter, library units (3) |
| 94 | [Steven-S1020__Nixos-Configuration](configs/Steven-S1020__Nixos-Configuration.md) | [Steven-S1020/Nixos-Configuration](https://github.com/Steven-S1020/Nixos-Configuration) | 36.0 | 3 | 7 | 2 | 5 | 5 | 3 | 2 | 2 | 4 | 2 | library units (1) |
| 94 | [vodfsh__nixos-config](configs/vodfsh__nixos-config.md) | [vodfsh/nixos-config](https://github.com/vodfsh/nixos-config) | 36.0 | 3 | 5 | 3 | 5 | 5 | 2 | 2 | 4 | 4 | 2 | — |
| 96 | [clemak27__homelab](configs/clemak27__homelab.md) | [clemak27/homelab](https://github.com/clemak27/homelab) | 34.5 | 2 | 5 | 2 | 6 | 5 | 2 | 5 | 5 | 2 | 2 | library units (1) |
| 97 | [DJ-Laser__nixos](configs/DJ-Laser__nixos.md) | [DJ-Laser/nixos](https://github.com/DJ-Laser/nixos) | 34.0 | 2 | 8 | 3 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 97 | [Erastos__nixos-dotfiles](configs/Erastos__nixos-dotfiles.md) | [Erastos/nixos-dotfiles](https://github.com/Erastos/nixos-dotfiles) | 34.0 | 2 | 7 | 4 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 97 | [talarys__den](configs/talarys__den.md) | [talarys/den](https://github.com/talarys/den) | 34.0 | 2 | 8 | 4 | 5 | 3 | 1 | 2 | 2 | 5 | 2 | library units (1) |
| 100 | [Heromercer__nixfiles](configs/Heromercer__nixfiles.md) | [Heromercer/nixfiles](https://github.com/Heromercer/nixfiles) | 33.0 | 2 | 5 | 2 | 5 | 4 | 1 | 2 | 5 | 5 | 2 | library units (3) |
| 101 | [pdarulewski__dotfiles](configs/pdarulewski__dotfiles.md) | [pdarulewski/dotfiles](https://github.com/pdarulewski/dotfiles) | 31.0 | 2 | 6 | 3 | 5 | 3 | 2 | 2 | 2 | 4 | 2 | library units (1) |
| 102 | [SyahrulBhudiF__dotfiles](configs/SyahrulBhudiF__dotfiles.md) | [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles) | 30.0 | 2 | 5 | 2 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 103 | [jcranney__nix-configuration](configs/jcranney__nix-configuration.md) | [jcranney/nix-configuration](https://github.com/jcranney/nix-configuration) | 25.0 | 2 | 4 | 2 | 2 | 5 | 2 | 2 | 2 | 2 | 2 | — |

## Partial vectors

A category that does not apply (for example, operations for a repo with no host or home) is left out. Partial totals are never rescaled to 100, so these configs are not ranked against the others.

| config | upstream | known sum | applicable maximum | missing | D | I | S | R | P | L | V | O | B | X | shortlists |
|---|---|---:|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| [FastTrackStudios__task](configs/FastTrackStudios__task.md) | [FastTrackStudios/task](https://github.com/FastTrackStudios/task) | 51.0 | 90 | O | 2 | 9 | 9 | 9 | 8 | 7 | 4 | – | 2 | 2 | library units (1) |
| [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md) | [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config) | 44.5 | 90 | O | 6 | 9 | 5 | 5 | 5 | 3 | 2 | – | 2 | 5 | showcase, library units (1) |

## Category distributions

All 108 scored configs, including those not listed. Each cell counts configs with that score; null means not applicable.

| category | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | null |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| D | 0 | 18 | 10 | 6 | 43 | 10 | 17 | 3 | 1 | 0 | 0 |
| I | 0 | 0 | 0 | 1 | 16 | 20 | 25 | 31 | 15 | 0 | 0 |
| S | 0 | 7 | 10 | 24 | 32 | 26 | 6 | 1 | 2 | 0 | 0 |
| R | 0 | 1 | 1 | 4 | 70 | 8 | 17 | 1 | 6 | 0 | 0 |
| P | 0 | 0 | 3 | 9 | 59 | 7 | 17 | 8 | 5 | 0 | 0 |
| L | 10 | 33 | 14 | 7 | 13 | 4 | 12 | 8 | 7 | 0 | 0 |
| V | 0 | 31 | 13 | 10 | 31 | 10 | 2 | 4 | 7 | 0 | 0 |
| O | 0 | 21 | 7 | 8 | 37 | 15 | 14 | 3 | 1 | 0 | 2 |
| B | 0 | 10 | 14 | 17 | 32 | 19 | 10 | 6 | 0 | 0 | 0 |
| X | 0 | 96 | 0 | 0 | 9 | 0 | 1 | 1 | 1 | 0 | 0 |


## Showcase

Configs worth showing the den community for a mechanism they demonstrate well.

- [sini__nix-config](configs/sini__nix-config.md)
- [auscyber__dotfiles](configs/auscyber__dotfiles.md)
- [megadots](configs/megadots.md)
- [Aor-Li__Infra](configs/Aor-Li__Infra.md)
- [repparw__nix](configs/repparw__nix.md)
- [r17x__universe](configs/r17x__universe.md)
- [soriPhoono__homelab](configs/soriPhoono__homelab.md)
- [Kykero__Nazunix](configs/Kykero__Nazunix.md)
- [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md)
- [mrbandler__nix](configs/mrbandler__nix.md)
- [lorenzorapetti__nix](configs/lorenzorapetti__nix.md)
- [Le0-dot__config.nix](configs/Le0-dot__config.nix.md)
- [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md)
- [neonvoidx__nix](configs/neonvoidx__nix.md)
- [nixpedition](configs/nixpedition.md)
- [sk4rd__mikos-den](configs/sk4rd__mikos-den.md)
- [Gwenodai__nixos](configs/Gwenodai__nixos.md)
- [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md)
- [greysilly7__nixos-config](configs/greysilly7__nixos-config.md)
- [aveeryy__kadachi](configs/aveeryy__kadachi.md)
- [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md)
- [ivokun__kebun](configs/ivokun__kebun.md)
- [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md)
- [anders130__dotfiles](configs/anders130__dotfiles.md)
- [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md)
- [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md)
- [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md)

## Starter

Configs a newcomer can learn from: a short path from entry to output, few prerequisites, clear host and user variation.

- [Occhima__nix-conf](configs/Occhima__nix-conf.md)
- [amatos__magnanix](configs/amatos__magnanix.md)
- [Kykero__Nazunix](configs/Kykero__Nazunix.md)
- [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md)
- [motheki__nix](configs/motheki__nix.md)
- [lucasshiva](configs/lucasshiva.md)
- [nixos.den](configs/nixos.den.md)

## Library units

Self-contained aspects graded A (drop-in) or B (light parametrizing) in each review's §4, nominated for a community aspect library.

- [sini__nix-config](configs/sini__nix-config.md): age-secrets quirk+collector (A/B), nix-builders pipe chain (B), host-aspect settings mirror recipe (B), classes/home-platform.nix (B), tmux (A), starship (A), zellij (A), aerospace (A), nvf (B)
- [Occhima__nix-conf](configs/Occhima__nix-conf.md): calibre
- [auscyber__dotfiles](configs/auscyber__dotfiles.md): file-local, bluetooth-a2dp-pipewire, llama-cpp-darwin
- [megadots](configs/megadots.md): persist quirk + impermanence consumer (A), LAN firewall quirk (B), syncthing mesh pipe (B), terminal quirk (B)
- [Aor-Li__Infra](configs/Aor-Li__Infra.md): aspect-settings, workspace-links
- [closure-labs__foundation](configs/closure-labs__foundation.md): espanso-user-service
- [amatos__magnanix](configs/amatos__magnanix.md): repo-dir
- [icebluerabbit__nixos](configs/icebluerabbit__nixos.md): homelab overlay discovery
- [repparw__nix](configs/repparw__nix.md): desktop.bitwarden
- [r17x__universe](configs/r17x__universe.md): runtime-manifest
- [closure-labs__mish](configs/closure-labs__mish.md): mish USB coordinator mode
- [soriPhoono__homelab](configs/soriPhoono__homelab.md): sops wiring, Media appliance
- [Kykero__Nazunix](configs/Kykero__Nazunix.md): desktop-bluetooth
- [nazarewk-iac__nix-configs](configs/nazarewk-iac__nix-configs.md): service-syncthing, den-library-surface
- [adda-nixos-config](configs/adda-nixos-config.md): aspect-settings, shell aliases/abbreviations classes, editor quirk collectors, private-overlay stub
- [closure-labs__maestro](configs/closure-labs__maestro.md): xo-service-suite, management CIDR guard
- [lorenzorapetti__nix](configs/lorenzorapetti__nix.md): Managed Flatpak/Flathub
- [adanoelle__fern](configs/adanoelle__fern.md): secrets-guard
- [henriquekirchheck__nixos-flake](configs/henriquekirchheck__nixos-flake.md): services.sshd
- [nixpedition](configs/nixpedition.md): traefik dynamic-file quirk (A), terranix global/local routing (B), nixos-containers options layer (B), clan instantiate/intoAttr override (B)
- [hmajid2301__nixicle](configs/hmajid2301__nixicle.md): vpn, tuios-home-module
- [sk4rd__mikos-den](configs/sk4rd__mikos-den.md): openssh
- [sonntag__nix](configs/sonntag__nix.md): nixible playbook bridge, Kanata Darwin integration
- [DylanRJohnston__nixos](configs/DylanRJohnston__nixos.md): fstrim
- [Gwenodai__nixos](configs/Gwenodai__nixos.md): activeAspects schema
- [Keyruu__shinyflakes](configs/Keyruu__shinyflakes.md): collect-service-facts
- [greysilly7__nixos-config](configs/greysilly7__nixos-config.md): Disko class bridge
- [andreshungbz__nixconfig](configs/andreshungbz__nixconfig.md): bluetooth
- [jadestar1864__nix-config](configs/jadestar1864__nix-config.md): Firefox privacy/search preset
- [andrewix](configs/andrewix.md): wsl variant, mkHost monitors
- [aveeryy__kadachi](configs/aveeryy__kadachi.md): podman, autofirma-firefox, amd-cpu
- [byte-sized-emi__nix-config](configs/byte-sized-emi__nix-config.md): fleet-http-services
- [raphaelladinig__dotfiles](configs/raphaelladinig__dotfiles.md): app-preferences
- [theutz](configs/theutz.md): deploy, homebrew quirks
- [anders130__dotfiles](configs/anders130__dotfiles.md): audio
- [motheki__nix](configs/motheki__nix.md): linux-builder
- [AnonymousRand__nix_config](configs/AnonymousRand__nix_config.md): nix-ld aggregation
- [eldios__dotfiles](configs/eldios__dotfiles.md): AMD GPU integration
- [muhammadtalha-quant__denix](configs/muhammadtalha-quant__denix.md): disko.ext4-simple
- [redxtech__nixfiles](configs/redxtech__nixfiles.md): host-settings
- [Sharparam__nix-config](configs/Sharparam__nix-config.md): direnv-instant
- [loystonpais__lunar](configs/loystonpais__lunar.md): audio
- [RafaelMuijsert__nixos-config](configs/RafaelMuijsert__nixos-config.md): stylix
- [Shochraos__nixfiles](configs/Shochraos__nixfiles.md): fingerprint
- [SuNNjek__nixos-config](configs/SuNNjek__nixos-config.md): add-user-to-group
- [danielgafni__nixos](configs/danielgafni__nixos.md): Colima Darwin service
- [jasperro__dotfiles](configs/jasperro__dotfiles.md): encrypted BTRFS filesystem
- [rhedgeco__nix-config](configs/rhedgeco__nix-config.md): schema-primary
- [KGB33__.dotfiles](configs/KGB33__.dotfiles.md): stable
- [Spebby__NixOS](configs/Spebby__NixOS.md): ideapad-bluetooth, plex-streaming-inhibitor
- [akeuben__dotfiles](configs/akeuben__dotfiles.md): upower
- [lucasshiva](configs/lucasshiva.md): host-guards policy (A), kitty shell option (B), fonts feature with readOnly font options (B)
- [scoiatael__dotfiles](configs/scoiatael__dotfiles.md): openssh-host-keys, mpv-uosc, comma
- [vitalyavolyn__dotfiles](configs/vitalyavolyn__dotfiles.md): fail2ban
- [jkopano__nixiak](configs/jkopano__nixiak.md): OpenSSH client/agent
- [oxce5__chimera](configs/oxce5__chimera.md): privileged-user
- [voidlily__dotfiles](configs/voidlily__dotfiles.md): direnv
- [Draculestein__nixos-config](configs/Draculestein__nixos-config.md): incus-preseed-reconcile, direnv-shell-integration
- [derangga__dotfiles](configs/derangga__dotfiles.md): OmniWM writable preset
- [recursivepaws__nix](configs/recursivepaws__nix.md): Native VST discovery
- [acrobertson__infra](configs/acrobertson__infra.md): 1password-shell-integration
- [aullisia__nixos-config](configs/aullisia__nixos-config.md): ghostty, helix, direnv
- [elianiva__dotfiles](configs/elianiva__dotfiles.md): gpg
- [KGB33__homelab](configs/KGB33__homelab.md): podman
- [Shawn8901__nixos-configuration](configs/Shawn8901__nixos-configuration.md): desktop.audio
- [eugencowie__dotfiles](configs/eugencowie__dotfiles.md): vcs.git
- [moxie0420__dotfiles](configs/moxie0420__dotfiles.md): ripgrep
- [Likivik__spectacle](configs/Likivik__spectacle.md): direnv
- [quasigod-xyz-nixconfig](configs/quasigod-xyz-nixconfig.md): displays schema (A), privileged-user battery (A), catppuccin parametric theming (B)
- [phucisstupid__dotfiles](configs/phucisstupid__dotfiles.md): cli.fd
- [sm-f__nix](configs/sm-f__nix.md): work
- [dotfiles](configs/dotfiles.md): gitClass forward, proxmox-lxc template, polybar quirk
- [oceangreendev](configs/oceangreendev.md): define-user-adv battery (A), mount-cifs factory (B), accounts.google/exchange/apple mkEmail/mkCalendar/mkContact (B), impermanence perhost/perhome forwards (B), broken/unsupported batteries (B)
- [arichtman__nix](configs/arichtman__nix.md): nix-maintenance, loki-local
- [aeshakhzod__blazingly-fast](configs/aeshakhzod__blazingly-fast.md): hibernation
- [augustocdias__nixos](configs/augustocdias__nixos.md): bat
- [jmartindf__dendritic](configs/jmartindf__dendritic.md): Fish shell handoff
- [klchen0112__dotfiles](configs/klchen0112__dotfiles.md): fish, btrfs-scrub
- [drupol](configs/drupol.md): facter, nix-trusted-user
- [nixos.den](configs/nixos.den.md): auto-upgrade (B), hardened-server (B), nvidia (A)
- [Steven-S1020__Nixos-Configuration](configs/Steven-S1020__Nixos-Configuration.md): system/audio
- [clemak27__homelab](configs/clemak27__homelab.md): starship-preset
- [DJ-Laser__nixos](configs/DJ-Laser__nixos.md): ttypicker-yazi portal
- [Erastos__nixos-dotfiles](configs/Erastos__nixos-dotfiles.md): audio
- [talarys__den](configs/talarys__den.md): ghostty
- [Heromercer__nixfiles](configs/Heromercer__nixfiles.md): yt-audio, audio, starship
- [pdarulewski__dotfiles](configs/pdarulewski__dotfiles.md): fonts
- [SyahrulBhudiF__dotfiles](configs/SyahrulBhudiF__dotfiles.md): ghostty-nixgl
- [FastTrackStudios__task](configs/FastTrackStudios__task.md): task-server module
- [JoonasKajava__nvf-config](configs/JoonasKajava__nvf-config.md): nvf-integration

# Ranking

This page ranks the published configs by their totals, and shows the ten category scores behind each total. It is for readers who want to compare configs, or to find configs that are strong in one category. For the terms on this page, see the [glossary](GLOSSARY.md).

Each category is scored 1-10. The total is out of 100 and uses 2D + I + S + R + P + L + O + B + ½V + ½X. Shortlists are independent judgments, not awards. The anchors for each score are in [method/RUBRIC.md](method/RUBRIC.md). The README shows [how to read a scorecard](README.md#how-to-read-a-scorecard).

5 scored configs are counted but not listed, because their source is no longer public. They are part of the category distributions below and of the census totals.

`sini/nix-config` is the audit maintainer's own configuration and the rubric's reference anchor. It was scored under the same rubric as every other config.

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
| 1 | [sini/nix-config](configs/sini/nix-config.md) | [sini/nix-config](https://github.com/sini/nix-config) | 71.5 | 7 | 9 | 5 | 6 | 7 | 6 | 6 | 9 | 8 | 9 | showcase, library units (9) |
| 2 | [Occhima/nix-conf](configs/Occhima/nix-conf.md) | [Occhima/nix-conf](https://github.com/Occhima/nix-conf) | 69.0 | 6 | 9 | 6 | 7 | 8 | 8 | 9 | 5 | 7 | 5 | starter, library units (1) |
| 3 | [auscyber/dotfiles](configs/auscyber/dotfiles.md) | [auscyber/dotfiles](https://github.com/auscyber/dotfiles) | 68.5 | 7 | 8 | 6 | 7 | 7 | 6 | 7 | 8 | 5 | 8 | showcase, library units (3) |
| 4 | [tomwrw/megadots](configs/tomwrw/megadots.md) | [tomwrw/megadots](https://github.com/tomwrw/megadots) | 67.5 | 8 | 9 | 6 | 7 | 6 | 9 | 5 | 6 | 5 | 2 | showcase, library units (4) |
| 5 | [Aor-Li/Infra](configs/Aor-Li/Infra.md) | [Aor-Li/Infra](https://github.com/Aor-Li/Infra) | 66.5 | 7 | 8 | 5 | 9 | 8 | 8 | 3 | 5 | 7 | 2 | showcase, library units (2) |
| 6 | [closure-labs/foundation](configs/closure-labs/foundation.md) | [closure-labs/foundation](https://github.com/closure-labs/foundation) | 65.5 | 5 | 9 | 7 | 9 | 9 | 9 | 9 | 5 | 2 | 2 | library units (1) |
| 7 | [amatos/magnanix](configs/amatos/magnanix.md) | [amatos/magnanix](https://github.com/amatos/magnanix) | 64.0 | 5 | 8 | 6 | 5 | 9 | 9 | 6 | 6 | 7 | 2 | starter, library units (1) |
| 8 | [icebluerabbit/nixos](configs/icebluerabbit/nixos.md) | [icebluerabbit/nixos](https://github.com/icebluerabbit/nixos) | 63.0 | 5 | 8 | 5 | 7 | 7 | 7 | 5 | 7 | 7 | 5 | library units (1) |
| 8 | [repparw/nix](configs/repparw/nix.md) | [repparw/nix](https://github.com/repparw/nix) | 63.0 | 8 | 7 | 5 | 5 | 5 | 8 | 8 | 8 | 4 | 2 | showcase, library units (1) |
| 10 | [r17x/universe](configs/r17x/universe.md) | [r17x/universe](https://github.com/r17x/universe) | 62.5 | 7 | 9 | 7 | 5 | 5 | 7 | 8 | 6 | 3 | 5 | showcase, library units (1) |
| 11 | [closure-labs/mish](configs/closure-labs/mish.md) | [closure-labs/mish](https://github.com/closure-labs/mish) | 61.5 | 2 | 9 | 9 | 9 | 9 | 9 | 9 | 5 | 2 | 2 | library units (1) |
| 12 | [soriPhoono/homelab](configs/soriPhoono/homelab.md) | [soriPhoono/homelab](https://github.com/soriPhoono/homelab) | 61.0 | 5 | 7 | 6 | 7 | 7 | 7 | 6 | 7 | 6 | 2 | showcase, library units (2) |
| 13 | [Kykero/Nazunix](configs/Kykero/Nazunix.md) | [Kykero/Nazunix](https://github.com/Kykero/Nazunix) | 60.5 | 6 | 8 | 7 | 5 | 5 | 9 | 7 | 5 | 5 | 2 | showcase, starter, library units (1) |
| 14 | [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md) | [nazarewk-iac/nix-configs](https://github.com/nazarewk-iac/nix-configs) | 60.0 | 2 | 9 | 6 | 8 | 9 | 8 | 9 | 2 | 7 | 5 | showcase, library units (2) |
| 15 | [Adda/nixos-config](configs/Adda/nixos-config.md) | [Adda/nixos-config](https://codeberg.org/Adda/nixos-config) | 59.5 | 7 | 7 | 6 | 6 | 5 | 8 | 3 | 3 | 8 | 2 | library units (4) |
| 15 | [closure-labs/maestro](configs/closure-labs/maestro.md) | [closure-labs/maestro](https://github.com/closure-labs/maestro) | 59.5 | 4 | 6 | 7 | 9 | 7 | 9 | 9 | 6 | 2 | 2 | library units (2) |
| 15 | [mrbandler/nix](configs/mrbandler/nix.md) | [mrbandler/nix](https://github.com/mrbandler/nix) | 59.5 | 5 | 7 | 6 | 5 | 7 | 7 | 5 | 6 | 8 | 2 | showcase |
| 18 | [lorenzorapetti/nix](configs/lorenzorapetti/nix.md) | [lorenzorapetti/nix](https://github.com/lorenzorapetti/nix) | 59.0 | 7 | 6 | 4 | 7 | 5 | 7 | 6 | 7 | 5 | 2 | showcase, library units (1) |
| 19 | [adanoelle/fern](configs/adanoelle/fern.md) | [adanoelle/fern](https://github.com/adanoelle/fern) | 58.5 | 5 | 8 | 5 | 7 | 5 | 8 | 3 | 5 | 8 | 2 | library units (1) |
| 20 | [Le0-dot/config.nix](configs/Le0-dot/config.nix.md) | [Le0-dot/config.nix](https://github.com/Le0-dot/config.nix) | 57.5 | 6 | 7 | 6 | 5 | 7 | 5 | 6 | 7 | 3 | 5 | showcase |
| 20 | [henriquekirchheck/nixos-flake](configs/henriquekirchheck/nixos-flake.md) | [henriquekirchheck/nixos-flake](https://github.com/henriquekirchheck/nixos-flake) | 57.5 | 7 | 9 | 7 | 5 | 5 | 2 | 5 | 5 | 7 | 2 | showcase, library units (1) |
| 20 | [neonvoidx/nix](configs/neonvoidx/nix.md) | [neonvoidx/nix](https://github.com/neonvoidx/nix) | 57.5 | 5 | 9 | 5 | 5 | 5 | 8 | 5 | 6 | 6 | 2 | showcase |
| 20 | [zakuciael/nixpedition](configs/zakuciael/nixpedition.md) | [zakuciael/nixpedition](https://github.com/zakuciael/nixpedition) | 57.5 | 7 | 8 | 6 | 5 | 5 | 2 | 6 | 8 | 3 | 7 | showcase, library units (4) |
| 24 | [hmajid2301/nixicle](configs/hmajid2301/nixicle.md) | [hmajid2301/nixicle](https://github.com/hmajid2301/nixicle) | 57.0 | 6 | 6 | 4 | 9 | 6 | 2 | 6 | 7 | 7 | 2 | library units (2) |
| 24 | [sk4rd/mikos-den](configs/sk4rd/mikos-den.md) | [sk4rd/mikos-den](https://github.com/sk4rd/mikos-den) | 57.0 | 7 | 9 | 6 | 5 | 5 | 7 | 4 | 5 | 3 | 2 | showcase, library units (1) |
| 24 | [sonntag/nix](configs/sonntag/nix.md) | [sonntag/nix](https://github.com/sonntag/nix) | 57.0 | 5 | 6 | 5 | 5 | 7 | 8 | 4 | 7 | 6 | 2 | library units (2) |
| 27 | [DylanRJohnston/nixos](configs/DylanRJohnston/nixos.md) | [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos) | 56.5 | 5 | 8 | 5 | 5 | 8 | 5 | 9 | 5 | 5 | 2 | library units (1) |
| 28 | [Gwenodai/nixos](configs/Gwenodai/nixos.md) | [Gwenodai/nixos](https://github.com/Gwenodai/nixos) | 56.0 | 7 | 7 | 6 | 7 | 5 | 2 | 2 | 7 | 6 | 2 | showcase, library units (1) |
| 29 | [Keyruu/shinyflakes](configs/Keyruu/shinyflakes.md) | [Keyruu/shinyflakes](https://github.com/Keyruu/shinyflakes) | 55.5 | 7 | 8 | 4 | 5 | 5 | 3 | 5 | 5 | 8 | 2 | showcase, library units (1) |
| 29 | [greysilly7/nixos-config](configs/greysilly7/nixos-config.md) | [greysilly7/nixos-config](https://github.com/greysilly7/nixos-config) | 55.5 | 7 | 5 | 4 | 7 | 7 | 2 | 5 | 7 | 6 | 2 | showcase, library units (1) |
| 31 | [andreshungbz/nixconfig](configs/andreshungbz/nixconfig.md) | [andreshungbz/nixconfig](https://github.com/andreshungbz/nixconfig) | 54.5 | 5 | 8 | 5 | 5 | 8 | 5 | 3 | 5 | 6 | 2 | starter, library units (1) |
| 31 | [jadestar1864/nix-config](configs/jadestar1864/nix-config.md) | [jadestar1864/nix-config](https://github.com/jadestar1864/nix-config) | 54.5 | 7 | 5 | 5 | 5 | 6 | 5 | 5 | 5 | 6 | 2 | library units (1) |
| 33 | [hoanhxlyn/andrewix](configs/hoanhxlyn/andrewix.md) | [hoanhxlyn/andrewix](https://github.com/hoanhxlyn/andrewix) | 54.0 | 5 | 8 | 6 | 5 | 6 | 7 | 2 | 5 | 5 | 2 | library units (2) |
| 33 | [aveeryy/kadachi](configs/aveeryy/kadachi.md) | [aveeryy/kadachi](https://github.com/aveeryy/kadachi) | 54.0 | 8 | 8 | 5 | 5 | 4 | 2 | 2 | 7 | 5 | 2 | showcase, library units (3) |
| 33 | [byte-sized-emi/nix-config](configs/byte-sized-emi/nix-config.md) | [byte-sized-emi/nix-config](https://github.com/byte-sized-emi/nix-config) | 54.0 | 7 | 8 | 4 | 7 | 5 | 3 | 2 | 7 | 4 | 2 | showcase, library units (1) |
| 33 | [ivokun/kebun](configs/ivokun/kebun.md) | [ivokun/kebun](https://github.com/ivokun/kebun) | 54.0 | 5 | 7 | 6 | 5 | 5 | 9 | 6 | 3 | 5 | 2 | showcase |
| 37 | [raphaelladinig/dotfiles](configs/raphaelladinig/dotfiles.md) | [raphaelladinig/dotfiles](https://github.com/raphaelladinig/dotfiles) | 53.0 | 5 | 8 | 8 | 6 | 5 | 2 | 8 | 6 | 3 | 2 | showcase, library units (1) |
| 37 | [~theutz/flake](configs/theutz/flake.md) | [~theutz/flake](https://git.sr.ht/~theutz/flake) | 53.0 | 7 | 7 | 4 | 5 | 6 | 1 | 2 | 7 | 7 | 2 | library units (2) |
| 39 | [anders130/dotfiles](configs/anders130/dotfiles.md) | [anders130/dotfiles](https://github.com/anders130/dotfiles) | 52.5 | 5 | 6 | 5 | 7 | 5 | 4 | 5 | 7 | 5 | 2 | showcase, library units (1) |
| 39 | [motheki/nix](configs/motheki/nix.md) | [motheki/nix](https://github.com/motheki/nix) | 52.5 | 5 | 8 | 6 | 5 | 5 | 5 | 5 | 5 | 5 | 2 | starter, library units (1) |
| 41 | [AnonymousRand/nix_config](configs/AnonymousRand/nix_config.md) | [AnonymousRand/nix_config](https://github.com/AnonymousRand/nix_config) | 52.0 | 7 | 8 | 6 | 5 | 5 | 7 | 2 | 2 | 3 | 2 | showcase, library units (1) |
| 41 | [nolvyn/nixos](configs/nolvyn/nixos.md) | [nolvyn/nixos](https://github.com/nolvyn/nixos) | 52.0 | 5 | 8 | 6 | 5 | 7 | 2 | 6 | 5 | 5 | 2 | — |
| 43 | [eldios/dotfiles](configs/eldios/dotfiles.md) | [eldios/dotfiles](https://github.com/eldios/dotfiles) | 51.5 | 5 | 6 | 4 | 5 | 5 | 7 | 5 | 6 | 5 | 2 | library units (1) |
| 43 | [muhammadtalha-quant/denix](configs/muhammadtalha-quant/denix.md) | [muhammadtalha-quant/denix](https://github.com/muhammadtalha-quant/denix) | 51.5 | 5 | 8 | 5 | 5 | 5 | 6 | 5 | 5 | 4 | 2 | library units (1) |
| 43 | [redxtech/nixfiles](configs/redxtech/nixfiles.md) | [redxtech/nixfiles](https://github.com/redxtech/nixfiles) | 51.5 | 5 | 7 | 5 | 5 | 5 | 5 | 5 | 6 | 5 | 2 | library units (1) |
| 46 | [Sharparam/nix-config](configs/Sharparam/nix-config.md) | [Sharparam/nix-config](https://github.com/Sharparam/nix-config) | 51.0 | 6 | 5 | 3 | 5 | 7 | 2 | 4 | 6 | 8 | 2 | library units (1) |
| 46 | [loystonpais/lunar](configs/loystonpais/lunar.md) | [loystonpais/lunar](https://github.com/loystonpais/lunar) | 51.0 | 5 | 7 | 3 | 5 | 5 | 5 | 3 | 6 | 6 | 5 | library units (1) |
| 48 | [RafaelMuijsert/nixos-config](configs/RafaelMuijsert/nixos-config.md) | [RafaelMuijsert/nixos-config](https://github.com/RafaelMuijsert/nixos-config) | 50.5 | 6 | 8 | 5 | 5 | 4 | 4 | 3 | 5 | 5 | 2 | showcase, library units (1) |
| 48 | [Shochraos/nixfiles](configs/Shochraos/nixfiles.md) | [Shochraos/nixfiles](https://github.com/Shochraos/nixfiles) | 50.5 | 5 | 7 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 2 | library units (1) |
| 48 | [SuNNjek/nixos-config](configs/SuNNjek/nixos-config.md) | [SuNNjek/nixos-config](https://github.com/SuNNjek/nixos-config) | 50.5 | 6 | 9 | 5 | 5 | 5 | 2 | 5 | 5 | 4 | 2 | library units (1) |
| 48 | [danielgafni/nixos](configs/danielgafni/nixos.md) | [danielgafni/nixos](https://github.com/danielgafni/nixos) | 50.5 | 5 | 5 | 4 | 7 | 7 | 4 | 5 | 5 | 5 | 2 | library units (1) |
| 48 | [jasperro/dotfiles](configs/jasperro/dotfiles.md) | [jasperro/dotfiles](https://github.com/jasperro/dotfiles) | 50.5 | 5 | 5 | 5 | 5 | 7 | 4 | 3 | 6 | 6 | 2 | library units (1) |
| 48 | [rhedgeco/nix-config](configs/rhedgeco/nix-config.md) | [rhedgeco/nix-config](https://github.com/rhedgeco/nix-config) | 50.5 | 6 | 8 | 6 | 5 | 5 | 2 | 5 | 4 | 5 | 2 | library units (1) |
| 54 | [KGB33/.dotfiles](configs/KGB33/.dotfiles.md) | [KGB33/.dotfiles](https://github.com/KGB33/.dotfiles) | 48.5 | 2 | 8 | 5 | 5 | 8 | 2 | 9 | 5 | 6 | 2 | library units (1) |
| 54 | [Spebby/NixOS](configs/Spebby/NixOS.md) | [Spebby/NixOS](https://github.com/Spebby/NixOS) | 48.5 | 5 | 5 | 7 | 5 | 4 | 3 | 5 | 5 | 6 | 2 | library units (2) |
| 54 | [mio-19/config-public](configs/mio-19/config-public.md) | [mio-19/config-public](https://github.com/mio-19/config-public) | 48.5 | 5 | 5 | 6 | 5 | 7 | 3 | 4 | 2 | 6 | 5 | — |
| 57 | [akeuben/dotfiles](configs/akeuben/dotfiles.md) | [akeuben/dotfiles](https://github.com/akeuben/dotfiles) | 48.0 | 5 | 8 | 6 | 5 | 5 | 2 | 2 | 5 | 5 | 2 | library units (1) |
| 57 | [lucasshiva/nixconfig](configs/lucasshiva/nixconfig.md) | [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig) | 48.0 | 4 | 7 | 6 | 6 | 6 | 5 | 2 | 3 | 5 | 2 | starter, library units (3) |
| 57 | [scoiatael/dotfiles](configs/scoiatael/dotfiles.md) | [scoiatael/dotfiles](https://github.com/scoiatael/dotfiles) | 48.0 | 2 | 7 | 4 | 7 | 8 | 2 | 4 | 6 | 7 | 2 | library units (3) |
| 57 | [vitalyavolyn/dotfiles](configs/vitalyavolyn/dotfiles.md) | [vitalyavolyn/dotfiles](https://github.com/vitalyavolyn/dotfiles) | 48.0 | 5 | 8 | 5 | 7 | 8 | 1 | 2 | 2 | 5 | 2 | library units (1) |
| 61 | [jkopano/nixiak](configs/jkopano/nixiak.md) | [jkopano/nixiak](https://github.com/jkopano/nixiak) | 47.5 | 5 | 6 | 4 | 7 | 5 | 5 | 5 | 2 | 5 | 2 | library units (1) |
| 61 | [oxce5/chimera](configs/oxce5/chimera.md) | [oxce5/chimera](https://github.com/oxce5/chimera) | 47.5 | 5 | 8 | 6 | 5 | 5 | 5 | 3 | 2 | 4 | 2 | library units (1) |
| 61 | [voidlily/dotfiles](configs/voidlily/dotfiles.md) | [voidlily/dotfiles](https://github.com/voidlily/dotfiles) | 47.5 | 4 | 8 | 5 | 5 | 6 | 2 | 5 | 5 | 5 | 2 | library units (1) |
| 64 | [Draculestein/nixos-config](configs/Draculestein/nixos-config.md) | [Draculestein/nixos-config](https://github.com/Draculestein/nixos-config) | 47.0 | 5 | 7 | 4 | 5 | 5 | 2 | 4 | 5 | 6 | 2 | library units (2) |
| 65 | [derangga/dotfiles](configs/derangga/dotfiles.md) | [derangga/dotfiles](https://github.com/derangga/dotfiles) | 46.5 | 5 | 5 | 4 | 5 | 5 | 7 | 5 | 2 | 5 | 2 | library units (1) |
| 65 | [recursivepaws/nix](configs/recursivepaws/nix.md) | [recursivepaws/nix](https://github.com/recursivepaws/nix) | 46.5 | 5 | 5 | 3 | 7 | 5 | 2 | 5 | 6 | 5 | 2 | library units (1) |
| 67 | [acrobertson/infra](configs/acrobertson/infra.md) | [acrobertson/infra](https://github.com/acrobertson/infra) | 46.0 | 3 | 5 | 4 | 5 | 9 | 5 | 6 | 5 | 3 | 2 | library units (1) |
| 67 | [aullisia/nixos-config](configs/aullisia/nixos-config.md) | [aullisia/nixos-config](https://github.com/aullisia/nixos-config) | 46.0 | 5 | 6 | 5 | 7 | 3 | 2 | 4 | 5 | 5 | 2 | library units (3) |
| 69 | [nifoc/dotfiles](configs/nifoc/dotfiles.md) | [nifoc/dotfiles](https://github.com/nifoc/dotfiles) | 45.5 | 4 | 7 | 4 | 4 | 7 | 1 | 5 | 7 | 4 | 2 | — |
| 70 | [elianiva/dotfiles](configs/elianiva/dotfiles.md) | [elianiva/dotfiles](https://github.com/elianiva/dotfiles) | 45.0 | 3 | 8 | 5 | 5 | 5 | 7 | 2 | 2 | 5 | 2 | library units (1) |
| 70 | [trash-panda-v91-beta/dots.factory](configs/trash-panda-v91-beta/dots.factory.md) | [trash-panda-v91-beta/dots.factory](https://github.com/trash-panda-v91-beta/dots.factory) | 45.0 | 3 | 7 | 6 | 4 | 5 | 6 | 4 | 4 | 4 | 2 | — |
| 72 | [KGB33/homelab](configs/KGB33/homelab.md) | [KGB33/homelab](https://github.com/KGB33/homelab) | 44.5 | 5 | 6 | 5 | 5 | 5 | 3 | 5 | 5 | 2 | 2 | library units (1) |
| 72 | [Shawn8901/nixos-configuration](configs/Shawn8901/nixos-configuration.md) | [Shawn8901/nixos-configuration](https://github.com/Shawn8901/nixos-configuration) | 44.5 | 5 | 7 | 5 | 5 | 4 | 1 | 5 | 5 | 4 | 2 | library units (1) |
| 72 | [eugencowie/dotfiles](configs/eugencowie/dotfiles.md) | [eugencowie/dotfiles](https://github.com/eugencowie/dotfiles) | 44.5 | 5 | 6 | 5 | 5 | 7 | 3 | 3 | 2 | 4 | 2 | library units (1) |
| 72 | [moxie0420/dotfiles](configs/moxie0420/dotfiles.md) | [moxie0420/dotfiles](https://github.com/moxie0420/dotfiles) | 44.5 | 6 | 8 | 3 | 5 | 4 | 2 | 3 | 2 | 6 | 2 | library units (1) |
| 76 | [quasi-coherent/nix-config](configs/quasi-coherent/nix-config.md) | [quasi-coherent/nix-config](https://github.com/quasi-coherent/nix-config) | 43.5 | 2 | 9 | 6 | 5 | 5 | 1 | 5 | 5 | 5 | 2 | — |
| 77 | [Likivik/spectacle](configs/Likivik/spectacle.md) | [Likivik/spectacle](https://github.com/Likivik/spectacle) | 43.0 | 2 | 6 | 3 | 5 | 5 | 5 | 8 | 6 | 4 | 2 | library units (1) |
| 77 | [quasigod.xyz/nixconfig](configs/quasigod.xyz/nixconfig.md) | [quasigod.xyz/nixconfig](https://tangled.org/quasigod.xyz/nixconfig) | 43.0 | 5 | 7 | 4 | 6 | 5 | 2 | 2 | 2 | 5 | 2 | library units (3) |
| 79 | [cfrenette/nixos-config](configs/cfrenette/nixos-config.md) | [cfrenette/nixos-config](https://github.com/cfrenette/nixos-config) | 42.5 | 5 | 6 | 4 | 5 | 5 | 1 | 3 | 5 | 4 | 2 | — |
| 79 | [phucisstupid/dotfiles](configs/phucisstupid/dotfiles.md) | [phucisstupid/dotfiles](https://github.com/phucisstupid/dotfiles) | 42.5 | 3 | 8 | 4 | 5 | 5 | 3 | 5 | 2 | 6 | 2 | library units (1) |
| 79 | [sm-f/nix](configs/sm-f/nix.md) | [sm-f/nix](https://github.com/sm-f/nix) | 42.5 | 4 | 7 | 4 | 5 | 5 | 3 | 5 | 4 | 3 | 2 | library units (1) |
| 82 | [EzT32/nixos](configs/EzT32/nixos.md) | [EzT32/nixos](https://github.com/EzT32/nixos) | 42.0 | 3 | 9 | 5 | 5 | 4 | 4 | 2 | 2 | 5 | 2 | — |
| 83 | [arichtman/nix](configs/arichtman/nix.md) | [arichtman/nix](https://github.com/arichtman/nix) | 41.5 | 5 | 6 | 4 | 6 | 4 | 3 | 5 | 2 | 3 | 2 | library units (2) |
| 84 | [aeshakhzod/blazingly-fast](configs/aeshakhzod/blazingly-fast.md) | [aeshakhzod/blazingly-fast](https://github.com/aeshakhzod/blazingly-fast) | 41.0 | 2 | 8 | 5 | 5 | 5 | 1 | 2 | 5 | 6 | 2 | library units (1) |
| 84 | [augustocdias/nixos](configs/augustocdias/nixos.md) | [augustocdias/nixos](https://github.com/augustocdias/nixos) | 41.0 | 2 | 6 | 2 | 5 | 7 | 4 | 2 | 5 | 6 | 2 | library units (1) |
| 86 | [fmway/infra](configs/fmway/infra.md) | [fmway/infra](https://github.com/fmway/infra) | 40.5 | 5 | 7 | 4 | 3 | 5 | 2 | 2 | 4 | 2 | 5 | — |
| 86 | [jmartindf/dendritic](configs/jmartindf/dendritic.md) | [jmartindf/dendritic](https://github.com/jmartindf/dendritic) | 40.5 | 5 | 5 | 4 | 5 | 5 | 2 | 3 | 5 | 2 | 2 | library units (1) |
| 88 | [thomasgoulet/nixnites](configs/thomasgoulet/nixnites.md) | [thomasgoulet/nixnites](https://github.com/thomasgoulet/nixnites) | 40.0 | 3 | 7 | 5 | 5 | 5 | 3 | 2 | 3 | 4 | 2 | — |
| 89 | [klchen0112/dotfiles](configs/klchen0112/dotfiles.md) | [klchen0112/dotfiles](https://github.com/klchen0112/dotfiles) | 39.5 | 2 | 7 | 2 | 5 | 5 | 2 | 3 | 5 | 7 | 2 | library units (2) |
| 90 | [drupol/infra](configs/drupol/infra.md) | [drupol/infra](https://github.com/drupol/infra) | 39.0 | 3 | 6 | 3 | 4 | 5 | 3 | 2 | 4 | 6 | 2 | library units (2) |
| 91 | [espdesign/nixos.den](configs/espdesign/nixos.den.md) | [espdesign/nixos.den](https://github.com/espdesign/nixos.den) | 38.5 | 3 | 6 | 3 | 5 | 5 | 4 | 5 | 3 | 3 | 2 | starter, library units (3) |
| 92 | [Steven-S1020/Nixos-Configuration](configs/Steven-S1020/Nixos-Configuration.md) | [Steven-S1020/Nixos-Configuration](https://github.com/Steven-S1020/Nixos-Configuration) | 36.0 | 3 | 7 | 2 | 5 | 5 | 3 | 2 | 2 | 4 | 2 | library units (1) |
| 92 | [vodfsh/nixos-config](configs/vodfsh/nixos-config.md) | [vodfsh/nixos-config](https://github.com/vodfsh/nixos-config) | 36.0 | 3 | 5 | 3 | 5 | 5 | 2 | 2 | 4 | 4 | 2 | — |
| 94 | [clemak27/homelab](configs/clemak27/homelab.md) | [clemak27/homelab](https://github.com/clemak27/homelab) | 34.5 | 2 | 5 | 2 | 6 | 5 | 2 | 5 | 5 | 2 | 2 | library units (1) |
| 95 | [DJ-Laser/nixos](configs/DJ-Laser/nixos.md) | [DJ-Laser/nixos](https://github.com/DJ-Laser/nixos) | 34.0 | 2 | 8 | 3 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 95 | [Erastos/nixos-dotfiles](configs/Erastos/nixos-dotfiles.md) | [Erastos/nixos-dotfiles](https://github.com/Erastos/nixos-dotfiles) | 34.0 | 2 | 7 | 4 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 95 | [talarys/den](configs/talarys/den.md) | [talarys/den](https://github.com/talarys/den) | 34.0 | 2 | 8 | 4 | 5 | 3 | 1 | 2 | 2 | 5 | 2 | library units (1) |
| 98 | [Heromercer/nixfiles](configs/Heromercer/nixfiles.md) | [Heromercer/nixfiles](https://github.com/Heromercer/nixfiles) | 33.0 | 2 | 5 | 2 | 5 | 4 | 1 | 2 | 5 | 5 | 2 | library units (3) |
| 99 | [pdarulewski/dotfiles](configs/pdarulewski/dotfiles.md) | [pdarulewski/dotfiles](https://github.com/pdarulewski/dotfiles) | 31.0 | 2 | 6 | 3 | 5 | 3 | 2 | 2 | 2 | 4 | 2 | library units (1) |
| 100 | [SyahrulBhudiF/dotfiles](configs/SyahrulBhudiF/dotfiles.md) | [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles) | 30.0 | 2 | 5 | 2 | 5 | 5 | 2 | 2 | 2 | 3 | 2 | library units (1) |
| 101 | [jcranney/nix-configuration](configs/jcranney/nix-configuration.md) | [jcranney/nix-configuration](https://github.com/jcranney/nix-configuration) | 25.0 | 2 | 4 | 2 | 2 | 5 | 2 | 2 | 2 | 2 | 2 | — |

## Partial vectors

A category that does not apply (for example, operations for a repo with no host or home) is left out. Partial totals are never rescaled to 100, so these configs are not ranked against the others.

| config | upstream | known sum | applicable maximum | missing | D | I | S | R | P | L | V | O | B | X | shortlists |
|---|---|---:|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| [FastTrackStudios/task](configs/FastTrackStudios/task.md) | [FastTrackStudios/task](https://github.com/FastTrackStudios/task) | 51.0 | 90 | O | 2 | 9 | 9 | 9 | 8 | 7 | 4 | – | 2 | 2 | library units (1) |
| [JoonasKajava/nvf-config](configs/JoonasKajava/nvf-config.md) | [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config) | 44.5 | 90 | O | 6 | 9 | 5 | 5 | 5 | 3 | 2 | – | 2 | 5 | showcase, library units (1) |

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

- [sini/nix-config](configs/sini/nix-config.md)
- [auscyber/dotfiles](configs/auscyber/dotfiles.md)
- [tomwrw/megadots](configs/tomwrw/megadots.md)
- [Aor-Li/Infra](configs/Aor-Li/Infra.md)
- [repparw/nix](configs/repparw/nix.md)
- [r17x/universe](configs/r17x/universe.md)
- [soriPhoono/homelab](configs/soriPhoono/homelab.md)
- [Kykero/Nazunix](configs/Kykero/Nazunix.md)
- [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md)
- [mrbandler/nix](configs/mrbandler/nix.md)
- [lorenzorapetti/nix](configs/lorenzorapetti/nix.md)
- [Le0-dot/config.nix](configs/Le0-dot/config.nix.md)
- [henriquekirchheck/nixos-flake](configs/henriquekirchheck/nixos-flake.md)
- [neonvoidx/nix](configs/neonvoidx/nix.md)
- [zakuciael/nixpedition](configs/zakuciael/nixpedition.md)
- [sk4rd/mikos-den](configs/sk4rd/mikos-den.md)
- [Gwenodai/nixos](configs/Gwenodai/nixos.md)
- [Keyruu/shinyflakes](configs/Keyruu/shinyflakes.md)
- [greysilly7/nixos-config](configs/greysilly7/nixos-config.md)
- [aveeryy/kadachi](configs/aveeryy/kadachi.md)
- [byte-sized-emi/nix-config](configs/byte-sized-emi/nix-config.md)
- [ivokun/kebun](configs/ivokun/kebun.md)
- [raphaelladinig/dotfiles](configs/raphaelladinig/dotfiles.md)
- [anders130/dotfiles](configs/anders130/dotfiles.md)
- [AnonymousRand/nix_config](configs/AnonymousRand/nix_config.md)
- [RafaelMuijsert/nixos-config](configs/RafaelMuijsert/nixos-config.md)
- [JoonasKajava/nvf-config](configs/JoonasKajava/nvf-config.md)

## Starter

Configs a newcomer can learn from: a short path from entry to output, few prerequisites, clear host and user variation.

- [Occhima/nix-conf](configs/Occhima/nix-conf.md)
- [amatos/magnanix](configs/amatos/magnanix.md)
- [Kykero/Nazunix](configs/Kykero/Nazunix.md)
- [andreshungbz/nixconfig](configs/andreshungbz/nixconfig.md)
- [motheki/nix](configs/motheki/nix.md)
- [lucasshiva/nixconfig](configs/lucasshiva/nixconfig.md)
- [espdesign/nixos.den](configs/espdesign/nixos.den.md)

## Library units

Self-contained aspects graded A (drop-in) or B (light parametrizing) in each review's §4, nominated for a community aspect library.

- [sini/nix-config](configs/sini/nix-config.md): age-secrets quirk+collector (A/B), nix-builders pipe chain (B), host-aspect settings mirror recipe (B), classes/home-platform.nix (B), tmux (A), starship (A), zellij (A), aerospace (A), nvf (B)
- [Occhima/nix-conf](configs/Occhima/nix-conf.md): calibre
- [auscyber/dotfiles](configs/auscyber/dotfiles.md): file-local, bluetooth-a2dp-pipewire, llama-cpp-darwin
- [tomwrw/megadots](configs/tomwrw/megadots.md): persist quirk + impermanence consumer (A), LAN firewall quirk (B), syncthing mesh pipe (B), terminal quirk (B)
- [Aor-Li/Infra](configs/Aor-Li/Infra.md): aspect-settings, workspace-links
- [closure-labs/foundation](configs/closure-labs/foundation.md): espanso-user-service
- [amatos/magnanix](configs/amatos/magnanix.md): repo-dir
- [icebluerabbit/nixos](configs/icebluerabbit/nixos.md): homelab overlay discovery
- [repparw/nix](configs/repparw/nix.md): desktop.bitwarden
- [r17x/universe](configs/r17x/universe.md): runtime-manifest
- [closure-labs/mish](configs/closure-labs/mish.md): mish USB coordinator mode
- [soriPhoono/homelab](configs/soriPhoono/homelab.md): sops wiring, Media appliance
- [Kykero/Nazunix](configs/Kykero/Nazunix.md): desktop-bluetooth
- [nazarewk-iac/nix-configs](configs/nazarewk-iac/nix-configs.md): service-syncthing, den-library-surface
- [Adda/nixos-config](configs/Adda/nixos-config.md): aspect-settings, shell aliases/abbreviations classes, editor quirk collectors, private-overlay stub
- [closure-labs/maestro](configs/closure-labs/maestro.md): xo-service-suite, management CIDR guard
- [lorenzorapetti/nix](configs/lorenzorapetti/nix.md): Managed Flatpak/Flathub
- [adanoelle/fern](configs/adanoelle/fern.md): secrets-guard
- [henriquekirchheck/nixos-flake](configs/henriquekirchheck/nixos-flake.md): services.sshd
- [zakuciael/nixpedition](configs/zakuciael/nixpedition.md): traefik dynamic-file quirk (A), terranix global/local routing (B), nixos-containers options layer (B), clan instantiate/intoAttr override (B)
- [hmajid2301/nixicle](configs/hmajid2301/nixicle.md): vpn, tuios-home-module
- [sk4rd/mikos-den](configs/sk4rd/mikos-den.md): openssh
- [sonntag/nix](configs/sonntag/nix.md): nixible playbook bridge, Kanata Darwin integration
- [DylanRJohnston/nixos](configs/DylanRJohnston/nixos.md): fstrim
- [Gwenodai/nixos](configs/Gwenodai/nixos.md): activeAspects schema
- [Keyruu/shinyflakes](configs/Keyruu/shinyflakes.md): collect-service-facts
- [greysilly7/nixos-config](configs/greysilly7/nixos-config.md): Disko class bridge
- [andreshungbz/nixconfig](configs/andreshungbz/nixconfig.md): bluetooth
- [jadestar1864/nix-config](configs/jadestar1864/nix-config.md): Firefox privacy/search preset
- [hoanhxlyn/andrewix](configs/hoanhxlyn/andrewix.md): wsl variant, mkHost monitors
- [aveeryy/kadachi](configs/aveeryy/kadachi.md): podman, autofirma-firefox, amd-cpu
- [byte-sized-emi/nix-config](configs/byte-sized-emi/nix-config.md): fleet-http-services
- [raphaelladinig/dotfiles](configs/raphaelladinig/dotfiles.md): app-preferences
- [~theutz/flake](configs/theutz/flake.md): deploy, homebrew quirks
- [anders130/dotfiles](configs/anders130/dotfiles.md): audio
- [motheki/nix](configs/motheki/nix.md): linux-builder
- [AnonymousRand/nix_config](configs/AnonymousRand/nix_config.md): nix-ld aggregation
- [eldios/dotfiles](configs/eldios/dotfiles.md): AMD GPU integration
- [muhammadtalha-quant/denix](configs/muhammadtalha-quant/denix.md): disko.ext4-simple
- [redxtech/nixfiles](configs/redxtech/nixfiles.md): host-settings
- [Sharparam/nix-config](configs/Sharparam/nix-config.md): direnv-instant
- [loystonpais/lunar](configs/loystonpais/lunar.md): audio
- [RafaelMuijsert/nixos-config](configs/RafaelMuijsert/nixos-config.md): stylix
- [Shochraos/nixfiles](configs/Shochraos/nixfiles.md): fingerprint
- [SuNNjek/nixos-config](configs/SuNNjek/nixos-config.md): add-user-to-group
- [danielgafni/nixos](configs/danielgafni/nixos.md): Colima Darwin service
- [jasperro/dotfiles](configs/jasperro/dotfiles.md): encrypted BTRFS filesystem
- [rhedgeco/nix-config](configs/rhedgeco/nix-config.md): schema-primary
- [KGB33/.dotfiles](configs/KGB33/.dotfiles.md): stable
- [Spebby/NixOS](configs/Spebby/NixOS.md): ideapad-bluetooth, plex-streaming-inhibitor
- [akeuben/dotfiles](configs/akeuben/dotfiles.md): upower
- [lucasshiva/nixconfig](configs/lucasshiva/nixconfig.md): host-guards policy (A), kitty shell option (B), fonts feature with readOnly font options (B)
- [scoiatael/dotfiles](configs/scoiatael/dotfiles.md): openssh-host-keys, mpv-uosc, comma
- [vitalyavolyn/dotfiles](configs/vitalyavolyn/dotfiles.md): fail2ban
- [jkopano/nixiak](configs/jkopano/nixiak.md): OpenSSH client/agent
- [oxce5/chimera](configs/oxce5/chimera.md): privileged-user
- [voidlily/dotfiles](configs/voidlily/dotfiles.md): direnv
- [Draculestein/nixos-config](configs/Draculestein/nixos-config.md): incus-preseed-reconcile, direnv-shell-integration
- [derangga/dotfiles](configs/derangga/dotfiles.md): OmniWM writable preset
- [recursivepaws/nix](configs/recursivepaws/nix.md): Native VST discovery
- [acrobertson/infra](configs/acrobertson/infra.md): 1password-shell-integration
- [aullisia/nixos-config](configs/aullisia/nixos-config.md): ghostty, helix, direnv
- [elianiva/dotfiles](configs/elianiva/dotfiles.md): gpg
- [KGB33/homelab](configs/KGB33/homelab.md): podman
- [Shawn8901/nixos-configuration](configs/Shawn8901/nixos-configuration.md): desktop.audio
- [eugencowie/dotfiles](configs/eugencowie/dotfiles.md): vcs.git
- [moxie0420/dotfiles](configs/moxie0420/dotfiles.md): ripgrep
- [Likivik/spectacle](configs/Likivik/spectacle.md): direnv
- [quasigod.xyz/nixconfig](configs/quasigod.xyz/nixconfig.md): displays schema (A), privileged-user battery (A), catppuccin parametric theming (B)
- [phucisstupid/dotfiles](configs/phucisstupid/dotfiles.md): cli.fd
- [sm-f/nix](configs/sm-f/nix.md): work
- [arichtman/nix](configs/arichtman/nix.md): nix-maintenance, loki-local
- [aeshakhzod/blazingly-fast](configs/aeshakhzod/blazingly-fast.md): hibernation
- [augustocdias/nixos](configs/augustocdias/nixos.md): bat
- [jmartindf/dendritic](configs/jmartindf/dendritic.md): Fish shell handoff
- [klchen0112/dotfiles](configs/klchen0112/dotfiles.md): fish, btrfs-scrub
- [drupol/infra](configs/drupol/infra.md): facter, nix-trusted-user
- [espdesign/nixos.den](configs/espdesign/nixos.den.md): auto-upgrade (B), hardened-server (B), nvidia (A)
- [Steven-S1020/Nixos-Configuration](configs/Steven-S1020/Nixos-Configuration.md): system/audio
- [clemak27/homelab](configs/clemak27/homelab.md): starship-preset
- [DJ-Laser/nixos](configs/DJ-Laser/nixos.md): ttypicker-yazi portal
- [Erastos/nixos-dotfiles](configs/Erastos/nixos-dotfiles.md): audio
- [talarys/den](configs/talarys/den.md): ghostty
- [Heromercer/nixfiles](configs/Heromercer/nixfiles.md): yt-audio, audio, starship
- [pdarulewski/dotfiles](configs/pdarulewski/dotfiles.md): fonts
- [SyahrulBhudiF/dotfiles](configs/SyahrulBhudiF/dotfiles.md): ghostty-nixgl
- [FastTrackStudios/task](configs/FastTrackStudios/task.md): task-server module
- [JoonasKajava/nvf-config](configs/JoonasKajava/nvf-config.md): nvf-integration

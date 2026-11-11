# recursivepaws__nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/recursivepaws__nix.md)

- Upstream: [recursivepaws/nix](https://github.com/recursivepaws/nix)
- Reviewed revision: [`c4317eb95fad`](https://github.com/recursivepaws/nix/commit/c4317eb95fad0ffcb7b5ce2056e83b82f046920a)
- Author: recursivepaws
- Score: **46.5 / 100**, rank 65 of 103 ranked configs. D 5 · I 5 · S 3 · R 7 · P 5 · L 2 · V 5 · O 6 · B 5 · X 2. Shortlists: library units (1).
- Summary: Scoped host/context facts and independent audio presets coexist with global personal identity, app-level fleet dependencies, thin docs and a concrete sync failure-reporting flaw.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

## Contents

- [1. Shape](#1-shape)
- [2. Common patterns](#2-common-patterns)
- [3. Novel patterns](#3-novel-patterns)
- [4. Library candidates](#4-library-candidates)
- [5. den friction](#5-den-friction)
- [6. Docs and complexity](#6-docs-and-complexity)
- [6a. Defects and scoring notes](#6a-defects-and-scoring-notes)
- [7. Template notes](#7-template-notes)
- [8. Scorecard](#8-scorecard)

## 1. Shape

Feature aspects and global defaults are separate; schema-level user integration enables HM and mutual providers (`modules/default/default.nix:11`, `modules/default/default.nix:14`). Host inventory is explicit (`modules/hosts/hosts.nix:12`).

## 2. Common patterns

- mutual-provider in the user schema (`modules/default/default.nix:14`).
- define-user is selected per user (`modules/users/vera.nix:5`).

## 3. Novel patterns

A schema helper defines package-function projection into OS/HM overlays (`modules/default/packages.nix:12`, `modules/default/packages.nix:31`). No live aspect-level package-function producer was verified in the inspected source; this definition earns no routing credit.

## 4. Library candidates

- packageClass · `modules/default/packages.nix:4` · builds overlays from aspect package functions · inputs: Den, nixpkgs lib · parameterization: fn args aspect-chain and package function arguments · C; needs documented chaining/merge semantics before reuse.

- **Native VST discovery** · `modules/aspects/audio/native-vst-plugins.nix:3`: supplies native plugin packages, discovery environment and profile-directory links (`modules/aspects/audio/native-vst-plugins.nix:13`, `modules/aspects/audio/native-vst-plugins.nix:50`, `modules/aspects/audio/native-vst-plugins.nix:62`). Inputs: Den and Nixpkgs; ordinary Linux Home Manager config. Parameterization: native home/profile paths, no author identity. Reuse **A** for the whole native VST envelope; no independent consumer example is supplied.

## 5. den friction

The package extension relies on lib.head aspect-chain and manually filters function arguments, an integration surface requiring version scrutiny (`modules/default/packages.nix:12`, `modules/default/packages.nix:25`).

## 6. Docs and complexity

Docs 2: README explains personal/work separation briefly (`README.md:3`, `README.md:5`). Complexity 4: custom package projection atop multi-host inventory (`modules/default/packages.nix:37`, `modules/hosts/hosts.nix:12`).

## 6a. Defects and scoring notes

- **S moderate:** global Git/signing identity is Vera-specific but also applies to the work user (`modules/default/git.nix:56`, `modules/users/work.nix:3`); another person must patch shared settings.
- **O moderate:** iPod music/podcast sync pipelines end with `|| true` and are followed by completion messages (`scripts/ipod-sync.sh:197`, `scripts/ipod-sync.sh:199`, `scripts/ipod-sync.sh:220`, `scripts/ipod-sync.sh:222`), so failed transfers can appear successful; static impact, not runtime-tested.
- **L minor:** README provides no explanation of the package-function contract (`README.md:3`, `modules/default/packages.nix:15`).
Right-biased package merging is not separately charged without a demonstrated collision failure (`modules/default/packages.nix:27`).

## 7. Template notes

Useful advanced extension example, but the package protocol needs more teaching before becoming a beginner template (`modules/default/packages.nix:15`).

## 8. Scorecard

### D (5, high)
Score: 5. Confidence: high. Scope: entity/context derivation. Pros: host.desktop controls desktop selection and 1Password policy derives from host users (`modules/hosts/hosts.nix:6`, `modules/default/default.nix:21`, `modules/default/default.nix:178`); user profilePicture feeds OS AccountsService and HM shell (`modules/users/users.nix:12`, `modules/aspects/noctalia-greeter.nix:12`, `modules/aspects/noctalia.nix:172`). Cons: these are schema facts through context, capped at 5; host-to-user providers deliver native configuration, not a traced policy/quirk facts channel (`modules/hosts/amanita.nix:70`, `modules/hosts/ampulex.nix:54`). Package projection is build plumbing, earning no additional D (`modules/default/packages.nix:31`).

### I (5, high)
Score: 5. Confidence: high. Scope: feature isolation. Pros: work and personal includes are explicit, and cross-app additions are guarded on actual aspect membership (`modules/users/vera.nix:11`, `modules/users/work.nix:8`, `modules/aspects/artcraft.nix:54`). Cons: shared desktop selection is a broad capability bundle, and headless HM still receives generic GUI packages (`modules/default/default.nix:21`, `modules/default/default.nix:245`); this is scope coupling, not an invented correctness defect. Anchor 5.

### S (3, medium)
Score: 3. Confidence: medium. Scope: shared defaults and features, excluding correct host hardware. Pros: desktop/headless variation has an explicit boolean and separate host facts (`modules/hosts/hosts.nix:6`, `modules/hosts/hosts.nix:24`, `modules/hosts/barkstation.nix:58`). Cons: every user inherits Vera Git/signing identity (`modules/default/git.nix:56`, `modules/users/work.nix:3`); cache and region are global (`modules/default/cachix.nix:3`, `modules/default/default.nix:68`); audio helper fixes UID/card (`modules/aspects/audio-fix.nix:10`, `modules/aspects/audio-fix.nix:11`). Shared sync fixes four peer IDs/names and a special storage host (`modules/aspects/syncthing.nix:23`, `modules/aspects/syncthing.nix:41`), GTK/iPod assume NAS endpoint/login/share (`modules/default/gtk.nix:74`, `scripts/ipod-sync.sh:16`, `scripts/ipod-sync.sh:18`), and cloud wallpaper/tailnet/project roots remain personal (`modules/aspects/noctalia.nix:34`, `modules/aspects/hightouch/kubernetes.nix:19`, `modules/aspects/claude/claude.nix:261`, `modules/default/rebuild.nix:15`). Twenty grouped choices (at least 40 raw sites: identity, cache, region, audio UID/card, peer IDs and default names, NAS names/address/share, bucket account, tailnet and checkout roots) cap coverage at 5. Contract 3 controls S.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":5,"distinct_leaks":20,"raw_leaks":40}}
```

### R (7, high)
Score: 7. Confidence: high. Scope: best independent app unit. Pros: native VST discovery owns its plugin packages, environment search paths and profile-directory links, using only ordinary HM config (`modules/aspects/audio/native-vst-plugins.nix:13`, `modules/aspects/audio/native-vst-plugins.nix:50`, `modules/aspects/audio/native-vst-plugins.nix:62`). AMD integration likewise owns its ROCm closure (`modules/aspects/amd.nix:24`). Cons: no independent consumer example is supplied, and the packageClass candidate still needs protocol explanation (`README.md:3`, `modules/default/packages.nix:15`). Interpolation 7 for substantial A units without the consumer example required by 9.

### P (5, high)
Score: 5. Confidence: high. Scope: supported Linux host/home boundaries. Pros: actual desktop and headless consumers select different capabilities (`modules/hosts/hosts.nix:12`, `modules/hosts/hosts.nix:24`); application wrappers clearly target Linux FHS/Wine (`modules/aspects/audio/bitwig-studio.nix:106`, `modules/aspects/audio/rekordbox.nix:134`). Cons / limit: plugin discovery and services assume a NixOS system path, not a demonstrated non-NixOS home (`modules/aspects/audio/plugins/yabridge.nix:21`, `modules/default/network.nix:5`). Anchor 5 for honest narrow support.

### L (2, high)
Score: 2. Confidence: high. Scope: explanation. Pros: README states Den usage and personal/work separation (`README.md:3`, `README.md:5`). Cons: those two purpose statements give no entry-to-feature or new-host instructions; the custom package-function protocol lives only in source (`modules/default/packages.nix:15`). Anchor 2.

### V (5, high)
Score: 5. Confidence: high. Scope: declared CI. Pros: workflow evaluates three named native host outputs and checks generated flake-file consistency (`.github/workflows/flake-check.yml:21`, `.github/workflows/flake-check.yml:28`, `.github/workflows/flake-check.yml:36`). Cons / limit: the headless barkstation inventory entry is not in that matrix (`modules/hosts/hosts.nix:24`, `.github/workflows/flake-check.yml:28`), and CI evaluation is not a runtime audio/desktop test (`.github/workflows/flake-check.yml:36`). Anchor 5; no passing execution observed.

### O (6, high)
Score: 6. Confidence: high. Scope: selected operational contributions. Pros: user-aware OAuth secrets are emitted per aspect (`modules/aspects/claude/google-workspace.nix:42`), and Cachix queues actual build outputs with bounded failure handling and a credentialed daemon (`modules/default/cachix.nix:29`, `modules/default/cachix.nix:39`, `modules/default/cachix.nix:52`). Cons: iPod sync explicitly suppresses transfer-pipeline failure and then reports completion (`scripts/ipod-sync.sh:197`, `scripts/ipod-sync.sh:199`, `scripts/ipod-sync.sh:220`, `scripts/ipod-sync.sh:222`). Interpolation 6: secrets plus an output-driven cache concern, with a concrete lifecycle failure-reporting defect and no inventory-derived deployment layer (`modules/default/rebuild.nix:9`).

### B (5, medium)
Score: 5. Confidence: medium. Scope: complete visible native app references. Pros: 13 units below include audio libraries, actual conversion/activation workflows, hardware integration and managed desktop presets (`modules/aspects/audio/native-vst-plugins.nix:50`, `modules/aspects/beets.nix:149`, `modules/aspects/audio/plugins/yabridge.nix:75`). Cons: personal Git/MPD/Syncthing are excluded (`modules/default/git.nix:56`, `modules/aspects/music.nix:129`, `modules/aspects/syncthing.nix:41`); Noctalia needs fleet profilePicture and Niri-specific branches (`modules/aspects/noctalia.nix:92`, `modules/aspects/noctalia.nix:172`), while terminal/DaVinci/Varnam name an outside fleet aspect (`modules/aspects/terminal.nix:13`, `modules/aspects/davinci.nix:41`, `modules/aspects/varnam.nix:148`). Neovim explicitly needs compiler/build tools supplied outside its envelope (`modules/default/default.nix:112`, `modules/default/neovim.nix:177`); MCP leaves rely on imports owned by Claude (`modules/aspects/claude/claude.nix:197`, `modules/aspects/claude/hevy.nix:19`). Packaging-only theme-editor/overlay leaves are not extra units (`modules/aspects/audio/bitwig-theme-editor.nix:63`, `modules/aspects/audio/custom-wine.nix:76`). Census 4.5→3; references 13→7; B=5.
```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"AMD ROCm integration","evidence":"modules/aspects/amd.nix:6"},{"name":"Bitwig FHS desktop integration","evidence":"modules/aspects/audio/bitwig-studio.nix:106"},{"name":"DJ library export integration","evidence":"modules/aspects/audio/dj.nix:100"},{"name":"Native VST discovery","evidence":"modules/aspects/audio/native-vst-plugins.nix:50"},{"name":"Yabridge activation","evidence":"modules/aspects/audio/plugins/yabridge.nix:11"},{"name":"Beets conversion/library preset","evidence":"modules/aspects/beets.nix:44"},{"name":"Chrome WebGPU profile","evidence":"modules/aspects/browser.nix:14"},{"name":"Keyd/QMK keyboard integration","evidence":"modules/aspects/keyboard.nix:36"},{"name":"Spicetify preset","evidence":"modules/aspects/spotify.nix:15"},{"name":"Obsidian vault/plugin preset","evidence":"modules/aspects/obsidian.nix:17"},{"name":"Instant Direnv integration","evidence":"modules/default/direnv.nix:8"},{"name":"Ollama GPU/model integration","evidence":"modules/aspects/ollama.nix:5"},{"name":"Steam/Heroic gaming integration","evidence":"modules/aspects/gaming.nix:4"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: non-host targets. Pros / limit: Kubernetes code generates a client kubeconfig inside Home Manager, not a Den class driving cluster manifests (`modules/aspects/hightouch/kubernetes.nix:71`, `modules/aspects/hightouch/kubernetes.nix:123`). Cons: package projection remains ordinary native OS/home overlays (`modules/default/packages.nix:31`); neither mechanism earns extra X. Baseline 2.

Total: **46.5/100**. Shortlists: showcase no; library_units Native VST discovery; starter no. Native VST discovery is a useful independent library reference; the broad personal defaults and two-sentence README do not support a starter or showcase shortlist.

Overall pros:
- Explicit desktop/headless boundary (`modules/hosts/hosts.nix:6`, `modules/hosts/hosts.nix:24`).
- Native VST paths and filesystem discovery are packaged together (`modules/aspects/audio/native-vst-plugins.nix:13`, `modules/aspects/audio/native-vst-plugins.nix:62`).
- User-aware OAuth secret ownership (`modules/aspects/claude/google-workspace.nix:42`).
- Representative host-evaluation CI is declared (`.github/workflows/flake-check.yml:28`, `.github/workflows/flake-check.yml:36`).

Overall cons / limits:
- Shared Git identity also reaches the work profile (`modules/default/git.nix:56`, `modules/users/work.nix:3`).
- iPod transfer failures are suppressed before success messages (`scripts/ipod-sync.sh:197`, `scripts/ipod-sync.sh:199`).
- Shared audio routing fixes UID/card (`modules/aspects/audio-fix.nix:10`, `modules/aspects/audio-fix.nix:11`).
- README provides purpose but no adoption workflow (`README.md:3`, `README.md:5`).

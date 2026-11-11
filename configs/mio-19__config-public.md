# mio-19__config-public

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/mio-19__config-public.md)

- Upstream: [mio-19/config-public](https://github.com/mio-19/config-public)
- Reviewed revision: [`a269164a1be6`](https://github.com/mio-19/config-public/commit/a269164a1be6a90eecb533f54d362e2d2bdef629)
- Author: mio-19
- Score: **48.5 / 100**, rank 54 of 103 ranked configs. D 5 · I 5 · S 6 · R 5 · P 7 · L 3 · V 4 · O 2 · B 6 · X 5. Shortlists: —.
- Summary: Direct schema guard D5; mixed migration I5; validated visible options S6/four adaptations; five complete units; explicit platform branches P7; debug docs L3; nonblocking builds V4; no derived ops O2; BSD instantiation X5.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

## Contents

- [1. Shape.](#1-shape)
- [2. Common patterns.](#2-common-patterns)
- [3. Novel patterns.](#3-novel-patterns)
- [4. Library candidates.](#4-library-candidates)
- [5. den friction.](#5-den-friction)
- [6. Docs and complexity.](#6-docs-and-complexity)
- [6a. Defects and scoring notes.](#6a-defects-and-scoring-notes)
- [7. Template notes.](#7-template-notes)
- [8. Scorecard.](#8-scorecard)

## 1. Shape.

Top-level flake combines separate NixOS, Darwin and BSD subflakes (`flake.nix:8`, `flake.nix:23`). Den is introduced incrementally through shared evalModules and a class-resolving adapter around a large existing module tree (`den-config.nix:1`, `aspect.nix:20`, `modules/hosts.nix:2`).


## 2. Common patterns.

- os-class: basic combines OS-wide registry and HM policy (`modules/basic.nix:6`).
- host-aspects: den entities declare per-user HM classes while other machines remain conventional outputs (`modules/hosts.nix:2`).
- parametric aspect (fn args): aspect factory resolves the selected aspect by system class (`aspect.nix:12`).


## 3. Novel patterns.

The adapter resolves OS and platform classes, then injects any NixOS HM branch into sharedModules (`aspect.nix:24`, `aspect.nix:32`, `aspect.nix:37`). This offers a gradual migration seam rather than requiring immediate entity conversion.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Custom aspect.resolveImports/resolve plumbing duplicates framework boundary work and treats HM extraction differently on Darwin (`aspect.nix:25`). Publication intentionally removes details and supplies stubs (`README.md:15`, `modules/users.nix:1`).


## 6. Docs and complexity.

Docs 2: README explains public/debug limitations, not a den onboarding flow (`README.md:7`, `README.md:13`); factory comments document integration (`aspect.nix:7`). Complexity 5: three subflakes and a broad incremental migration with a custom class adapter (`flake.nix:8`, `modules/hosts.nix:2`, `aspect.nix:20`).


## 6a. Defects and scoring notes.

- S · minor: four shared adaptation groups enumerated in S remain visible (`modules/basic.nix:39`, `modules/basic.nix:40`, `modules/waydroid.nix:61`, `modules/persistent.nix:31`).
- V · moderate: sampled build workflow marks every host build continue-on-error, preventing failed builds from failing CI (`.github/workflows/build.yml:38`, `.github/workflows/build.yml:40`, `.github/workflows/build.yml:44`).
Publication stubs and custom migration adapter are disclosed scope/maintenance limits, not inherent defects.

## 7. Template notes.

Real den usage, but unsuitable first template: public stubs and mixed conventional/den entrypoints require migration context (`README.md:15`, `modules/hosts.nix:2`).

## 8. Scorecard.

### D
Scope: actual Den entity guards and conventional registry derivation. Pros: user flag plus host class select shell contribution and current username; registry derives from inputs (`modules/nixos-zsh-user.nix:40`, `modules/nixos-zsh-user.nix:16`, `modules/basic.nix:29`). Cons: manual aspect resolve/OS extraction is module adaptation, not shared fact transport (`aspect.nix:24`, `aspect.nix:32`). Literal5 direct schema/context derivation cap. Score **5**; confidence **medium**.

### I
Scope: incremental migration and feature boundaries. Pros: named aspects and explicit host/user records give migration seams (`modules/hosts.nix:2`, `modules/users.nix:3`, `aspect.nix:12`). Cons: shared common/desktop-full remain large mixed owners and many features depend on global include scope (`modules/common.nix:235`, `modules/desktop-full.nix:1`, `modules/printing.nix:13`). Literal5 useful boundaries amid substantial legacy coupling; no size-only penalty. Score **5**; confidence **medium**.

### S
Scope: visible typed domain and shared constants. Pros: options expose platform-dependent switches with cross-option assertions; Harmonia owns typed service config (`modules/options.nix:26`, `modules/options.nix:263`, `modules/harmonia.nix:28`). Contract6 beyond5 meaningful validated interfaces, below7 global include dependency (`modules/options.nix:13`). Cons: four visible adaptation groups: two personal cache URL/key pairs, shared default identity, persistence root (`modules/basic.nix:39`, `modules/basic.nix:40`, `modules/waydroid.nix:61`, `modules/persistent.nix:31`). Coverage6; min6. Publication removes settings, so hidden scope could increase adaptation cost or reveal stronger contracts (`README.md:15`); visible score, not null. Score **6**; confidence **low**.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":6,"distinct_leaks":4}}
```

### R
Scope: visible independent application owners. Pros: Harmonia Darwin owns complete options/rendering/launchd; scanner, Sunshine, XRDP and Ollama provide coherent working presets (`modules/harmonia.nix:28`, `modules/harmonia.nix:81`, `modules/scan.nix:18`, `modules/xrdp.nix:8`). Cons: most large desktop/user presets and helper-dependent wrappers are not independently complete (`modules/gemini-desktop.nix:31`, `modules/printing.nix:18`, `modules/users/_/baseline_cli.nix:62`). Literal5 useful references, no §4 nomination/export; hidden publication pieces could alter completeness. Score **5**; confidence **low**.

### P
Scope: actual Linux/Darwin branches. Pros: typed defaults check architecture/platform, shell policy explicitly restricts NixOS, root exports multiple OS outputs (`modules/options.nix:33`, `modules/options.nix:47`, `modules/nixos-zsh-user.nix:44`, `flake.nix:23`). Cons: legacy adapter projects HM imports only for NixOS, requiring separate Darwin shared-module route (`aspect.nix:25`, `modules/common.nix:831`). Score7 beyond5 explicit boundaries, below9 fixtures/clean common bridge. BSD novelty counted X once. Score **7**; confidence **medium**.

### L
Scope: debugging publication and inline adapter guidance. Pros: README clearly discloses stubs, factory documents usage and class projection (`README.md:13`, `README.md:15`, `aspect.nix:3`). Cons: no worked new-host/feature/policy onboarding route; root describes debugging focus (`README.md:7`). Score3 above2 contextless links, below5 authoring guide; disclosed stubs are a limit, not defect. Score **3**; confidence **medium**.

### V
Scope: real build workflows and assertions. Pros: host builds cover literal selected machines and options assert invalid combinations (`.github/workflows/build.yml:37`, `modules/options.nix:278`, `modules/zswap.nix:25`). Cons: all sampled host build steps continue on error, so failures do not fail workflow (`.github/workflows/build.yml:38`, `.github/workflows/build.yml:40`). Score4 above2 assertions-only, below5 enforcing structural checks; static only. Score **4**; confidence **medium**.

### O
Scope: operations derived from Den inventory. Pros: visible persistence and remote-builder app settings exist (`modules/persistent.nix:31`, `modules/nixbuild.nix:19`). Cons: those are conventional settings, not demonstrated Den-inventory deploy/secret/recovery generators; root exports configs only (`flake.nix:23`). Baseline2. Private details may hide stronger operations but do not justify null. Score **2**; confidence **low**.

### X
Scope: evaluated additional OS family. Pros: BSD subflake declares FreeBSD host, custom nixbsdSystem instantiation and output path (`bsd/flake.nix:25`, `bsd/flake.nix:26`, `bsd/flake.nix:27`). Cons: ordinary Android container service modules and packages are not further Den target families (`modules/miodroid.nix:23`, `modules/waydroid.nix:35`). Literal5 one concrete additional evaluated family. Score **5**; confidence **medium**.

### B
Scope: visible complete app envelopes and selected census diversity. Pros: five counted units are meaningful, independently owned application contributions; scan unused include binding does not force a fleet dependency because its actual expressions use lexical lib/pkgs (`modules/scan.nix:13`, `modules/scan.nix:18`). Cons: common/baseline/user/desktop bags cannot split per inner program; helper-dependent printing/Gemini/SCX and identity-specific Waydroid excluded; Harmonia standalone module counted once across platform envelope (`modules/users/_/baseline_cli.nix:62`, `modules/printing.nix:18`, `modules/gemini-desktop.nix:31`, `modules/scx.nix:44`, `modules/waydroid.nix:61`). Removed material limits completeness; no guessed reference units. Score **6**; confidence **low**.
B_div: 9 points → 7; B_ref: 5 units → 4; half-up mean → 6.
```score-evidence
{"B":{"diversity_points":9,"diversity_grade":7,"reference_grade":4,"reference_units":[{"name":"harmonia","evidence":"modules/harmonia.nix:135"},{"name":"scan","evidence":"modules/scan.nix:3"},{"name":"sunshine","evidence":"modules/sunshine.nix:3"},{"name":"xrdp","evidence":"modules/xrdp.nix:3"},{"name":"ollama","evidence":"modules/ollama.nix:3"}]}}
```

Total: **48.5/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Incremental Den migration has an explicit adapter (`aspect.nix:12`).
- Typed options assert incompatible settings (`modules/options.nix:263`).
- FreeBSD instantiation is a concrete extension (`bsd/flake.nix:26`).

Overall cons / limits:
- Build failures are nonblocking (§6a V; `.github/workflows/build.yml:38`).
- Many app owners require global helper scope (`modules/printing.nix:13`).
- Publication stubs limit source completeness without score nullification (`README.md:15`).

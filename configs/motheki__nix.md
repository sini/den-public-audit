# motheki__nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/motheki__nix.md)

- Upstream: [motheki/nix](https://github.com/motheki/nix)
- Reviewed revision: [`e75e72ed08cc`](https://github.com/motheki/nix/commit/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3)
- Author: motheki
- Score: **52.5 / 100**, rank 39 of 103 ranked configs. D 5 · I 8 · S 6 · R 5 · P 5 · L 5 · V 5 · O 5 · B 5 · X 2. Shortlists: starter, library units (1).
- Summary: Direct typed inventory D5; profile/identity ownership I8; owned Hunk settings S6/no leaks; useful units with broken export R5; honest Darwin P5; workflow docs L5; structural V5; generated NH ops O5; standard targets X2.

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

Generated flake-parts/import-tree loads dendritic wiring and a compact Darwin inventory (`flake.nix:6`, `modules/den.nix:3`, `modules/inventory/hosts.nix:4`). Profiles select feature aspects while a separate serializable inventory export omits entity functions (`modules/aspects/profiles/workstation.nix:1`, `modules/inventory/access.nix:1`).


## 2. Common patterns.

- den.default includes: define-user and hostname with shared compatibility defaults (`modules/defaults.nix:8`).
- host-aspects composition: workstation profile only composes capabilities (`modules/aspects/profiles/workstation.nix:4`).
- custom classes selection: users receive HM by default (`modules/defaults.nix:36`).


## 3. Novel patterns.

An explicit typed flake.inventory projects only host identity and user class data, keeping tool-facing output serializable (`modules/inventory/access.nix:8`, `modules/inventory/access.nix:24`).


## 4. Library candidates.

- linux-builder · `modules/aspects/features/linux-builder.nix:3` · opt-in persistent ARM Linux builder on Darwin · nix-darwin/nixpkgs · none · A: independent focused aspect.


## 5. den friction.

No verified den-specific workaround in inspected inventory/profile/default modules (`modules/inventory/access.nix:24`, `modules/aspects/profiles/workstation.nix:4`).


## 6. Docs and complexity.

Docs 3: README explains devenv activation, maintenance and generated inputs (`README.md:21`, `README.md:35`, `README.md:46`); source documents inventory safety and profile responsibility (`modules/inventory/access.nix:1`, `modules/aspects/profiles/workstation.nix:1`). Complexity 3: one workstation but reusable profiles and a typed tool inventory (`modules/inventory/hosts.nix:4`, `modules/inventory/access.nix:8`).


## 6a. Defects and scoring notes.

- R · moderate: exported homeManagerModules.coding-agents references den.aspects.features.coding-agents.homeManager, but pinned source has no coding-agents definition (`modules/reusable-modules.nix:6`).
No additional verified concrete defect in narrow Darwin support or native app defaults.

## 7. Template notes.

A clean Darwin starter for feature/profile/inventory boundaries; teach serializable output as separate from authorization (`modules/inventory/access.nix:1`).

## 8. Scorecard.

### D
Scope: serializable inventory projection and input-derived configuration. Pros: host/user names/classes are projected without entity functions and supported systems follow Den (`modules/inventory/access.nix:24`, `modules/inventory/systems.nix:4`). Cons: this is direct host walk, not independently routed facts; NH package exports are ordinary activation plumbing (`modules/packages/commands.nix:5`). Literal5 direct derivation cap. Score **5**; confidence **medium**.

### I
Scope: profiles, features, host policy and identity. Pros: profiles only compose capabilities; personal signing/keys are separate user owner; host owns hardware/trust (`modules/aspects/profiles/workstation.nix:1`, `modules/aspects/users/motheki.nix:8`, `modules/aspects/hosts/mothekis-macbook-pro.nix:8`). Cons: shell and command-line retain broad application bags (`modules/aspects/features/shell.nix:10`, `modules/aspects/features/command-line.nix:8`). Score8 strong ownership beyond5, below9 wholly independent app selection. Score **8**; confidence **medium**.

### S
Scope: native settings and local typed app module. Pros: Hunk package/settings types feed guarded package/file consumer; HM backup policy deliberately refuses overwrite (`modules/_modules/home-manager/hunk.nix:11`, `modules/_modules/home-manager/hunk.nix:24`, `modules/defaults.nix:24`). Cons: most feature settings use ordinary upstream interfaces rather than a broader shared domain contract (`modules/aspects/features/shell.nix:33`). Contract6: real owned format interface beyond5, below7 validated multi-consumer domain. No verified shared author adaptation group: identity and trust remain user/host-owned (`modules/aspects/users/motheki.nix:8`, `modules/aspects/hosts/mothekis-macbook-pro.nix:11`). Coverage9, min6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":9,"distinct_leaks":0}}
```

### R
Scope: app owner envelopes and explicit reusable exports. Pros: Nixvim core owns its import/dependencies/LSP/plugins; code-review owns Hunk module and preset; reusable modules exported (`modules/aspects/features/editor-core.nix:4`, `modules/aspects/features/editor-core.nix:13`, `modules/aspects/features/code-review.nix:6`, `modules/reusable-modules.nix:4`). Cons: coding-agents export references an aspect absent from source definitions (`modules/reusable-modules.nix:6`); generic VCS config also expects unowned hunk/nvim commands (`modules/aspects/features/version-control.nix:36`, `modules/aspects/features/version-control.nix:67`). Literal5 useful references despite one broken advertised export, below9 complete polished library. Score **5**; confidence **medium**.

### P
Scope: declared ARM Darwin workstation. Pros: host metadata and platform-specific preferences are explicitly bounded; systemd-only Radicle disabled with explanation (`modules/inventory/hosts.nix:4`, `modules/aspects/features/version-control.nix:5`). Cons: no non-Darwin managed target or negative-context fixture; builder is opt-in, not selected (`modules/aspects/hosts/mothekis-macbook-pro.nix:13`). Literal5 honest narrow scope. Score **5**; confidence **medium**.

### L
Scope: developer workflow and source architecture guidance. Pros: README explains activation, tool inheritance, maintenance, formatter/check and generated inputs; profiles/inventory have clear responsibility comments (`README.md:25`, `README.md:31`, `README.md:35`, `README.md:46`, `modules/aspects/profiles/workstation.nix:1`). Cons: no worked host/aspect authoring example in README (`README.md:7`). Literal5 usable orientation, below9 complete authoring route. Score **5**; confidence **medium**.

### V
Scope: structural checks. Pros: shared treefmt enables Alejandra/deadnix/statix and README supplies flake-check command (`modules/_modules/treefmt.nix:4`, `modules/formatter.nix:3`, `README.md:44`). Cons: no fixture verifies every reusable export resolves, including missing coding-agents (`modules/reusable-modules.nix:6`). Literal5 structural tooling, no run claimed. Score **5**; confidence **medium**.

### O
Scope: inventory-derived activation tools. Pros: Den nh.denPackages generates per-target commands and serializable inventory is available to tools (`modules/packages/commands.nix:5`, `modules/inventory/access.nix:24`). Cons: builder is an unselected definition and no derived deploy/secret/recovery pipeline verified (`modules/aspects/hosts/mothekis-macbook-pro.nix:13`). Literal5 useful derived activation, below9 fleet lifecycle. Score **5**; confidence **medium**.

### X
Scope: standard Darwin/HM and ordinary package tooling. Pros: editor imports upstream Nixvim HM module and Homebrew integration is explicit (`modules/aspects/features/editor-core.nix:4`, `modules/aspects/features/homebrew.nix:25`). Cons: no distinct Den nixvim class evaluation bridge; standard imports do not establish another target family (`modules/defaults.nix:36`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: five complete app owners and selected census max-depth. Pros: Nixvim, Hunk, Homebrew, opt-in Linux builder and yt-dlp own coherent preset/integration envelopes (`modules/aspects/features/editor-core.nix:31`, `modules/aspects/features/code-review.nix:8`, `modules/aspects/features/homebrew.nix:24`, `modules/aspects/features/linux-builder.nix:3`, `modules/aspects/features/media.nix:5`). Cons: shell/command-line/version-control mixed bodies cannot split per inner program; agent-search supplies client settings without owning activated clients; coding-agents missing (`modules/aspects/features/shell.nix:10`, `modules/aspects/features/agent-search.nix:17`, `modules/reusable-modules.nix:6`). Nixvim languages/count counted once across files. Score **5**; confidence **medium**.
B_div: 5.5 points → 5; B_ref: 5 units → 4; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":5.5,"diversity_grade":5,"reference_grade":4,"reference_units":[{"name":"nixvim","evidence":"modules/aspects/features/editor-core.nix:3"},{"name":"hunk","evidence":"modules/aspects/features/code-review.nix:3"},{"name":"homebrew","evidence":"modules/aspects/features/homebrew.nix:24"},{"name":"linux-builder","evidence":"modules/aspects/features/linux-builder.nix:3"},{"name":"yt-dlp","evidence":"modules/aspects/features/media.nix:5"}]}}
```

Total: **52.5/100**. Shortlists: showcase false; library_units ['linux-builder']; starter true.

Overall pros:
- Profiles contain composition and identity has its own owner (`modules/aspects/profiles/workstation.nix:1`).
- Inventory export avoids function/entity leakage (`modules/inventory/access.nix:1`).
- Native settings modules and tool workflows are explained (`modules/_modules/home-manager/hunk.nix:11`, `README.md:35`).

Overall cons / limits:
- One advertised reusable export references missing aspect (§6a R; `modules/reusable-modules.nix:6`).
- Broad shell bags reduce granular selection (`modules/aspects/features/shell.nix:10`).
- No export-resolution fixture verified (`modules/reusable-modules.nix:4`).

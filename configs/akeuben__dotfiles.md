# akeuben__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/akeuben__dotfiles.md)

- Upstream: [akeuben/dotfiles](https://github.com/akeuben/dotfiles)
- Reviewed revision: [`48183786da04`](https://github.com/akeuben/dotfiles/commit/48183786da040379d88ad2f23dbdc796de4093dc)
- Author: akeuben
- Score: **48.0 / 100**, rank 57 of 103 ranked configs. D 5 · I 8 · S 6 · R 5 · P 5 · L 2 · V 2 · O 5 · B 5 · X 2. Shortlists: library units (1).
- Summary: Readable feature boundaries, entity-derived settings and several complete application presets; author constants and stale onboarding limit transfer as a starter.

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
Despite template language in its README, this snapshot declares four named Linux hosts and personalized features, so it is a den configuration (`modules/hosts.nix:12`, `modules/hosts.nix:30`, `modules/config/kappashell.nix:2`). Flake-parts/import-tree loads the module tree (`flake.nix:2`).

## 2. Common patterns
- Central host inventory separates ds9, spacedock, voyager and enterprise (`modules/hosts.nix:12`, `modules/hosts.nix:18`, `modules/hosts.nix:24`, `modules/hosts.nix:30`).
- User class schema defaults to HM while defaults coordinate embedded HM packages (`modules/defaults.nix:5`, `modules/defaults.nix:10`).
- Feature bundles can be assembled independently from leaf aspects (`modules/feature/productivity.nix:2`, `modules/config/upower.nix:2`).

## 3. Novel patterns
An empty productivity bundle reserves a stable composition point without enabling applications (`modules/feature/productivity.nix:2`); useful scaffolding, but it contributes no actual feature yet (`modules/feature/productivity.nix:3`).

## 4. Library candidates
- upower · `modules/config/upower.nix:2` · enables the system power information service · inputs: NixOS/nixpkgs · parameterization: none (`modules/config/upower.nix:4`) · **A**, a minimal independently includable service aspect.

## 5. den friction
No verified den-specific friction in reviewed host/default/leaf wiring (`modules/hosts.nix:12`, `modules/defaults.nix:10`, `modules/config/upower.nix:2`).

## 6. Docs and complexity
Docs **2**: README gives template build and VM guidance (`README.md:13`, `README.md:29`) but still tells readers to run igloo while real hosts are named ds9 and enterprise (`README.md:19`, `modules/hosts.nix:12`, `modules/hosts.nix:30`). Complexity **3**: four hosts, shared HM defaults and feature bundles (`modules/hosts.nix:12`, `modules/defaults.nix:5`, `modules/feature/productivity.nix:2`).

## 6a. Defects and scoring notes

- **S · moderate:** seven grouped author constants remain in shared aspects: identities, literal host selection and monitor routing (`modules/config/fish/default.nix:17`, `modules/config/bigscreen.nix:15`, `modules/config/openrgb.nix:7`, `modules/config/hypr/default.nix:75`, `modules/config/kodi/default.nix:49`).
- **L · moderate:** published build examples select nonexistent igloo instead of the actual inventory (`README.md:19`, `modules/hosts.nix:12`).
The empty productivity placeholder is not a functional defect (`modules/feature/productivity.nix:2`); remaining non-9 scores reflect anchor coverage.

## 7. Template notes
Simple leaf aspects are approachable; copied template command names should be reconciled with the actual inventory before treating README as a tutorial (`README.md:19`, `modules/hosts.nix:12`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Host facts feed hostname (`modules/config/hostname.nix:4`), NH checkout (`modules/config/nh.nix:6`) and generated monitor records (`modules/config/hypr/default.nix:98`). These are real entity-derived settings, the5 anchor; no policy/quirk routed channel is established by those bodies. Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: Feature leaves separate applications from host and user identity (`modules/config/git.nix:3`, `modules/hosts.nix:2`); Kodi has its own typed settings/profile schema (`modules/config/kodi/module.nix:251`). Eight interpolates toward isolated9: shared desktop behavior still includes the project-specific shell (`modules/config/hypr/default.nix:3`). Empty productivity grouping is scaffolding rather than a charged defect (`modules/feature/productivity.nix:2`). Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Git uses explicit user fields and monitor defaults tolerate missing facts (`modules/config/git.nix:6`, `modules/config/hypr/default.nix:102`), contract7. Ten raw references group into seven adaptations: Avery identity/session/trusted-user (`modules/config/fish/default.nix:17`, `modules/config/nix.nix:8`, `modules/config/kodi/default.nix:45`), HTPC login (`modules/config/bigscreen.nix:15`), enterprise hostname (`modules/config/openrgb.nix:7`), DP-1 monitor (`modules/config/hypr/default.nix:75`), and Abbey/Serena/Chris profile identities (`modules/config/kodi/default.nix:49`, `modules/config/kodi/default.nix:53`, `modules/config/kodi/default.nix:57`). Coverage6 cap gives min6; identities in the entity inventory itself are not leaks. Score **6**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":7}}
```

### R

Scope · pros · cons/coverage: The nominated UPower leaf drops in without author edits (`modules/config/upower.nix:2`); more substantive editor and session packages carry their own configuration assets (`modules/config/nvim/default.nix:11`, `modules/config/tmux/default.nix:11`). Grade5 reflects usable units without a documented minimal outside consumer/dependency contract; the tiny UPower toggle alone does not establish9. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Declared targets are x86_64 Linux (`modules/hosts.nix:12`, `modules/hosts.nix:30`), and features address NixOS/HM (`modules/defaults.nix:5`). This is an honest narrow platform5; no second-platform claim is charged as a defect. Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: README links Den and gives editing/build/VM steps (`README.md:5`, `README.md:13`, `README.md:25`), but build examples invoke igloo (`README.md:19`) against a different actual host inventory (`modules/hosts.nix:12`). Operation-only/stale template guidance supports2, not a composition tutorial. Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: A VM launch helper selects voyager and forwards to its VM executable (`modules/vm.nix:13`, `modules/vm.nix:16`). This is manual smoke-test access without assertions or representative test fixtures, baseline2; the README VM command (`README.md:32`) does not turn it into an automated check. Score **2**; confidence **high**.

### O

Scope · pros · cons/coverage: Generated NH packages use den.lib.nh.denPackages (`modules/package/nh.nix:3`), and deployed NH consumes host.flakepath rather than duplicating the inventory path (`modules/config/nh.nix:6`). This reaches fact-driven local operations5; the VM helper selects one literal configuration (`modules/vm.nix:13`), not fleet orchestration9. Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: Visible class defaults target ordinary NixOS/HM (`modules/defaults.nix:3`, `modules/defaults.nix:10`); wrapper packages are ordinary application packages (`modules/config/nvim/default.nix:11`). No first-class non-host target integration is established, baseline2. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Enabled verified census families total5.5points, grade5. The complete application units below include actual plugin/backend integration for Evolution (`modules/config/evolution.nix:4`) and editor LSP/formatter wiring (`modules/config/nvim/lua/lsp.lua:2`). Kitty only installs a package (`modules/config/kitty/default.nix:4`); its nearby native config is not wired there. Zen depends on an external Stylix option tree (`modules/config/zen.nix:8`), Kodi and Fish retain author identities (`modules/config/kodi/default.nix:45`, `modules/config/fish/default.nix:17`), and bare UPower is excluded (`modules/config/upower.nix:4`). Six complete units yield reference5 and B5. Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":5.5,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"git","evidence":"modules/config/git.nix:2"},{"name":"evolution","evidence":"modules/config/evolution.nix:2"},{"name":"nvim","evidence":"modules/config/nvim/default.nix:2"},{"name":"tmux","evidence":"modules/config/tmux/default.nix:2"},{"name":"ssh","evidence":"modules/config/ssh.nix:2"},{"name":"steam","evidence":"modules/config/steam.nix:2"}]}}
```

**Total:** 48.0/100. **Shortlists:** showcase no; library upower; starter no. Readable feature boundaries, entity-derived settings and several complete application presets; author constants and stale onboarding limit transfer as a starter.

Overall pros:
- Host facts drive monitors and NH (`modules/config/hypr/default.nix:98`, `modules/config/nh.nix:6`).
- Git obtains identity from user fields (`modules/config/git.nix:6`).
- Editor packages include native configuration and dependencies (`modules/config/nvim/default.nix:11`).

Overall cons / scope limits:
- Build examples still name igloo (`README.md:19`).
- Shared Fish session names Avery (`modules/config/fish/default.nix:17`).
- Shared Kodi profiles retain four personal names (`modules/config/kodi/default.nix:45`).

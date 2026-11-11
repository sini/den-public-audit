# SyahrulBhudiF__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/SyahrulBhudiF__dotfiles.md)

- Upstream: [SyahrulBhudiF/dotfiles](https://github.com/SyahrulBhudiF/dotfiles)
- Reviewed revision: [`ba537827987e`](https://github.com/SyahrulBhudiF/dotfiles/commit/ba537827987edc4e00a574d1748d37a34a3b69ff)
- Author: SyahrulBhudiF
- Score: **30.0 / 100**, rank 102 of 103 ranked configs. D 2 · I 5 · S 2 · R 5 · P 5 · L 2 · V 2 · O 2 · B 3 · X 2. Shortlists: library units (1).
- Summary: Useful grade-B graphics wrapper merits library discovery; direct personalized home settings and absent setup guide do not merit showcase or starter.

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
A raw evalModules entry explicitly imports den and a short module list (`flake.nix:40`). One standalone Linux home owns a personalized ryuko aspect, with a custom package set and HM instantiator (`modules/den.nix:5`, `modules/den.nix:28`).

## 2. Common patterns
- homes (standalone HM): ryuko uses a custom instantiate hook supplying inputs/flakePkgs (`modules/den.nix:28`).
- den.default supplies HM stateVersion (`modules/den.nix:3`).
- Several files contribute to the same user aspect (`modules/home.nix:3`, `modules/git.nix:3`, `modules/terminal.nix:3`).

## 3. Novel patterns
A locally adapted nixGL package set replaces pcregrep with pcre2grep in generated checks, and Ghostty is wrapped through nixGLMesa for a non-NixOS desktop (`modules/den.nix:14`, `modules/terminal.nix:10`).

## 4. Library candidates
- ghostty-nixgl · `modules/terminal.nix:3` · wraps Ghostty with nixGLMesa and links its configuration · inputs: HM, nixpkgs providing nixgl.nixGLMesa, external Ghostty config · parameterization: none (`modules/terminal.nix:11`) · **B**, extract a feature aspect, expose config source and bundle/document the nixGL overlay (`modules/den.nix:20`).

## 5. den friction
No verified den-specific friction in the standalone instantiator; custom extraSpecialArgs carries dependencies needed by the user modules (`modules/den.nix:28`, `modules/home.nix:4`).

## 6. Docs and complexity
Docs **1**: root README only describes the intent and promises updates (`README.md:2`, `README.md:4`). Complexity **3**: one home but a custom nixGL overlay, custom instantiation and broad agent/editor configuration (`modules/den.nix:10`, `modules/den.nix:28`, `modules/home.nix:60`).

## 6a. Defects and scoring notes

- **S · moderate:** Raw 17 literals form **7 grouped leaks** in the intended reusable fragments: ryuko and /home/ryuko plus checkout root ~/dotfiles (`modules/home.nix:35`, `modules/home.nix:36`, `modules/terminal.nix:17`); personal email (`modules/git.nix:6`); Cavos and Najla names/emails (four values, `modules/git.nix:52`, `modules/git.nix:53`, `modules/git.nix:60`, `modules/git.nix:61`); three key-file identities (`modules/git.nix:19`, `modules/git.nix:25`, `modules/git.nix:32`); work domain/port (`modules/git.nix:29`, `modules/git.nix:30`); two project roots (`modules/git.nix:91`, `modules/git.nix:94`); gh-cavos alias and cavos-io organization (`modules/git.nix:16`, `modules/git.nix:119`). Groups are personal identity/home, dotfiles checkout root, Cavos identity/key/alias/org, Najla identity/key, Sobat network endpoint/port, Sobat key identity, and Codes project-root tree. Generic SSH paths excluded.
- **I · minor:** unrelated home/terminal/Git fragments have one indivisible aspect identity (`modules/home.nix:3`, `modules/git.nix:3`, `modules/terminal.nix:3`).
- **L · moderate:** placeholder README gives no adaptation or activation path (`README.md:2`, `README.md:4`).

## 7. Template notes
A personalized foreign-Linux HM example with useful graphics wrapping; substantial identity, checkout and SSH material must be replaced before reuse (`modules/home.nix:35`, `modules/git.nix:16`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Explicit module list (`flake.nix:40`) writes HM values directly (`modules/home.nix:34`); custom constructor supplies dependencies (`modules/den.nix:28`). No routed facts demonstrated: literal baseline 2, with no size deduction. Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Git/terminal/home concern files are visible (`flake.nix:44`), but all merge ryuko and home mixes agents/input methods/fonts (`modules/home.nix:3`, `modules/home.nix:125`, `modules/home.nix:147`). Middle anchor 5 for file ownership, with the inseparable feature boundary charged here. Score **5**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract 2: checkout/identity variation requires edits (`modules/terminal.nix:17`, `modules/git.nix:6`). Coverage 6: 7 grouped leaks from 17 raw literals listed in §6a; min(2,6)=2. Home-relative derivation helps paths (`modules/home.nix:45`) but does not supply a checkout contract. Score **2**; confidence **high**.

```score-evidence
{"S":{"contract_design":2,"leak_coverage":6,"distinct_leaks":7}}
```

### R

Scope · pros · cons/coverage: ghostty-nixgl wraps the real application (`modules/terminal.nix:10`). Two identified value changes—aspect key (`modules/terminal.nix:3`) and config source (`modules/terminal.nix:17`)—preserve the body; dependency is pkgs.nixgl.nixGLMesa supplied by overlay (`modules/den.nix:20`). Literal B/5, without a second S deduction. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Explicit x86 Linux home and genericLinux/nixGL boundary (`modules/den.nix:5`, `modules/home.nix:32`, `modules/terminal.nix:11`). Honest narrow support meets 5; no platform boundary fixtures claimed. Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: Short entry is easy to locate (`flake.nix:40`); README only promises future updates (`README.md:2`, `README.md:4`). Literal placeholder anchor 2; missing setup path charged L. Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: Entry lists only configuration modules (`flake.nix:41`); instantiator builds ordinary HM (`modules/den.nix:29`). No relevant configuration checks/CI found in inspected entry/tree; baseline 2, not a failing-test assertion. Score **2**; confidence **medium**.

### O

Scope · pros · cons/coverage: One actual home (`modules/den.nix:5`) assumes externally prepared signing paths (`modules/git.nix:108`). Manual single-home activation is baseline 2 under ruling, not not_applicable or an invented fleet defect. Score **2**; confidence **high**.

### X

Scope · pros · cons/coverage: Custom constructor still calls standard HM (`modules/den.nix:29`); nixGL wrapper is a package adaptation (`modules/terminal.nix:11`). Standard-home baseline 2, no separate Den target class. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Enabled census maximum depth: Zsh/Starship/Neovim/Nushell = 4 → diversity 3. Whole Nix module scan has no complete nonidentity application aspect: all app fragments merge ryuko (`modules/home.nix:3`, `modules/git.nix:3`, `modules/terminal.nix:3`); Ghostty additionally requires external live config. Reference 2 with empty list; rounded mean is 3. Score **3**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":4,"diversity_grade":3,"reference_grade":2,"reference_units":[]}}
```

**Total:** 30.0/100. **Shortlists:** showcase no; library ghostty-nixgl; starter no. Useful grade-B graphics wrapper merits library discovery; direct personalized home settings and absent setup guide do not merit showcase or starter.

Overall pros:
- Explicit entry and dependency constructor (`flake.nix:40`, `modules/den.nix:28`).
- Real nixGL Ghostty integration (`modules/terminal.nix:11`).
- Missing Starship source safely falls back (`modules/home.nix:27`).

Overall cons / scope limits:
- S: checkout root must be patched (`modules/terminal.nix:17`).
- I: concern files share the user identity (`modules/home.nix:3`).
- L: no setup route in placeholder docs (`README.md:4`).

# Kykero/Nazunix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/Kykero/Nazunix.md)

- Upstream: [Kykero/Nazunix](https://github.com/Kykero/Nazunix)
- Reviewed revision: [`469bacd7b841`](https://github.com/Kykero/Nazunix/commit/469bacd7b841df5aaea43ad6027049cb152f394b)
- Author: Kykero
- Score: **60.5 / 100**, rank 13 of 101 ranked configs. D 6 · I 8 · S 7 · R 5 · P 5 · L 9 · V 7 · O 5 · B 5 · X 2. Shortlists: showcase, starter, library units (1).
- Summary: Strong documented profile/class composition and native format validation; local operations and reusable app units are real, while author constants and limited routed-channel breadth constrain S/D.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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
Flake-parts/import-tree loads the module tree ([`flake.nix:61`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/flake.nix#L61)). A host schema pointcut selects an aspect from each host profile, matching the documented base/full deployment model ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4), [`README.md:6`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L6)).

## 2. Common patterns
- custom schema/classes: host profile selects profile-${host.profile} dynamically ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4)).
- den.default includes hostname and sets HM class defaults ([`modules/defaults.nix:9`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/defaults.nix#L9), [`modules/defaults.nix:13`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/defaults.nix#L13)).
- VM autologin is enabled for both full and base host variants ([`modules/vm.nix:5`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/vm.nix#L5), [`modules/vm.nix:7`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/vm.nix#L7)).

## 3. Novel patterns
Each physical machine has a base twin used as an install gateway, separating initial provisioning from the full desktop profile ([`README.md:6`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L6)). The schema pointcut makes that difference inventory-driven ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4)).

## 4. Library candidates
- desktop-bluetooth · [`modules/desktop/bluetooth.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4) · enables BlueZ with powered-on adapters · inputs: NixOS/nixpkgs · parameterization: none ([`modules/desktop/bluetooth.nix:5`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L5)) · **A**, independent of Noctalia despite explaining its consumer ([`modules/desktop/bluetooth.nix:1`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L1)).

## 5. den friction
No verified den-specific friction in profile selection or default/VM wiring ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4), [`modules/defaults.nix:9`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/defaults.nix#L9), [`modules/vm.nix:5`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/vm.nix#L5)).

## 6. Docs and complexity
Docs **5**: root links installation, day-two procedures and per-folder README guides ([`README.md:9`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L9), [`README.md:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L14), [`README.md:19`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L19), [`README.md:31`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L31)). Complexity **4**: profile schema plus paired installation/full host variants ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4), [`README.md:6`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L6)).

## 6a. Defects and scoring notes

- **S · moderate:** shared Git identity, checkout root and installer origin require three author-specific changes ([`modules/shell/git.nix:17`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/shell/git.nix#L17), [`modules/nh.nix:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/nh.nix#L14), [`modules/apps/bootstrap.nix:116`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/apps/bootstrap.nix#L116)).
- **D · minor:** the class bridge selects aspect-chain with head without a local empty-chain guard ([`modules/neovim/neovim.nix:24`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L24)); this is a bounded robustness limit, not a reproduced failure.
Other non-9 limits describe anchor coverage, not additional charged defects.

## 7. Template notes
A strong example of explicit provisioning profiles and entity-driven aspect selection; use per-folder docs to follow the pointcut ([`README.md:39`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L39), [`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4)).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Editor settings are produced by the vimzuna profile ([`modules/neovim/profile.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/profile.nix#L4)), forwarded from vim into NixOS programs.nvf.settings.vim ([`modules/neovim/neovim.nix:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L14), [`modules/neovim/neovim.nix:18`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L18)) and consumed by the imported NVF module ([`modules/neovim/neovim.nix:36`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L36)). This exceeds schema-only selection; one class bridge and an unchecked aspect-chain head ([`modules/neovim/neovim.nix:24`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L24)) support 6 rather than cross-scope missing/duplicate-safe 9. Score **6**; confidence **high**.

### I

Scope · pros · cons/coverage: Separate host profile selection and isolated editor namespace give strong concern boundaries ([`modules/schema/profile-pointcut.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile-pointcut.nix#L4), [`modules/neovim/namespace.nix:8`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/namespace.nix#L8)); Herdr owns its typed settings and plugin contract ([`modules/homes/ai/herdr.nix:55`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L55)). Eight interpolates toward 9: Niri application installation and configuration still rely on a surrounding multi-aspect profile ([`modules/profiles/README.md:10`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/README.md#L10)). Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Profile enum and typed Herdr extension points are explicit contracts ([`modules/schema/profile.nix:6`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/profile.nix#L6), [`modules/homes/ai/herdr.nix:55`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L55)), contract grade7. Four raw constants form three adaptation groups: Git name/email identity ([`modules/shell/git.nix:17`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/shell/git.nix#L17)), checkout root ([`modules/nh.nix:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/nh.nix#L14)) and installer repository origin ([`modules/apps/bootstrap.nix:116`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/apps/bootstrap.nix#L116)). Coverage9 has no grouped-count cap; min with contract7 is7. Host hardware and upstream service URLs are outside this author-leak count. Score **7**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":9,"distinct_leaks":3}}
```

### R

Scope · pros · cons/coverage: The nominated BlueZ unit needs no author edits ([`modules/desktop/bluetooth.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4)), while substantive Herdr has explicit settings/plugins options and its own checked configuration ([`modules/homes/ai/herdr.nix:35`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L35), [`modules/homes/ai/herdr.nix:55`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L55)). Grade5 reflects usable units without a demonstrated minimal outside consumer for the larger integration; Bluetooth alone is too small to establish the9 anchor. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: The documented scope is a NixOS laptop/desktop fleet ([`README.md:3`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L3)); Linux binary targets are explicit in the Herdr-projects integration ([`modules/homes/ai/herdr-projects.nix:38`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr-projects.nix#L38)). Honest narrow scope earns5; the selected CI checks desktop hosts rather than a cross-platform matrix ([`.github/workflows/check.yml:42`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/.github/workflows/check.yml#L42)). Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: The schema guide explains producer field, pointcut and resulting profile inclusion ([`modules/schema/README.md:7`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/README.md#L7), [`modules/schema/README.md:10`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/README.md#L10)), and the profile guide traces host selection through feature bundles ([`modules/profiles/README.md:3`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/README.md#L3), [`modules/profiles/README.md:26`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/README.md#L26)). This teaches composition at9, beyond the linked installation/day-two procedures ([`README.md:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L14), [`README.md:19`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/README.md#L19)); its examples remain this fleet. Score **9**; confidence **high**.

### V

Scope · pros · cons/coverage: CI evaluates every declared host and builds operational apps ([`.github/workflows/check.yml:28`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/.github/workflows/check.yml#L28), [`.github/workflows/check.yml:35`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/.github/workflows/check.yml#L35)), then builds generated Niri configuration to trigger native validation ([`.github/workflows/check.yml:39`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/.github/workflows/check.yml#L39)). Herdr checks TOML and plugin manifests in derivations ([`modules/homes/ai/herdr.nix:35`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L35), [`modules/homes/ai/herdr.nix:47`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L47)). Seven interpolates above representative5 for these distinct boundaries; explicit Den missing/duplicate negative cases are not shown in that workflow. Score **7**; confidence **high**.

### O

Scope · pros · cons/coverage: NH packages derive from Den through den.lib.nh.denPackages ([`modules/nh.nix:7`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/nh.nix#L7)); rebuilding discovers the running hostname and consumes its generated cache settings ([`modules/apps/rebuild.nix:41`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/apps/rebuild.nix#L41), [`modules/apps/rebuild.nix:47`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/apps/rebuild.nix#L47)). This is actual fact-driven local operation5. The installer explicitly uses runtime checkout discovery rather than Den entities ([`modules/apps/bootstrap.nix:3`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/apps/bootstrap.nix#L3)), so its size is not credited as richer entity-driven fleet orchestration. Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: The custom vim class routes into ordinary NixOS NVF ([`modules/neovim/neovim.nix:17`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L17), [`modules/neovim/neovim.nix:36`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L36)); VM variants are ordinary host variants ([`modules/desktop/vm.nix:11`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/vm.nix#L11)). These remain OS/home output scope, baseline2, with operations credited only under O ([`modules/nh.nix:7`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/nh.nix#L7)). Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census diversity uses enabled, selection-verified families only. Complete reference units below were body-read: shells/session presets, browser/desktop app integrations and Herdr/OmO. Niri configuration fragments require the surrounding profile ([`modules/profiles/README.md:10`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/README.md#L10)); Claude extension fragments do not install their CLI ([`modules/neovim/claude.nix:2`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/claude.nix#L2)). Bare flags and token preferences, including Btop theme_background ([`modules/homes/tui/btop.nix:8`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/tui/btop.nix#L8)), are excluded. Several Neovim plugin files remain one editor, not separate apps ([`modules/neovim/profile.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/profile.nix#L4)). Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"home-fish","evidence":"modules/homes/shell/fish.nix:7"},{"name":"home-bash","evidence":"modules/homes/shell/bash.nix:5"},{"name":"home-tmux","evidence":"modules/homes/shell/tmux.nix:13"},{"name":"home-fastfetch","evidence":"modules/homes/tui/fastfetch.nix:12"},{"name":"desktop-browser","evidence":"modules/desktop/browser.nix:14"},{"name":"desktop-craftapps","evidence":"modules/desktop/pdfcraft-xwayland.nix:11"},{"name":"desktop-files","evidence":"modules/desktop/files.nix:20"},{"name":"desktop-images","evidence":"modules/desktop/images.nix:48"},{"name":"desktop-greeter","evidence":"modules/desktop/greeter.nix:14"},{"name":"desktop-onedrive","evidence":"modules/desktop/onedrive.nix:15"},{"name":"desktop-proton","evidence":"modules/desktop/proton.nix:11"},{"name":"desktop-terminal","evidence":"modules/desktop/terminal.nix:24"},{"name":"desktop-outlook","evidence":"modules/desktop/outlook.nix:15"},{"name":"home-herdr","evidence":"modules/homes/ai/herdr.nix:23"},{"name":"home-omo","evidence":"modules/homes/ai/omo.nix:27"}]}}
```

**Total:** 60.5/100. **Shortlists:** showcase yes; library desktop-bluetooth; starter yes. Strong documented profile/class composition and native format validation; local operations and reusable app units are real, while author constants and limited routed-channel breadth constrain S/D.

Overall pros:
- Profile selection is explained end to end ([`modules/schema/README.md:7`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/schema/README.md#L7)).
- Editor class settings reach the NVF consumer ([`modules/neovim/neovim.nix:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L14), [`modules/neovim/neovim.nix:36`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L36)).
- Herdr validates generated config and plugin manifests ([`modules/homes/ai/herdr.nix:35`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L35), [`modules/homes/ai/herdr.nix:47`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/homes/ai/herdr.nix#L47)).

Overall cons / scope limits:
- Shared checkout and Git identity need adaptation ([`modules/nh.nix:14`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/nh.nix#L14), [`modules/shell/git.nix:17`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/shell/git.nix#L17)).
- Forwarding selects an unchecked chain head ([`modules/neovim/neovim.nix:24`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/neovim/neovim.nix#L24)).
- Larger desktop integrations rely on the surrounding profile ([`modules/profiles/README.md:10`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/profiles/README.md#L10)).

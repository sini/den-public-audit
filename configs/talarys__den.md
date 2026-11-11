# talarys__den

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/talarys__den.md)

- Upstream: [talarys/den](https://github.com/talarys/den)
- Reviewed revision: [`469df2c2de88`](https://github.com/talarys/den/commit/469df2c2de88614d17a0f557cb19eaaa18ed0415)
- Author: talarys
- Score: **34.0 / 100**, rank 97 of 103 ranked configs. D 2 · I 8 · S 4 · R 5 · P 3 · L 1 · V 2 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: D direct settings; I distinct feature branches; S three grouped adaptations/partial path contract; R Ghostty B; P class-envelope defects; L no project guide; V no semantic checks; O manual helpers; X standard targets; B census+seven complete units.

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

Flake-parts/import-tree loads den and feature branches grouped under apps, shell, system and desktop (`flake.nix:2`, `modules/apps/ghostty.nix:2`). Two explicit hosts include a WSL machine and a desktop-style system (`modules/hosts/void.nix:7`, `modules/hosts/argos.nix:7`).


## 2. Common patterns.

- angle-bracket refs: __findFile is provided by den and features are selected by path (`modules/den.nix:5`, `modules/hosts/argos.nix:39`).
- den.default includes: primary-user, hostname and host-aspects establish global conventions (`modules/defaults.nix:63`).
- provides tree: nested apps branch contains terminal aspects (`modules/apps/ghostty.nix:2`).


## 3. Novel patterns.

One host combines WSL import and desktop integration while reusing only selected shared system aspects (`modules/hosts/void.nix:11`, `modules/hosts/void.nix:20`).


## 4. Library candidates.

- ghostty · `modules/apps/ghostty.nix:2` · terminal appearance and split/navigation bindings · HM and Ghostty package · none · B: expose font/theme choices and lift from apps namespace.


## 5. den friction.

No verified den-specific workaround in the inspected integration and defaults (`modules/den.nix:5`, `modules/defaults.nix:63`).


## 6. Docs and complexity.

Docs 2: defaults explain the roles of each battery inline (`modules/defaults.nix:64`); host composition is readable but hardware-local (`modules/hosts/argos.nix:26`). Complexity 3: shared hierarchical features combine WSL and full desktop hosts (`modules/hosts/void.nix:11`, `modules/hosts/argos.nix:39`).


## 6a. Defects and scoring notes.

- S · moderate: shared shells fix author home/checkout paths; Git/virt share author identity, and container timezone is fixed. Three grouped adaptations are enumerated in S card (`modules/shell/nushell.nix:8`, `modules/shell/fish.nix:26`, `modules/shell/git.nix:18`, `modules/containers/audiobookshelf.nix:15`).
- P · moderate: selected ssh uses homeManger and selected locale puts i18n/time directly on the aspect instead of nixos (`modules/system/ssh.nix:3`, `modules/system/locale.nix:2`, `modules/hosts/argos.nix:43`, `modules/hosts/argos.nix:44`).
Ghostty font/theme are ordinary overrideable preset choices, and global Disko has no verified WSL defect; neither is deducted.

## 7. Template notes.

Useful angle-reference example, but remove hardcoded disk identifiers and explain branch hierarchy for beginners (`modules/hosts/argos.nix:26`, `modules/apps/ghostty.nix:2`).

## 8. Scorecard.

### D
Scope: hosts, defaults and app branches. Pros: shared feature selection is visible (`modules/hosts/argos.nix:39`, `modules/users/talarys.nix:9`). Cons: inspected features directly set application values; flavor/accent arguments are local preset variation, not a routed fact channel (`modules/desktop/catppuccin.nix:5`). Literal2; no deduction for a small fleet. Score **2**; confidence **medium**.

### I
Scope: apps/shell/system/desktop feature branches. Pros: names and class arms localize applications (`modules/apps/ghostty.nix:2`, `modules/system/podman.nix:2`). Cons: utils combines several independently configurable tools (`modules/shell/utils.nix:5`); this is a bounded layout ceiling, not a new defect. Interpolated8: clean ownership beyond5, some broad bundles below9. Score **8**; confidence **medium**.

### S
Scope: reusable shell/desktop/container settings. Pros: Catppuccin exposes flavor/accent arguments and ordinary HM application settings remain overrideable (`modules/desktop/catppuccin.nix:5`, `modules/apps/ghostty.nix:8`). Cons: contract4: derived-home NH path helps but other shells fix the author checkout/home (`modules/shell/nh.nix:16`, `modules/shell/fish.nix:26`, `modules/shell/nushell.nix:8`). Coverage8 for three grouped changes: owner identity/home paths including Git and virt account; checkout root (NH/fish name disagreement grouped once); household timezone (`modules/shell/git.nix:18`, `modules/system/virt.nix:8`, `modules/containers/audiobookshelf.nix:15`). These are shared definitions, including unselected ones; host/user identity declarations and standard service paths excluded. min(4,8)=4: above2 for home/context-aware paths, below5 uniform expected variation. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":8,"distinct_leaks":3}}
```

### R
Scope: existing §4 Ghostty. Pros: terminal settings/bindings are complete and use standard HM/Ghostty only (`modules/apps/ghostty.nix:3`, `modules/apps/ghostty.nix:18`). Cons: a consumer rebinds the apps namespace and documents the preset; no substantial external consumer tutorial (`modules/apps/ghostty.nix:2`, `flake.nix:2`). Literal5 gradeB; font/theme defaults are ordinary opinions, not an S defect. Score **5**; confidence **medium**.

### P
Scope: desktop/WSL and standalone home boundaries. Pros: WSL explicitly imports its module and selects a small system set (`modules/hosts/void.nix:11`, `modules/hosts/void.nix:20`). Cons: selected ssh feature spells homeManger rather than homeManager (`modules/system/ssh.nix:3`); selected locale places OS keys directly at aspect root (`modules/system/locale.nix:2`). Interpolated3: useful actual WSL split, but these class envelopes do not deliver their intended settings; no eval-success/failure claim. Score **3**; confidence **medium**.

### L
Scope: tracked project entry and source comments, excluding vendored Anime4K documentation. Pros: battery comments explain their purpose (`modules/defaults.nix:64`). Cons: no root README or project Markdown authoring guide in inventory; entry merely imports modules (`flake.nix:2`). Literal1 absent project documentation, despite useful scattered comments. Score **1**; confidence **medium**.

### V
Scope: root outputs and feature definitions. Pros: configs and inputs are explicit (`flake.nix:2`, `modules/hosts/argos.nix:7`). Cons: no relevant semantic checks/CI found in inspected authored tree; native MPV comments are usage advice, not check invocation (`modules/apps/mpv/mpv.conf:1`). Literal2, passing status unknown. Score **2**; confidence **medium**.

### O
Scope: rebuild helpers and host/user setup. Pros: NH and Fish expose rebuild commands (`modules/shell/nh.nix:14`, `modules/shell/fish.nix:26`). Cons: these point to local checkout conventions, with no Den-derived deployment/provisioning inventory (`modules/shell/nh.nix:16`). Literal2 manual activation; not a requirement to add fleet machinery. Score **2**; confidence **medium**.

### X
Scope: OS/home and container settings. Pros: OCI audiobookshelf configuration is explicit (`modules/containers/audiobookshelf.nix:10`). Cons: it is standard NixOS container configuration, not a non-host Den target class (`modules/containers/audiobookshelf.nix:2`); WSL is a host platform. Baseline2. Score **2**; confidence **medium**.

### B
Scope: enabled census diversity plus complete application references, including unselected live definitions. Pros: Ghostty/Kitty include real settings, MPV supplies native configuration and tracked shader/font assets (`modules/apps/mpv/mpv.nix:24`, `modules/apps/mpv/mpv.conf:11`). Cons: bare enables/package bundles, identity-bound Fish/Nu/Git/virt, multi-app utils, Yazi missing epy runtime, and Niri without its DMS module import are excluded (`modules/shell/yazi.nix:51`, `modules/desktop/niri.nix:24`). Fontconfig has real rendering defaults, unlike a package-only font list (`modules/system/fonts.nix:9`). Score **5**; confidence **medium**.
B_div: 6.0 points → 5; B_ref: 7 units → 5; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":6.0,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"apps/ghostty","evidence":"modules/apps/ghostty.nix:2"},{"name":"apps/kitty","evidence":"modules/apps/kitty.nix:2"},{"name":"apps/mpv","evidence":"modules/apps/mpv/mpv.nix:2"},{"name":"desktop/hyprland","evidence":"modules/desktop/hyprland.nix:3"},{"name":"system/fonts","evidence":"modules/system/fonts.nix:2"},{"name":"system/podman","evidence":"modules/system/podman.nix:2"},{"name":"system/systemd-boot","evidence":"modules/system/systemd-boot.nix:2"}]}}
```

Total: **34.0/100**. Shortlists: showcase false; library_units ['ghostty']; starter false.

Overall pros:
- Feature names make selection readable (`modules/hosts/argos.nix:39`).
- Small WSL composition is explicit (`modules/hosts/void.nix:20`).
- Ghostty is a complete substantive terminal preset (`modules/apps/ghostty.nix:18`).

Overall cons / limits:
- SSH home-class typo (§6a P; `modules/system/ssh.nix:3`).
- Locale keys lack OS class envelope (§6a P; `modules/system/locale.nix:2`).
- Shell paths/identity need shared settings (§6a S; `modules/shell/nushell.nix:8`).
- No project entry guide (L scope; `flake.nix:2`).

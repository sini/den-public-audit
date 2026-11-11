---
title: "talarys/den"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/talarys/den/)

- Upstream: [talarys/den](https://github.com/talarys/den)
- Reviewed revision: [`469df2c2de88`](https://github.com/talarys/den/commit/469df2c2de88614d17a0f557cb19eaaa18ed0415)
- Author: talarys
- Score: **34.0 / 100**, rank 95 of 101 ranked configs. D 2 · I 8 · S 4 · R 5 · P 3 · L 1 · V 2 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: D direct settings; I distinct feature branches; S three grouped adaptations/partial path contract; R Ghostty B; P class-envelope defects; L no project guide; V no semantic checks; O manual helpers; X standard targets; B census+seven complete units.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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

Flake-parts/import-tree loads den and feature branches grouped under apps, shell, system and desktop ([`flake.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/flake.nix#L2), [`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2)). Two explicit hosts include a WSL machine and a desktop-style system ([`modules/hosts/void.nix:7`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L7), [`modules/hosts/argos.nix:7`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L7)).


## 2. Common patterns.

- angle-bracket refs: __findFile is provided by den and features are selected by path ([`modules/den.nix:5`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/den.nix#L5), [`modules/hosts/argos.nix:39`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L39)).
- den.default includes: primary-user, hostname and host-aspects establish global conventions ([`modules/defaults.nix:63`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/defaults.nix#L63)).
- provides tree: nested apps branch contains terminal aspects ([`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2)).


## 3. Novel patterns.

One host combines WSL import and desktop integration while reusing only selected shared system aspects ([`modules/hosts/void.nix:11`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L11), [`modules/hosts/void.nix:20`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L20)).


## 4. Library candidates.

- ghostty · [`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2) · terminal appearance and split/navigation bindings · HM and Ghostty package · none · B: expose font/theme choices and lift from apps namespace.


## 5. den friction.

No verified den-specific workaround in the inspected integration and defaults ([`modules/den.nix:5`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/den.nix#L5), [`modules/defaults.nix:63`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/defaults.nix#L63)).


## 6. Docs and complexity.

Docs 2: defaults explain the roles of each battery inline ([`modules/defaults.nix:64`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/defaults.nix#L64)); host composition is readable but hardware-local ([`modules/hosts/argos.nix:26`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L26)). Complexity 3: shared hierarchical features combine WSL and full desktop hosts ([`modules/hosts/void.nix:11`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L11), [`modules/hosts/argos.nix:39`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L39)).


## 6a. Defects and scoring notes.

- S · moderate: shared shells fix author home/checkout paths; Git/virt share author identity, and container timezone is fixed. Three grouped adaptations are enumerated in S card ([`modules/shell/nushell.nix:8`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nushell.nix#L8), [`modules/shell/fish.nix:26`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/fish.nix#L26), [`modules/shell/git.nix:18`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/git.nix#L18), [`modules/containers/audiobookshelf.nix:15`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/containers/audiobookshelf.nix#L15)).
- P · moderate: selected ssh uses homeManger and selected locale puts i18n/time directly on the aspect instead of nixos ([`modules/system/ssh.nix:3`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/ssh.nix#L3), [`modules/system/locale.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/locale.nix#L2), [`modules/hosts/argos.nix:43`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L43), [`modules/hosts/argos.nix:44`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L44)).
Ghostty font/theme are ordinary overrideable preset choices, and global Disko has no verified WSL defect; neither is deducted.

## 7. Template notes.

Useful angle-reference example, but remove hardcoded disk identifiers and explain branch hierarchy for beginners ([`modules/hosts/argos.nix:26`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L26), [`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2)).

## 8. Scorecard.

### D
Scope: hosts, defaults and app branches. Pros: shared feature selection is visible ([`modules/hosts/argos.nix:39`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L39), [`modules/users/talarys.nix:9`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/users/talarys.nix#L9)). Cons: inspected features directly set application values; flavor/accent arguments are local preset variation, not a routed fact channel ([`modules/desktop/catppuccin.nix:5`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/desktop/catppuccin.nix#L5)). Literal2; no deduction for a small fleet. Score **2**; confidence **medium**.

### I
Scope: apps/shell/system/desktop feature branches. Pros: names and class arms localize applications ([`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2), [`modules/system/podman.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/podman.nix#L2)). Cons: utils combines several independently configurable tools ([`modules/shell/utils.nix:5`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/utils.nix#L5)); this is a bounded layout ceiling, not a new defect. Interpolated8: clean ownership beyond5, some broad bundles below9. Score **8**; confidence **medium**.

### S
Scope: reusable shell/desktop/container settings. Pros: Catppuccin exposes flavor/accent arguments and ordinary HM application settings remain overrideable ([`modules/desktop/catppuccin.nix:5`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/desktop/catppuccin.nix#L5), [`modules/apps/ghostty.nix:8`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L8)). Cons: contract4: derived-home NH path helps but other shells fix the author checkout/home ([`modules/shell/nh.nix:16`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nh.nix#L16), [`modules/shell/fish.nix:26`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/fish.nix#L26), [`modules/shell/nushell.nix:8`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nushell.nix#L8)). Coverage8 for three grouped changes: owner identity/home paths including Git and virt account; checkout root (NH/fish name disagreement grouped once); household timezone ([`modules/shell/git.nix:18`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/git.nix#L18), [`modules/system/virt.nix:8`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/virt.nix#L8), [`modules/containers/audiobookshelf.nix:15`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/containers/audiobookshelf.nix#L15)). These are shared definitions, including unselected ones; host/user identity declarations and standard service paths excluded. min(4,8)=4: above2 for home/context-aware paths, below5 uniform expected variation. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":8,"distinct_leaks":3}}
```

### R
Scope: existing §4 Ghostty. Pros: terminal settings/bindings are complete and use standard HM/Ghostty only ([`modules/apps/ghostty.nix:3`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L3), [`modules/apps/ghostty.nix:18`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L18)). Cons: a consumer rebinds the apps namespace and documents the preset; no substantial external consumer tutorial ([`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2), [`flake.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/flake.nix#L2)). Literal5 gradeB; font/theme defaults are ordinary opinions, not an S defect. Score **5**; confidence **medium**.

### P
Scope: desktop/WSL and standalone home boundaries. Pros: WSL explicitly imports its module and selects a small system set ([`modules/hosts/void.nix:11`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L11), [`modules/hosts/void.nix:20`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L20)). Cons: selected ssh feature spells homeManger rather than homeManager ([`modules/system/ssh.nix:3`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/ssh.nix#L3)); selected locale places OS keys directly at aspect root ([`modules/system/locale.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/locale.nix#L2)). Interpolated3: useful actual WSL split, but these class envelopes do not deliver their intended settings; no eval-success/failure claim. Score **3**; confidence **medium**.

### L
Scope: tracked project entry and source comments, excluding vendored Anime4K documentation. Pros: battery comments explain their purpose ([`modules/defaults.nix:64`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/defaults.nix#L64)). Cons: no root README or project Markdown authoring guide in inventory; entry merely imports modules ([`flake.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/flake.nix#L2)). Literal1 absent project documentation, despite useful scattered comments. Score **1**; confidence **medium**.

### V
Scope: root outputs and feature definitions. Pros: configs and inputs are explicit ([`flake.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/flake.nix#L2), [`modules/hosts/argos.nix:7`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L7)). Cons: no relevant semantic checks/CI found in inspected authored tree; native MPV comments are usage advice, not check invocation ([`modules/apps/mpv/mpv.conf:1`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/mpv/mpv.conf#L1)). Literal2, passing status unknown. Score **2**; confidence **medium**.

### O
Scope: rebuild helpers and host/user setup. Pros: NH and Fish expose rebuild commands ([`modules/shell/nh.nix:14`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nh.nix#L14), [`modules/shell/fish.nix:26`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/fish.nix#L26)). Cons: these point to local checkout conventions, with no Den-derived deployment/provisioning inventory ([`modules/shell/nh.nix:16`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nh.nix#L16)). Literal2 manual activation; not a requirement to add fleet machinery. Score **2**; confidence **medium**.

### X
Scope: OS/home and container settings. Pros: OCI audiobookshelf configuration is explicit ([`modules/containers/audiobookshelf.nix:10`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/containers/audiobookshelf.nix#L10)). Cons: it is standard NixOS container configuration, not a non-host Den target class ([`modules/containers/audiobookshelf.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/containers/audiobookshelf.nix#L2)); WSL is a host platform. Baseline2. Score **2**; confidence **medium**.

### B
Scope: enabled census diversity plus complete application references, including unselected live definitions. Pros: Ghostty/Kitty include real settings, MPV supplies native configuration and tracked shader/font assets ([`modules/apps/mpv/mpv.nix:24`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/mpv/mpv.nix#L24), [`modules/apps/mpv/mpv.conf:11`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/mpv/mpv.conf#L11)). Cons: bare enables/package bundles, identity-bound Fish/Nu/Git/virt, multi-app utils, Yazi missing epy runtime, and Niri without its DMS module import are excluded ([`modules/shell/yazi.nix:51`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/yazi.nix#L51), [`modules/desktop/niri.nix:24`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/desktop/niri.nix#L24)). Fontconfig has real rendering defaults, unlike a package-only font list ([`modules/system/fonts.nix:9`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/fonts.nix#L9)). Score **5**; confidence **medium**.
B_div: 6.0 points → 5; B_ref: 7 units → 5; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":6.0,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"apps/ghostty","evidence":"modules/apps/ghostty.nix:2"},{"name":"apps/kitty","evidence":"modules/apps/kitty.nix:2"},{"name":"apps/mpv","evidence":"modules/apps/mpv/mpv.nix:2"},{"name":"desktop/hyprland","evidence":"modules/desktop/hyprland.nix:3"},{"name":"system/fonts","evidence":"modules/system/fonts.nix:2"},{"name":"system/podman","evidence":"modules/system/podman.nix:2"},{"name":"system/systemd-boot","evidence":"modules/system/systemd-boot.nix:2"}]}}
```

Total: **34.0/100**. Shortlists: showcase false; library_units ['ghostty']; starter false.

Overall pros:
- Feature names make selection readable ([`modules/hosts/argos.nix:39`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/argos.nix#L39)).
- Small WSL composition is explicit ([`modules/hosts/void.nix:20`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L20)).
- Ghostty is a complete substantive terminal preset ([`modules/apps/ghostty.nix:18`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L18)).

Overall cons / limits:
- SSH home-class typo (§6a P; [`modules/system/ssh.nix:3`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/ssh.nix#L3)).
- Locale keys lack OS class envelope (§6a P; [`modules/system/locale.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/system/locale.nix#L2)).
- Shell paths/identity need shared settings (§6a S; [`modules/shell/nushell.nix:8`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/shell/nushell.nix#L8)).
- No project entry guide (L scope; [`flake.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/flake.nix#L2)).

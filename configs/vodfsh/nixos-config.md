# vodfsh/nixos-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/vodfsh/nixos-config.md)

- Upstream: [vodfsh/nixos-config](https://github.com/vodfsh/nixos-config)
- Reviewed revision: [`a0ff916b0b31`](https://github.com/vodfsh/nixos-config/commit/a0ff916b0b31a66554323355f9557b7e4c223eff)
- Author: vodfsh
- Score: **36.0 / 100**, rank 92 of 101 ranked configs. D 3 · I 5 · S 3 · R 5 · P 5 · L 2 · V 2 · O 4 · B 4 · X 2. Shortlists: —.
- Summary: D OS stateVersion projection only; I broad profiles; S fixed checkout/account paths; R reusable Zsh/Kitty presets; P honest Linux scope; L operations-only guide; V manual VM recipe; O Den-derived nh targets; B three complete presets; X standard hosts/packages.

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

A small explicit entity inventory includes OS hosts and a standalone home ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6), [`modules/entities.nix:7`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L7)). Defaults and user schema are separate ([`modules/defaults.nix:3`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/defaults.nix#L3), [`modules/schema.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/schema.nix#L9)).

## 2. Common patterns

- define-user+primary-user in user aspect ([`modules/users/vodfsh.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L9)).
- host-aspects projects host settings to the user ([`modules/users/vodfsh.nix:11`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L11)).

## 3. Novel patterns

The same identity has an integrated host and a standalone home entry ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6), [`modules/entities.nix:7`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L7)).

## 4. Library candidates

None verified as a useful independent library unit in the reviewed composition.

## 5. den friction

No verified Den-specific friction in the reviewed entity declarations ([`modules/entities.nix:4`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L4)).

## 6. Docs and complexity

Docs 2: README focuses on build/VM commands ([`README.md:5`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L5), [`README.md:19`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L19)). Complexity 2: short host/home inventory and conventional batteries ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6), [`modules/users/vodfsh.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L9)).

## 6a. Defects and scoring notes

- S · moderate: shared common/audio/workstation aspects fix the checkout root, music project and earlyoom account rather than exposing their variation ([`modules/aspects/common/common.nix:33`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/common/common.nix#L33), [`modules/aspects/profiles/audio.nix:71`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/audio.nix#L71), [`modules/aspects/profiles/workstation.nix:95`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/workstation.nix#L95)).
- L · minor: README VM link targets modules/hosts/run-test-vm.nix, but the real launcher lives in modules/hosts/test-vm.nix ([`README.md:21`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L21), [`modules/hosts/test-vm.nix:1`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L1)).
- Final pass drops repeated define-user selection as a deduction: duplicate battery selection alone establishes no consumer-impact defect ([`modules/defaults.nix:5`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/defaults.nix#L5), [`modules/users/vodfsh.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L9)).

## 7. Template notes

Compact host/home contrast; inventory comments help locate configuration ([`modules/entities.nix:1`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L1)), but README gives limited architecture guidance ([`README.md:5`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L5)).

## 8. Scorecard

### D (3, medium)
Scope: entity inventory, user/stateVersion and output wiring. Pros: integrated users derive home stateVersion from the OS configuration ([`modules/users/vodfsh.nix:30`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L30)); host/home inventory is explicit ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6)). Cons: this is one narrow context projection, not structured application facts or quirk routing; package overlays are build plumbing ([`modules/flake/outputs.nix:31`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/flake/outputs.nix#L31)). Interpolation 3 above direct-setting 2, below useful shared fact-channel 5. Confidence: medium.

### I (5, medium)
Scope: all feature/profile/host modules. Pros: common, user schema and concrete host files are separated ([`modules/defaults.nix:3`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/defaults.nix#L3), [`modules/schema.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/schema.nix#L9), [`modules/hosts/home/home.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/home/home.nix#L6)). Cons: workstation combines fonts, desktop, media and applications in one selectable boundary ([`modules/aspects/profiles/workstation.nix:12`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/workstation.nix#L12), [`modules/aspects/profiles/workstation.nix:153`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/workstation.nix#L153)). Anchor 5: named features localize edits but broad profiles remain. Confidence: medium.

### S (3, medium)
Scope: shared common/profile/user bodies. Pros: homeDirectory/XDG-derived Zsh paths and native options permit local overrides ([`modules/aspects/zsh.nix:41`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L41)). Cons: shared checkout root, audio project and earlyoom user remain constants (§6a, [`modules/aspects/common/common.nix:33`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/common/common.nix#L33), [`modules/aspects/profiles/audio.nix:71`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/audio.nix#L71), [`modules/aspects/profiles/workstation.nix:95`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/workstation.nix#L95)). Three grouped leaks (checkout root, music-project root, account identity), raw ≥3. Contract 3: native options exist, but author variation still edits implementation; above wholly fixed 2, below mostly explicit 5. Coverage 8 (no cap at ≤3); min(3,8)=3. Confidence: medium.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":8,"distinct_leaks":3,"raw_leaks":3}}
```

### R (5, medium)
Scope: independent Kitty and Zsh definitions. Pros: Kitty owns settings/keybindings, and Zsh owns plugins/integration without author identity ([`modules/aspects/kitty.nix:3`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/kitty.nix#L3), [`modules/aspects/zsh.nix:30`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L30)). Cons: no exported independent aspect/minimal consumer example in inspected entry ([`flake.nix:4`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/flake.nix#L4)); profiles also assume custom package overlays ([`modules/aspects/profiles/audio.nix:65`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/audio.nix#L65)). Anchor 5 for useful light-extraction presets; S constants are not charged again. Confidence: medium.

### P (5, medium)
Scope: Linux hosts plus declared home and class arguments. Pros: NixOS hardware stays in concrete hosts ([`modules/hosts/nautilus/nautilus.nix:26`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/nautilus/nautilus.nix#L26)); HM schema is explicit ([`modules/schema.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/schema.nix#L9)). Cons: user home body requests osConfig, so independent-home reachability depends on context delivery rather than a documented standalone boundary ([`modules/users/vodfsh.nix:17`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L17)). No claim of evaluated parity or failure. Anchor 5 for narrow Linux support; unresolved context is a scope limit, not invented defect. Confidence: medium.

### L (2, medium)
Scope: README and module comments. Pros: run/build/switch and VM commands are visible ([`README.md:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L9), [`modules/hosts/test-vm.nix:1`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L1)). Cons: architecture/adaptation path is unexplained, and the VM link points to a nonexistent filename (§6a, [`README.md:21`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L21)). Operations-only anchor 2. Confidence: medium.

### V (2, medium)
Scope: full module/check/workflow inventory and VM wrapper. Pros: a manual test-VM command can exercise the shared profile ([`modules/hosts/test-vm.nix:33`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L33)). Cons: no authored assertions/expected behavior or relevant CI invocation was found; it is a launch recipe, not a test suite ([`modules/hosts/test-vm.nix:36`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L36)). Baseline 2, no pass asserted. Confidence: medium.

### O (4, medium)
Scope: nh builder apps and VM launcher. Pros: nh target packages use Den inventory-aware helper ([`modules/nh.nix:1`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/nh.nix#L1), [`modules/nh.nix:7`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/nh.nix#L7)), rather than a hand-maintained app per host. Cons: no demonstrated deploy/provisioning/secret lifecycle derives from the model; account/bootstrap remains explicit user setup ([`modules/users/vodfsh.nix:33`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/users/vodfsh.nix#L33)). Interpolation 4: generated operational entry points exceed manual baseline 2 but do not implement a full provisioning concern at 5. Confidence: medium.

### B (4, medium)
Scope: every authored aspect/profile, including unselected definitions. Pros: Kitty, Zsh and the gaming integration have coherent presets ([`modules/aspects/kitty.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/kitty.nix#L6), [`modules/aspects/zsh.nix:64`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L64), [`modules/aspects/profiles/gaming.nix:8`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/gaming.nix#L8)). Cons: broad common/workstation/development profiles, token toggles and package lists add no separate references; audio depends on pkgs.my and a personal project ([`modules/aspects/profiles/audio.nix:65`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/audio.nix#L65), [`modules/aspects/profiles/audio.nix:71`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/audio.nix#L71)). Census maximum-depth total 4 → diversity 3; three complete units → reference 4; mean 3.5 rounds up to B4. Confidence: medium.
```score-evidence
{"B":{"diversity_points":4.0,"diversity_grade":3,"reference_grade":4,"reference_units":[{"name":"kitty","evidence":"modules/aspects/kitty.nix:3"},{"name":"zsh","evidence":"modules/aspects/zsh.nix:30"},{"name":"gaming","evidence":"modules/aspects/profiles/gaming.nix:8"}]}}
```

### X (2, medium)
Scope: classes, custom packages and VM output. Pros: ordinary NixOS and HM targets are explicit ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6), [`modules/schema.nix:9`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/schema.nix#L9)). Cons: the VM is a standard NixOS build and packages are normal per-system outputs ([`modules/hosts/test-vm.nix:36`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/hosts/test-vm.nix#L36), [`modules/flake/outputs.nix:15`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/flake/outputs.nix#L15)), not distinct non-host classes. Baseline 2. Confidence: medium.

Total: **36.0/100**. Shortlists: showcase no; library_units none; starter no. No routed showcase, curated independent library nomination or sufficiently explained starter path; the complete shell/terminal presets remain discoverable in B.

Overall pros:
- Explicit inventory separates host and home outputs ([`modules/entities.nix:6`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L6)).
- Zsh integrates completion/plugins and Starship coherently ([`modules/aspects/zsh.nix:30`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L30), [`modules/aspects/zsh.nix:96`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/zsh.nix#L96)).
- Den-backed nh helper avoids separate app declarations ([`modules/nh.nix:7`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/nh.nix#L7)).

Overall cons / limits:
- S: shared checkout location is fixed ([`modules/aspects/common/common.nix:33`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/common/common.nix#L33)).
- I scope: workstation is a broad combined desktop profile ([`modules/aspects/profiles/workstation.nix:12`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/aspects/profiles/workstation.nix#L12)).
- L: VM documentation links to the wrong file ([`README.md:21`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/README.md#L21)).

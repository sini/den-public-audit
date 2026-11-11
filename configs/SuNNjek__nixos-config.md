# SuNNjek__nixos-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/SuNNjek__nixos-config.md)

- Upstream: [SuNNjek/nixos-config](https://github.com/SuNNjek/nixos-config)
- Reviewed revision: [`f40297e9d045`](https://github.com/SuNNjek/nixos-config/commit/f40297e9d045387227869245163e7e2b6c7799f9)
- Author: SuNNjek
- Score: **50.5 / 100**, rank 48 of 103 ranked configs. D 6 · I 9 · S 5 · R 5 · P 5 · L 2 · V 5 · O 5 · B 4 · X 2. Shortlists: library units (1).
- Summary: D real Nemo quirk with shallow merge collision; I feature ownership; S useful KDL/disk/locale interfaces; R simple battery; P honest Linux; L stale install guide; V native validator; O derived VM/NH; X standard; B nine presets.

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

Dendritic flake-file modules and import-tree load workstation features for two hosts (`flake.nix:4`, `modules/dendritic.nix:3`, `modules/hosts.nix:4`). Defaults enable HM, reciprocal providers and host-aspects globally (`modules/defaults.nix:7`).


## 2. Common patterns.

- mutual-provider: user schema enables the battery (`modules/defaults.nix:9`).
- den.default includes: hostname, host-aspects and overlays are shared (`modules/defaults.nix:12`).
- parametric aspect (fn args): a local battery creates group membership aspects (`modules/batteries/add-user-to-group.nix:7`).


## 3. Novel patterns.

VM launchers are derived from each generated nixosConfiguration, keeping VM wrappers synchronized with host outputs (`modules/vm.nix:26`).


## 4. Library candidates.

- add-user-to-group · `modules/batteries/add-user-to-group.nix:7` · adds a group to the current user through NixOS · den/NixOS · fn args (group plus user scope) · A: independent small battery.


## 5. den friction.

Local add-user-to-group writes nixos.users.users directly instead of the user class (`modules/batteries/add-user-to-group.nix:10`); usable but Linux-specific battery duplication signal.


## 6. Docs and complexity.

Docs 2: README gives installation steps but points to a hosts/ hierarchy and manual flake edits (`README.md:9`) while actual hosts are in modules/hosts.nix (`modules/hosts.nix:4`). Complexity 3: two machines, shared providers and custom VM launchers (`modules/hosts.nix:4`, `modules/vm.nix:26`).


## 6a. Defects and scoring notes.

- D · moderate: shallow mergeAttrsList overwrites the whole actions attribute when desktop and development both contribute, rather than retaining both action names (`modules/aspects/nemo.nix:21`, `modules/aspects/desktop.nix:97`, `modules/aspects/development.nix:69`).
- L · moderate: README new-host instructions contradict modules inventory/generated flake (`README.md:9`, `README.md:10`, `modules/hosts.nix:4`, `flake.nix:1`).
- S · minor: shared monitor topology and greeter keyboard are fixed rather than parameterized (`modules/aspects/kanshi.nix:5`, `modules/aspects/dux.nix:64`).
The NixOS-specific membership battery is honest scope, not a defect.

## 7. Template notes.

Teaches feature reuse and VM iteration, but correct onboarding paths and explain the custom batteries (`README.md:9`, `modules/vm.nix:1`).

## 8. Scorecard.

### D
Scope: Nemo action quirk producer/collector/consumer. Pros: desktop emits MediaInfo action and development emits VSCode action, collected through declared nemo quirk into generated INI files (`modules/aspects/desktop.nix:97`, `modules/aspects/development.nix:69`, `modules/aspects/nemo.nix:2`, `modules/aspects/nemo.nix:31`). Cons: mergeAttrsList is shallow, so two actions attrsets overwrite rather than combine; both producers are selected (`modules/aspects/nemo.nix:21`, `modules/robin-pc.nix:14`, `modules/robin-pc.nix:23`). Interpolated6 for live routed quirk beyond5, collision loss prevents stronger routing. Score **6**; confidence **medium**.

### I
Scope: aspects, providers and thin host lists. Pros: desktop/media/development feature owners and compositor bindings/rules are separate (`modules/aspects/desktop.nix:3`, `modules/aspects/niri/niri.nix:7`, `modules/robin-thinkpad.nix:8`). Cons: no additional concrete isolation defect verified; host lists intentionally select different hardware/features. Literal9 for ownership, not file count. Score **9**; confidence **medium**.

### S
Scope: useful local configuration contracts. Pros: typed KDL module, action records, rootDrive disk argument and parameterized locale helper (`modules/aspects/niri/_hm.nix:16`, `modules/aspects/nemo.nix:21`, `modules/aspects/disko/btrfs.nix:6`, `modules/aspects/locales.nix:2`). Contract5: useful explicit variation but some plain/untyped records and globals. Cons: two shared adaptation groups: monitor topology and German greeter keyboard (`modules/aspects/kanshi.nix:5`, `modules/aspects/dux.nix:64`). Named locale-de is an explicit preset, owner identity stays in named user. Coverage8 for <=3 grouped leaks; min(5,8)=5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":8,"distinct_leaks":2}}
```

### R
Scope: small batteries and app presets. Pros: add-user-to-group takes one parameter and derives current account; Kitty and PipeWire are independent (`modules/batteries/add-user-to-group.nix:7`, `modules/aspects/kitty.nix:4`, `modules/aspects/pipewire.nix:4`). Cons: no worked second consumer; compositor bundles depend on separately selected desktop/Dux/runtime settings (`modules/aspects/niri/binds.nix:369`, `modules/aspects/hyprland/binds.nix:31`). Literal5 useful extraction, not9 packaged documented A example. Score **5**; confidence **medium**.

### P
Scope: intentionally Linux/NixOS HM. Pros: group helper explicitly writes NixOS, while terminal config uses HM (`modules/batteries/add-user-to-group.nix:11`, `modules/aspects/kitty.nix:3`). Cons: no standalone or Darwin boundary guarantee claimed. Literal5: narrow honest support; the Linux-only group helper is not a portability defect by itself. Score **5**; confidence **medium**.

### L
Scope: installation README and inline authoring hints. Pros: explains install.sh host argument (`README.md:14`), source comments identify inventory (`modules/hosts.nix:1`). Cons: directs new hosts into a nonexistent hosts hierarchy/manual generated-flake edit (`README.md:9`, `README.md:10`, `flake.nix:1`). Literal2 stale onboarding rather than reliable worked authoring. Score **2**; confidence **medium**.

### V
Scope: generated config validation. Pros: custom Niri HM config runs niri validate in writeTextFile checkPhase (`modules/aspects/niri/_hm.nix:61`, `modules/aspects/niri/_hm.nix:65`). Cons: no multi-producer Nemo collision fixture; VM helper is manual iteration, not a passing test (`modules/aspects/nemo.nix:21`, `modules/vm.nix:1`). Literal5 relevant structural validation, no execution performed. Score **5**; confidence **medium**.

### O
Scope: inventory-derived operator artifacts. Pros: VM launchers map actual nixosConfigurations and NH denPackages derives host/home wrappers (`modules/vm.nix:26`, `modules/vm.nix:40`, `modules/nh.nix:7`). Cons: no deploy/builder/secret orchestration or rollback flow verified. Literal5 useful derived operation, not9 full operational system. Score **5**; confidence **medium**.

### X
Scope: standard NixOS/HM plus VM launchers. Pros: custom HM Niri config is real module work (`modules/aspects/niri/_hm.nix:12`). Cons: it remains an HM program; ordinary NixOS VM wrapper is O, not custom microvm target class (`modules/vm.nix:36`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: selected census max depth and coherent reference units. Pros: Firefox policies/native messaging, Kitty settings/terminal integration, Vesktop owned autostart, Nemo generator and other listed presets have real behavior (`modules/aspects/firefox.nix:8`, `modules/aspects/kitty.nix:21`, `modules/aspects/vesktop.nix:6`). Cons: enable-only apps, multi-app development/desktop bundles, fleet monitor presets, compositor external Kitty/Firefox/DMS dependencies and Matugen provider fragments excluded (`modules/aspects/development.nix:65`, `modules/aspects/kanshi.nix:5`, `modules/aspects/hyprland/binds.nix:31`, `modules/aspects/niri/binds.nix:369`). Nemo collision charged D, standard empty collector contract is still a complete unit. Score **4**; confidence **medium**.
B_div: 3.5 points → 3; B_ref: 9 units → 5; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":3.5,"diversity_grade":3,"reference_grade":5,"reference_units":[{"name":"nemo","evidence":"modules/aspects/nemo.nix:13"},{"name":"firefox","evidence":"modules/aspects/firefox.nix:8"},{"name":"fastfetch","evidence":"modules/aspects/fastfetch.nix:8"},{"name":"kitty","evidence":"modules/aspects/kitty.nix:6"},{"name":"gpg","evidence":"modules/aspects/gpg.nix:9"},{"name":"pipewire","evidence":"modules/aspects/pipewire.nix:4"},{"name":"plymouth","evidence":"modules/aspects/plymouth.nix:5"},{"name":"vesktop","evidence":"modules/aspects/vesktop.nix:6"},{"name":"limine","evidence":"modules/aspects/limine.nix:6"}]}}
```

Total: **50.5/100**. Shortlists: showcase false; library_units ['add-user-to-group']; starter false.

Overall pros:
- Real Nemo action producer-to-generator flow (`modules/aspects/nemo.nix:31`).
- Niri output has native build-time validation (`modules/aspects/niri/_hm.nix:65`).
- VM and NH tools follow generated inventory (`modules/vm.nix:40`, `modules/nh.nix:7`).

Overall cons / limits:
- Shallow action merge loses contributions (§6a D; `modules/aspects/nemo.nix:21`).
- New-host directions are stale (§6a L; `README.md:9`).
- Monitor assumptions remain in shared profiles (§6a S; `modules/aspects/kanshi.nix:5`).

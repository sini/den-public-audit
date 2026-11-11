---
title: "oxce5/chimera"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/oxce5/chimera/)

- Upstream: [oxce5/chimera](https://github.com/oxce5/chimera)
- Reviewed revision: [`cc96a65abd5d`](https://github.com/oxce5/chimera/commit/cc96a65abd5df81cdf2c8829ddff64111d616027)
- Author: oxce5
- Score: **47.5 / 100**, rank 61 of 101 ranked configs. D 5 · I 8 · S 6 · R 5 · P 5 · L 5 · V 3 · O 2 · B 4 · X 2. Shortlists: library units (1).
- Summary: Typed direct display derivation D5; central roles I8; S typed interfaces/nine adaptations; standalone NVF reference; Linux role scope; bundled docs L5; stale CI V3; O/X baseline.

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

Flake-parts/import-tree exposes a chimera namespace and separate host and user role bundles ([`flake.nix:3`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/flake.nix#L3), [`modules/den.nix:15`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/den.nix#L15), [`modules/assignments.nix:6`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L6)). A single assignments module joins entities to roles ([`modules/assignments.nix:114`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L114)).


## 2. Common patterns.

- namespace + angle-bracket refs: chimera is registered and referenced by feature path ([`modules/den.nix:7`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/den.nix#L7), [`modules/den.nix:15`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/den.nix#L15), [`modules/assignments.nix:10`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L10)).
- mutual-provider: user schema enables the battery ([`modules/den.nix:9`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/den.nix#L9)).
- provides tree: VM host contributes an additional feature to its users ([`modules/assignments.nix:131`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L131)).
- define-user+primary-user: defaults define users and individual user bundles select primary-user ([`modules/default.nix:8`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/default.nix#L8), [`modules/assignments.nix:136`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L136)).


## 3. Novel patterns.

Host roles and user roles deliberately include separate class halves; VM users explicitly receive HM content that would be inert in host scope ([`modules/assignments.nix:32`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L32), [`modules/assignments.nix:108`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L108)).


## 4. Library candidates.

- privileged-user · [`modules/groups.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/groups.nix#L2) · maps configurable privileged groups into current user membership · den/NixOS · fn args (user), options (users.privilegedGroups) · B: namespace-lift and document group ownership.


## 5. den friction.

Role comments explicitly describe host-role HM content as inert and repeat selected aspects on the user side ([`modules/assignments.nix:102`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L102)); this is a teaching/ergonomics signal for class routing.


## 6. Docs and complexity.

Docs 2: README lists framework links without a walkthrough ([`README.md:4`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/README.md#L4)); assignments comments explain host/user role boundaries ([`modules/assignments.nix:6`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L6), [`modules/assignments.nix:47`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L47)). Complexity 4: namespace roles, providers, VM storage and user routing compose a broad configuration ([`modules/assignments.nix:30`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L30), [`modules/assignments.nix:95`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L95)).


## 6a. Defects and scoring notes.

- V · moderate: host CI matrix targets desktop/vm, absent from declared overlord/machina-mori inventory ([`.github/workflows/flake.yml:53`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/.github/workflows/flake.yml#L53), [`.github/workflows/flake.yml:55`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/.github/workflows/flake.yml#L55), [`modules/hosts/overlord/default.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/hosts/overlord/default.nix#L2), [`modules/hosts/machina-mori/default.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/hosts/machina-mori/default.nix#L2)).
- S · minor: nine shared adaptation groups enumerated in S remain outside entities ([`modules/programs/git.nix:23`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/git.nix#L23), [`modules/programs/nh.nix:12`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/nh.nix#L12), [`modules/services/syncthing.nix:8`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/services/syncthing.nix#L8), [`modules/storage.nix:14`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/storage.nix#L14)).
- R · minor: Yazi compression/opening calls ouch/plugin without owning installation, limiting copied unit completeness ([`modules/programs/yazi.nix:12`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/yazi.nix#L12), [`modules/programs/yazi.nix:19`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/yazi.nix#L19)).

## 7. Template notes.

Strong role-separation example once class routing is explained; its large security-tool/VM bundles make a heavy first template ([`modules/assignments.nix:30`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L30), [`modules/assignments.nix:95`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L95)).

## 8. Scorecard.

### D
Scope: typed displays and host/user role delivery. Pros: host display data produces compositor outputs; VM to-users provider delivers user feature ([`modules/toplevel/display-properties.nix:125`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L125), [`modules/desktops/niri/default.nix:55`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/desktops/niri/default.nix#L55), [`modules/assignments.nix:131`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L131)). Cons: these are schema/context derivation and named delivery, with no independent quirk/policy fact route verified ([`modules/den.nix:9`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/den.nix#L9)). Literal5 direct derivation cap. Score **5**; confidence **medium**.

### I
Scope: namespace and role ownership. Pros: assignments centrally connects named host/user roles, and app owners contain class halves ([`modules/assignments.nix:114`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L114), [`modules/programs/browsers/helium.nix:36`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/browsers/helium.nix#L36)). Cons: shared GUI bag also acquires NH and custom Blender wrapper, reducing independent selection ([`modules/programs/gui.nix:7`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/gui.nix#L7), [`modules/programs/nh.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/nh.nix#L2)). Score8 between5 mixed ownership and9 consistently independent concerns. Explicitly selecting class halves is not a duplication defect. Score **8**; confidence **medium**.

### S
Scope: display/extension contracts and shared author values. Pros: typed display geometry includes custom-mode/primary validation and maps directly to Niri; Helium CRX contract checks mutually exclusive sources ([`modules/toplevel/display-properties.nix:27`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L27), [`modules/toplevel/display-properties.nix:151`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L151), [`modules/toplevel/display-properties.nix:167`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L167), [`modules/programs/browsers/helium.nix:128`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/browsers/helium.nix#L128)). Contract7 useful domain interfaces beyond5. Cons: nine grouped adaptations remain: locale/timezone, owner identity, repo checkout root, bastion alias, persistence root, three Syncthing peer IDs, storage remote/account ([`modules/default.nix:33`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/default.nix#L33), [`modules/programs/git.nix:23`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/git.nix#L23), [`modules/programs/nh.nix:12`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/nh.nix#L12), [`modules/programs/fish.nix:21`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/fish.nix#L21), [`modules/impermanence.nix:30`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/impermanence.nix#L30), [`modules/services/syncthing.nix:8`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/services/syncthing.nix#L8), [`modules/services/syncthing.nix:16`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/services/syncthing.nix#L16), [`modules/services/syncthing.nix:20`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/services/syncthing.nix#L20), [`modules/storage.nix:14`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/storage.nix#L14)). Entity-owned physical displays excluded. Coverage6; min=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":9}}
```

### R
Scope: reusable app files and extraction. Pros: NVF base owns meaningful editor behavior and module import; privileged-user is a compact typed §4 candidate ([`modules/programs/neovim/default.nix:5`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L5), [`modules/programs/neovim/default.nix:26`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L26), [`modules/groups.nix:9`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/groups.nix#L9)). Cons: many application owners require a separate Niri schema or another unowned tool; Yazi invokes ouch but does not own installation ([`modules/desktops/vicinae.nix:7`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/desktops/vicinae.nix#L7), [`modules/programs/yazi.nix:19`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/yazi.nix#L19)). Literal5 useful reference with dependency repair, not9 polished library. Score **5**; confidence **medium**.

### P
Scope: two Linux host roles. Pros: VM/laptop get deliberately different storage/desktop roles and host-owned physical display data ([`modules/assignments.nix:20`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L20), [`modules/assignments.nix:30`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L30), [`modules/hosts/machina-mori/default.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/hosts/machina-mori/default.nix#L2)). Cons: generic display assertion mandates graphical outputs for every NixOS host, so scope is graphical fleet rather than arbitrary server ([`modules/toplevel/display-properties.nix:157`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L157)). Literal5 honest current boundary, no inherent narrow-support deduction. Score **5**; confidence **medium**.

### L
Scope: local role comments and bundled Den reference. Pros: comments teach host versus HM half routing; docs explain entity/class/context distinctions and include authoring examples ([`modules/assignments.nix:102`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L102), [`docs/den.md:45`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/docs/den.md#L45), [`docs/den.md:121`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/docs/den.md#L121)). Cons: README mainly links frameworks; long general reference does not replace a concise repo-specific host/role walkthrough ([`README.md:4`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/README.md#L4), [`modules/assignments.nix:114`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L114)). Literal5 orientation with examples, below9 complete local guide. Score **5**; confidence **medium**.

### V
Scope: workflow and declarative assertions. Pros: CI requests flake check; typed display and CRX checks encode negative cases ([`.github/workflows/flake.yml:43`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/.github/workflows/flake.yml#L43), [`modules/toplevel/display-properties.nix:167`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L167), [`modules/programs/browsers/helium.nix:131`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/browsers/helium.nix#L131)). Cons: host matrix names desktop/vm instead of declared overlord/machina-mori, so host smoke jobs address nonexistent outputs ([`.github/workflows/flake.yml:53`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/.github/workflows/flake.yml#L53), [`modules/hosts/overlord/default.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/hosts/overlord/default.nix#L2), [`modules/hosts/machina-mori/default.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/hosts/machina-mori/default.nix#L2)). Score3 above2 assertions present, below5 working structural host check route; no execution claimed. Score **3**; confidence **medium**.

### O
Scope: activation/persistence tools. Pros: preservation owns machine-id/SSH-state resources and NH configured ([`modules/impermanence.nix:30`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/impermanence.nix#L30), [`modules/programs/nh.nix:4`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/nh.nix#L4)). Cons: NH checkout path is literal and nixos-anywhere is a patched package export, not inventory-derived deployment ([`modules/programs/nh.nix:12`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/nh.nix#L12), [`modules/nixos-anywhere.nix:3`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/nixos-anywhere.nix#L3)). Baseline2 ordinary operational configuration. Score **2**; confidence **medium**.

### X
Scope: ordinary NixOS/HM app modules. Pros: NVF settings use upstream module and packaged Blender is real ([`modules/programs/neovim/default.nix:5`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L5), [`modules/programs/blender.nix:5`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/blender.nix#L5)). Cons: no distinct Den editor/custom nonhost class evaluation; package build/export is ordinary plumbing ([`modules/programs/blender.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/blender.nix#L2)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: complete independent presets and census max-depth. Pros: single counted NVF base file owns module import/options/autocmds/keymaps ([`modules/programs/neovim/default.nix:5`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L5), [`modules/programs/neovim/default.nix:98`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L98)). Cons: mixed shell bag cannot split per program; Fish/Git contain author-specific commands/identity; Yazi lacks owned ouch/plugin; Helium/Firefox/Vicinae write unowned Niri options; Blender build alone is package plumbing ([`modules/shell.nix:8`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/shell.nix#L8), [`modules/programs/fish.nix:21`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/fish.nix#L21), [`modules/programs/git.nix:23`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/git.nix#L23), [`modules/programs/yazi.nix:12`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/yazi.nix#L12), [`modules/programs/browsers/helium.nix:177`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/browsers/helium.nix#L177), [`modules/programs/browsers/firefox.nix:9`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/browsers/firefox.nix#L9), [`modules/desktops/vicinae.nix:7`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/desktops/vicinae.nix#L7), [`modules/programs/blender.nix:5`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/blender.nix#L5)). Token leaves and include-only profiles excluded. Score **4**; confidence **medium**.
B_div: 5.5 points → 5; B_ref: 1 units → 2; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":5.5,"diversity_grade":5,"reference_grade":2,"reference_units":[{"name":"nvf-base","evidence":"modules/programs/neovim/default.nix:3"}]}}
```

Total: **47.5/100**. Shortlists: showcase false; library_units ['privileged-user']; starter false.

Overall pros:
- Role connection is centralized and explained ([`modules/assignments.nix:114`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L114)).
- Display settings have useful typed/validation surface ([`modules/toplevel/display-properties.nix:132`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/toplevel/display-properties.nix#L132)).
- NVF base is a substantive independently owned editor preset ([`modules/programs/neovim/default.nix:26`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/neovim/default.nix#L26)).

Overall cons / limits:
- Host CI names do not match inventory (§6a V; [`.github/workflows/flake.yml:53`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/.github/workflows/flake.yml#L53)).
- Shared app settings retain personal adaptation groups (§6a S; [`modules/programs/git.nix:23`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/git.nix#L23)).
- Several app definitions need unowned compositor/tool envelope (§6a R; [`modules/programs/yazi.nix:19`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/programs/yazi.nix#L19)).

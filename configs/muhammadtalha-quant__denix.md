# muhammadtalha-quant__denix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/muhammadtalha-quant__denix.md)

- Upstream: [muhammadtalha-quant/denix](https://github.com/muhammadtalha-quant/denix)
- Reviewed revision: [`70e67b484b5e`](https://github.com/muhammadtalha-quant/denix/commit/70e67b484b5efe04a60d9982e41c3a66eeb0135c)
- Author: muhammadtalha-quant
- Score: **51.5 / 100**, rank 43 of 103 ranked configs. D 5 · I 8 · S 5 · R 5 · P 5 · L 6 · V 5 · O 5 · B 4 · X 2. Shortlists: library units (1).
- Summary: Typed direct host derivation D5; namespace ownership I8; invalid defaults/settings S5/two adaptations; three complete units R5; honest Linux P5; detailed map L6; CI V5; NH/storage ops O5; standard classes X2.

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

Generated flake-parts/import-tree organizes desktop, extras and disko namespaces (`flake.nix:4`, `modules/namespaces.nix:3`). Host metadata drives state version, disk settings and a desktop profile (`modules/defaults.nix:25`, `modules/disko/ext4-simple.nix:10`, `modules/desktop.nix:3`).


## 2. Common patterns.

- namespace: desktop/extras/disko are registered explicitly (`modules/namespaces.nix:3`).
- den.default includes: hostname and define-user are shared (`modules/defaults.nix:10`).
- parametric aspect (fn args): disk layout consumes host.disko settings (`modules/disko/ext4-simple.nix:2`).
- custom classes selection: HM is enabled through the user schema (`modules/defaults.nix:34`).


## 3. Novel patterns.

One storage aspect keeps disk device and swap size in host facts while retaining a reusable partition recipe (`modules/disko/ext4-simple.nix:10`, `modules/disko/ext4-simple.nix:27`).


## 4. Library candidates.

- disko.ext4-simple · `modules/disko/ext4-simple.nix:2` · GPT ESP/swap/ext4 root · disko/NixOS and host.disko schema · fn args · B: package host schema and expose ESP size.


## 5. den friction.

HM is manually imported in defaults alongside den HM user setup (`modules/defaults.nix:17`, `modules/defaults.nix:34`); integration duplication to simplify or document, not a verified failure.


## 6. Docs and complexity.

Docs 4: README names namespace responsibilities, primary entity and source locations (`README.md:10`, `README.md:15`, `README.md:50`, `README.md:58`). Complexity 3: one machine but typed host-driven storage and several composed desktop namespaces (`modules/hosts.nix:3`, `modules/disko/ext4-simple.nix:2`, `modules/desktop.nix:3`).


## 6a. Defects and scoring notes.

- S · moderate: firewallAllowedTCPPorts/UDPPorts declare listOf port but default null; a host omitting them receives an invalid typed default (`modules/schemas/host-schema.nix:28`, `modules/schemas/host-schema.nix:30`, `modules/schemas/host-schema.nix:32`, `modules/schemas/host-schema.nix:34`).
- S · moderate: user/root schema defaults reuse a committed credential (reported privately; not located here); a new user receives it unless overridden. Locale is the second shared adaptation group (`modules/nixos-core.nix:19`).
Normal ESP size and repeated HM import have no verified failure, so no defect deduction.

## 7. Template notes.

Helpful schema-backed starter after replacing the personal account, a committed credential (reported privately; not located here), and the local checkout path (`modules/hosts.nix:6`).

## 8. Scorecard.

### D
Scope: typed host/user facts and consumers. Pros: storage device/swap, stateVersion/firewall/timezone and NH checkout follow host data (`modules/disko/ext4-simple.nix:10`, `modules/defaults.nix:25`, `modules/nixos-core.nix:35`, `modules/nixos-core.nix:87`). Cons: direct schema derivation, no live independently routed quirk/policy fact chain verified (`modules/desktop.nix:3`). Literal5 cap. Score **5**; confidence **medium**.

### I
Scope: namespaces, feature implementation and entity values. Pros: desktop aggregator only composes; host record owns identity and storage; app implementations separate (`modules/desktop.nix:3`, `modules/hosts.nix:13`, `modules/hosts.nix:18`, `modules/desktop/zeditor.nix:2`). Cons: essentials retains a broad app bag (`modules/desktop/essentials.nix:4`). Score8 strong ownership beyond5, below9 wholly granular selection. Repeated native HM import is not itself a defect. Score **8**; confidence **medium**.

### S
Scope: typed host/user settings and defaults. Pros: disk/device/swap and access flags have explicit options with direct consumers (`modules/schemas/host-schema.nix:16`, `modules/schemas/host-schema.nix:36`, `modules/disko/ext4-simple.nix:27`). Cons: non-null listOf port options default to null (`modules/schemas/host-schema.nix:28`, `modules/schemas/host-schema.nix:32`); user defaults share a committed credential (reported privately; not located here). Contract5: useful typed surface weakened by invalid/default credential boundaries. Two grouped adaptations: the shared default above and locale (`modules/nixos-core.nix:19`). Coverage7; min5. Entity-owned checkout/identity/disk and normal ESP preset are not leaks. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":7,"distinct_leaks":2}}
```

### R
Scope: complete app references. Pros: Zed owns language helpers/settings/keymaps and Kitty owns meaningful settings/bindings; Stylix theme constructor owns assets/module (`modules/desktop/zeditor.nix:5`, `modules/desktop/zeditor.nix:136`, `modules/desktop/kitty.nix:8`, `modules/extras/theme.nix:32`). Cons: Fish/Hyprland/Noctalia need outside app commands, VCS needs custom user schema, storage needs host schema (`modules/desktop/fish.nix:7`, `modules/desktop/_dotfiles/hyprland/keybinds/applications.lua:12`, `modules/desktop/noctalia.nix:230`, `modules/desktop/vcs.nix:19`, `modules/disko/ext4-simple.nix:10`). Literal5 useful presets, below9 packaged exports. Score **5**; confidence **medium**.

### P
Scope: one explicit NixOS laptop. Pros: physical machine facts and parameterized storage remain separate from desktop feature (`modules/hosts.nix:3`, `modules/hosts/hp-probook-430g2.nix:1`, `modules/disko/ext4-simple.nix:2`). Cons: home and storage policy assumes Linux, no alternate target/negative-context fixture (`modules/schemas/user-schema.nix:18`). Literal5 honest scope, no automatic penalty for narrow support or ESP default. Score **5**; confidence **medium**.

### L
Scope: detailed source map and architectural orientation. Pros: README explains namespaces, hardware/schema ownership and native config orchestration (`README.md:10`, `README.md:31`, `README.md:50`, `README.md:58`). Cons: detailed map is stronger than a worked second-host/new-aspect authoring example (`README.md:73`). Score6 beyond5 orientation, below9 complete authoring route. Score **6**; confidence **medium**.

### V
Scope: real flake-check workflow. Pros: workflow checks metadata and flake after supplying explicit CI runtime arg (`.github/workflows/test.yml:25`, `.github/workflows/test.yml:27`, `.github/workflows/test.yml:32`). Cons: no fixture exercises omitted port defaults (`modules/schemas/host-schema.nix:30`) or the shared default boundary. Literal5 structural coverage; static only. Score **5**; confidence **medium**.

### O
Scope: host-driven activation/storage settings. Pros: Disko layout follows metadata and NH path follows host checkout, access services follow host flags (`modules/disko/ext4-simple.nix:10`, `modules/nixos-core.nix:87`, `modules/nixos-core.nix:62`). Cons: no generated deploy/recovery/secret inventory or second-host operational fixture (`modules/hosts.nix:3`). Literal5 useful derived operational configuration, below9 lifecycle automation. Score **5**; confidence **medium**.

### X
Scope: standard NixOS/HM and app modules. Pros: namespaces compose Disko/desktop classes (`modules/namespaces.nix:3`, `modules/disko/ext4-simple.nix:3`). Cons: no distinct evaluated nonhost target family verified (`modules/defaults.nix:34`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: three complete app-owner references and selected census max-depth. Pros: Zed/Kitty/Sty lix theme are coherent presets with owned helpers/assets (`modules/desktop/zeditor.nix:5`, `modules/desktop/kitty.nix:22`, `modules/extras/theme.nix:35`). Cons: no per-program splitting of essentials; Fish unowned command bag, Hyprland launcher commands, Noctalia external hyprctl, VCS fleet user fields and disk host schema excluded (`modules/desktop/essentials.nix:4`, `modules/desktop/fish.nix:49`, `modules/desktop/_dotfiles/hyprland/keybinds/applications.lua:12`, `modules/desktop/noctalia.nix:230`, `modules/desktop/vcs.nix:19`). Virtualization enable/package/root preference is token, not another reference (`modules/extras/virtualisation.nix:4`). Score **4**; confidence **medium**.
B_div: 3.5 points → 3; B_ref: 3 units → 4; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":3.5,"diversity_grade":3,"reference_grade":4,"reference_units":[{"name":"zed","evidence":"modules/desktop/zeditor.nix:2"},{"name":"kitty","evidence":"modules/desktop/kitty.nix:2"},{"name":"stylix-theme","evidence":"modules/extras/theme.nix:1"}]}}
```

Total: **51.5/100**. Shortlists: showcase false; library_units ['disko.ext4-simple']; starter false.

Overall pros:
- Entity metadata feeds storage/access/activation settings (`modules/nixos-core.nix:87`).
- Namespace composition keeps implementation separate (`modules/desktop.nix:3`).
- Zed preset includes actual language helpers (`modules/desktop/zeditor.nix:5`).

Overall cons / limits:
- Port-list defaults violate declared type (§6a S; `modules/schemas/host-schema.nix:30`).
- Shared defaults carry a committed credential (reported privately; not located here) (§6a S).
- Several app envelopes rely on outside commands (`modules/desktop/fish.nix:49`).

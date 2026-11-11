# rhedgeco/nix-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/rhedgeco/nix-config.md)

- Upstream: [rhedgeco/nix-config](https://github.com/rhedgeco/nix-config)
- Reviewed revision: [`fd875038e37f`](https://github.com/rhedgeco/nix-config/commit/fd875038e37fd1ab893ae25695fde8a9992cea47)
- Author: rhedgeco
- Score: **50.5 / 100**, rank 48 of 103 ranked configs. D 6 · I 8 · S 6 · R 5 · P 5 · L 2 · V 5 · O 4 · B 5 · X 2. Shortlists: library units (1).
- Summary: Live configuration forwarding D6; feature/entity ownership I8; typed utility S6; twelve complete app units; honest Linux P5; minimal docs L2; structural V5; writable activation issue O4; no new family X2.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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

Den integration is split between defaults, utility aspects and explicit host/user include lists ([`modules/defaults/den.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/defaults/den.nix#L8), [`modules/hosts/hedgebox.nix:6`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L6)). User schema fields express primary status while helper classes forward common settings ([`modules/utils/primary.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L8), [`modules/utils/nixpkgsClass.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L8)).


## 2. Common patterns.

- define-user: all user entities include the standard battery ([`modules/defaults/den.nix:12`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/defaults/den.nix#L12)).
- custom schema/classes: primary is an enable option that selects primary-user ([`modules/utils/primary.nix:9`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L9)).
- forward: nixpkgs pseudo-class content lands in OS and HM nixpkgs.config ([`modules/utils/nixpkgsClass.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L10)).
- parametric aspect (fn args): host directly applies autologin with username/session ([`modules/hosts/hedgebox.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L8)).


## 3. Novel patterns.

An HM option installs writable files/directories through a copy activation instead of immutable symlinks ([`modules/utils/create.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L15), [`modules/utils/create.nix:49`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L49)).


## 4. Library candidates.

- schema-primary · [`modules/utils/primary.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L8) · typed primary-user selection and Nix trusted-user membership · den/NixOS · options (user.primary), fn args · B: separate trusted-user policy from primary status.


## 5. den friction.

Hostname is manually derived from host.name instead of selecting the hostname battery ([`modules/defaults/hostname.nix:2`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/defaults/hostname.nix#L2)). Local pseudo-class forwarding is additional plumbing to explain ([`modules/utils/nixpkgsClass.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L8)).


## 6. Docs and complexity.

Docs 2: root README is just a banner ([`README.md:1`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/README.md#L1)), but primary and forwarding helpers explain intent inline ([`modules/utils/primary.nix:7`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L7), [`modules/utils/nixpkgsClass.nix:7`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L7)). Complexity 4: schema helpers, class forwarding and mutable-file activation extend ordinary host lists ([`modules/utils/create.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L15), [`modules/hosts/hedgebox.nix:13`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L13)).


## 6a. Defects and scoring notes.

- O · moderate: writable-file activation performs rm/mv/mkdir directly before guarded cp/chmod; an HM dry run can remove the previous backup/move the existing target ([`modules/utils/create.nix:42`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L42), [`modules/utils/create.nix:43`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L43), [`modules/utils/create.nix:47`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L47), [`modules/utils/create.nix:51`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L51)).
- L · moderate: banner-only README provides no helper/feature authoring path ([`README.md:1`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/README.md#L1)).
Manual hostname derivation and chosen replacement policy alone are not defects.

## 7. Template notes.

Interesting extension examples, but remove a committed credential (reported privately; not located here) and explain file-copy ownership before reuse ([`modules/utils/create.nix:39`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L39)).

## 8. Scorecard.

### D
Scope: common pseudo-class forwarding and context-derived persistence. Pros: selected default nix/nixpkgs payloads forward through explicit policies into OS/HM module paths ([`modules/defaults/nix.nix:3`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/defaults/nix.nix#L3), [`modules/defaults/nix.nix:19`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/defaults/nix.nix#L19), [`modules/utils/nixClass.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixClass.nix#L10), [`modules/utils/nixpkgsClass.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L10)); persistence derives current user resources ([`modules/utils/persist.nix:70`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L70)). Cons: forwarding handles shared module configuration, not cross-host discovered facts; head aspect-chain is implicit and no missing/duplicate fixture verified ([`modules/utils/nixClass.nix:18`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixClass.nix#L18)). Score6: actual producer/forward/consumer above5 direct derivation, below7 independent resource channels. Score **6**; confidence **medium**.

### I
Scope: feature owners, user selections and generic utilities. Pros: host contains entity metadata and explicitly chosen app owners; helpers separate primary/password/persistence ([`modules/hosts/hedgebox.nix:13`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L13), [`modules/utils/primary.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L8), [`modules/utils/password.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/password.nix#L8)). Cons: Glade is an intentional large desktop selection/configuration envelope ([`modules/aspects/glade.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/glade.nix#L8)). Score8: strong owners beyond5, one coarse composite below9. Score **8**; confidence **medium**.

### S
Scope: typed utility/settings contracts. Pros: primary/password/state persistence and app settings expose typed knobs and guarded consumers ([`modules/utils/primary.nix:9`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L9), [`modules/utils/password.nix:9`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/password.nix#L9), [`modules/utils/persist.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L15), [`modules/aspects/vicinae.nix:9`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/vicinae.nix#L9)). Cons: typed configuration format adapters need local mylib; mutable creation has broad string/path surface ([`modules/aspects/zed.nix:6`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/zed.nix#L6), [`modules/utils/create.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L15)). Contract6 beyond5 repeated useful interfaces, below7 stronger validated domain. No author identity leak inferred from a committed credential (reported privately; not located here): it is entity-owned. No additional verified shared adaptation group in inspected app/helper sources; coverage8, min6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":8,"distinct_leaks":0}}
```

### R
Scope: complete independently owned presets. Pros: parameterized greetd, packaged color picker/desktop entry, Fish plugins and keyring DBus integration own useful envelopes ([`modules/aspects/autologin.nix:2`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/autologin.nix#L2), [`modules/aspects/color-picker.nix:6`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/color-picker.nix#L6), [`modules/aspects/fish.nix:22`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/fish.nix#L22), [`modules/aspects/keyring.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/keyring.nix#L15)). Standard resource collector persist dependency allowed ([`modules/utils/persist.nix:81`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L81)). Cons: Zed/Noctalia/Vicinae require custom create/type helpers; no polished standalone import/export guide ([`modules/aspects/zed.nix:37`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/zed.nix#L37), [`modules/aspects/noctalia.nix:12`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/noctalia.nix#L12)). Literal5 useful references, below9 packaged library. Score **5**; confidence **medium**.

### P
Scope: explicit Linux hosts and generic helper boundaries. Pros: host/user data parameterizes primary and persistence, nullable persistence gates effects ([`modules/utils/persist.nix:30`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L30), [`modules/utils/persist.nix:69`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L69), [`modules/hosts/hedgebox.nix:3`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L3)). Cons: forwarding intentionally targets NixOS/HM and the fleet is Linux-only ([`modules/utils/nixClass.nix:11`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixClass.nix#L11)). Literal5 honest current scope; no unsupported-platform defect inferred. Score **5**; confidence **medium**.

### L
Scope: root docs versus inline comments. Pros: helper comments explain user persistence and class forwarding ([`modules/utils/persist.nix:58`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L58), [`modules/utils/nixpkgsClass.nix:7`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L7)). Cons: banner-only README supplies no host/feature/helper authoring path ([`README.md:1`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/README.md#L1)). Score2: inline orientation above1 absent explanation, below5 worked guide. Score **2**; confidence **medium**.

### V
Scope: structural check recipe. Pros: just check explicitly requests flake check including submodules ([`justfile:18`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/justfile#L18)). Cons: no targeted fixture for writable activation backup/dry-run behavior or forwarded class selection ([`modules/utils/create.nix:39`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L39), [`modules/utils/nixClass.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixClass.nix#L10)). Literal5 ordinary structural validation route; static only. Score **5**; confidence **medium**.

### O
Scope: derived persistence and writable activation. Pros: host persistence and user resource inventories feed impermanence; just defaults select current host ([`modules/utils/persist.nix:47`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L47), [`modules/utils/persist.nix:70`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/persist.nix#L70), [`justfile:1`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/justfile#L1)). Cons: custom create activation removes/moves backups outside HM run wrapper, so dry-run does not protect existing target/backup ([`modules/utils/create.nix:42`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L42), [`modules/utils/create.nix:43`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L43), [`modules/utils/create.nix:51`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L51)). Score4 below5 reliable derived lifecycle because this concrete mutation boundary is unsafe; generic just commands alone not Den ops credit. Score **4**; confidence **medium**.

### X
Scope: OS/HM pseudo-class forwarding. Pros: local nix/nixpkgs classes share module configuration ([`modules/utils/nixClass.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixClass.nix#L15), [`modules/utils/nixpkgsClass.nix:15`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L15)). Cons: neither is a new evaluated nonhost target family; yoink is an ordinary package input ([`modules/aspects/yoink.nix:3`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/yoink.nix#L3)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: all independently owned complete app integrations, one app once. Pros: twelve listed units own meaningful settings/integration; bare explicit Starship initialization is actual Fish integration, Dolphin has udev plus two state resources, Bambu owns TLS/runtime wrapper ([`modules/aspects/starship.nix:5`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/starship.nix#L5), [`modules/aspects/dolphin.nix:3`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/dolphin.nix#L3), [`modules/aspects/bambu.nix:54`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/bambu.nix#L54)). Cons: bare enable/one resource Discord/Spotify/Firefox and include-only Fishy excluded; Discord/Steam custom Vicinae settings, Rust custom Zed schema, Zed/Niri/Noctalia/Vicinae helper envelopes excluded ([`modules/aspects/spotify.nix:4`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/spotify.nix#L4), [`modules/aspects/discord.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/discord.nix#L10), [`modules/aspects/steam.nix:14`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/steam.nix#L14), [`modules/aspects/rust.nix:23`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/rust.nix#L23), [`modules/aspects/zed.nix:37`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/zed.nix#L37)). Generic standard-shaped persistence collector allowed; no per-inner-attr Glade inflation. Score **5**; confidence **medium**.
B_div: 4.0 points → 3; B_ref: 12 units → 7; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":4.0,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"fish","evidence":"modules/aspects/fish.nix:2"},{"name":"direnv","evidence":"modules/aspects/direnv.nix:2"},{"name":"devenv","evidence":"modules/aspects/devenv.nix:2"},{"name":"starship-fish-hook","evidence":"modules/aspects/starship.nix:2"},{"name":"dolphin","evidence":"modules/aspects/dolphin.nix:2"},{"name":"pipewire","evidence":"modules/aspects/pipewire.nix:2"},{"name":"networkmanager","evidence":"modules/aspects/network.nix:2"},{"name":"autologin","evidence":"modules/aspects/autologin.nix:2"},{"name":"color-picker","evidence":"modules/aspects/color-picker.nix:6"},{"name":"bambu","evidence":"modules/aspects/bambu.nix:17"},{"name":"grub","evidence":"modules/aspects/grub.nix:10"},{"name":"keyring","evidence":"modules/aspects/keyring.nix:2"}]}}
```

Total: **50.5/100**. Shortlists: showcase false; library_units ['schema-primary']; starter false.

Overall pros:
- Feature selections and entity values are separated ([`modules/hosts/hedgebox.nix:13`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L13)).
- Shared classes have actual forwarding consumers ([`modules/utils/nixpkgsClass.nix:10`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/nixpkgsClass.nix#L10)).
- Useful app runtime integrations own their dependencies ([`modules/aspects/color-picker.nix:6`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/color-picker.nix#L6)).

Overall cons / limits:
- Writable activation mutates during dry-run (§6a O; [`modules/utils/create.nix:42`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/create.nix#L42)).
- Root docs do not teach authoring (§6a L; [`README.md:1`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/README.md#L1)).
- Several rich apps require local helper closure ([`modules/aspects/zed.nix:37`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/aspects/zed.nix#L37)).

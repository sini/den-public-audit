# sm-f/nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/sm-f/nix.md)

- Upstream: [sm-f/nix](https://github.com/sm-f/nix)
- Reviewed revision: [`23820eea5e00`](https://github.com/sm-f/nix/commit/23820eea5e00f8b1d7faab4a9c3ce43603f78b52)
- Author: sm-f
- Score: **42.5 / 100**, rank 79 of 103 ranked configs. D 4 · I 7 · S 4 · R 5 · P 5 · L 3 · V 5 · O 4 · B 3 · X 2. Shortlists: library units (1).
- Summary: Direct host derivation D4; host/user ownership I7; untyped shared assumptions S4/seven groups; two complete references R5; honest Linux P5; structure docs L3; actual build V5; boot/update operations O4; ordinary Hjem X2.

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

A direct nixpkgs evalModules entry uses a local import-tree utility and imports den from a dedicated module ([`flake.nix:4`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/flake.nix#L4), [`modules/den.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L3)). One host has a concise aspect list while the travelling user gets separate dotfile/application aspects and hjem ([`modules/hosts/eris.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L3), [`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6)).


## 2. Common patterns.

- define-user+primary-user: user includes both through den.provides ([`modules/hosts/eris.nix:11`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L11)).
- host-aspects composition: eris selects system roles independently of scott user features ([`modules/hosts/eris.nix:17`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L17)).
- custom classes selection: users default to hjem ([`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6)).


## 3. Novel patterns.

Work environment bundles a combined multi-version .NET SDK with its runtime variables and an Azurite service account/state directory ([`modules/work.nix:7`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L7), [`modules/work.nix:37`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L37), [`modules/work.nix:42`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L42)).


## 4. Library candidates.

- work · [`modules/work.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L3) · Azure/.NET tools plus Azurite service · NixOS/nixpkgs · none · B: split Twingate and broad office tools from reusable .NET/Azurite core.


## 5. den friction.

No verified den-specific workaround in inspected integration and host composition ([`modules/den.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L3), [`modules/hosts/eris.nix:17`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L17)).


## 6. Docs and complexity.

Docs 2: README identifies the framework and desktop stack ([`README.md:4`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L4), [`README.md:15`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L15)); host comments explain hardware overrides ([`modules/hosts/eris.nix:39`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L39)). Complexity 3: one host/user but substantial workplace services, toolchain bundling and hardware tuning ([`modules/den.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L8), [`modules/work.nix:42`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L42)).


## 6a. Defects and scoring notes.

- S · moderate: seven shared adaptation groups enumerated in S, including direct scott lookups and fixed checkout metadata ([`modules/nix-update.nix:12`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L12), [`utils/default.nix:2`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/utils/default.nix#L2)), and a committed credential (reported privately; not located here).
- I · minor: work ties VPN, office tools, .NET and Azurite to one include, preventing independent selection ([`modules/work.nix:16`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L16), [`modules/work.nix:18`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L18), [`modules/work.nix:42`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L42)).

## 7. Template notes.

Useful hjem and host/user split example; the generic core still includes Intel-specific graphics and personal cache/locale choices ([`modules/core.nix:13`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L13), [`modules/core.nix:45`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L45), [`modules/core.nix:74`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L74)).

## 8. Scorecard.

### D
Scope: direct host/user context consumption. Pros: host LUKS/swap fields drive initrd and power configuration; host to-users provider supplies Hjem files ([`modules/tpm2-luks.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/tpm2-luks.nix#L8), [`modules/swap.nix:11`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/swap.nix#L11), [`modules/niri.nix:83`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L83)). Cons: literal user lookups and ordinary module/package composition dominate; no independent fact collector/policy route verified ([`modules/shells.nix:19`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L19), [`modules/nix-update.nix:12`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L12)). Score4 beyond2 lists, below5 substantial typed domain derivation. Score **4**; confidence **medium**.

### I
Scope: separate host/user selections and core/work bags. Pros: user applications and machine concerns have separate include lists and mostly own files ([`modules/hosts/eris.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L3), [`modules/hosts/eris.nix:17`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L17)). Cons: core address merges boot/security/update concerns; work combines unrelated VPN/office/toolchain/service selection ([`modules/boot.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/boot.nix#L3), [`modules/security.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/security.nix#L3), [`modules/nix-update.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L3), [`modules/work.nix:16`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L16)). Score7: usable feature owners beyond5, below9 independent concerns. Score **7**; confidence **medium**.

### S
Scope: host metadata versus shared author assumptions. Pros: LUKS names/swap sizing are entity-owned and directly consumed ([`modules/den.nix:10`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L10), [`modules/swap.nix:11`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/swap.nix#L11)). Cons: custom fields lack a local typed interface and seven adaptation groups remain: shared identity, checkout root, cache pair, locale, monitor topology, a committed credential (reported privately; not located here), Intel hardware assumption ([`modules/den.nix:10`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L10), [`modules/git.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/git.nix#L8), [`utils/default.nix:2`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/utils/default.nix#L2), [`modules/core.nix:15`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L15), [`modules/core.nix:47`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L47), [`modules/niri.nix:48`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L48), [`modules/core.nix:76`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L76)). Contract4 below5 because reusable leaves address scott directly; coverage6, min4. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":7}}
```

### R
Scope: independent complete app envelopes. Pros: Intune owns PAM/runtime/WebKit/broker integration; LibreWolf owns extensions, profile files and substantial chrome stylesheet ([`modules/intune.nix:31`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/intune.nix#L31), [`modules/intune.nix:46`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/intune.nix#L46), [`modules/librewolf.nix:25`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/librewolf.nix#L25), `dotfiles/librewolf/userChrome.css:188`). Cons: Ghostty/Nvim/Voxtype rely on fleet utils/theme; work is a mixed tool bag despite useful §4 extraction ([`modules/ghostty.nix:1`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/ghostty.nix#L1), [`modules/nvim.nix:1`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nvim.nix#L1), [`modules/voxtype.nix:15`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/voxtype.nix#L15), [`modules/work.nix:18`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L18)). Literal5 useful references, below9 packaged units. Score **5**; confidence **medium**.

### P
Scope: one explicit x86 Linux host and Hjem user. Pros: hardware overrides are entity-owned and build target is explicit ([`modules/hosts/eris.nix:39`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L39), [`modules/den.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L8)). Cons: shared core assumes Intel graphics and Niri embeds physical outputs, limiting second-host portability ([`modules/core.nix:76`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/core.nix#L76), [`modules/niri.nix:48`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L48)). Literal5 current honest single-platform boundary; adaptations charged S once. Score **5**; confidence **medium**.

### L
Scope: README structure/stack. Pros: names Den/Hjem and maps modules/dotfiles/editor/overlays ([`README.md:4`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L4), [`README.md:21`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L21)). Cons: no worked adding-host/aspect/context guide ([`README.md:23`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L23)). Score3 above2 stack links, below5 authoring route. Score **3**; confidence **medium**.

### V
Scope: actual host build workflow. Pros: CI evaluates exact Eris output then builds closure, including DisplayLink prefetch ([`.github/workflows/build.yml:39`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/.github/workflows/build.yml#L39), [`.github/workflows/build.yml:48`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/.github/workflows/build.yml#L48), [`.github/workflows/build.yml:57`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/.github/workflows/build.yml#L57)). Cons: no targeted Hjem provider/host-field/negative-context fixture verified ([`modules/den.nix:10`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L10), [`modules/niri.nix:83`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/niri.nix#L83)). Literal5 structural build coverage; static only. Score **5**; confidence **medium**.

### O
Scope: metadata-derived boot and update status lifecycle. Pros: LUKS metadata generates TPM enrollment boot settings; swap/resume values follow host; update checker serializes atomic status publication ([`modules/tpm2-luks.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/tpm2-luks.nix#L8), [`modules/power-management.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/power-management.nix#L9), [`modules/nix-update.nix:40`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L40)). Cons: update and shell activation use literal scott/checkout, not inventory-driven tools ([`modules/nix-update.nix:12`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L12), [`modules/shells.nix:118`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L118)). Score4 between2 ordinary tooling and5 derived operations; boot metadata is the verified Den input, checker itself receives no D credit. Score **4**; confidence **medium**.

### X
Scope: normal NixOS and alternate home environment. Pros: users explicitly use Hjem ([`modules/den.nix:6`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L6)). Cons: Hjem is a standard home environment and wrappers/build outputs are ordinary plumbing ([`modules/intune.nix:46`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/intune.nix#L46)). Baseline2, no new evaluated nonhost family. Score **2**; confidence **medium**.

### B
Scope: two complete app owners and census selected maximum depth. Pros: Intune runtime integration and LibreWolf coherent extension/profile/CSS envelope satisfy meaningful-unit threshold ([`modules/intune.nix:37`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/intune.nix#L37), [`modules/librewolf.nix:35`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/librewolf.nix#L35)). Cons: multiapp core/work/shell/dotfile bags cannot split per attr; shared-identity Syncthing/Podman/Git, utils/theme-dependent Ghostty/Nvim/Voxtype/Niri, host-field power helpers excluded ([`modules/work.nix:18`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L18), [`modules/shells.nix:18`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/shells.nix#L18), [`modules/syncthing.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/syncthing.nix#L9), [`modules/podman.nix:27`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/podman.nix#L27), [`modules/git.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/git.nix#L8), [`modules/voxtype.nix:15`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/voxtype.nix#L15), [`modules/power-management.nix:9`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/power-management.nix#L9)). No extra credit for ordinary package bags. Score **3**; confidence **medium**.
B_div: 5 points → 3; B_ref: 2 units → 2; half-up mean → 3.
```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":2,"reference_units":[{"name":"intune","evidence":"modules/intune.nix:3"},{"name":"librewolf","evidence":"modules/librewolf.nix:3"}]}}
```

Total: **42.5/100**. Shortlists: showcase false; library_units ['work']; starter false.

Overall pros:
- Host and user feature selections are distinct ([`modules/hosts/eris.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/hosts/eris.nix#L3)).
- Intune owns meaningful runtime integration ([`modules/intune.nix:46`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/intune.nix#L46)).
- CI addresses an actual declared host ([`.github/workflows/build.yml:40`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/.github/workflows/build.yml#L40)).

Overall cons / limits:
- Shared features address literal identity/root (§6a S; [`modules/nix-update.nix:12`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/nix-update.nix#L12)).
- Work bundle ties unrelated concerns (§6a I; [`modules/work.nix:16`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L16)).
- No repository authoring walkthrough ([`README.md:21`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/README.md#L21)).

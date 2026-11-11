# nolvyn/nixos

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/nolvyn/nixos.md)

- Upstream: [nolvyn/nixos](https://github.com/nolvyn/nixos)
- Reviewed revision: [`e0fd0f9f0537`](https://github.com/nolvyn/nixos/commit/e0fd0f9f0537a28b68ee802a75051f719a2af203)
- Author: nolvyn
- Score: **52.0 / 100**, rank 41 of 103 ranked configs. D 5 · I 8 · S 6 · R 5 · P 7 · L 2 · V 6 · O 5 · B 5 · X 2. Shortlists: —.
- Summary: D useful direct schema/report derivation; I app owners with host patch localization; S typed confinement limited by four groups; R few independent presets; P guarded platform paths; L minimal; V negative compatibility fixtures; O state reports; X standard; B strict schema exclusions.

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

Generated flake-parts/import-tree outputs load cross-platform aspects for Linux and Darwin ([`flake.nix:4`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/flake.nix#L4), [`modules/aspects/hosts/weebmachine/weebmachine.nix:3`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/weebmachine/weebmachine.nix#L3), [`modules/aspects/hosts/astraeus/astraeus.nix:3`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L3)). Shared defaults expose stable/warm/unstable package sets across OS and HM classes ([`modules/setup.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L8), [`modules/setup.nix:29`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L29)).


## 2. Common patterns.

- den.default includes: define-user and hostname apply globally ([`modules/setup.nix:45`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L45)).
- host-aspects composition: Linux host selects role bundles and applications ([`modules/aspects/hosts/weebmachine/weebmachine.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/weebmachine/weebmachine.nix#L8)).
- parametric aspect (fn args): Darwin host consumes host facts in its class module ([`modules/aspects/hosts/astraeus/astraeus.nix:18`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L18)).


## 3. Novel patterns.

Darwin mas module text is guarded by assertions and patched through builtins.toFile before import ([`modules/aspects/hosts/astraeus/astraeus.nix:37`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L37)). It preserves upstream module shape while fixing activation behavior.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Darwin HM overrides _module.args.pkgsPath to avoid inheriting the newer Darwin package source ([`modules/aspects/hosts/astraeus/astraeus.nix:78`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L78)); useful package-boundary friction, with no explicit den bug claimed.


## 6. Docs and complexity.

Docs 2: README is only a title/personal-config sentence ([`README.md:1`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/README.md#L1)), while Darwin patch comments explain the reason and guard strategy ([`modules/aspects/hosts/astraeus/astraeus.nix:24`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L24)). Complexity 4: mixed package sources and cross-platform host roles plus guarded module patching ([`modules/setup.nix:29`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L29), [`modules/aspects/hosts/astraeus/astraeus.nix:37`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L37)).


## 6a. Defects and scoring notes.

- S · moderate: four grouped shared assumptions remain, listed in S ([`modules/schema.nix:7`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/schema.nix#L7), [`modules/aspects/impermanence.nix:24`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L24), [`modules/aspects/audio.nix:26`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/audio.nix#L26), [`modules/aspects/locale.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/locale.nix#L8)).
- L · moderate: root README provides no authoring path despite custom multi-channel/platform interfaces ([`README.md:1`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/README.md#L1), [`modules/setup.nix:29`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L29)).
Guarded mas source transformation is compatibility work with explicit assertions, not a demonstrated composition defect.

## 7. Template notes.

Good advanced multi-channel example; avoid teaching source-text patches as a default starter mechanism ([`modules/setup.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L8), [`modules/aspects/hosts/astraeus/astraeus.nix:42`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L42)).

## 8. Scorecard.

### D
Scope: host metadata and state reporting. Pros: typed host identity/checkout facts feed Git/helpers; persistence records produce a report manifest ([`modules/schema.nix:5`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/schema.nix#L5), [`modules/aspects/git.nix:21`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/git.nix#L21), [`modules/aspects/impermanence.nix:24`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L24), [`modules/aspects/impermanence.nix:28`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L28)). Cons: direct schema/config derivation, no emitted Den fact channel/policy routing ([`modules/setup.nix:45`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/setup.nix#L45)). Literal5 useful structured model capped5. Score **5**; confidence **medium**.

### I
Scope: app owners and platform host concerns. Pros: apps own their OS/HM behavior and profiles compose them ([`modules/aspects/rofi.nix:3`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/rofi.nix#L3), [`modules/aspects/hosts/weebmachine/weebmachine.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/weebmachine/weebmachine.nix#L8)). Cons: generic mas compatibility transformation sits in a host file rather than app/integration owner ([`modules/aspects/hosts/astraeus/astraeus.nix:21`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L21)). Interpolated8 strong ownership below9 with this localization limit; guarded source patch is not inherently a defect. Score **8**; confidence **medium**.

### S
Scope: typed metadata and confinement options. Pros: schema defaults derive checkout path, confinement exposes typed approved download roots and asserts AppArmor/literal paths ([`modules/schema.nix:10`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/schema.nix#L10), [`modules/aspects/qbittorrent.nix:95`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/qbittorrent.nix#L95), [`modules/aspects/qbittorrent.nix:110`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/qbittorrent.nix#L110)). Contract7 broad purposeful guarded settings above5, not9 consistently documented surface. Cons: four grouped assumptions remain: default owner/Git/password identity, persistent-root/storage layout, one Bluetooth audio device, household locale ([`modules/schema.nix:7`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/schema.nix#L7), [`modules/schema.nix:19`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/schema.nix#L19), [`modules/aspects/agenix.nix:21`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/agenix.nix#L21), [`modules/aspects/impermanence.nix:24`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L24), [`modules/aspects/audio.nix:26`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/audio.nix#L26), [`modules/aspects/locale.nix:8`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/locale.nix#L8)). Coverage6; schema-exposed checkout and ordinary disk/port defaults not counted as hidden leaks. min(7,6)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":4}}
```

### R
Scope: independent references versus schema-dependent fleet apps. Pros: Rofi owns its Rasi preset and runtime terminal path; Ghostty owns platform package and Fish integration ([`modules/aspects/rofi.nix:7`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/rofi.nix#L7), [`modules/aspects/rofi.nix:17`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/rofi.nix#L17), [`modules/aspects/ghostty.nix:10`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/ghostty.nix#L10)). Cons: no §4 independent polished nomination/guide; most apps require host.userName/flakeDir or package-channel overlays ([`modules/aspects/fastfetch.nix:27`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/fastfetch.nix#L27), [`modules/aspects/vesktop.nix:16`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/vesktop.nix#L16)). Literal5 useful complete references, not9 substantial documented A unit. Score **5**; confidence **medium**.

### P
Scope: Linux/Darwin package and activation boundaries. Pros: Ghostty uses platform-specific package, Fish reconciles native account shell with guards and Darwin host separates HM package source ([`modules/aspects/ghostty.nix:12`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/ghostty.nix#L12), [`modules/aspects/fish.nix:20`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/fish.nix#L20), [`modules/aspects/hosts/astraeus/astraeus.nix:80`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L80)). Cons: platform compatibility still relies on guarded upstream source rewriting ([`modules/aspects/hosts/astraeus/astraeus.nix:40`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L40)). Interpolated7 beyond5 concrete counterpart boundaries, below9 broad negative-context proof. Score **7**; confidence **medium**.

### L
Scope: root README versus local comments. Pros: option descriptions explain confinement contract ([`modules/aspects/qbittorrent.nix:100`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/qbittorrent.nix#L100)). Cons: root README is only project identification, no host/feature/platform authoring path ([`README.md:1`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/README.md#L1)). Literal2. Score **2**; confidence **medium**.

### V
Scope: compatibility fixtures and guard assertions. Pros: Blender compatibility test mutates each pinned helper anchor missing/duplicate and demands failure; mas imports assert anchors ([`scripts/blender-codex-compat-test.py:39`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/scripts/blender-codex-compat-test.py#L39), [`scripts/blender-codex-compat-test.py:50`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/scripts/blender-codex-compat-test.py#L50), [`scripts/blender-codex-compat-test.py:84`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/scripts/blender-codex-compat-test.py#L84), [`modules/aspects/hosts/astraeus/astraeus.nix:40`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L40)). Cons: no general Den class/provider fixture; source tests not executed here. Interpolated6 above5 targeted negative compatibility checks, below9 broad composition suite. Score **6**; confidence **medium**.

### O
Scope: derived persistence reporting and bootstrap state. Pros: selected state declarations produce report manifest, scheduled constrained service and Fish notice; agenix uses persisted host identity ([`modules/aspects/impermanence.nix:28`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L28), [`modules/aspects/impermanence.nix:85`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L85), [`modules/aspects/impermanence.nix:143`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L143), [`modules/aspects/agenix.nix:18`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/agenix.nix#L18)). Cons: root/home rollback is tied to a fixed storage layout and native scripts ([`modules/aspects/impermanence.nix:125`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L125), [`modules/aspects/impermanence.nix:135`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L135)). Literal5 useful operational derivation, not9 generalized fleet deploy/rollback. Score **5**; confidence **medium**.

### X
Scope: ordinary OS/HM programs and helper packages. Pros: app confinement is substantial module work ([`modules/aspects/qbittorrent.nix:95`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/qbittorrent.nix#L95)). Cons: no independently evaluated non-host Den class; helpers remain package plumbing ([`modules/aspects/impermanence.nix:15`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/impermanence.nix#L15)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: selected census max depth and all independent complete presets. Pros: listed Rofi/Ghostty/Geoclue units own actual configuration and dependencies ([`modules/aspects/rofi.nix:12`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/rofi.nix#L12), [`modules/aspects/ghostty.nix:12`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/ghostty.nix#L12), [`modules/aspects/location.nix:5`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/location.nix#L5)). Cons: most app units depend on fleet host.userName/flakeDir, custom pkgs.warm/stable/unstable/llm-agents overlays, mutable native checkout or missing generated colors; token Btop and package-only leaves excluded ([`modules/aspects/ai/claude.nix:7`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/ai/claude.nix#L7), [`modules/aspects/vesktop.nix:16`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/vesktop.nix#L16), [`modules/aspects/kitty.nix:20`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/kitty.nix#L20), [`modules/aspects/btop.nix:13`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/btop.nix#L13)). Whole bodies excluded rather than extracted clean cores; generic upstream resource plumbing alone does not create reference substance. Score **5**; confidence **medium**.
B_div: 5.5 points → 5; B_ref: 3 units → 4; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":5.5,"diversity_grade":5,"reference_grade":4,"reference_units":[{"name":"rofi","evidence":"modules/aspects/rofi.nix:7"},{"name":"ghostty","evidence":"modules/aspects/ghostty.nix:10"},{"name":"geoclue2","evidence":"modules/aspects/location.nix:5"}]}}
```

Total: **52.0/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Typed confinement and path validation ([`modules/aspects/qbittorrent.nix:95`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/qbittorrent.nix#L95)).
- Explicit cross-platform package/activation boundaries ([`modules/aspects/ghostty.nix:12`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/ghostty.nix#L12)).
- Missing/duplicate compatibility fixtures ([`scripts/blender-codex-compat-test.py:50`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/scripts/blender-codex-compat-test.py#L50)).

Overall cons / limits:
- Four shared adaptation groups (§6a S; [`modules/aspects/audio.nix:26`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/audio.nix#L26)).
- Minimal root authoring docs (§6a L; [`README.md:1`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/README.md#L1)).
- Many units require custom channel/host schema ([`modules/aspects/vesktop.nix:16`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/vesktop.nix#L16)).

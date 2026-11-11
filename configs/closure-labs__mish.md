# closure-labs__mish

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/closure-labs__mish.md)

- Upstream: [closure-labs/mish](https://github.com/closure-labs/mish)
- Reviewed revision: [`6587ee6dbb2f`](https://github.com/closure-labs/mish/commit/6587ee6dbb2fa81a0075d08c8a118f3032176645)
- Author: closure-labs
- Score: **61.5 / 100**, rank 11 of 103 ranked configs. D 2 · I 9 · S 9 · R 9 · P 9 · L 9 · V 9 · O 5 · B 2 · X 2. Shortlists: library units (1).
- Summary: D direct appliance composition; I orthogonal feature/mode/architecture owners; S typed validated operator settings without author leaks; R exported complete mode with minimal consumer; P architecture guards; L composition guide; V positive/negative checks and CI; O Den-host-derived installer images; B one product unit and no surveyed families; X standard targets.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

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

A product appliance uses genuine flake-scope Den composition, with host/mode/architecture selection (`nix/den/hosts.nix:7`, `nix/den/hosts.nix:27`). This is an appliance repository rather than a general personal dotfile template.

## 2. Common patterns

- provides tree divides features, modes and architectures (`nix/den/aspects.nix:19`, `nix/den/aspects.nix:63`).
- parametric aspect (fn args) asserts architecture compatibility (`nix/den/aspects.nix:7`).

## 3. Novel patterns

One hardware target overrides instantiate for Raspberry Pi’s system constructor (`nix/den/hosts.nix:14`). Legacy NixOS options named den are explicitly distinguished from real Den (`modules/nixos/mish/den.nix:22`).

## 4. Library candidates

- mish USB coordinator mode · `nix/den/outputs.nix:16` · complete Mish coordinator service with optional USB radio integration · inputs: exported Mish flake module, NixOS/nixpkgs; its package overlay and native service travel with the mode (`nix/den/aspects.nix:21`) · parameterization: services.mish options, notably actual stable device path · grade A as exported; minimal independent consumer at `docs/den-architecture.md:69`. Specialized to the Mish application, with no author identity or private assets.

## 5. den friction

Legacy capability metadata retains Den-like names in an independent option namespace; readers must distinguish it from composition (`modules/nixos/mish/den.nix:18`).

## 6. Docs and complexity

Docs 4: README explains the operational model (`README.md:3`, `README.md:11`), and source explains compatibility (`modules/nixos/mish/den.nix:22`). Complexity 4: multiple architectures and custom instantiation (`nix/den/hosts.nix:12`).

## 6a. Defects and scoring notes

No additional concrete defect verified in this scoped reading. Legacy metadata naming raises a reading cost, but its compatibility purpose is explicitly documented (`modules/nixos/mish/den.nix:22`).

## 7. Template notes

Good advanced example of orthogonal modes and hardware; appliance assumptions dominate the feature module (`nix/den/aspects.nix:25`).

## 8. Scorecard

### D (2, high)
Scope: real outer Den composition and legacy native metadata. Pros: feature/mode/architecture composition is explicit (`nix/den/aspects.nix:19`, `nix/den/hosts.nix:27`). Cons: services.mish values render native module configuration directly (`modules/nixos/mish/control.nix:13`); native den.quirks is explicitly compatibility metadata, not a framework channel (`modules/nixos/mish/den.nix:22`). Anchor 2: no qualifying Den producer→routed consumer verified; legacy names earn no ceremony credit. Confidence: high.

### I (9, high)
Scope: all Den aspects, outputs, hardware and native service owners. Pros: features, modes and architecture providers have distinct responsibilities (`nix/den/aspects.nix:20`, `nix/den/aspects.nix:63`, `nix/den/aspects.nix:90`); native service pieces import separately (`modules/nixos/mish/default.nix:12`). Cons: compatibility metadata adds a documented reading step (`modules/nixos/mish/den.nix:22`), not a verified isolation defect. Literal 9 within this appliance scope; no scale bonus. Confidence: high.

### S (9, medium)
Scope: appliance options, modes and architecture/radio/TLS validation. Pros: documented typed runtime inputs/defaults are separate from implementations (`modules/nixos/mish/default.nix:43`, `modules/nixos/mish/default.nix:74`); invalid hardware paths and TLS secrets fail explicitly (`nix/den/aspects.nix:38`, `modules/nixos/mish/control.nix:99`). Cons: no additional settings defect verified; product defaults such as mish.local are overrideable product identity, not author identity (`modules/nixos/mish/default.nix:43`). Contract 9; grouped author leaks 0, raw 0 in these bodies, coverage 10; S=min(9,10)=9. Confidence: medium: static source, not physical commissioning.
```score-evidence
{"S":{"contract_design":9,"leak_coverage":10,"distinct_leaks":0,"raw_leaks":0}}
```

### R (9, high)
Scope: resolved mode exports and independent NixOS consumer. Pros: exported mish-meshtastic includes coordinator/package/service machinery (`nix/den/outputs.nix:16`, `nix/den/aspects.nix:21`), and the guide supplies a minimal import plus one device setting (`docs/den-architecture.md:69`). Cons: consumer still supplies actual hardware and runtime commissioning (`docs/den-architecture.md:78`); this is the explicit contract, not a hidden author prerequisite. Literal 9: substantial grade-A unit, explicit NixOS/Mish input and option contract, minimal consumer. Confidence: high.

### P (9, high)
Scope: x86/ARM appliance hosts, Pi constructor and Darwin development outputs. Pros: architecture provider checks actual hostPlatform (`nix/den/aspects.nix:7`); wrong-architecture rejection is checked (`nix/checks.nix:166`), and Pi5 constructor override is isolated (`nix/den/hosts.nix:14`). Cons: Darwin is explicitly package/development-only and physical Pi qualification remains open (`docs/den-architecture.md:57`, `README.md:131`), not a false cross-platform promise. Meets 9 within stated support. Confidence: high.

### L (9, high)
Scope: root entry, architecture guide and consumer/acceptance sections. Pros: README leads readers to composition/operations/qualification (`README.md:72`, `README.md:91`); guide maps every layer and gives a concrete adoption example (`docs/den-architecture.md:24`, `docs/den-architecture.md:69`). Cons: appliance prerequisites remain substantial but are separated from framework internals (`docs/den-architecture.md:105`); no additional navigation defect verified. Literal 9 for teaching the actual path and its limits. Confidence: high.

### V (9, high)
Scope: composition fixtures, booted VM definition and native CI. Pros: shipped/disabled modes, old stateVersion, placeholder/unstable devices, incompatible radio selections and architecture mismatch have focused assertions (`nix/checks.nix:130`, `nix/checks.nix:153`, `nix/checks.nix:162`); VM imports the real simulation mode (`tests/appliance.nix:5`), and CI invokes checks on both Linux architectures (`.github/workflows/ci.yml:45`, `.github/workflows/ci.yml:67`). Cons: physical RF and commissioning remain explicitly unverified (`README.md:131`); this review does not certify prior reported passes. Meets 9 for intent/invocation. Confidence: high.

### O (5, medium)
Scope: installer aspect, image output projection and operator credentials. Pros: installer is a real Den host/mode and generated NixOS outputs feed VM/ISO/SD artifacts (`nix/den/hosts.nix:31`, `nix/den/aspects.nix:76`, `nix/outputs.nix:25`). Cons: image names remain an explicit product map, while credentials and physical commissioning are operator-owned (`nix/outputs.nix:23`, `README.md:69`). Anchor 5 for one Den-backed installation/image concern; no credit for a unified fleet deploy/rekey/builder lifecycle. Confidence: medium.

### B (2, high)
Scope: all Den feature/mode/architecture definitions and their native modules. Pros: one complete Mish service unit owns its package overlay and native module (`nix/den/aspects.nix:21`). Cons: local-https/radio fragments need that same product service, so are not separate app units; modes/architectures and package/check wrappers add no reference count (`nix/den/aspects.nix:29`, `nix/den/aspects.nix:64`, `nix/den/outputs.nix:25`). Standalone native mesh-services is not a Den aspect. Census diversity 0 → 2; one reference unit → 2; B2. No desktop domain is required or deducted elsewhere. Confidence: high.
```score-evidence
{"B":{"diversity_points":0,"diversity_grade":2,"reference_grade":2,"reference_units":[{"name":"mish-control","evidence":"nix/den/aspects.nix:22"}]}}
```

### X (2, high)
Scope: outer Den class exports, appliance constructors and image outputs. Pros: ordinary NixOS hosts and per-system outputs have explicit ownership (`nix/den/hosts.nix:7`, `nix/den/outputs.nix:25`). Cons: VM images remain ordinary NixOS build outputs (`nix/outputs.nix:27`), and device radio modules run on those hosts rather than as device-target Den classes (`nix/den/aspects.nix:30`). Baseline 2; installation earns O only. Confidence: high.

Total: **61.5/100**. Shortlists: showcase no; library_units mish USB coordinator mode; starter no. Library yes for the documented complete appliance mode. Showcase no without routed Den facts; starter no because this is an operator/hardware appliance with explicit commissioning gates, not a minimal personal setup.

Overall pros:
- Features, modes and hardware compose orthogonally (`nix/den/aspects.nix:19`).
- Independent consumers get an explicit import/device recipe (`docs/den-architecture.md:69`).
- Positive and rejection cases exercise real modes and architecture guards (`nix/checks.nix:153`, `nix/checks.nix:162`).

Overall cons / limits:
- Scope limit: native capability metadata is not Den dataflow (`modules/nixos/mish/den.nix:22`).
- Operational scope: private credentials/commissioning remain runtime operator actions (`README.md:69`).
- Coverage limit: physical hardware and RF acceptance remain open (`README.md:131`); static scoring asserts no pass.

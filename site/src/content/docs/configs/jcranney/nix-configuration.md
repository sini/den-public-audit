---
title: "jcranney/nix-configuration"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/jcranney/nix-configuration/)

- Upstream: [jcranney/nix-configuration](https://github.com/jcranney/nix-configuration)
- Reviewed revision: [`12376d630e3e`](https://github.com/jcranney/nix-configuration/commit/12376d630e3e344d6b57cbb9eca31bb83a175a7e)
- Author: jcranney
- Score: **25.0 / 100**, rank 101 of 101 ranked configs. D 2 · I 4 · S 2 · R 2 · P 5 · L 2 · V 2 · O 2 · B 2 · X 2. Shortlists: —.
- Summary: Compact direct provider selection, but broad personal bundles and source-patched shared values; honest narrow Linux scope, manual operations and no authored checks.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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

A compact defaults module wires shared batteries and HM class ([`modules/defaults.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L3), [`modules/defaults.nix:12`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L12)). Host modules declare inventory and per-user variants ([`modules/hosts/agnes.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L3), [`modules/hosts/agnes.nix:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L11)).

## 2. Common patterns

- mutual-provider enables host/user exchange ([`modules/defaults.nix:13`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L13)).
- den.default includes define-user and hostname ([`modules/defaults.nix:4`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L4)).

## 3. Novel patterns

Host-specific provides variants grant primary-user behavior to both accounts on a shared NixOS machine ([`modules/hosts/agnes.nix:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L11)).

## 4. Library candidates

None verified as a useful independent library unit in the reviewed composition.

## 5. den friction

No verified Den-specific friction in the reviewed default schema ([`modules/defaults.nix:12`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L12)).

## 6. Docs and complexity

Docs 3: README describes users and host roles ([`README.md:19`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L19), [`README.md:27`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L27)). Complexity 3: shared-host user variants plus a personal cross-class user aspect ([`modules/hosts/agnes.nix:4`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L4), [`modules/jcranney.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L7), [`modules/jcranney.nix:29`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L29)).

## 6a. Defects and scoring notes
- moderate · **I**: one personal aspect combines Docker, Tailscale, hardware udev rules, Git identity and shell preferences ([`modules/jcranney.nix:16`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L16), [`modules/jcranney.nix:24`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L24), [`modules/jcranney.nix:42`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L42), [`modules/jcranney.nix:62`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L62)). Boot/common similarly selects printing, discovery and SSH together ([`modules/bootable.nix:52`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L52), [`modules/bootable.nix:66`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L66), [`modules/bootable.nix:77`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L77)).
- moderate · **S**: shared VPN helper fixes an institutional endpoint, while the Git body fixes personal identity ([`modules/gpclient.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/gpclient.nix#L7), [`modules/jcranney.nix:47`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L47)). PARA locations are literal preferences rather than consumer settings ([`modules/para.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/para.nix#L7)). These cost S, not platform support again.
- minor · **L**: README's account/host graph describes bambi/etna and undeclared ruth/jeice, while source declares abdu and three concrete hosts ([`README.md:23`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L23), [`README.md:32`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L32), [`modules/hosts/agnes.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L3), [`modules/hosts/burter.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/burter.nix#L3)).
Two primary-user includes on Agnes are not inherently conflicting on NixOS: locked Den0f7675b0b789eabe1a62f8a31b5323a7ad3ca5c4 modules/aspects/batteries/primary-user.nix:23–28 adds groups to each user; uniqueness applies to Darwin/WSL scalar fields, not these NixOS users ([`modules/hosts/agnes.nix:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L11)). No evaluation was run.

## 7. Template notes

Useful primary-user scoping example; the large personal aspect combines identity, system services and shell preferences ([`modules/jcranney.nix:16`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L16), [`modules/jcranney.nix:47`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L47)).

## 8. Scorecard

### D (2, high)
Scope: Pros: explicit host/user and mutual-provider selection ([`modules/hosts/burter.nix:24`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/burter.nix#L24), [`modules/defaults.nix:13`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L13)). Cons: authored settings are direct module assignments; no live authored Den fact-routing channel is established ([`modules/jcranney.nix:42`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L42)). Baseline2; using batteries alone is not an authored routed-data contract. Confidence: high.

### I (4, high)
Scope: Pros: work, graphical and package families have named owners ([`modules/work.nix:2`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/work.nix#L2), [`modules/graphical.nix:2`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L2)). Cons: personal and common boot bundles carry unrelated system/user effects (§6a; [`modules/jcranney.nix:16`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L16), [`modules/bootable.nix:52`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L52)). Interpolation4 below localized5, above wholly undifferentiated2. Confidence: high.

### S (2, high)
Scope: Pros: effective home directory is used for some relative settings ([`modules/graphical.nix:93`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L93)). Cons: §6a identity/endpoint/device/path values must be patched in source ([`modules/jcranney.nix:47`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L47), [`modules/gpclient.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/gpclient.nix#L7), [`modules/bootable.nix:18`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L18), [`modules/para.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/para.nix#L7)). Contract2, leak coverage6: four grouped values (personal identity, anu.edu.au VPN endpoint, PARA dataset root, PARA repository root). Email/name/GitHub identity variants group together; timezones/locales and host-owned devices are not additional shared leaks. min(2,6)=2. Confidence: high.
```score-evidence
{"S": {"contract_design": 2, "leak_coverage": 6, "distinct_leaks": 4}}
```

### R (2, medium)
Scope: Pros: names make intended feature selection visible ([`modules/hosts/burter.nix:24`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/burter.nix#L24)). Cons: importable owners drag personal identity, global defaults, companion tools or a fixed institutional endpoint ([`modules/jcranney.nix:16`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L16), [`modules/gpclient.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/gpclient.nix#L7), [`modules/graphical.nix:97`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L97)). Literal2 for these as-written reuse boundaries; useful sub-block ideas require extracting and rewriting, not an independently importable unit. Confidence: medium.

### P (5, high)
Scope: Pros: all declared machines are x86_64 NixOS and hardware modules are per host ([`modules/hosts/agnes.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L3), [`modules/hosts/burter.nix:12`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/burter.nix#L12), [`modules/hosts/recoome.nix:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/recoome.nix#L11)). Cons/limit: hardcoded secondary x86 package import has no wider platform contract ([`modules/graphical.nix:73`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L73)), but no other architecture is promised. Literal5 honest narrow scope; S hardware defaults are not deducted twice. Confidence: high.

### L (2, high)
Scope: Pros: README gives rebuild command and inventory intentions ([`README.md:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L11), [`README.md:27`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L27)). Cons: operation-only notes do not explain entry-to-feature wiring, and inventory is stale (§6a; [`README.md:23`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L23)). Literal operation-only2, not absent1. Confidence: high.

### V (2, high)
Scope: Pros: flake inputs are pinned by lock and generated entry is identified ([`flake.nix:1`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/flake.nix#L1)). Cons: no authored representative checks or workflow invocation in the tracked entry/module inventory ([`flake.nix:5`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/flake.nix#L5), [`modules/dendritic.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/dendritic.nix#L3)). Baseline2 is observed absence of verification intent, not a failing test claim. Confidence: high.

### O (2, high)
Scope: Pros: operator rebuild workflow is documented ([`README.md:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L11)). Cons: it is a manual nixos-rebuild command, with no Den-derived deploy/secrets/bootstrap inventory ([`README.md:14`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L14), [`modules/defaults.nix:3`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/defaults.nix#L3)). Baseline2; normal service enablement is not operational inventory. Confidence: high.

### X (2, high)
Scope: Pros: host and home contributions are distinct ([`modules/jcranney.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L7), [`modules/jcranney.nix:29`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L29)). Cons: external tool package outputs remain ordinary packages, not separate Den classes ([`modules/shmim.nix:4`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/shmim.nix#L4), [`modules/yorick.nix:4`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/yorick.nix#L4)). Baseline2. Confidence: high.

### B (2, medium)
Scope: Census max-depth: Zsh1 + Niri.5 + installed-only VSCode.5 =2→diversity2. Reference0→2; mean2. Pros: real shell and home-server presets exist ([`modules/jcranney.nix:62`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L62), [`modules/hosts/agnes.nix:113`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L113)). Cons: they are bound into personal/host or broad multi-app owners, not complete independent reference units; installation lists, enables and token preference leaves count zero ([`modules/graphical.nix:77`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/graphical.nix#L77), [`modules/bootable.nix:26`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/bootable.nix#L26)). No count is inferred from package-list length. Confidence: medium.
```score-evidence
{"B": {"diversity_points": 2, "diversity_grade": 2, "reference_grade": 2, "reference_units": []}}
```

Total: **25.0/100**. Shortlists: showcase no; library_units none; starter no. No standout independently usable unit verified.

Overall pros:
- Named host/user selections are compact ([`modules/hosts/burter.nix:24`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/burter.nix#L24)).
- Hardware ownership stays per machine ([`modules/hosts/recoome.nix:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/recoome.nix#L11)).
- Rebuild instructions are explicit ([`README.md:11`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L11)).

Overall cons / limits:
- Broad personal aspect owns unrelated services ([`modules/jcranney.nix:16`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L16)).
- Shared Git/VPN bodies retain personal facts ([`modules/jcranney.nix:47`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/jcranney.nix#L47), [`modules/gpclient.nix:7`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/gpclient.nix#L7)).
- Inventory docs lag actual declarations ([`README.md:23`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/README.md#L23), [`modules/hosts/agnes.nix:4`](https://github.com/jcranney/nix-configuration/blob/12376d630e3e344d6b57cbb9eca31bb83a175a7e/modules/hosts/agnes.nix#L4)).

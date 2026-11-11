---
title: "jmartindf/dendritic"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/jmartindf/dendritic/)

- Upstream: [jmartindf/dendritic](https://github.com/jmartindf/dendritic)
- Reviewed revision: [`db88ba8d4a10`](https://github.com/jmartindf/dendritic/commit/db88ba8d4a1081f7bcd3be81037c54d007298bbf)
- Author: jmartindf
- Score: **40.5 / 100**, rank 86 of 101 ranked configs. D 5 · I 5 · S 4 · R 5 · P 5 · L 2 · V 3 · O 5 · B 2 · X 2. Shortlists: library units (1).
- Summary: D capability/context projection capped at5; I broad shared base; S shared installation facts remain; R light-adaptation Fish shell handoff; P actual Linux scope; L placeholder; V deploy schema/format checks; O selected per-host rekey integration but separate legacy deploy registry; B census2.5 and two complete app-file closures; X OS/HM only.

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

A private df namespace wraps shared Den defaults and host assembly ([`modules/desertflood/den/desertflood-namespaces.nix:5`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/desertflood-namespaces.nix#L5), [`modules/desertflood/den/defaults.nix:8`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/defaults.nix#L8)). Host capability flags control custom account/HM projection ([`modules/hosts/fossil/configuration.nix:28`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/fossil/configuration.nix#L28), [`modules/desertflood/den/docker/dockeras.nix:38`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L38)).

## 2. Common patterns

- namespace df is local ([`modules/desertflood/den/desertflood-namespaces.nix:5`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/desertflood-namespaces.nix#L5)).
- den.default includes define-user, HM and allow-unfree batteries ([`modules/desertflood/den/defaults.nix:10`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/defaults.nix#L10)).

## 3. Novel patterns

Docker-admin aspect builds an HM user entity by hand, resolves its class, and injects the module conditionally on a host capability ([`modules/desertflood/den/docker/dockeras.nix:15`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L15), [`modules/desertflood/den/docker/dockeras.nix:33`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L33), [`modules/desertflood/den/docker/dockeras.nix:38`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L38)).

## 4. Library candidates

**Fish shell handoff** — [`modules/desertflood/den/cli/fish.nix:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L3); NixOS/Darwin Bash entry → packaged Fish, with HM enable ([`modules/desertflood/den/cli/fish.nix:35`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L35), [`modules/desertflood/den/cli/fish.nix:92`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L92)). Inputs: Den0.8 context helpers, lib, pkgs and a local df namespace; parameter contract: OS/host/user contexts, no fleet identity. **B**: register/rename the namespace and retain this file's own OS/HM closure; no desktop/service fleet schema needed.

## 5. den friction

The pinned Den0.8 integration constructs a custom HM context and resolves it explicitly; this is additional adoption machinery, not a demonstrated incompatibility ([`flake.nix:64`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/flake.nix#L64), [`modules/desertflood/den/docker/dockeras.nix:22`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L22), [`modules/desertflood/den/docker/dockeras.nix:33`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L33)).

## 6. Docs and complexity

Docs 2: README is essentially TODO ([`README.md:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/README.md#L3)), with limited source comments explaining defaults ([`modules/desertflood/den/defaults.nix:11`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/defaults.nix#L11)). Complexity 5: capability-controlled manual HM entity resolution and multiple service-bearing hosts ([`modules/desertflood/den/docker/dockeras.nix:22`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L22), [`modules/hosts/france/configuration.nix:70`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/france/configuration.nix#L70)).

## 6a. Defects and scoring notes

- S · moderate: shared base fixes installation-specific DNS/cache and checkout policy, requiring edits for another deployment ([`modules/desertflood/den/base.nix:103`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L103), [`modules/desertflood/den/base.nix:195`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L195), [`modules/desertflood/den/base-server.nix:72`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base-server.nix#L72)).
- L · moderate: README leaves the custom capability/HM setup undocumented ([`README.md:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/README.md#L3), [`modules/desertflood/den/docker/dockeras.nix:85`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L85)).
- Manual HM construction and a fixed generic service-account name are not independently demonstrated defects ([`modules/desertflood/den/docker/dockeras.nix:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L3), [`modules/desertflood/den/docker/dockeras.nix:33`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L33)).

## 7. Template notes

An advanced historical/integration example, requiring readers to understand manual aspect resolution and custom OS/HM contexts ([`modules/desertflood/den/docker/dockeras.nix:22`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L22)).

## 8. Scorecard

### D (5, medium)
Scope: live host capability → Docker/account/HM consumers. Pros: fossil sets the capability, Docker branches on it, and the account module explicitly has an empty false branch ([`modules/hosts/fossil/configuration.nix:28`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/fossil/configuration.nix#L28), [`modules/desertflood/den/docker/docker-server.nix:15`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-server.nix#L15), [`modules/desertflood/den/docker/dockeras.nix:55`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L55)). Cons: these are direct entity facts and conditional projections, without a routed quirk/policy channel. Non-routing cap5; manual HM resolution adds no extra D ([`modules/desertflood/den/docker/dockeras.nix:33`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L33)). Confidence: medium.

### I (5, medium)
Scope: df namespace, shared defaults and host assembly. Pros: Docker selection has a named boundary and capability contract ([`modules/desertflood/den/docker/docker-server.nix:42`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-server.nix#L42)); hosts select server features explicitly ([`modules/hosts/fossil/configuration.nix:36`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/fossil/configuration.nix#L36)). Cons: df.base owns packages, SSH, sudo, DNS and Nix policy together ([`modules/desertflood/den/base.nix:63`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L63), [`modules/desertflood/den/base.nix:103`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L103), [`modules/desertflood/den/base.nix:139`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L139)). Anchor5: workable features with broad baseline ownership. Confidence: medium.

### S (4, low)
Scope: visible Den defaults/base/server/CLI/Docker bodies; the older native service forest is not an exhaustive leak census. Pros: host capability and user contexts supply real variation ([`modules/desertflood/den/docker/docker-server.nix:15`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-server.nix#L15), [`modules/desertflood/den/base.nix:257`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L257)). Cons: the shared base fixes three unrelated domain roots and a private cache URL/key, while base-server fixes one checkout root ([`modules/desertflood/den/base.nix:103`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L103), [`modules/desertflood/den/base.nix:195`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L195), [`modules/desertflood/den/base.nix:202`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L202), [`modules/desertflood/den/base-server.nix:72`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base-server.nix#L72)). Five grouped changes (three domains, cache pair, checkout), raw at least6 literals. Contract4: some context contracts but substantial installation policy implicit, below5; coverage6 capped by five groups; min=4. Fixed dockeras is a service-account name, not an inferred personal-identity leak ([`modules/desertflood/den/docker/dockeras.nix:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L3)). Confidence: low.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":5,"raw_leaks":6}}
```

### R (5, medium)
Scope: §4 Fish shell handoff. Pros: its OS and HM branches own Fish enablement and packaged Bash handoff ([`modules/desertflood/den/cli/fish.nix:12`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L12), [`modules/desertflood/den/cli/fish.nix:40`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L40), [`modules/desertflood/den/cli/fish.nix:92`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L92)). Cons: adopt the pinned Den0.8 context helpers and register/rename df; no standalone consumer documentation ([`flake.nix:64`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/flake.nix#L64), [`modules/desertflood/den/cli/fish.nix:101`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L101)). Grade B, anchor5. The shared pc/CLI aspect address does not itself disqualify an independently importable app-file closure. Confidence: medium.

### P (5, medium)
Scope: four declared x86_64-linux hosts and OS/HM context boundaries. Pros: OS contexts explicitly distinguish NixOS and Darwin, and HM projection receives the chosen host class ([`modules/desertflood/den/base.nix:47`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L47), [`modules/desertflood/den/docker/dockeras.nix:37`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L37)). Cons: actual host support is Linux; Darwin branches are not independently demonstrated by a declared target ([`modules/hosts/fossil/configuration.nix:18`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/fossil/configuration.nix#L18), [`modules/hosts/france/configuration.nix:18`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/france/configuration.nix#L18)). Anchor5 for honest Linux scope with hand-owned boundaries; no unsupported-platform failure inferred. Confidence: medium.

### L (2, medium)
Scope: README and feature comments. Pros: defaults document why user/HM batteries are selected ([`modules/desertflood/den/defaults.nix:11`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/defaults.nix#L11)). Cons: README is only a title and TODO, with no host/capability/HM adaptation path ([`README.md:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/README.md#L3)). Placeholder anchor2. Confidence: medium.

### V (3, medium)
Scope: authored check exports and formatting setup. Pros: deploy-rs schema checks are actually exported and treefmt enables its flake check ([`modules/flake/deploy-rs.nix:45`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/deploy-rs.nix#L45), [`modules/flake/treefmt.nix:19`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/treefmt.nix#L19)). Cons: these do not assert the custom capability false path or manually resolved HM consumer; pre-commit hook configuration is empty ([`modules/flake/pre-commit-hooks.nix:18`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/pre-commit-hooks.nix#L18)). Interpolation3 above absent checks2, below representative Den semantic tests5; no execution claimed. Confidence: medium.

### O (5, medium)
Scope: selected Den host secrets integration and deployment generation. Pros: df.base imports the agenix/rekey module; rekey storage varies by resulting hostName, and hosts supply their own public key ([`modules/desertflood/den/base.nix:64`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L64), [`modules/desertflood/bases/agenix.nix:20`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/bases/agenix.nix#L20), [`modules/hosts/fossil/configuration.nix:70`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/hosts/fossil/configuration.nix#L70)). Cons: deploy nodes traverse a separate desertflood.hosts registry, not den.hosts; fixed SSH identity is another manual operational convention ([`modules/flake/deploy-rs.nix:23`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/deploy-rs.nix#L23), [`modules/flake/deploy-rs.nix:35`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/deploy-rs.nix#L35)). Anchor5 for the selected aspect-owned per-host secrets path; the adjacent legacy deployment registry earns no Den-derived orchestration increment. Confidence: medium.

### B (2, low)
Scope: all visible Den definition files, excluding unrelated legacy native service/package definitions. Pros: Fish and Eza each have an independently importable coherent app-file closure; Eza's Fish integration retains the Fish helper file ([`modules/desertflood/den/cli/fish.nix:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L3), [`modules/desertflood/den/cli/eza.nix:11`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/eza.nix#L11)). Cons: broad profiles, package-only coreutils and a single Lazydocker command are excluded; server/Docker units require fleet schema or local packages ([`modules/desertflood/den/cli/coreutils.nix:17`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/coreutils.nix#L17), [`modules/desertflood/den/docker/docker-tools.nix:38`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-tools.nix#L38), [`modules/desertflood/den/docker/docker-server.nix:21`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-server.nix#L21)). Shared aspect address is not an exclusion by itself. Census2.5→diversity2; two references→2; B2. Confidence: low.
```score-evidence
{"B":{"diversity_points":2.5,"diversity_grade":2,"reference_grade":2,"reference_units":[{"name":"Fish shell handoff","evidence":"modules/desertflood/den/cli/fish.nix:3"},{"name":"Eza Fish functions","evidence":"modules/desertflood/den/cli/eza.nix:11"}]}}
```

### X (2, medium)
Scope: custom contexts and class projection. Pros: the manual projection resolves a real HM class ([`modules/desertflood/den/docker/dockeras.nix:33`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L33)). Cons: it still targets ordinary OS/HM configuration, not an additional nonoperational target family ([`modules/desertflood/den/docker/dockeras.nix:17`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L17)). Baseline2. Confidence: medium.

Total: **40.5/100**. Shortlists: showcase no; library_units Fish shell handoff; starter no. A useful source example of capability-driven account projection, with a light-adaptation Fish library nomination; no routed showcase or short documented starter path.

Overall pros:
- Capability selection reaches Docker and account consumers ([`modules/desertflood/den/docker/docker-server.nix:15`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/docker-server.nix#L15), [`modules/desertflood/den/docker/dockeras.nix:55`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/docker/dockeras.nix#L55)).
- OS/HM bodies have explicit context boundaries ([`modules/desertflood/den/base.nix:47`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L47), [`modules/desertflood/den/base.nix:257`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L257)).
- Deployment schema checks are exported ([`modules/flake/deploy-rs.nix:45`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/deploy-rs.nix#L45)).

Overall cons / limits:
- S: shared DNS/cache/checkout policy requires second-consumer edits ([`modules/desertflood/den/base.nix:103`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L103), [`modules/desertflood/den/base.nix:195`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base.nix#L195), [`modules/desertflood/den/base-server.nix:72`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/base-server.nix#L72)).
- L: README remains TODO ([`README.md:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/README.md#L3)).
- O limit: deployment inventory is separately maintained ([`modules/flake/deploy-rs.nix:35`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/flake/deploy-rs.nix#L35)).

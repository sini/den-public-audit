# Le0-dot__config.nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/Le0-dot__config.nix.md)

- Upstream: [Le0-dot/config.nix](https://github.com/Le0-dot/config.nix)
- Reviewed revision: [`4171c4b9f1f2`](https://github.com/Le0-dot/config.nix/commit/4171c4b9f1f2ad0dbcab61f829cea31135064057)
- Author: Le0-dot
- Score: **57.5 / 100**, rank 20 of 103 ranked configs. D 6 · I 7 · S 6 · R 5 · P 7 · L 5 · V 6 · O 7 · B 3 · X 5. Shortlists: showcase.
- Summary: D routed Quadlet limited by selected OCI adapter error; I repeated host notifications; S five adaptation groups; P explicit SystemManager bridge checks; O host-derived tools; X custom container family; B two independent presets.

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

A flake-parts/import-tree configuration models NixOS and system-manager hosts plus nested container entities (`flake.nix:53`, `modules/infra.nix:2`). Container classes select quadlet or OCI runtimes while policies adapt common behavior by host class (`modules/containers/schema.nix:36`, `modules/policies/hostname.nix:3`).


## 2. Common patterns.

- custom schema/classes: container inherits conf and has host parent (`modules/containers/schema.nix:11`).
- policies: host-to-containers resolves each nested container in shared scope (`modules/containers/schema.nix:16`).
- define-user: standard battery is paired with system-manager-specific user creation (`modules/policies/define-user.nix:3`).


## 3. Novel patterns.

Container aspect lookup combines name@host and plain name so shared services can have host-specific refinements (`modules/containers/schema.nix:54`).


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Container lookup imports den internal _types.nix directly (`modules/containers/schema.nix:8`). Hostname policy excludes systemManager and define-user adds a custom system-manager branch (`modules/policies/hostname.nix:5`, `modules/policies/define-user.nix:3`), suggesting broader class-aware battery needs.


## 6. Docs and complexity.

Docs 3: README teaches branch-based deployment and promotion (`README.md:5`, `README.md:15`). Complexity 5: nested entities and runtime classes span three declared hosts, including systemManager (`modules/infra.nix:2`, `modules/infra.nix:30`, `modules/containers/schema.nix:25`).


## 6a. Defects and scoring notes.

- D · major: OCI route adaptArgs applies a plain attrset to a function, a structural type error on the selected OCI branch (`modules/containers/oci-container.nix:19`, `modules/infra.nix:32`). No evaluation performed.
- I · moderate: Nu repeats notification script/service behavior across backup jobs, increasing coordinated edits (`modules/aspects/hosts/nu.nix:266`, `modules/aspects/hosts/nu.nix:299`, `modules/aspects/hosts/nu.nix:356`).
- S · moderate: five grouped adaptation values remain in shared bodies, enumerated in S (`modules/aspects/auto-upgrade.nix:6`, `modules/aspects/containers/ntfy.nix:32`, `modules/aspects/containers/adguardhome.nix:35`).
Custom policies/classes and private Den helper use are functionality/maintenance boundaries, not inherently defects.

## 7. Template notes.

Advanced schema reference rather than first template; internal lookup dependency needs a public API before generalizing (`modules/containers/schema.nix:8`).

## 8. Scorecard.

### D
Scope: container inventory → class route → host resources. Pros: host-to-containers resolves each declared entity, Quadlet route adapts config/resources and imports its module (`modules/containers/schema.nix:16`, `modules/containers/quadlet.nix:10`, `modules/containers/quadlet.nix:26`, `modules/containers/quadlet.nix:43`). Cons: selected OCI counterpart calls a plain attrset as a function (`modules/containers/oci-container.nix:19`); no explicit duplicate-resource policy demonstrated. Interpolated6: live routed composition beyond5, broken alternate route prevents strong generalized routing. Score **6**; confidence **medium**.

### I
Scope: aspects versus host composition. Pros: container features and routing mechanisms have separate owners (`modules/aspects/containers/adguardhome.nix:6`, `modules/containers/quadlet.nix:10`). Cons: Nu embeds repeated backup notification implementations rather than composing one notification feature (`modules/aspects/hosts/nu.nix:266`, `modules/aspects/hosts/nu.nix:299`, `modules/aspects/hosts/nu.nix:356`). Interpolated7: strong feature organization with this concrete repeated behavior below9. Score **7**; confidence **medium**.

### S
Scope: typed entity/options and shared deployment/container assumptions. Pros: typed container class/lookup, Samba user records and Neovim configPath parameter (`modules/containers/schema.nix:36`, `modules/aspects/server/samba.nix:12`, `modules/aspects/terminal/neovim.nix:2`). Contract6, beyond useful5 with multiple purposeful interfaces, below9 comprehensive surfaces. Cons: five grouped adaptation values remain: upgrade repository, tailnet domain, ntfy administrator identity, fleet Btrfs layout, external editor checkout (`modules/aspects/auto-upgrade.nix:6`, `modules/aspects/containers/ntfy.nix:32`, `modules/aspects/containers/ntfy.nix:37`, `modules/aspects/containers/adguardhome.nix:35`, `modules/aspects/terminal/neovim.nix:26`). Coverage6; repeated image ports are normal defaults, host disk IDs remain host-local. min(6,6)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":6,"distinct_leaks":5}}
```

### R
Scope: independently usable definitions rather than complete fleet. Pros: Samba exposes typed accounts/password files and coherent protocol/discovery behavior; Stylix owns its upstream import (`modules/aspects/server/samba.nix:11`, `modules/aspects/server/samba.nix:26`, `modules/aspects/stylix.nix:5`). Cons: no documented extraction consumer; many containers depend on external self.lib and disk schema (`modules/aspects/containers/adguardhome.nix:35`). Literal5 useful units, not9 documented substantial A-unit. Score **5**; confidence **medium**.

### P
Scope: NixOS/SystemManager/HM bridging. Pros: supported OS paths and parentArg are explicit, SystemManager avoids managing OS accounts and has a boundary assertion (`modules/home-manager.nix:8`, `modules/home-manager.nix:38`, `modules/policies/define-user.nix:7`, `modules/aspects/hosts/omega.nix:22`). Cons: no Darwin concrete consumer or negative-context fixtures shown. Interpolated7 beyond honest-narrow5 for explicit multiple boundaries and selected SystemManager assertion, below9 exhaustive boundary evidence. Score **7**; confidence **medium**.

### L
Scope: operator README. Pros: branch promotion/deployment model and commands are explained (`README.md:5`, `README.md:19`). Cons: authoring a new container/host and route failure semantics are not worked through alongside custom classes (`modules/containers/schema.nix:16`). Literal5 useful system explanation, not9 comprehensive worked authoring. Score **5**; confidence **medium**.

### V
Scope: CI and per-target assertions. Pros: CI invokes flake check, host checks include Omega HM/account boundary assertions (`.github/workflows/check.yaml:15`, `modules/policies/assert.nix:7`, `modules/aspects/hosts/omega.nix:22`). Cons: OCI argument adapter has no targeted fixture; CI configuration alone does not prove passing (`modules/containers/oci-container.nix:19`). Interpolated6 above5 structural checks for explicit boundary assertion, below9 failure/collision fixtures. Static review only. Score **6**; confidence **medium**.

### O
Scope: host-derived switch/install artifacts and branch operations. Pros: each host gets switch/remote-switch/remote-install packages selected by class, and upgrades derive branch from hostname (`modules/policies/switch.nix:9`, `modules/policies/switch.nix:23`, `modules/policies/switch.nix:54`, `modules/aspects/auto-upgrade.nix:6`). Cons: upgrade source is author-specific and deployment workflow repeats branch/SSH conventions (`.github/workflows/deploy.yaml:9`). Interpolated7 for several actual operational outputs, below9 failure/rollback safeguards. Score **7**; confidence **medium**.

### X
Scope: non-host container entities/classes. Pros: first-class container schema routes Quadlet resources into host modules (`modules/containers/schema.nix:36`, `modules/containers/quadlet.nix:13`). Cons: extension is bounded to containers and alternate OCI route is defective, charged only under D (`modules/containers/oci-container.nix:19`). Literal5 one substantial custom target family; disk/switch operations counted O and SystemManager counted P. Score **5**; confidence **medium**.

### B
Scope: selected census diversity and all independently complete application presets. Pros: Samba and Stylix own meaningful behavior/dependencies (`modules/aspects/server/samba.nix:26`, `modules/aspects/stylix.nix:5`). Cons: Dunst/Ghostty/Tofi/Wlogout require external Stylix schema, terminal bundle also assumes it, container storage relies on self.lib, Television declares runtime requirements without owning their installation, Neovim native config is external (`modules/aspects/desktop/dunst.nix:4`, `modules/aspects/terminal/default.nix:17`, `modules/aspects/containers/adguardhome.nix:35`, `modules/aspects/terminal/television.nix:16`, `modules/aspects/terminal/neovim.nix:26`). Excluded whole dependent units, not silently extracted cores. Score **3**; confidence **medium**.
B_div: 4 points → 3; B_ref: 2 units → 2; half-up mean → 3.
```score-evidence
{"B":{"diversity_points":4,"diversity_grade":3,"reference_grade":2,"reference_units":[{"name":"samba","evidence":"modules/aspects/server/samba.nix:11"},{"name":"stylix","evidence":"modules/aspects/stylix.nix:5"}]}}
```

Total: **57.5/100**. Shortlists: showcase true; library_units []; starter false.

Overall pros:
- Real container entities and class routing (`modules/containers/schema.nix:16`).
- SystemManager account boundary is asserted (`modules/aspects/hosts/omega.nix:22`).
- Inventory derives operational packages (`modules/policies/switch.nix:9`).

Overall cons / limits:
- OCI adapter is a call of a plain attrset (§6a D; `modules/containers/oci-container.nix:19`).
- Host repeats notification behavior (§6a I; `modules/aspects/hosts/nu.nix:299`).
- Shared ntfy identity/domain and storage assumptions remain (§6a S; `modules/aspects/containers/ntfy.nix:32`).

# FastTrackStudios__task

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/FastTrackStudios__task.md)

- Upstream: [FastTrackStudios/task](https://github.com/FastTrackStudios/task)
- Reviewed revision: [`a40932117efa`](https://github.com/FastTrackStudios/task/commit/a40932117efadcace0179d510514d6470df318cd)
- Author: FastTrackStudios
- Score: **partial: 51.0 of 90 applicable** (not ranked). D 2 · I 9 · S 9 · R 9 · P 8 · L 7 · V 4 · O – · B 2 · X 2. Shortlists: library units (1).
- Summary: Substantial native module merits library selection under actual reuse-contract anchors; packaging with prospective Den wiring is neither a Den showcase nor host/user starter.

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
This is application packaging, not a deployed den fleet: flake-parts/import-tree loads typed fts perSystem build modules (`flake.nix:4`, `flake.nix:19`). Den is imported as a future sharing surface; the task-node example is commented documentation (`nix/modules/den.nix:8`, `nix/modules/den.nix:13`).

## 2. Common patterns
- Dendritic loading organizes packaging concerns, but does not establish active host/aspect composition (`flake.nix:8`, `flake.nix:20`).
- Den module import exists without an active task-node declaration in that wiring file (`nix/modules/den.nix:13`, `nix/modules/den.nix:18`).

## 3. Novel patterns
Typed fts options share packaging values while a plain NixOS module exposes the server to arbitrary system flakes, deliberately keeping deployment independent of den (`flake.nix:11`, `nix/modules/den.nix:10`).

## 4. Library candidates
- task-server module · `nix/nixos/task-server.nix:64` · complete ordinary NixOS service API, intentionally independent of Den · inputs: nixpkgs/lib and task-server package (default supplied by exported wrapper, `nix/modules/nixos-modules.nix:20`) · typed options for mode, data, bind/port, credentials and runtime user · **A**, substantial native unit with minimal consumer at `nix/nixos/task-server.nix:18`; it is not an implemented Den aspect.

## 5. den friction
No verified den-specific failure: current heavy outputs intentionally remain ordinary perSystem modules (`nix/modules/den.nix:8`). Counting the commented task-node example as an implemented den feature would overstate adoption (`nix/modules/den.nix:13`).

## 6. Docs and complexity
Docs **4**: packaging ownership, input pin policy and runtime installation modes are explained (`flake.nix:4`, `flake.nix:26`, `README.md:18`). Complexity **3**: application packaging separates toolchain/dependency pins from runtime module exports (`flake.nix:26`, `nix/modules/den.nix:10`); den-specific complexity is low.

## 6a. Defects and scoring notes

No additional concrete scored defects verified in the scoped packaging/native-module contract. The imported Den sharing surface remains prospective, explicitly documented (`nix/modules/den.nix:8`); this is classification/anchor coverage, not a defect. Test invocation/negative-case coverage is limited at `nix/modules/nixos-modules.nix:34` and is not presented as a failed check.

## 7. Template notes
Helpful application-packaging reference, unsuitable as a host/user den template because its actual sharing API is a plain NixOS module (`nix/modules/den.nix:10`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Den import is active but task-node is a documented example (`nix/modules/den.nix:13`, `nix/modules/den.nix:18`). fts.* native perSystem values connect packages (`nix/modules/options.nix:1`), without a Den fact/route/consumer chain. Literal2 for Den flow, not a penalty to the application build system. Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Packaging modules share one declared fts contract instead of reaching into siblings (`nix/modules/options.nix:1`); runtime module/export wrapper are separated (`nix/modules/nixos-modules.nix:18`, `nix/nixos/task-server.nix:64`). Clear concern ownership fits packaging/library scope and9; no unrelated-bundle defect verified. Score **9**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract9: native service API types mode, port, credentials and data/user paths, with coherent defaults and documented nulls (`nix/nixos/task-server.nix:75`, `nix/nixos/task-server.nix:105`, `nix/nixos/task-server.nix:140`); consumer changes settings, not implementation (`nix/nixos/task-server.nix:18`). Coverage9, zero grouped leaks in this reusable unit; release pins/upstream source URLs and examples are not author leaks. Score **9**; confidence **medium**.

```score-evidence
{"S":{"contract_design":9,"leak_coverage":9,"distinct_leaks":0}}
```

### R

Scope · pros · cons/coverage: Newly verified task-server module is substantial A with explicit package dependency, configurable runtime and a minimal external consumer (`nix/nixos/task-server.nix:18`, `nix/modules/nixos-modules.nix:20`, `nix/nixos/task-server.nix:165`). Fits9 actual reuse contract. Native NixOS API earns R without pretending task-node exists. Score **9**; confidence **high**.

### P

Scope · pros · cons/coverage: Supported systems explicitly replace broad defaults (`nix/modules/systems.nix:5`, `nix/modules/systems.nix:11`); NixOS module check is Linux-guarded (`nix/modules/nixos-modules.nix:38`). Clean package/native boundary exceeds5; no comprehensive failing-unsupported/context matrix verified, hence8. Score **8**; confidence **medium**.

### L

Scope · pros · cons/coverage: Entry explains module ownership and pin coupling (`flake.nix:4`, `flake.nix:26`); native service teaches consumer import, sign-in and update semantics (`nix/nixos/task-server.nix:18`, `nix/nixos/task-server.nix:24`). Above5 for concrete prerequisites, below9 because default packaging and external fleet layers remain separate learning paths (`flake.nix:32`). Score **7**; confidence **high**.

### V

Scope · pros · cons/coverage: Rendered-unit check substitutes a stub and asserts service environment/state/user (`nix/modules/nixos-modules.nix:41`, `nix/modules/nixos-modules.nix:61`, `nix/modules/nixos-modules.nix:71`). Relevant positive output check exceeds2; no tracked invocation/negative module-context fixture established, so4 below representative automated5. App CI exists (`.github/workflows/checks.yml:43`) but is not assumed to run this check. Score **4**; confidence **medium**.

### O

Scope · pros · cons/coverage: Explicit packaging-only root (`flake.nix:4`) and module export (`nix/modules/nixos-modules.nix:25`) own no host/home; deployment workflows for the app are not a Den fleet. Truly not_applicable. Score **null**; confidence **high**.

### X

Scope · pros · cons/coverage: Images/packages and native NixOS module are built beside Den (`nix/modules/den.nix:8`, `nix/modules/nixos-modules.nix:25`). No Den custom target class drives them; baseline2, independent of real app release breadth. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census verified Bash installation in Linux image only gives0.5 → B_div2. Complete native Task module is valuable R evidence but no active application aspect exists (`nix/modules/den.nix:13`), so reference-aspect list is empty/B_ref2. Mean2; no package count substitution. Score **2**; confidence **high**.

```score-evidence
{"B":{"diversity_points":0.5,"diversity_grade":2,"reference_grade":2,"reference_units":[]}}
```

**Total:** 51.0/90; score null, missing O. **Shortlists:** showcase no; library task-server module; starter no. Substantial native module merits library selection under actual reuse-contract anchors; packaging with prospective Den wiring is neither a Den showcase nor host/user starter.

Overall pros:
- Native API has typed caller variation (`nix/nixos/task-server.nix:75`, `nix/nixos/task-server.nix:105`).
- Complete minimal consumer and package default (`nix/nixos/task-server.nix:18`, `nix/modules/nixos-modules.nix:20`).
- Rendered service has inspectable assertions (`nix/modules/nixos-modules.nix:71`).

Overall cons / scope limits:
- Scope: task-node remains an example (`nix/modules/den.nix:13`).
- Coverage: module check is one enabled rendering, no negative contexts shown (`nix/modules/nixos-modules.nix:49`).
- Prerequisite: packaging inherits external fleet pins (`flake.nix:32`).

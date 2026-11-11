# closure-labs__foundation

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/closure-labs__foundation.md)

- Upstream: [closure-labs/foundation](https://github.com/closure-labs/foundation)
- Reviewed revision: [`0715d5823b45`](https://github.com/closure-labs/foundation/commit/0715d5823b453f4b8d5a2fa4aaa368ef669a2796)
- Author: closure-labs
- Score: **65.5 / 100**, rank 6 of 103 ranked configs. D 5 · I 9 · S 7 · R 9 · P 9 · L 9 · V 9 · O 5 · B 2 · X 2. Shortlists: library units (1).
- Summary: Strong exported and checked profile constructor; direct context-derived facts capped5, narrow platform boundaries explicit, app descriptor count not mistaken for complete presets.

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

This is a home-environment product with a real instantiated home output, not only an aspect library (`modules/flake/exports/_outputs.nix:6`, `modules/flake/exports/_outputs.nix:14`). A profile compiler generates Den aspect membership and a custom HM constructor (`modules/home/construction/_module.nix:29`).

## 2. Common patterns

- homes (standalone HM) selects identity and package set from normalized profile (`modules/home/construction/_module.nix:29`).
- provides-like feature aliases sit over dependency-generated aspect includes (`modules/home/construction/_aspects.nix:4`).

## 3. Novel patterns

The independent feature graph is checked against resolved Den membership, making composition drift an explicit assertion (`modules/home/construction/_module.nix:61`). Profile data reaches HM through extraSpecialArgs (`modules/home/construction/_module.nix:40`); this is not a verified Den quirk/pipe route.

## 4. Library candidates
- **espanso-user-service · A:** independently importable HM user-service module, with store-owned executable, graphical-session lifecycle and restart policy; standard pkgs only, Wayland package choice explicit (`modules/apps/espanso/_settings.nix:1`, `modules/apps/espanso/_settings.nix:9`). Rewrite as an optional service with configurable package.

## 5. den friction
HM instantiate injects product-specific composition/assets through extraSpecialArgs (`modules/home/construction/_module.nix:33`). This is a custom constructor choice, not a verified Den defect. Independent graph closure is checked against actual Den-delivered feature membership (`modules/home/construction/_module.nix:61`).

## 6. Docs and complexity
Docs5: README separates supported substrate, personal configuration ownership and default update path (`README.md:7`, `README.md:12`, `README.md:74`); API guide supplies a minimal consumer and parameter contracts (`docs/API.md:7`, `docs/API.md:53`). Complexity5: normalized profile graph, custom instantiation and parity assertions (`modules/home/construction/_module.nix:11`, `modules/home/construction/_module.nix:61`).

## 6a. Defects and scoring notes
- minor · **S**: two application launchers embed the Vates organization endpoint instead of a per-consumer URL setting; one grouped registered-domain leak (`modules/apps/grist/_settings.nix:5`, `modules/apps/vates-notes/_settings.nix:5`). This is outside the otherwise explicit normalized profile contract.
No additional functional defect verified. Narrow x86_64 Bluefin support is documented and validated, not a portability defect (`README.md:7`, `modules/hosts/identity/_catalog.nix:37`). Head selection in password-manager discovery is guarded by a <=1 assertion, so it is not an unguarded duplicate drop (`modules/home/password-managers/_home.nix:19`, `modules/home/password-managers/_home.nix:71`).

## 7. Template notes
Advanced product/graph example rather than a minimal Den starter: it requires Bluefin, Homebrew and a graphical session (`README.md:17`) plus custom constructor/composition machinery (`modules/home/construction/_module.nix:16`).

## 8. Scorecard

### D (5, high)
Scope: profile/schema facts, Den membership and HM context. Pros: normalized identity selects den.homes, and host/composition facts reach HM through explicit special args (`modules/home/construction/_module.nix:11`, `modules/home/construction/_module.nix:29`, `modules/home/construction/_module.nix:40`); camera facts control Firefox policies (`modules/apps/firefox/_home.nix:20`). Cons: graph-generated includes and direct args are not authored quirk/policy/pipe routing (`modules/home/construction/_aspects.nix:4`). Non-quirk channel cap5 applies; sophisticated graph resolution and package plumbing do not lift D. Confidence: high.

### I (9, high)
Scope: feature ownership and generated selection. Pros: each feature owns its descriptor/configuration; constructor derives includes from graph dependencies (`modules/apps/espanso/_feature.nix:14`, `modules/home/construction/_aspects.nix:4`), and actual membership is asserted against graph closure (`modules/home/construction/_module.nix:61`). Cons/limit: there is substantial machinery, but default routes are separate and optional app configuration remains behind selected features (`modules/profiles/composition/_selection.nix:14`). Literal9 for clear ownership at this product scale, not file count. Confidence: high.

### S (7, medium)
Scope: profile inputs, constructor contracts and application settings. Pros: account/host/roles are normalized and consumer modules and package policy are explicit parameters (`modules/flake/exports/_api.nix:48`, `modules/hosts/identity/_catalog.nix:20`, `docs/API.md:53`). Owned-input collisions fail before construction (`modules/flake/exports/_api.nix:61`). Cons: app endpoints escape this contract (§6a; `modules/apps/grist/_settings.nix:5`). Contract7 interpolates between mostly explicit5 and comprehensive9; coverage9 on one grouped vates.tech domain (two raw endpoint literals, subdomains grouped). Generic finite defaults and vendor package endpoints are not author leaks (`modules/home/base/_home.nix:7`). min(7,9)=7. Confidence: medium.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":9,"distinct_leaks":1,"raw_leaks":2}}
```

### R (9, high)
Scope: exported whole-home constructor plus independent small service unit. Pros: mkHomeConfiguration exposes profile/modules/extraInputs/packagePolicy with validation (`modules/flake/exports/_api.nix:48`); the minimal consumer invokes this API without copying internals (`templates/default/flake.nix:6`, `docs/API.md:15`). Espanso service is separately importable (`modules/apps/espanso/_settings.nix:1`). Cons/limit: many individual applications depend on product composition and are not independently reusable aspect units (`modules/profiles/composition/_application.nix:1`). Literal9 for an actual substantial public constructor and consumer, not the app count. Confidence: high.

### P (9, high)
Scope: explicitly supported x86_64 Linux/Bluefin substrate. Pros: supported choices are enumerated; unsupported systems and contradictory Dell hardware fail with explicit messages (`modules/hosts/identity/_catalog.nix:4`, `modules/hosts/identity/_catalog.nix:37`, `modules/hosts/identity/_catalog.nix:43`); positive/negative hardware tests include ARM rejection and duplicate GPUs (`tests/test_host_profiles.py:37`, `tests/test_host_profiles.py:53`). Cons/limit: no ARM/Darwin promise; fixed output system matches documented scope (`modules/flake/exports/_outputs.nix:2`, `README.md:7`). Literal9 for clear checked boundaries within scope. Confidence: high.

### L (9, high)
Scope: user path versus library internals. Pros: prerequisites and a build-before-activation default path are explicit (`README.md:17`, `README.md:23`); API docs explain constructor collision and policy behavior with examples (`docs/API.md:7`, `docs/API.md:17`, `docs/API.md:53`). Cons/limit: advanced architecture still requires several concepts, but the default path does not start there (`README.md:15`). Literal9 for composition/prerequisite teaching, not documentation volume. Confidence: high.

### V (9, high)
Scope: source-declared checks and invocation. Pros: graph extension fixtures reject mismatched/missing/cyclic dependencies (`tests/test_feature_graph.py:59`, `tests/test_feature_graph.py:79`); constructor fixtures reject owned-input collisions before evaluation (`tests/test_constructor_inputs.py:59`), and hardware tests exercise contexts (`tests/test_host_profiles.py:37`). Workflow invokes fixture unittest discovery and Nix checks (`.github/workflows/check.yml:54`, `.github/workflows/check.yml:73`, `tests/ci.sh:8`). Cons/limit: no passing status or activation success claimed. Literal9 for focused boundary cases with invocation. Confidence: high.

### O (5, medium)
Scope: selected home generation and privileged helper requirement. Pros: selected home packages produce a precise browser-helper requirement through the aspect's generation output (`modules/home/password-managers/_home.nix:10`, `modules/home/password-managers/_home.nix:81`); requirement hashes the chosen helper/wrapper (`modules/home/password-managers/_package.nix:39`) and the operational reader consumes the resulting generation manifest (`scripts/password_manager_requirements.py:21`, `scripts/password_manager_requirements.py:58`). Cons: administrator installation remains an explicit external step, and no multi-host deployment/builders graph is established (`README.md:55`). Literal5 for one selected-aspect-derived operational contract, not broad CLI packaging. Confidence: medium.

### X (2, high)
Scope: class/output contract. Pros: real standalone HM construction is explicit (`modules/home/construction/_module.nix:29`). Cons: Flatpak/nixGL remain HM configuration and scripts/packages remain normal outputs, not separate Den target classes (`modules/providers/graphics/_home.nix:26`, `modules/flake/exports/_outputs.nix:15`). Baseline2. Confidence: high.

### B (2, medium)
Scope: all app descriptors, actual configuration owners and census adoption. Census: Zsh1 + installed-only Neovim.5 =1.5→diversity2. One complete unit→reference2; mean2. Pros: Espanso module owns the executable/service lifecycle (`modules/apps/espanso/_settings.nix:1`). Cons: descriptor app installs depend on foundationComposition/provider graph and are not complete presets (`modules/profiles/composition/_application.nix:1`, `modules/apps/neovim/_feature.nix:14`); Firefox needs product host/package/graphics conventions, Ghostty's package patch alone is one preference, and devops is an inseparable multi-app capability (`modules/apps/firefox/_home.nix:9`, `modules/apps/ghostty/_package.nix:10`, `modules/capabilities/devops/_home.nix:3`). Password-manager manifests require external privileged setup, not a standalone usable app unit (`README.md:55`). Confidence: medium.
```score-evidence
{"B":{"diversity_points":1.5,"diversity_grade":2,"reference_grade":2,"reference_units":[{"name":"espanso-user-service","evidence":"modules/apps/espanso/_settings.nix:1"}]}}
```

Total: **65.5/100**. Shortlists: showcase no (D direct-context cap); library_units espanso-user-service; starter no (product prerequisites/machinery). Notable for a checked public profile constructor and graph-to-Den membership parity.

Overall pros:
- Public constructor has a minimal independent consumer (`templates/default/flake.nix:6`).
- Graph closure is checked against delivered Den membership (`modules/home/construction/_module.nix:61`).
- Negative context and collision cases are invoked by CI (`tests/test_constructor_inputs.py:59`, `.github/workflows/check.yml:54`).

Overall cons / limits:
- Organization-specific launcher URLs remain shared constants (`modules/apps/grist/_settings.nix:5`).
- Individual package descriptors require the product composition contract (`modules/profiles/composition/_application.nix:1`).
- Privileged browser helper setup remains an external administrator action (`README.md:55`).

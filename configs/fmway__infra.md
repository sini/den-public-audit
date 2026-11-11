# fmway__infra

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/fmway__infra.md)

- Upstream: [fmway/infra](https://github.com/fmway/infra)
- Reviewed revision: [`ad5b83625ade`](https://github.com/fmway/infra/commit/ad5b83625aded5e8679a87c706734edce341da7f)
- Author: fmway
- Score: **40.5 / 100**, rank 88 of 103 ranked configs. D 5 · I 7 · S 4 · R 3 · P 5 · L 2 · V 2 · O 4 · B 2 · X 5. Shortlists: —.
- Summary: D visible structured peer derivation, external route unproven; I service owners; S typed contracts/helper error and three adaptation groups; R token unit; P narrow honest scope; L minimal; V internal only; O partial generator integration; X Clan class; B lower bound.

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

Clan inventory drives the infrastructure; den hosts mirror that inventory for debugging (`flake.nix:10`). The flake imports an external Clan integration and uses den namespace/schema/policies to customize Clan machines (`flake.nix:6`, `modules/clan/default.nix:100`).


## 2. Common patterns.

- namespace: fclan is exposed as a den namespace (`modules/clan/default.nix:2`).
- policies: clan-core lib is resolved to every default scope (`modules/default.nix:3`).
- custom schema/classes: clan-machine includes vary by tags (`modules/clan/default.nix:100`).


## 3. Novel patterns.

An inventory tag controls local-machine update/state-version behavior via a den schema extension (`modules/clan/default.nix:101`).


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Debug-only host declarations and explicitly FAKE filesystem/boot values make den outputs an unsuitable deployment example (`flake.nix:10`, `flake.nix:14`).


## 6. Docs and complexity.

Docs 2: README only identifies Clan orchestration (`README.md:1`), while inline comments explain inventory tags (`modules/clan/default.nix:17`). Complexity 4: role/tag-based service inventory and custom schema integration (`modules/clan/default.nix:27`, `modules/clan/default.nix:100`).


## 6a. Defects and scoring notes.

- S · moderate: ranges-port attrs input passes its first shape predicate but p recursively refers to itself before p.start can be checked (`modules/_lib/types.nix:13`, `modules/_lib/types.nix:17`, `modules/_lib/types.nix:19`).
- S · moderate: three shared fleet adaptation groups remain, enumerated in S (`modules/clan/services/vaultwarden.nix:7`, `modules/clan/services/dns/_adguardhome.nix:34`).
- O · minor: Vaultwarden database-url generator is declared while its environmentFile consumer is commented, so this prompt cannot configure the service database (`modules/clan/services/vaultwarden.nix:9`, `modules/clan/services/vaultwarden.nix:24`).
Explicitly labeled debug/FAKE outputs are a scope caveat, not a major newcomer defect.

## 7. Template notes.

Classify as barely-den infrastructure for corpus purposes: den is present mainly as an integration/debug layer, with Clan providing the primary inventory (`flake.nix:10`, `modules/clan/default.nix:16`).

## 8. Scorecard.

### D
Scope: visible Clan entity/export data projected through Den integration. Pros: ZeroTier emits peer records, DNS consumes exported peer hosts and derives DNS/hosts maps (`modules/clan/services/zerotier.nix:8`, `modules/clan/services/dns/default.nix:16`, `modules/clan/services/dns/_adguardhome.nix:8`). Cons: Den policy shown only resolves clanLib; class routing belongs to external garden adapter, not a locally traced policy pipeline (`modules/default.nix:3`, `flake.nix:6`). Literal5 useful structured derivation, capped at5 for direct schema/export calculation without proven Den policy routing. Score **5**; confidence **medium**.

### I
Scope: role/service owners. Pros: DNS, tokens, ZeroTier and users have separate files (`modules/clan/services/dns/default.nix:5`, `modules/clan/services/nix-token/default.nix:2`). Cons: dyndns also owns AdGuard TLS and nginx behavior coupled to a separate named DNS inventory instance (`modules/clan/services/dyndns.nix:2`, `modules/clan/services/dyndns.nix:33`). Interpolated7 substantial feature ownership, below9 clean independent service concerns. Score **7**; confidence **medium**.

### S
Scope: role interfaces and local helper contracts. Pros: typed DNS port/hostname, extra devices, token sharing option (`modules/clan/services/dns/default.nix:60`, `modules/clan/services/zerotier.nix:14`, `modules/clan/services/nix-token/default.nix:12`). Cons: ranges-port advertises attrs input but its non-string p branch recursively refers to itself (`modules/_lib/types.nix:13`, `modules/_lib/types.nix:17`); three shared adaptation groups remain: author domain/Cloudflare credential namespace, administrator identity with a committed credential (reported privately; not located here), fixed ZeroTier instance name (`modules/clan/services/vaultwarden.nix:7`, `modules/clan/services/dns/_adguardhome.nix:34`). Contract4 below useful5 for faulty advertised helper shape; coverage8 for <=3 grouped changes; min(4,8)=4. Inventory-local endpoints are not counted as hidden shared constants. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":8,"distinct_leaks":3}}
```

### R
Scope: visible self-contained units. Pros: token service owns input prompt, secret generation and Nix consumption, with one sharing parameter (`modules/clan/services/nix-token/default.nix:10`, `modules/clan/services/nix-token/default.nix:17`). Cons: other service units depend on fleet-specific named instances/helper schema, and §4 nominates no independent Den aspect (`modules/clan/services/dyndns.nix:2`, `modules/clan/services/vaultwarden.nix:48`). Interpolated3 above2 no reusable example for a useful unit, below5 independently demonstrated community extraction. Score **3**; confidence **medium**.

### P
Scope: NixOS Clan services and explicitly debug Den hosts. Pros: output is clearly labeled debug/FAKE; no promise of portable deployable host topology (`flake.nix:10`, `flake.nix:14`). Cons: external adapter/platform coverage is not locally proven (`flake.nix:6`). Literal5 honest narrow Linux scope; declared perSystem Darwin is not a managed Darwin host. Score **5**; confidence **medium**.

### L
Scope: project and service docs. Pros: root names Clan and service manifests attach readmes (`README.md:2`, `modules/clan/services/nix-token/default.nix:7`). Cons: root has no explanation of Den/Clan ownership boundary or new machine route (`README.md:1`, `flake.nix:6`). Literal2 minimal root authoring guidance; explicit debug comments prevent treating placeholders as deceptive documentation. Score **2**; confidence **medium**.

### V
Scope: static helper assertions. Pros: extra-device duplicate check is explicit (`modules/clan/services/zerotier.nix:18`). Cons: no dedicated fixture for ranges-port attrs branch or DNS empty/multiple-server behavior (`modules/_lib/types.nix:13`, `modules/clan/services/dns/default.nix:9`). Literal2 limited internal checks, not a test suite; none executed. Score **2**; confidence **medium**.

### O
Scope: visible secret/bootstrap integration. Pros: token generator prompt is consumed by Nix include; Vaultwarden env file ownership and DNS token use are declared (`modules/clan/services/nix-token/default.nix:18`, `modules/clan/services/nix-token/default.nix:21`, `modules/clan/services/vaultwarden.nix:11`). Cons: external Clan adapter owns deployment/inventory realization; generated Vaultwarden database env is not consumed because environmentFile is commented (`modules/clan/services/vaultwarden.nix:24`). Interpolated4 below5 fully traced Den-derived operation, above2 manual-only for real visible generator/consumer integration. Score **4**; confidence **medium**.

### X
Scope: custom Clan-machine/service module family. Pros: namespace and clan-machine schema customize role/tag-generated targets (`modules/clan/default.nix:5`, `modules/clan/default.nix:100`, `modules/clan/services/dns/default.nix:96`). Cons: adapter is external and local target artifacts are not a separate k8s/terranix pipeline (`flake.nix:6`). Literal5 one substantial integration target family, no duplicate O credit for secret generators. Score **5**; confidence **medium**.

### B
Scope: census confirmed selections and independent app units. Pros: nix-token is a complete nonidentity unit with typed share input and actual consumer (`modules/clan/services/nix-token/default.nix:12`, `modules/clan/services/nix-token/default.nix:18`). Cons: Fish/Starship machine file adoption remains external-adapter ambiguous, not zero or confirmed diversity; other services require named fleet/ZeroTier/domain schema (`modules/clan/services/dns/_adguardhome.nix:34`, `modules/clan/services/dyndns.nix:2`). Only visible complete token unit counted; incomplete census scope may move breadth upward. Score **2**; confidence **medium**.
B_div: 0 points → 2; B_ref: 1 units → 2; half-up mean → 2.
```score-evidence
{"B":{"diversity_points":0,"diversity_grade":2,"reference_grade":2,"reference_units":[{"name":"nix-token","evidence":"modules/clan/services/nix-token/default.nix:10"}]}}
```

Total: **40.5/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Peer exports drive generated DNS (`modules/clan/services/dns/default.nix:16`).
- Token prompt/generator/consumer complete (`modules/clan/services/nix-token/default.nix:18`).
- Tag behavior is described inline (`modules/clan/default.nix:19`).

Overall cons / limits:
- Faulty advertised attrs helper branch (§6a S; `modules/_lib/types.nix:13`).
- Shared services retain fleet identifiers (§6a S; `modules/clan/services/dns/_adguardhome.nix:34`).
- Vaultwarden generated database env is disconnected (§6a O; `modules/clan/services/vaultwarden.nix:24`).
- External adapter limits local certainty (`flake.nix:6`).

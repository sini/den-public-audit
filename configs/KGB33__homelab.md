# KGB33__homelab

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/KGB33__homelab.md)

- Upstream: [KGB33/homelab](https://github.com/KGB33/homelab)
- Reviewed revision: [`6ee44f24e022`](https://github.com/KGB33/homelab/commit/6ee44f24e022c95d0f8010fa63616e5366d20dbf)
- Author: KGB33
- Score: **44.5 / 100**, rank 72 of 103 ranked configs. D 5 · I 6 · S 5 · R 5 · P 5 · L 3 · V 5 · O 5 · B 2 · X 2. Shortlists: library units (1).
- Summary: Useful A engine policy and host-module VM test pattern are discoverable; direct identity flow, fleet constants and incomplete authoring docs prevent showcase/starter selection.

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
Generated flake-parts/import-tree loads nixos instead of modules (`flake.nix:1`, `flake.nix:4`). A shared system bundle combines service aspects and local DNS policy (`nixos/systems/default.nix:2`, `nixos/systems/default.nix:11`).

## 2. Common patterns
- namespace: o11y is exported (`nixos/namespace.nix:3`).
- Host inventory declares users beside host-driven checks (`nixos/hosts/ghost.nix:2`).
- Shared includes compose system-minimal, telemetry, containers, deployment and SSH (`nixos/systems/default.nix:2`).

## 3. Novel patterns
A NixOS VM test reuses the den host mainModule directly, checking the deployed composition rather than maintaining a second test-node module (`nixos/hosts/ghost.nix:5`, `nixos/hosts/ghost.nix:7`). Its script only starts the guest, so it is a boot smoke check (`nixos/hosts/ghost.nix:11`).

## 4. Library candidates
- podman · `nixos/services/podman.nix:2` · Podman container backend, Docker CLI compatibility and socket · inputs: NixOS/nixpkgs · parameterization: none (`nixos/services/podman.nix:3`) · **A**, self-contained opt-in engine policy; consumers should deliberately accept the socket choice (`nixos/services/podman.nix:9`).

## 5. den friction
No verified den-specific friction in the reviewed service bundle or host test integration (`nixos/systems/default.nix:2`, `nixos/hosts/ghost.nix:7`).

## 6. Docs and complexity
Docs **3**: root README points to dedicated IaC docs and explains local rendering (`README.md:3`, `README.md:9`). Complexity **4**: shared deployment/telemetry/container services and host-level VM integration (`nixos/systems/default.nix:2`, `nixos/hosts/ghost.nix:5`).

## 6a. Defects and scoring notes

- **S · moderate:** 26 raw selected constants group into11 change-once facts: domain/subdomains (`nixos/services/caddy.nix:60`, `nixos/o11y/otelcol.nix:46`, `nixos/services/hickory-dns.nix:13`); resolver host .100 and SigNoz host .104 (`nixos/systems/default.nix:14`, `nixos/services/caddy.nix:73`); repository (`nixos/services/comin.nix:21`); kgb33 home/data/key root (`nixos/services/sops.nix:13`, `nixos/apps/minecraft.nix:41`, `nixos/apps/valheim.nix:38`); timezone (`nixos/apps/mealie.nix:20`); Wireguard network/CIDRs (`nixos/services/wireguard.nix:53`, `nixos/services/wireguard.nix:59`); three peer identities (`nixos/services/wireguard.nix:65`, `nixos/services/wireguard.nix:72`, `nixos/services/wireguard.nix:79`); interface (`nixos/services/wireguard.nix:38`). Raw breakdown9 domain spellings+2 host IPs+repository+4 home-derived paths+timezone+5 network addresses+3 keys+interface. Secret material itself is not disclosed/count-inferred.
- **I · moderate:** selecting reverse proxy also runs the author blog container (`nixos/services/caddy.nix:30`); unrelated side effect caps I6.
- **V · moderate:** hello-world test expects lowercase world although generated page uses World (`nixos/services/hello-world.nix:12`, `nixos/services/hello-world.nix:49`). Existing ghost boot-only test is coverage, not a separate bug (`nixos/hosts/ghost.nix:11`).
- **L · minor:** testing guide names modules/hosts while actual root uses nixos/hosts (`docs/src/nixos/README.md:23`, `nixos/hosts/ghost.nix:2`).

## 7. Template notes
Useful for combining den hosts with NixOS tests; replace local DNS and domain policy when copying the system bundle (`nixos/systems/default.nix:14`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Host declaration (`nixos/hosts/ghost.nix:2`) → selected hostname battery (`nixos/hosts/ghost/configuration.nix:2`) → OTel resource/telemetry host labels (`nixos/o11y/otelcol.nix:38`, `nixos/o11y/otelcol.nix:57`). Actual entity-derived identity channel reaches5; no explicit policy/pipe collection or duplicate/missing producer contract earns6+. Score **5**; confidence **medium**.

### I

Scope · pros · cons/coverage: App/service aspects and included infrastructure localize features (`nixos/apps/npwd.nix:11`, `nixos/systems/default.nix:2`). Caddy additionally starts the author blog (`nixos/services/caddy.nix:30`), an unrelated app side effect; bundle cap6 applies despite otherwise clear ownership. Score **6**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract5: Valheim constructor exposes slug/world/port/env (`nixos/apps/valheim.nix:5`), but shared DNS, credentials and endpoints still embed fleet facts (`nixos/systems/default.nix:14`, `nixos/services/sops.nix:13`). Coverage5 from 11 grouped leaks (§6a); min(5,5)=5. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":5,"distinct_leaks":11}}
```

### R

Scope · pros · cons/coverage: Existing A Podman engine policy is independently selectable (`nixos/services/podman.nix:2`) and needs only standard NixOS. Its small size is not a penalty, but it is not the substantial A plus consumer teaching required for9. Literal5 useful-unit adoption; author credential assets limit larger app extraction (`nixos/apps/couchdb.nix:7`). Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Declared production/check hosts are explicit x86 Linux (`nixos/hosts/ghost.nix:2`, `nixos/apps/npwd.nix:94`); custom binary also targets x86 Linux (`nixos/apps/npwd.nix:67`). Honest narrow5, no speculative penalty for missing Darwin; no broad support boundary proof claimed. Score **5**; confidence **medium**.

### L

Scope · pros · cons/coverage: Root links book and local rendering (`README.md:3`, `README.md:9`); testing page teaches co-located checks (`docs/src/nixos/README.md:19`). Its directory-layout section is empty and example path stale (`docs/src/nixos/README.md:8`, `docs/src/nixos/README.md:23`). Interpolate3 above operation-only2, below a reliable5 authoring route. Score **3**; confidence **high**.

### V

Scope · pros · cons/coverage: NPWD waits for DB/app health (`nixos/apps/npwd.nix:137`), and manual workflow runs flake check (`.github/workflows/nix-check.yaml:13`). Real representative intent meets5; simple host smoke only starts (`nixos/hosts/ghost.nix:11`) and hello-world assertion has wrong case (`nixos/services/hello-world.nix:12`, `nixos/services/hello-world.nix:49`). No passing claim or9 negative/boundary coverage. Score **5**; confidence **high**.

### O

Scope · pros · cons/coverage: Feature-owned SOPS restart/ownership derives from actual service config (`nixos/apps/couchdb.nix:8`, `nixos/apps/valheim.nix:29`), satisfying one aspect-driven provisioning concern at5. Comin selects repository externally (`nixos/services/comin.nix:21`); no fleet-derived deploy/install/builder target set is verified. Score **5**; confidence **medium**.

### X

Scope · pros · cons/coverage: Den hosts are NixOS; VM tests reuse mainModule (`nixos/hosts/ghost.nix:7`) through standard runNixOSTest, not a first-class guest entity/class. Namespace export (`nixos/namespace.nix:3`) is not an integration target. Baseline2. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Only Fish enable/default in census gives0.5 → diversity2. Full app/service scan counts two complete nonidentity substantive units below. Podman is engine enable/compat policy, not substantive app settings (`nixos/services/podman.nix:4`); other apps fix author domains, data roots or encrypted credential assets (`nixos/apps/mealie.nix:21`, `nixos/apps/couchdb.nix:7`). Reference2; mean2. Score **2**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":1,"diversity_grade":2,"reference_grade":2,"reference_units":[{"name":"openssh","evidence":"nixos/services/ssh.nix:2"},{"name":"hello-world-server","evidence":"nixos/services/hello-world.nix:2"}]}}
```

**Total:** 44.5/100. **Shortlists:** showcase no; library podman; starter no. Useful A engine policy and host-module VM test pattern are discoverable; direct identity flow, fleet constants and incomplete authoring docs prevent showcase/starter selection.

Overall pros:
- Service tests reuse actual Den host modules (`nixos/apps/npwd.nix:115`).
- Service readiness checks go beyond host boot (`nixos/apps/npwd.nix:137`).
- Valheim exposes meaningful constructor variation (`nixos/apps/valheim.nix:5`).

Overall cons / scope limits:
- S: shared DNS and key paths embed one fleet (`nixos/systems/default.nix:14`, `nixos/services/sops.nix:13`).
- I: proxy selection starts unrelated blog (`nixos/services/caddy.nix:30`).
- V/L: contradictory HTTP assertion and stale guide path (`nixos/services/hello-world.nix:49`, `docs/src/nixos/README.md:23`).

# byte-sized-emi__nix-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/byte-sized-emi__nix-config.md)

- Upstream: [byte-sized-emi/nix-config](https://github.com/byte-sized-emi/nix-config)
- Reviewed revision: [`8df6aa42d1bb`](https://github.com/byte-sized-emi/nix-config/commit/8df6aa42d1bbcc42b6a2b82447a26a340ce62655)
- Author: byte-sized-emi
- Score: **54.0 / 100**, rank 33 of 103 ranked configs. D 7 · I 8 · S 4 · R 7 · P 5 · L 3 · V 2 · O 7 · B 4 · X 2. Shortlists: showcase, library units (1).
- Summary: A compact real cross-host service-discovery showcase, with explicit normalization and two operational consumers; cardinality, backup status and personal application contracts need repair before fleet reuse.

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
A raw evalModules/import-tree entry produces flake outputs and exposes module options (`flake.nix:75`, `flake.nix:81`). Private apps/stacks namespaces hold features, and a host-schema policy collects HTTP service facts across the fleet (`modules/den.nix:14`, `modules/fleet.nix:43`).

## 2. Common patterns
- namespace: apps and stacks are private (`modules/den.nix:14`).
- define-user+primary-user are split between user-schema and identity includes (`modules/den.nix:49`, `modules/den.nix:54`).
- quirks/policies: ntfy emits its service endpoint (`modules/stacks/ntfy.nix:3`), collectAll normalizes service URLs (`modules/fleet.nix:20`, `modules/fleet.nix:30`) and auto-update consumes those endpoints (`modules/auto-update.nix:20`).

## 3. Novel patterns
The fleet transforms service_name/host/https/port into normalized URLs before consumers see them (`modules/fleet.nix:22`). Comin notifications use ntfy’s discovered URL and log forwarding uses the discovered Loki host/port, avoiding duplicated endpoint addresses (`modules/auto-update.nix:43`, `modules/auto-update.nix:97`).

## 4. Library candidates
- fleet-http-services · `modules/fleet.nix:3` · collect and normalize HTTP service descriptions for all hosts · inputs: den policy.pipe; emitters with service_name and host · parameterization: records with optional https/port/url (`modules/fleet.nix:5`, `modules/fleet.nix:26`) · **A**, self-contained collector/normalizer attached to host schema (`modules/fleet.nix:43`).

## 5. den friction
The user schema comment explicitly wonders whether host-aspects should be added (`modules/den.nix:47`); otherwise the reviewed fleet transport has a concrete emitter/consumer path (`modules/stacks/ntfy.nix:3`, `modules/auto-update.nix:21`).

## 6. Docs and complexity
Docs **3**: service record shape and normalization are commented (`modules/fleet.nix:5`, `modules/fleet.nix:23`); root README is mostly TODOs and hardware troubleshooting (`README.md:3`, `README.md:23`). Complexity **4**: multi-host service discovery plus shared deployment/logging and typed service registry (`modules/fleet.nix:14`, `modules/auto-update.nix:61`, `modules/service.nix:6`).

## 6a. Defects and scoring notes

- **D · moderate:** fleet consumers select the first Loki/ntfy match without zero/multiple cardinality assertions (`modules/auto-update.nix:20`, `modules/auto-update.nix:21`, `modules/dms.nix:7`).
- **S · moderate:** deployment and shared application leaves embed personal origin, account paths and identities outside their record contracts (`modules/auto-update.nix:50`, `modules/auto-update.nix:111`, `modules/apps/git.nix:80`, `modules/apps/vicinae.nix:47`).
- **O · moderate:** backup preparation increments a failure counter but ends with successful completion output and no failing exit, allowing callers to proceed after failed preparation (`modules/backup-registry.nix:49`, `modules/backup-registry.nix:55`, `modules/backup-registry.nix:59`). This is runtime backup reliability, not Den composition.
- **L · minor:** root README labels the fleet provider/consumer mechanism TODO although the policy is implemented (`README.md:21`, `modules/fleet.nix:14`).
- Hidden submodule and inactive checks limit visible evidence; they are not invented platform defects (`.gitmodules:2`, `modules/outputs.nix:20`).

## 7. Template notes
Good compact cross-host service discovery example; add explicit provider cardinality checks before depending on it for automatic deployment (`modules/auto-update.nix:20`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Live cross-host chain: selected nixnest ntfy emits service facts (`modules/hosts/nixnest/configuration.nix:28`, `modules/stacks/ntfy.nix:3`); host-schema policy collectAll transforms optional HTTPS/port/URL defaults (`modules/fleet.nix:20`, `modules/fleet.nix:26`, `modules/fleet.nix:43`); selected nixdort auto-update consumes discovered URL and Loki endpoint (`modules/hosts/nixdort/configuration.nix:5`, `modules/auto-update.nix:43`, `modules/auto-update.nix:97`). Loki producer is concrete (`modules/hosts/nixnest/monitoring.nix:3`). Grade7: real cross-host transformation exceeds basic routed6, but unchecked head makes absence fail and multiple providers silently choose one (`modules/auto-update.nix:20`), capping below8–9. Score **7**; confidence **high**.

### I

Scope · pros · cons/coverage: Namespaced application leaves, a separate transport/normalizer and typed native service/backup registries separate responsibilities (`modules/den.nix:14`, `modules/fleet.nix:14`, `modules/service.nix:6`, `modules/backup-registry.nix:64`). Duplicate port/domain and HTTPS-certificate checks strengthen interfaces (`modules/service.nix:126`, `modules/service.nix:134`, `modules/service.nix:142`). Grade8: better contracts than ordinary5, with registry defaults still coupled to host-owned settings and certificate secrets (`modules/service.nix:43`, `modules/service.nix:200`). Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract4: consumer records and native registries expose useful fields (`modules/fleet.nix:5`, `modules/service.nix:22`), but shared apps embed identity, personal deployment remote, endpoints and checkout paths (`modules/apps/git.nix:80`, `modules/auto-update.nix:50`, `modules/apps/vicinae.nix:47`, `modules/auto-update.nix:111`). Grouped visible adaptation inventory50: 31 institution SSH peers (`modules/fachschaft.nix:77`, `modules/fachschaft.nix:95`), author identity1 and four other SSO identities (`modules/stacks/sso.nix:84`, `modules/stacks/sso.nix:102`, `modules/stacks/sso.nix:112`, `modules/stacks/sso.nix:120`, `modules/stacks/sso.nix:128`), personal domain/subdomains1, checkout1, three Syncthing peer identities (`modules/syncthing.nix:19`), two VPN network sets (`modules/fachschaft.nix:19`, `modules/vpn.nix:21`), Borg endpoint1 (`modules/stacks/borg.nix:72`), Zed lookup hostnames2 (`modules/apps/zed.nix:314`), two additional SSH network peers (`modules/apps/git.nix:22`, `modules/apps/git.nix:27`), encrypted asset1 and certificate root1 (`modules/secrets.nix:7`, `modules/service.nix:199`). Raw inventoried literal values77 collapse to50; repeated occurrences are not extra groups. Coverage4 cap; S=min(4,4). Hidden submodule may add or remove adaptation requirements; visible code determines this score (`.gitmodules:2`). Score **4**; confidence **low**.

```score-evidence
{"S":{"contract_design":4,"leak_coverage":4,"distinct_leaks":50,"raw_leaks":77}}
```

### R

Scope · pros · cons/coverage: The generic HTTP collector has documented required/optional record fields and attaches itself to host schema (`modules/fleet.nix:5`, `modules/fleet.nix:43`); Cloudflared and Rayfish expose substantial native APIs (`modules/cloudflared.nix:214`, `modules/rayfish.nix:11`). Grade7 above light adaptation5: useful parameter contracts exist, but no isolated minimal external consumer accompanies the collector; most application stacks depend on fleet-owned my.services/settings (`modules/stacks/ntfy.nix:11`, `modules/stacks/ntfy.nix:17`). Score **7**; confidence **medium**.

### P

Scope · pros · cons/coverage: All four declared hosts are x86_64 NixOS (`modules/den.nix:22`), an honest narrow scope5. Desktop/server selections are explicit (`modules/graphical.nix:30`, `modules/server-default.nix:2`). No Darwin/ARM support is inferred from generic package expressions (`modules/per-system.nix:29`). Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: Root documentation is mainly operational TODOs and hardware troubleshooting (`README.md:3`, `README.md:23`). Grade3 between operation-only2 and host/user/feature wiring5 because source comments do specify the service-record API and normalization (`modules/fleet.nix:5`, `modules/fleet.nix:23`), but no composition onboarding is supplied and README still marks the implemented fleet mechanism TODO (`README.md:21`). Score **3**; confidence **high**.

### V

Scope · pros · cons/coverage: A fleet-wide toplevel-check aspect is defined (`modules/nixos-checks.nix:11`) but its output selection is commented out (`modules/outputs.nix:20`), so it receives no active-check credit. Visible output wiring includes ordinary package/devshell builds, no composition fixtures or negative-context tests (`modules/outputs.nix:16`); baseline2. Hidden submodule may contain additional verification, which is not demonstrated by visible source (`.gitmodules:2`). Score **2**; confidence **low**.

### O

Scope · pros · cons/coverage: Two Den-derived concerns are visible: discovered HTTP services configure automatic deployment notifications/log shipping (`modules/auto-update.nix:43`, `modules/auto-update.nix:97`), and user facts determine secret paths/ownership (`modules/secrets.nix:21`, `modules/secrets.nix:32`). Grade7 between one concern5 and comprehensive9; install/builders are not derived here, deployment origin remains personal, and backup preparation can report completion after failure (`modules/auto-update.nix:50`, `modules/backup-registry.nix:49`, `modules/backup-registry.nix:59`). Native backup registry metadata is not counted again as Den inventory. Score **7**; confidence **medium**.

### X

Scope · pros · cons/coverage: Visible deployment/configuration targets are standard NixOS/Home Manager (`modules/den.nix:20`, `modules/den.nix:22`), baseline2. A generated kube/config secret does not establish a Kubernetes module/output target (`modules/secrets.nix:44`); fleet diagrams and packages are ordinary derived/build outputs (`modules/packages/diagrams.nix:37`, `modules/outputs.nix:8`). No operations flow is double-counted here. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Enabled selection-verified census diversity5 gives grade3; four complete nonidentity substantive reference units below give grade4; rounded B4. Cloudflared owns its complete typed tunnel/runtime contract and Rayfish owns settings/spec generation (`modules/cloudflared.nix:378`, `modules/cloudflared.nix:414`, `modules/rayfish.nix:7`, `modules/rayfish.nix:83`). Steam includes its own unfree allowance and native/desktop integration (`modules/apps/steam.nix:5`, `modules/apps/steam.nix:18`). Excluded are token Browser/Anki, identity-bound email/Git/Vicinae/SSH/Syncthing, fleet-registry-dependent stacks, encrypted Beeper/Tailscale assets, custom perSystem-dependent AI/Zed, outside-app-dependent Signal/Niri/Noctalia, and package-only utilities (`modules/apps/browser.nix:6`, `modules/anki.nix:3`, `modules/apps/email.nix:169`, `modules/apps/git.nix:80`, `modules/apps/vicinae.nix:47`, `modules/ssh-server.nix:12`, `modules/syncthing.nix:19`, `modules/stacks/ntfy.nix:11`, `modules/stacks/beeper.nix:5`, `modules/tailscale-server.nix:12`, `modules/ai/ai.nix:6`, `modules/apps/zed.nix:6`, `modules/apps/signal.nix:5`, `modules/niri.nix:159`, `modules/noctalia.nix:40`, `modules/packages/nw-usage.nix:2`). The unavailable submodule prevents a complete hidden-unit inventory; its unknown units receive no reference credit (`.gitmodules:2`). Score **4**; confidence **low**.

```score-evidence
{"B":{"diversity_points":5.0,"diversity_grade":3,"reference_grade":4,"reference_units":[{"name":"Steam desktop integration","evidence":"modules/apps/steam.nix:18"},{"name":"Podman/Quadlet integration","evidence":"modules/podman.nix:4"},{"name":"Cloudflared tunnel module","evidence":"modules/cloudflared.nix:214"},{"name":"Rayfish daemon/spec module","evidence":"modules/rayfish.nix:24"}]}}
```

**Total:** 54.0/100. **Shortlists:** showcase yes; library fleet-http-services; starter no. A compact real cross-host service-discovery showcase, with explicit normalization and two operational consumers; cardinality, backup status and personal application contracts need repair before fleet reuse.

Overall pros:
- Concrete producer→collectAll→normalizer→cross-host consumer (`modules/stacks/ntfy.nix:3`, `modules/fleet.nix:20`, `modules/auto-update.nix:43`).
- Typed service registry checks duplicate domains/ports (`modules/service.nix:126`, `modules/service.nix:134`).
- Generic native service modules are independently useful (`modules/cloudflared.nix:214`, `modules/rayfish.nix:11`).

Overall cons / scope limits:
- Unchecked service selection lacks cardinality guarantees (`modules/auto-update.nix:20`).
- Personal endpoints and account paths remain in shared leaves (`modules/auto-update.nix:50`, `modules/apps/vicinae.nix:47`).
- Backup failure counter does not fail the wrapper (`modules/backup-registry.nix:55`, `modules/backup-registry.nix:59`).
- Checks are defined but not selected (`modules/outputs.nix:20`).

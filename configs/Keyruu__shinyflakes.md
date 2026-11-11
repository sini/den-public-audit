# Keyruu__shinyflakes

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/Keyruu__shinyflakes.md)

- Upstream: [Keyruu/shinyflakes](https://github.com/Keyruu/shinyflakes)
- Reviewed revision: [`021ee48343db`](https://github.com/Keyruu/shinyflakes/commit/021ee48343db2893c2a041a49690e92896352e82)
- Author: Keyruu
- Score: **55.5 / 100**, rank 29 of 103 ranked configs. D 7 · I 8 · S 4 · R 5 · P 5 · L 3 · V 5 · O 5 · B 8 · X 2. Shortlists: showcase, library units (1).
- Summary: Live cross-host service-fact channels and typed contracts; silent first-value selection, shared operator constants and stale entry documentation constrain the result.

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
Den supplies host/user schemas while a service-fact policy gathers cross-host dashboard, monitor and proxy data (`modules/den.nix:22`, `modules/policies/services-collect.nix:23`). Shared defaults select standard hostname/input batteries (`modules/den.nix:66`).

## 2. Common patterns
- custom schema/classes: host display groups and positions are typed options (`modules/den.nix:23`).
- policies and quirks: service facts are collected into named streams (`modules/policies/services-collect.nix:6`, `modules/policies/services-collect.nix:23`).
- den.default includes hostname, inputs-prime and self-prime batteries (`modules/den.nix:70`).

## 3. Novel patterns
A people entity models service access as inventory rather than duplicating authorization lists across services (`modules/entities/people.nix:79`); dashboard/proxy/monitor facts use separate collection channels (`modules/policies/services-collect.nix:24`).

Service dashboard facts are emitted from enabled services.my entries (`modules/aspects/options/my/services.nix:499`, `modules/aspects/options/my/services.nix:515`), collected across hosts (`modules/policies/services-collect.nix:24`), then consumed as dashboard app metadata (`modules/aspects/server/dashboard.nix:5`, `modules/aspects/server/dashboard.nix:25`). This verifies a complete producer/route/consumer path, beyond mere quirk declarations.

## 4. Library candidates
- collect-service-facts · `modules/policies/services-collect.nix:6` · declares five service-fact quirks and attaches collection to every host · inputs: den policy.pipe API · parameterization: fn args host (`modules/policies/services-collect.nix:23`) · **B**, generalize stream naming and supply consumer policies; the collector alone does not deploy services.

## 5. den friction
The author explicitly could not get withProvenance working (`modules/policies/services-collect.nix:22`). README’s Blueprint structure description is stale relative to the den import (`README.md:147`, `modules/den.nix:9`).

## 6. Docs and complexity
Docs **3**: service rationale is extensive (`README.md:83`) but the structure section disagrees with current wiring (`README.md:147`, `modules/den.nix:9`). Complexity **5**: custom people entities, typed display schema and cross-host policy collection (`modules/entities/people.nix:92`, `modules/den.nix:23`, `modules/policies/services-collect.nix:23`).

## 6a. Defects and scoring notes
- moderate · **D**: same-name scrape groups take the first metrics path and interval without checking agreement; routing exists, but silent first-value semantics cap D at 7 (`modules/aspects/server/monitoring/prometheus.nix:44`, `modules/aspects/server/monitoring/prometheus.nix:45`). This identifies an unguarded conflict case, not an observed runtime collision.
- major · **S**: shared application owners carry personal domains, identities, hardware identifiers and paths; the grouped inventory is in the S card (`modules/aspects/tools/git.nix:36`, `modules/aspects/services/home-assistant/automations.nix:13`). Home Assistant definitions count as shared source scope, not verified adoption.
- major · **L**: entry documentation describes Blueprint rather than the current Den module tree (`README.md:147`, `modules/den.nix:9`).
Manual SOPS enrollment and fixed Comin remotes limit higher O bands; they do not disqualify aspect-owned secrets (`README.md:238`, `modules/aspects/server/comin.nix:69`). The provenance comment is a reported friction signal, not proof of a broken policy (`modules/policies/services-collect.nix:22`).

## 7. Template notes
Strong advanced policy example, with an explicit provenance pain point; unsuitable as a minimal first configuration (`modules/policies/services-collect.nix:22`, `modules/entities/people.nix:92`).

## 8. Scorecard

### D (7, medium)
Scope: authored live data channels. Pros: enabled service definitions emit dashboard/monitor/proxy/OIDC facts, policy collects across hosts, dashboard and Prometheus consume them (`modules/aspects/options/my/services.nix:499`, `modules/policies/services-collect.nix:24`, `modules/aspects/server/dashboard.nix:25`, `modules/aspects/server/monitoring/prometheus.nix:29`). Cons: grouped scrape fields silently take the head (`modules/aspects/server/monitoring/prometheus.nix:44`); cap7 applies despite cross-scope routing. Confidence: medium.

### I (8, medium)
Scope: ownership and boundaries. Pros: roles, typed service options, people inventory and collection policies have separate owners (`modules/aspects/roles/server.nix:3`, `modules/entities/people.nix:79`, `modules/policies/services-collect.nix:6`). Cons: application consumers still depend on the shared services.my envelope, so independence is weaker than a completely closed leaf (`modules/aspects/options/my/services.nix:350`). Interpolation8 for clear multi-concern separation with explicit shared contracts, below fully isolated9. Confidence: medium.

### S (4, low)
Scope: visible shared definitions, including unselected alternatives; entity metadata itself is not a leak. Pros: typed service and backup settings expose meaningful interfaces (`modules/aspects/options/my/services.nix:42`, `modules/aspects/options/backup.nix:14`). Cons: 35 conservative adaptation groups, not occurrence counts. Non-HA21: keyruu.de (`modules/aspects/services/actualbudget.nix:7`), peeraten.net (`modules/aspects/services/calibre-web.nix:7`), zimtix.de (`modules/aspects/services/blocky.nix:81`), buymeaspezi.com (`modules/aspects/server/webpages.nix:27`), Tailnet (`modules/aspects/browsers/browser-picker.nix:37`), personal/work identity (`modules/aspects/tools/git.nix:36`), cache URL/key (`modules/aspects/core/nixConfig.nix:55`), LAN address set (`modules/aspects/services/blocky.nix:7`), mesh subnet (`modules/aspects/options/mesh.nix:18`), prime address (`modules/aspects/shell/ssh.nix:26`), checkout root (`modules/aspects/editors/vscode.nix:187`), mainpool root (`modules/aspects/services/copyparty.nix:70`), runner UUID (`modules/aspects/services/forgejo-runner.nix:16`), Beszel key (`modules/aspects/server/beszel-agent.nix:13`), GeoIP account (`modules/aspects/server/edge-protection.nix:31`), audio hardware (`modules/aspects/workstation/sound.nix:60`), Sonoff serial (`modules/aspects/services/home-assistant/zigbee2mqtt.nix:80`), ZBT serial (`modules/aspects/services/home-assistant/openthread.nix:7`), Munich location (`modules/aspects/tools/noctalia.nix:252`), private cluster contexts (`modules/aspects/tools/k9s.nix:83`), repository catalog (`modules/aspects/tools/repos.nix:87`). HA14 further physical-device groups: hall sensor/switch, office button/light, bedroom voice box, two other assistants, door intercom, two phones and four window sensors; device/entity aliases of one device are grouped once (`modules/aspects/services/home-assistant/automations.nix:13`, `modules/aspects/services/home-assistant/automations.nix:29`, `modules/aspects/services/home-assistant/automations.nix:55`, `modules/aspects/services/home-assistant/automations.nix:69`, `modules/aspects/services/home-assistant/automations.nix:105`, `modules/aspects/services/home-assistant/automations.nix:125`, `modules/aspects/services/home-assistant/automations.nix:172`). Raw repeated occurrences were not separately enumerated. Contract7, coverage4 because >30 groups; min4. Private submodule content is unavailable and could change the visible scope in either direction (`README.md:311`). Confidence: low.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":4,"distinct_leaks":35}}
```

### R (5, medium)
Scope: independently liftable visible contracts. Pros: collect-service-facts is a concrete B extraction with a traced consumer (`modules/policies/services-collect.nix:6`, `modules/aspects/server/dashboard.nix:25`); backup options own their typed extension and timers (`modules/aspects/options/backup.nix:14`, `modules/aspects/options/backup.nix:91`). Cons: service consumers need the wider fleet schema and personal values (§6a); no small independent consumer documents that complete envelope (`modules/aspects/options/my/services.nix:350`). Anchor5. Confidence: medium.

### P (5, medium)
Scope: visible host/home variation. Pros: typed host display settings and context-derived user secret paths handle actual variation (`modules/den.nix:23`, `modules/aspects/workstation/secrets.nix:5`). Cons: separate phone configuration is outside the Den instantiation; personal Linux service/device assumptions constrain reuse (`modules/phone.nix:1`, `modules/aspects/workstation/sound.nix:60`). Honest but bounded portability5. Confidence: medium.

### L (3, medium)
Scope: newcomer navigation. Pros: service rationale and secret-enrollment guidance exist (`README.md:83`, `README.md:238`). Cons: stale Blueprint structure and private-submodule prerequisites obstruct reproducing the current entry path (`README.md:147`, `README.md:311`, `modules/den.nix:9`). Interpolation3, above a placeholder but below a reliable entry guide. Confidence: medium.

### V (5, medium)
Scope: static validation intent. Pros: CI builds a matrix derived from flake host outputs, and service definitions contain conflict/missing-field assertions (`.forgejo/workflows/build.yml:32`, `modules/aspects/options/my/services.nix:363`, `modules/aspects/options/my/services.nix:374`). Cons: no focused negative fixture proves cross-host collection or alternate display/user contexts; head selection remains unguarded (`modules/aspects/server/monitoring/prometheus.nix:44`). Anchor5; no build was run. Confidence: medium.

### O (5, medium)
Scope: operational derivation. Pros: aspect-owned secret definitions/consumers supply one Den-driven operational concern (`modules/aspects/workstation/secrets.nix:5`, `modules/aspects/roles/server.nix:3`). Cons: recipients remain manually enrolled, an upper-band limit; generic Comin uses fixed remotes and adds no generated target inventory (`README.md:238`, `modules/aspects/server/comin.nix:69`, `modules/aspects/server/comin.nix:78`). O5 under the explicit per-aspect-secret ruling. Confidence: medium.

### X (2, medium)
Scope: Den-driven nonstandard target contracts. Pros: broader project includes Droid and Terraform (`modules/phone.nix:1`, `terraform/default.nix:1`). Cons: these constructors live beside Den rather than being driven by a distinct Den class; normal host/home wiring earns P, not X (`modules/den.nix:22`). Baseline2. Confidence: medium.

### B (8, low)
Scope: census diversity plus complete visible reference owners. Pros: B_div11.5→9, deduplicated family maximum depth. Twelve complete units listed below give reference grade7; mean8. Standard native HM accounts, owned assets and resource collectors are allowed interfaces. Cons: many themed/fleet app owners require custom settings or another owner's module import; Gluetun lacks its own Quadlet import, and personal Git is not a clean reference (`modules/aspects/tools/git.nix:36`, `modules/aspects/core/podman.nix:5`). Unavailable private content could add or alter units; only visible complete bodies count. Confidence: low.
```score-evidence
{"B": {"diversity_points": 11.5, "diversity_grade": 9, "reference_grade": 7, "reference_units": [{"name": "core.podman", "evidence": "modules/aspects/core/podman.nix:5"}, {"name": "browsers.chromium", "evidence": "modules/aspects/browsers/chromium.nix:11"}, {"name": "tools.calendar", "evidence": "modules/aspects/tools/calendar.nix:7"}, {"name": "tools.file-explorer", "evidence": "modules/aspects/tools/file-explorer.nix:4"}, {"name": "tools.nix-index-database", "evidence": "modules/aspects/tools/nix-index-database.nix:7"}, {"name": "tools.screenshot", "evidence": "modules/aspects/tools/screenshot.nix:7"}, {"name": "workstation.bluetooth", "evidence": "modules/aspects/workstation/bluetooth.nix:5"}, {"name": "workstation.printing", "evidence": "modules/aspects/workstation/printing.nix:5"}, {"name": "workstation.sunshine", "evidence": "modules/aspects/workstation/sunshine.nix:5"}, {"name": "workstation.kanata", "evidence": "modules/aspects/workstation/kanata.nix:5"}, {"name": "workstation.wm.lock", "evidence": "modules/aspects/workstation/wm/lock.nix:13"}, {"name": "options.backup", "evidence": "modules/aspects/options/backup.nix:14"}]}}
```

Total 55.5/100. Showcase: yes, routed service-fact example. Library: collect-service-facts (B). Starter: no. Overall pros: live routed facts; typed contracts; explicit application ownership; real CI intent. Overall cons: silent head semantics; shared operator constants; stale entry guide; private prerequisites.

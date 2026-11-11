# auscyber__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/auscyber__dotfiles.md)

- Upstream: [auscyber/dotfiles](https://github.com/auscyber/dotfiles)
- Reviewed revision: [`96be028eaba6`](https://github.com/auscyber/dotfiles/commit/96be028eaba642d74c7e1ed19db00fe4b41356ca)
- Author: auscyber
- Score: **68.5 / 100**, rank 3 of 103 ranked configs. D 7 · I 8 · S 6 · R 7 · P 7 · L 6 · V 7 · O 8 · B 5 · X 8. Shortlists: showcase, library units (3).
- Summary: Traced cross-scope cache facts, generated builders/deploy/rekey and real iOS/ESPHome module contracts; silent transport precedence and fleet-bound app owners limit extraction.

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
A generated flake resolves layered lock data and patched inputs before flake-parts imports aspect files (`flake.nix:14`, `flake.nix:31`, `flake.nix:47`). The framework adds den schemas, policies and capabilities over a Linux/Darwin/ARM household fleet (`aspects/framework/den.nix:26`, `README.md:8`, `README.md:14`).

## 2. Common patterns
- quirks and policies: celler-caches is emitted by the server (`aspects/base/celler/server.nix:169`), collected fleet-wide (`aspects/base/celler/push.nix:298`) and consumed to resolve user cache choices (`aspects/base/celler/push.nix:538`).
- custom schema/policies: host.serves declarations include their service aspects automatically (`aspects/base/service-propagate.nix:10`, `aspects/base/service-propagate.nix:16`).
- define-user and hostname are centrally attached to their appropriate scopes (`aspects/framework/den.nix:46`, `aspects/framework/den.nix:49`).

## 3. Novel patterns
Celler transport carries config-derived endpoints while cache membership follows included aspects, separating evaluated network facts from entity identity (`aspects/base/celler/server.nix:159`, `aspects/base/celler/server.nix:178`). A declaration-level cross-host dependency checker over-approximates possible recursion without evaluating every host (`aspects/framework/cross-host-dag.nix:26`, `aspects/framework/cross-host-dag.nix:47`).

## 4. Library candidates
- file-local · `aspects/base/file-local.nix:8` · maps source-tree paths to a live checkout and creates out-of-store links · inputs: HM, lib, rootPath, user entity with optional flakeFolder (`aspects/base/file-local.nix:19`) · parameterization: fn args plus entity option · **B**, support standalone home identity explicitly and validate source paths belong under rootPath (`aspects/base/file-local.nix:21`).

- bluetooth-a2dp-pipewire · `aspects/nixos/bluetooth.nix:7` · **A**, native NixOS BlueZ Source/Sink/Media/Socket, experimental features, Blueman and PipeWire/ALSA/Pulse/WirePlumber integration (`aspects/nixos/bluetooth.nix:20`). No author identity or custom router; included by a real appliance (`aspects/hosts/birdsarentreal.nix:77`). Inputs: NixOS module context; platform: Linux. This is an app/service integration, not a token enable.
- llama-cpp-darwin · `aspects/services/llama-cpp.nix:59` · **B**, typed model, alias, port and package; owned launchd activation/cache/logs (`aspects/services/llama-cpp.nix:111`). Scope the extraction to Darwin: Linux ignores the package override and has no automatic target installation (`aspects/services/llama-cpp.nix:146`). Inputs: HM module context, package/model settings; no fleet broker.

## 5. den friction
The source reports standalone user@host scope collisions and overrides both name and aspect to restore identity (`aspects/base/home-standalone.nix:6`, `aspects/base/home-standalone.nix:25`). The framework patches den.lib.gen (`aspects/framework/den.nix:15`, `aspects/framework/den.nix:19`); its cycle checker documents gaps in den’s cross-host diagnostics (`aspects/framework/cross-host-dag.nix:21`). These are static author reports, not reproduced here.

## 6. Docs and complexity
Docs **5**: fleet/network inventory and detailed mechanism comments explain why data moves across scopes (`README.md:4`, `README.md:21`, `aspects/base/celler/server.nix:159`). Complexity **5**: layered input resolution, patched den, service propagation and cross-host cache thunks (`flake.nix:14`, `aspects/framework/den.nix:15`, `aspects/base/service-propagate.nix:10`, `aspects/base/celler/push.nix:298`).

## 6a. Defects and scoring notes
- moderate · **D**: cache requests merge pull/push sets explicitly, but competing non-null transport choices silently take the first; comments promise merging without documenting a precedence contract (`aspects/base/celler/_lib.nix:7`, `aspects/base/celler/_lib.nix:37`). This caps D at7 despite real cross-scope routes.
- moderate · **S**: eight confirmed adaptation groups in the inspected shared owners: Ivy identity (`aspects/shell/shell.nix:51`, `aspects/services/rclone.nix:14`); ivymect.in domain including subdomains (`aspects/services/searchix.nix:44`, `aspects/services/searchix.nix:63`); Searchix publication root (`aspects/services/searchix.nix:19`); OneDrive drive ID (`aspects/services/rclone.nix:63`); local agenix directory root (`aspects/security/agenix-rekey.nix:32`, `aspects/security/agenix-rekey.nix:293`); Zotero profile ID (`aspects/programs/zotero.nix:104`); Time Machine default peer (`aspects/darwin/time-machine.nix:115`); Obsidian personal vault/template layout (`aspects/programs/obsidian.nix:163`, `aspects/programs/obsidian.nix:269`). This is twelve cited raw sites grouped into eight changes, a confirmed lower bound, not an exhaustive fleet leak count. Host/person inventory and generic locale/font choices do not count. Additional unchecked service bodies could lower coverage further.
- minor · **P**: file-local assumes a user entity without a standalone-home adaptation (`aspects/base/file-local.nix:12`). The Linux llama-cpp service ignores its declared package setting and lacks an Install target, whereas Darwin owns activation (`aspects/services/llama-cpp.nix:96`, `aspects/services/llama-cpp.nix:139`). Static contract gaps, not observed runtime failures.
- minor · **L**: generated fleet inventory is useful, but some long documents are explicitly intent/oracle rather than implementation documentation, and an ESPHome design document still says no device is implemented despite the current Dyson constructor (`docs/entity-model.md:3`, `docs/esphome-devices.md:23`, `aspects/hosts/dyson.nix:362`). A reader must distinguish current wiring from design history.
- minor · **V**: the capability-reader check's second grep branch can accept a reference in comments because that branch lacks the comment filter used by the first branch; no isolated negative fixture for that case was found (`aspects/framework/checks.nix:321`, `aspects/framework/checks.nix:352`). CI checks exist; their success was not measured.

The earlier notes charging an intentional dependency over-approximation as a defect and treating Australian locale as leaked identity are withdrawn. The former is an honest diagnostic bound, not proof of a bad dependency (`aspects/framework/cross-host-dag.nix:49`). Patched-source import is a regression-inventory IFD risk, not an automatic scoring deduction (`lib/inputs.nix:508`, `aspects/security/agenix-rekey.nix:243`).

## 7. Template notes
A strong advanced dataflow reference with a verified producer/collect/consumer chain; the input layering and framework patches make it a demanding first template (`aspects/base/celler/server.nix:169`, `aspects/base/celler/push.nix:299`, `flake.nix:31`).

## 8. Scorecard

### D (7, medium)
Scope: cache producer, policy routing, request merge and consumers. Pros: enabled server emits cache records (`aspects/base/celler/server.nix:169`), collectAll gathers across hosts and expose sends user requests to host (`aspects/base/celler/push.nix:298`, `aspects/base/celler/push.nix:307`), native clients consume the result (`aspects/base/celler/push.nix:538`). Unknown servers/transports throw, and pull/push union is explicit (`aspects/base/celler/_lib.nix:32`, `aspects/base/celler/_lib.nix:47`). Cons: transport agreement is unchecked at the first-value merge (`aspects/base/celler/_lib.nix:37`), so the silent-selection cap7 applies. Confidence: medium.

### I (8, medium)
Scope: framework, resource owners, platform modules and sampled app closures. Pros: service ownership and delivery are explicit rather than copied host configs (`aspects/base/service-propagate.nix:10`); mobile classes, operational scope adapters and native app files own separate concerns (`aspects/framework/mobile/default.nix:35`, `aspects/security/age-scope.nix:85`, `aspects/nixos/bluetooth.nix:7`). Cons: the capability/input framework raises the number of contracts a maintainer must understand before moving a feature; e.g. an otherwise native Zotero owner also names fleet providers (`aspects/programs/zotero.nix:90`, `flake.nix:31`). Clear scale-appropriate boundaries, short of a simple universal extraction surface. Confidence: medium.

### S (6, low)
Scope: typed cache, builder, secret and mobile contracts plus inspected shared native/service owners; not an exhaustive read of all396 Nix files. Pros: contract_design8: cache errors are explicit and builder settings/keys derive from entity records (`aspects/base/celler/_lib.nix:47`, `aspects/base/builders.nix:164`); native model/package options are typed (`aspects/services/llama-cpp.nix:59`). Leak_coverage6: eight grouped adaptations from twelve cited raw sites are listed in §6a, including publication endpoint, personal storage ID, root and vault layout (`aspects/services/searchix.nix:19`, `aspects/services/rclone.nix:63`, `aspects/programs/obsidian.nix:269`). Cons: shared native owners still carry those values; typed framework quality does not erase them. min(8,6)=6. Further unread author constants could lower this grade; confidence: low.
```score-evidence
{"S":{"contract_design":8,"leak_coverage":6,"distinct_leaks":8}}
```

### R (7, medium)
Scope: closed native units and actual consumer. Pros: BlueZ/PipeWire integration is a substantial identity-free native owner and a declared appliance includes it (`aspects/nixos/bluetooth.nix:7`, `aspects/hosts/birdsarentreal.nix:77`); Finder and Mopidy are similarly direct (`aspects/darwin/finder.nix:3`, `aspects/services/mopidy.nix:3`). Cons: the appliance is not an isolated minimal consumer, and many other attractive app owners require custom fleet capabilities or scope machinery, e.g. Zotero (`aspects/programs/zotero.nix:90`). Above R5 through demonstrated closed native contracts, below R9's minimal adoption example. Confidence: medium.

### P (7, medium)
Scope: standard OS/home classes and native service guards. Pros: Linux/Darwin clients share the builder settings contract while host classes are filtered explicitly (`aspects/base/builders.nix:147`, `aspects/base/builders.nix:193`); llama-cpp separates launchd/systemd branches (`aspects/services/llama-cpp.nix:111`, `aspects/services/llama-cpp.nix:139`). Cons: standalone-home file-local context and the Linux package/autostart discrepancy remain (§6a); no focused consumer fixture for all those boundaries was verified. Broad honest support, not P9. Confidence: medium.

### L (6, medium)
Scope: README fleet map, capability tutorial and selected design documents. Pros: current systems and network routes are visible (`README.md:6`, `README.md:53`); capability documentation explains contracts, typed fields and routing preference with examples (`docs/capabilities.md:31`, `docs/capabilities.md:52`, `docs/capabilities.md:111`). Cons: intent/oracle and historical design status must be reconciled against actual constructors (`docs/entity-model.md:3`, `docs/esphome-devices.md:23`). More teaching than an operation-only README, but the default adoption path is less clear than the internals. Confidence: medium.

### V (7, medium)
Scope: host assertions, framework findings/check derivations and actual CI invocation. Pros: representative real host output facts are asserted (`aspects/hosts/checks.nix:38`, `aspects/hosts/checks.nix:72`); findings become failing checks unless explicitly report-only (`aspects/framework/checks.nix:170`, `aspects/framework/checks.nix:177`); checks.yml passes attr=checks to the action that builds the selected family (`.github/workflows/checks.yml:54`, `.github/actions/build-system/action.yml:183`, `.github/actions/build-system/action.yml:192`). Cons: grep-based reader proof has a comment false-positive gap (§6a), and one host is explicitly omitted from generated build coverage (`aspects/tooling/ci-matrix.nix:32`). Above representative checks5, below focused enabled/disabled/context/collision coverage9. Static invocation intent only, no passing claim. Confidence: medium.

### O (8, medium)
Scope: deploy, cache credential generators, distributed builders and recipient projection. Pros: deploy nodes derive from actual NixOS outputs (`aspects/tooling/deploy.nix:23`); cache tokens track their generator dependencies (`aspects/base/celler/_lib.nix:136`); builder peers, systems, per-link SSH secrets and host public keys derive from entities (`aspects/base/builders.nix:164`, `aspects/base/builders.nix:209`); rekey recipients use actual host keys (`aspects/security/agenix-rekey.nix:263`). Cons: master trust still has an operator-local directory and explicit trust identities (`aspects/security/agenix-rekey.nix:293`); a general host-install/bootstrap inventory was not traced. Three substantial derived concerns justify8, short of the full deploy/secrets/install/builders anchor9. These operational classes earn no X credit. Confidence: medium.

### X (8, medium)
Scope: custom mobile/iOS and ESPHome module systems, actual declarations and artifact ownership. Pros: mobile-to-ios routing feeds an independent evalModules constructor (`aspects/framework/mobile/default.nix:39`, `aspects/framework/mobile/default.nix:93`) with profiles, manifests, owned activation and runtime secret rendering (`aspects/framework/mobile/toplevel.nix:139`, `aspects/framework/mobile/toplevel.nix:174`); an actual iPhone is instantiated (`aspects/hosts/iphone.nix:44`). ESPHome owns typed device evaluation/YAML and an offline-check artifact, used by Dyson (`aspects/framework/esphome/default.nix:109`, `aspects/framework/esphome/default.nix:119`, `aspects/hosts/dyson.nix:362`). Cons: mobile installation remains explicitly interactive/device-dependent (`aspects/framework/mobile/toplevel.nix:165`, `aspects/framework/mobile/toplevel.nix:180`); these two substantial families have less breadth than the several-target anchor9. No package-output or operational-class credit. Confidence: medium.

### B (5, low)
Scope: census family diversity plus six confirmed complete native app/service owners; this is a confirmed lower-bound inventory from source reading, not a claim that every export was audited for extraction. B_div=6.0→5; B_ref=6→5; half-up mean5. Counted: bluetooth-a2dp-pipewire, Finder, Mopidy, Difftastic native HM integration, llama-cpp Darwin contract, Kodi. Pros: these own activation or are built-in OS app settings with coherent presets (`aspects/nixos/bluetooth.nix:7`, `aspects/services/llama-cpp.nix:111`). Cons: Zotero/Obsidian rely on custom class/fleet contracts or personal layouts; Alloy needs an unowned Loki/nginx dependency, and Yabai needs a custom HM bridge (`aspects/programs/obsidian.nix:145`, `aspects/services/alloy.nix:28`, `aspects/wms/yabai.nix:4`). Airplay's system-wide PipeWire socket prerequisite was not proven owned, so it is not counted (`aspects/services/airplay-bluetooth.nix:197`). Token PAM/OpenRGB leaves are excluded. Unreviewed remaining bodies could increase B_ref; confidence: low.
```score-evidence
{"B": {"diversity_points": 6.0, "diversity_grade": 5, "reference_grade": 5, "reference_units": [{"name": "bluetooth-a2dp-pipewire", "evidence": "aspects/nixos/bluetooth.nix:7"}, {"name": "finder", "evidence": "aspects/darwin/finder.nix:3"}, {"name": "mopidy", "evidence": "aspects/services/mopidy.nix:3"}, {"name": "difftastic", "evidence": "aspects/dev/difftastic.nix:3"}, {"name": "llama-cpp-darwin", "evidence": "aspects/services/llama-cpp.nix:111"}, {"name": "kodi", "evidence": "aspects/apps/kodi.nix:4"}]}}
```

Total 68.5/100. Showcase: yes, live cross-scope cache and operational resource flows. Library: file-local(B), bluetooth-a2dp-pipewire(A), llama-cpp-darwin(B). Starter: no. Overall pros: routed facts; generated credentials/builders/deploy; real custom target module contracts; invoked checks. Overall cons: silent transport precedence; shared author constants; demanding custom extraction contracts; historical documentation and incomplete breadth coverage.

# repparw__nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/repparw__nix.md)

- Upstream: [repparw/nix](https://github.com/repparw/nix)
- Reviewed revision: [`b2a680435a4e`](https://github.com/repparw/nix/commit/b2a680435a4e1c3451e76b73ed361f064029ab88)
- Author: repparw
- Score: **63.0 / 100**, rank 8 of 103 ranked configs. D 8 · I 7 · S 5 · R 5 · P 5 · L 8 · V 8 · O 8 · B 4 · X 2. Shortlists: showcase, library units (1).
- Summary: Provenance registry and explicit missing/duplicate semantics D8; mixed CLI ownership I7; typed contracts7 capped by sixteen adaptation groups to S5; extraction R5; honest Linux P5; extensive architecture/runbooks L8; generated/VM behavioral fixtures V8; derived deployment/backup O8; standard target X2.

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

Generated flake-parts/import-tree supports an x86 workstation and ARM server fleet (`flake.nix:4`, `modules/entities.nix:3`). Services emit registry metadata collected fleet-wide with provenance before a service-host consumer interprets it (`modules/service-graph.nix:6`, `modules/aspects/services/default.nix:3`).


## 2. Common patterns.

- quirks: service-registry names structured routing/monitoring/backup data (`modules/service-graph.nix:6`).
- policies: collectAll plus withProvenance routes contributions (`modules/service-graph.nix:11`).
- provides tree: service features live under nixos-services providers (`modules/aspects/services/jellyfin.nix:7`).
- den.default includes: monitoring, reboot and system concerns apply fleet-wide (`modules/defaults.nix:14`).


## 3. Novel patterns.

Jellyfin emits service identity, port and monitoring metadata (`modules/aspects/services/jellyfin.nix:8`); collect-service-registry gathers it (`modules/service-graph.nix:11`) and service-host consumes provenance-wrapped values (`modules/aspects/services/default.nix:13`). This is verified emitter/route/consumer dataflow.


## 4. Library candidates.

- desktop.bitwarden · `modules/aspects/bitwarden.nix:16` · OS polkit/keyring integration and user background broker · NixOS/HM/nixpkgs · none · B: separate browser-specific operational assumptions and document manual unlock setup.


## 5. den friction.

No verified den-specific workaround in inspected registry policy and consumer (`modules/service-graph.nix:8`, `modules/aspects/services/default.nix:13`). The machines.target default is documented as an upstream nspawn compatibility fix (`modules/defaults.nix:29`).


## 6. Docs and complexity.

Docs 4: README links architecture, fleet operations and recovery guides (`README.md:33`); service comments teach why the broker spans OS/HM (`modules/aspects/bitwarden.nix:20`). Complexity 5: multi-architecture fleet, service provenance and several global operational concerns (`modules/entities.nix:19`, `modules/service-graph.nix:11`, `modules/defaults.nix:14`).


## 6a. Defects and scoring notes.

- S · moderate: sixteen shared adaptation groups in identity, infrastructure defaults and physical context (§8 inventory); typed interfaces do not relocate these defaults to entities (`modules/aspects/cli/git.nix:45`, `modules/service-definitions.nix:106`, `modules/aspects/gui/wm.nix:51`).
- I · minor: Git owner combines FZF/Eza/FD/Git/Lazygit rather than independently selectable application owners (`modules/aspects/cli/git.nix:7`).
No additional verified defect; global Hermes secret placement alone is not proof of a broken consumer.

## 7. Template notes.

Standout service dataflow example, but strip fleet-specific defaults and secret coupling before making a starter (`modules/defaults.nix:46`, `modules/entities.nix:5`).

## 8. Scorecard.

### D
Scope: cross-host service facts. Pros: Jellyfin emits registry facts; policy collects all hosts with provenance; consumer resolves source host, rejects duplicate names, validates missing hosts/ports, and allocates container addresses used by ingress (`modules/aspects/services/jellyfin.nix:8`, `modules/service-graph.nix:10`, `modules/aspects/services/default.nix:13`, `modules/aspects/services/default.nix:33`, `modules/service-definitions.nix:93`, `modules/_services/address-allocator.nix:6`, `modules/_services/proxy.nix:12`). Cons: this is one principal registry rather than several independent policy channels (`modules/service-graph.nix:6`). Score8 beyond7 live collection through cross-scope provenance and explicit missing/duplicate semantics, below9 broader routed concerns. Score **8**; confidence **medium**.

### I
Scope: feature owners and host/user composition. Pros: inventory owns target/user choices; desktop delivers user-derived autologin through to-hosts; service owners retain declarations and implementations (`modules/entities.nix:7`, `modules/aspects/desktop.nix:25`, `modules/aspects/services/edge.nix:9`). Cons: Git owner combines unrelated CLI apps and identity; shell owner couples fleet-update schema (`modules/aspects/cli/git.nix:7`, `modules/aspects/cli/shell.nix:178`). Score7 beyond5 clear ownership, below9 consistently narrow identity-free units. Score **7**; confidence **medium**.

### S
Scope: typed registry/backup/monitoring contracts versus shared adaptations. Pros: service fields typed with null defaults; validator rejects invalid routing facts; backup exports describe freshness behavior; telemetry destinations require HTTPS (`modules/service-definitions.nix:5`, `modules/service-definitions.nix:93`, `modules/aspects/backup.nix:84`, `modules/aspects/monitoring.nix:68`). Contract7 beyond5 real interfaces/validation, below9 uniformly exposed personal context. Cons: sixteen adaptation groups: identity; domain; Discord; container/media/external roots; two edge-host defaults; bridge network; Grafana account; Bluetooth inventory; display topology; location; TV address; GCP project; locale (`modules/aspects/cli/git.nix:45`, `modules/service-definitions.nix:106`, `modules/service-definitions.nix:136`, `modules/service-definitions.nix:144`, `modules/service-definitions.nix:168`, `modules/service-definitions.nix:174`, `modules/service-definitions.nix:180`, `modules/aspects/monitoring.nix:44`, `modules/aspects/audio.nix:39`, `modules/aspects/gui/wm.nix:59`, `modules/aspects/gui/wm.nix:51`, `modules/aspects/cli/ssh.nix:36`, `modules/aspects/ai/mcp.nix:30`, `modules/aspects/system.nix:7`). Repeated identity/path occurrences grouped once; 11–30 groups cap coverage5; min5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":5,"distinct_leaks":16}}
```

### R
Scope: complete app presets and registry-dependent services. Pros: Bitwarden owns system polkit/keyring and home service, Tmux owns plugin/keybinding setup (`modules/aspects/bitwarden.nix:24`, `modules/aspects/bitwarden.nix:42`, `modules/aspects/cli/tmux.nix:12`). Cons: most service owners require fleet modules.services registry/helpers, and editor package is external personal input (`modules/aspects/services/jellyfin.nix:25`, `modules/aspects/nixvim.nix:14`). Literal5 useful extraction candidates with adaptation, no independent generic public library/export contract. Score **5**; confidence **medium**.

### P
Scope: NixOS x86/ARM fleet. Pros: host-specific selection separates desktop from ARM servers; deployment builds platform-specific activation packages (`modules/entities.nix:3`, `modules/entities.nix:20`, `modules/deploy.nix:26`, `modules/deploy.nix:209`). Cons: ordinary NixOS/HM and Linux service assumptions, no Darwin/home-only portability fixture (`modules/defaults.nix:4`, `modules/aspects/gui/phone.nix:15`). Literal5 honest declared scope. Score **5**; confidence **medium**.

### L
Scope: architecture and operational authoring guidance. Pros: composition guide distinguishes includes/imports and entity ownership; runbook documents retained failures, incomplete backups and recovery links (`docs/architecture/den-aspect-composition.md:14`, `docs/architecture/den-aspect-composition.md:18`, `docs/runbooks/fleet-operations.md:28`, `docs/runbooks/fleet-operations.md:43`). Cons: examples remain closely tied to named fleet and external live operations skill (`docs/runbooks/fleet-operations.md:13`, `docs/runbooks/fleet-operations.md:63`). Score8 beyond5 worked architecture/failure guidance, below9 independently reusable onboarding across contexts. Score **8**; confidence **medium**.

### V
Scope: actual resolved configurations and generated behavior. Pros: checks enumerate actual host toplevels, inspect generated shell packages, wire monitoring and persistence VM fixtures; monitoring variants test present/absent signals and local versus remote service placement (`modules/checks.nix:8`, `modules/checks.nix:35`, `modules/checks.nix:118`, `modules/_tests/monitoring-fleet.nix:116`, `modules/_tests/monitoring-fleet.nix:168`). CI delegates revision validation (`.github/workflows/ci.yml:35`). Cons: no verified dedicated negative fixture for duplicate registry producer names; source throw is not a test (`modules/aspects/services/default.nix:33`). Score8 beyond5 behavioral and real-target coverage, below9 every policy failure edge; nothing executed here. Score **8**; confidence **medium**.

### O
Scope: fleet deployment, derived addresses and recovery-aware backups. Pros: deploy nodes derive inventory addresses and actual activation outputs; local container-unit lists derive registry facts; host backups derive boot mounts and export hooks gate pruning on complete/fresh artifacts (`modules/deploy.nix:31`, `modules/deploy.nix:188`, `modules/deploy.nix:209`, `modules/aspects/host-backup.nix:20`, `modules/aspects/backup.nix:46`, `modules/aspects/backup.nix:52`). Cons: controller and SSH identity remain literal fleet choices, not all lifecycle roles inferred (`modules/deploy.nix:50`, `modules/deploy.nix:76`). Score8 beyond5 several inventory/resource-derived operational concerns plus documented recovery, below9 entirely derived/portable lifecycle. Score **8**; confidence **medium**.

### X
Scope: standard NixOS/HM and packaged tools. Pros: Nixvim configuration package integrates via overlay (`modules/aspects/nixvim.nix:25`). Cons: package import/export is ordinary build plumbing, not an independently evaluated Den nonhost class (`modules/aspects/nixvim.nix:27`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: eight complete app-owner envelopes and selected census breadth. Pros: Bitwarden, Tmux, speech wrapper, Logiops, Zathura, Stylix, Steam integration and KDE Connect own meaningful presets/integrations (`modules/aspects/bitwarden.nix:16`, `modules/aspects/cli/tmux.nix:12`, `modules/aspects/ai/speech.nix:12`, `modules/aspects/gui/logid.nix:8`, `modules/aspects/gui/zathura.nix:12`, `modules/aspects/style.nix:20`, `modules/aspects/gaming.nix:42`, `modules/aspects/gui/phone.nix:38`). Cons: do not split mixed Git/shell/guiApps bodies into inner apps; Fish needs external y binding, MPV fixes author display, services need fleet schema, T3code needs externally supplied CODEX_HOME (`modules/aspects/cli/git.nix:7`, `modules/aspects/cli/fish.nix:91`, `modules/aspects/gui/mpv.nix:45`, `modules/aspects/services/jellyfin.nix:25`, `modules/aspects/ai/t3code.nix:37`). Tiny package/enable leaves and upstream patch owners excluded. Score **4**; confidence **medium**.
B_div: 4.5 points → 3; B_ref: 8 units → 5; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":5,"reference_units":[{"name":"bitwarden","evidence":"modules/aspects/bitwarden.nix:16"},{"name":"tmux","evidence":"modules/aspects/cli/tmux.nix:12"},{"name":"speech","evidence":"modules/aspects/ai/speech.nix:12"},{"name":"logiops","evidence":"modules/aspects/gui/logid.nix:8"},{"name":"zathura","evidence":"modules/aspects/gui/zathura.nix:12"},{"name":"stylix","evidence":"modules/aspects/style.nix:20"},{"name":"steam","evidence":"modules/aspects/gaming.nix:42"},{"name":"kdeconnect","evidence":"modules/aspects/gui/phone.nix:38"}]}}
```

Total: **63.0/100**. Shortlists: showcase true; library_units ['desktop.bitwarden']; starter false.

Overall pros:
- Service facts route with provenance and explicit duplicate/missing validation (`modules/aspects/services/default.nix:33`).
- Deployment consumes actual host inventory and activation outputs (`modules/deploy.nix:31`).
- Behavioral fixtures cover generated resolved monitoring variants (`modules/_tests/monitoring-fleet.nix:168`).
- Recovery runbook explains incomplete-backup consequences (`docs/runbooks/fleet-operations.md:43`).

Overall cons / limits:
- Shared identity/topology remains distributed (§6a S; `modules/aspects/cli/git.nix:45`).
- CLI Git owner combines several independently useful tools (§6a I; `modules/aspects/cli/git.nix:7`).
- Most service presets require fleet registry/schema envelope (`modules/aspects/services/jellyfin.nix:25`).

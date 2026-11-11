# nazarewk-iac__nix-configs

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/nazarewk-iac__nix-configs.md)

- Upstream: [nazarewk-iac/nix-configs](https://github.com/nazarewk-iac/nix-configs)
- Reviewed revision: [`a1a10f5c8272`](https://github.com/nazarewk-iac/nix-configs/commit/a1a10f5c82721c402c8df10edd58145c8fc6f106)
- Author: nazarewk-iac
- Score: **60.0 / 100**, rank 14 of 103 ranked configs. D 2 · I 9 · S 6 · R 8 · P 9 · L 8 · V 9 · O 2 · B 7 · X 5. Shortlists: showcase, library units (2).
- Summary: Strong public composition/export, native portability and negative-consumer tests; custom Devenv integration and confirmed reference breadth. Den routed facts and production operational adoption remain baseline; mixed legacy identity and one credential prerequisite limit portability.

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
The parallel tree also loads a real, explicitly incomplete `orr` host, including six aspects (`hosts-den/orr/default.nix:23`, `hosts-den/orr/default.nix:31`, `hosts-den/orr/default.nix:33`); build-only fixtures remain separate.
A parallel den migration sits beside the older option-driven module tree (`README.md:7`, `modules/den/aspects/dev-rust.nix:3`). The flake explicitly pins both den and nix-effects (`flake.nix:40`, `flake.nix:60`).

## 2. Common patterns
- define-user+primary-user: the test user includes both account batteries (`checks/den-mvp/users/default.nix:21`, `checks/den-mvp/users/default.nix:25`).
- Class-specific targets share a package function across NixOS, Darwin and HM (`modules/den/aspects/dev-rust.nix:26`, `modules/den/aspects/dev-rust.nix:44`).

## 3. Novel patterns
Syncthing publishes read-only persistence directory outputs instead of writing another aspect’s options; consumers own the integration (`modules/den/aspects/service-syncthing.nix:31`, `modules/den/aspects/service-syncthing.nix:69`).

## 4. Library candidates
- service-syncthing · **A** through the supplied `denLib.imports { class = "homeManager"; aspects = [ "service-syncthing" ]; }` surface (`modules/den/lib.nix:478`): locked inputs supply the owned helper and namespace, caller supplies ordinary HM identity/state (`modules/den/lib.nix:292`, `modules/den/aspects/service-syncthing.nix:57`). Linux-only activation, nullable GUI address and persistence outputs are explicit (`modules/den/aspects/service-syncthing.nix:60`, `modules/den/aspects/service-syncthing.nix:96`).
- den-library-surface · **A**, independent class/aspect selection wrapper with optional extraInputs/modules/select; requires the supplied locked Den/nix-effects inputs and ordinary native target evaluation (`modules/den/lib.nix:274`, `modules/den/lib.nix:478`). Minimal adopter import example and bare-consumer comparison are supplied (`modules/den/README.md:163`, `checks/den-mvp/tests.nix:837`).

## 5. den friction
The aspect comments report entity arguments silently losing imports across the export boundary (`modules/den/aspects/service-syncthing.nix:41`); this is author-reported friction, not independently reproduced.

## 6. Docs and complexity
Docs **5**: port comments teach ownership and inclusion rules (`modules/den/aspects/service-syncthing.nix:23`). Complexity **5**: parallel implementations and cross-class package filtering add migration machinery (`modules/den/aspects/dev-rust.nix:3`, `modules/den/aspects/dev-rust.nix:35`).

## 6a. Defects and scoring notes

- **S · moderate:** the mixed legacy shared profiles embed five fleet hostnames, the grouped kdn.im domain and a credential tag; seven grouped adaptations cap leak coverage at 6 (`modules/universal/profile/remote-builders/default.nix:54`, `modules/universal/profile/remote-builders/default.nix:144`, `modules/universal/profile/machine/workstation/default.nix:59`).
- **R · minor:** Photoprism unconditionally expects `/tmp/photoprism-admin` without provisioning it or exposing a required credential input; a caller needs an override and external setup (`modules/den/aspects/program-photoprism.nix:35`). Excluded from reference count.
- **L · minor:** frozen status counts misdescribe the substantially expanded surface (`modules/den/README.md:277`, `modules/den/README.md:285`, `checks/README.md:83`).
- The earlier helper-dependency deduction is withdrawn: exported modules supply their owned lexical closure (`modules/den/lib.nix:292`, `modules/den/lib.nix:416`). Entity-argument limitations are documented and guarded API boundaries, not an independently reproduced Den bug (`modules/den/lib.nix:318`).

## 7. Template notes
Useful advanced migration material, but start with a single port rather than the whole tree (`modules/den/aspects/dev-rust.nix:18`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Den composition scope: the custom policy instantiates a shell using host name/system, but this is target construction, credited under X; the persistence lists are native option outputs without a verified Den producer→policy→consumer fact channel (`modules/den/classes/devenv.nix:156`, `modules/den/aspects/service-syncthing.nix:69`). Baseline 2; native SSH/CA option graphs are not routed Den data. Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Namespace ownership separates public definitions from personal data, while the library exports class-resolved modules and includes their owned dependencies (`modules/den/namespaces.nix:55`, `modules/den/lib.nix:292`, `modules/den/lib.nix:409`). The wrapper rejects unknown/empty selections rather than exporting no-ops (`modules/den/lib.nix:318`, `modules/den/lib.nix:494`). Strong 9 anchor; parallel migration is documented scope, not a composition defect (`hosts-den/orr/default.nix:23`). Score **9**; confidence **high**.

### S

Scope · pros · cons/coverage: Mixed repository scope: contract design 8 combines typed nullable caller credentials and structurally private namespace ownership with legacy shared fleet assumptions (`modules/den/aspects/service-iperf3.nix:101`, `modules/den/namespaces.nix:55`, `modules/universal/profile/remote-builders/default.nix:198`). Seven confirmed adaptation groups: five builder hostnames briv/etra/brys/oams/anji (`modules/universal/profile/remote-builders/default.nix:54`, `modules/universal/profile/remote-builders/default.nix:64`, `modules/universal/profile/remote-builders/default.nix:70`, `modules/universal/profile/remote-builders/default.nix:76`, `modules/universal/profile/remote-builders/default.nix:82`); one kdn.im domain shared by two suffixes and Grafana, and one Tailscale credential tag (`modules/universal/profile/remote-builders/default.nix:144`, `modules/universal/profile/remote-builders/default.nix:148`, `modules/universal/profile/machine/workstation/default.nix:32`, `modules/universal/profile/machine/workstation/default.nix:59`). Raw nine occurrences/grouped seven cap coverage at 6; S=min(8,6)=6. This is visible evidence, not a claim that the large legacy tree has no further leaks; additional shared constants could lower coverage. Named user profiles, fixture identities and declared overrideable defaults are excluded. Score **6**; confidence **low**.

```score-evidence
{"S":{"contract_design":8,"leak_coverage":6,"distinct_leaks":7}}
```

### R

Scope · pros · cons/coverage: The supplied closure exports independently consumable native modules; the wrapper exposes class/aspects/select/modules/extraInputs and docs provide a minimal consumer (`modules/den/lib.nix:478`, `modules/den/README.md:163`). Read-only persistence output is a declared consumer integration, not a hidden fleet write (`modules/den/aspects/service-syncthing.nix:69`). Interpolate 8 below 9 for Photoprism’s undeclared credential prerequisite (`modules/den/aspects/program-photoprism.nix:35`). Score **8**; confidence **high**.

### P

Scope · pros · cons/coverage: NixOS/Darwin/HM/Devenv have explicit native consumers, Linux-only services guard their effects, and bare consumers require no legacy special arguments (`checks/den-mvp/harness.nix:55`, `checks/den-mvp/harness.nix:77`, `checks/den-mvp/harness.nix:104`, `modules/den/aspects/service-syncthing.nix:96`). Strong 9 scope coverage; it promises neither fleet migration completion nor universal hardware portability (`hosts-den/orr/default.nix:23`). Score **9**; confidence **high**.

### L

Scope · pros · cons/coverage: The guide explains namespace merge keys, class boundaries, library inputs, failure modes and minimal adoption (`modules/den/namespaces.nix:44`, `modules/den/README.md:163`, `modules/den/README.md:210`, `modules/den/README.md:226`). Interpolate 8 below 9 because its frozen 21-aspect/26-check status tables trail the registry and bundle documentation (`modules/den/README.md:277`, `modules/den/README.md:285`, `checks/README.md:83`). Score **8**; confidence **high**.

### V

Scope · pros · cons/coverage: Bare native targets compare actual option values; negative tests require unknown selections and whole-aspect no-ops to fail, and check derivations fail on mismatches (`checks/den-mvp/tests.nix:538`, `checks/den-mvp/tests.nix:550`, `checks/den-mvp/harness.nix:23`). Artifact dependencies and real shell smoke commands supplement those tests (`checks/den-mvp/tests.nix:71`, `checks/den-mvp/tests.nix:100`). Documented bundle recipes include core, Den, artifacts and slow checks (`checks/README.md:31`, `checks/bundles.nix:75`). Strong 9 runnable-recipe anchor; no execution or CI success is asserted by this static audit. Score **9**; confidence **high**.

### O

Scope · pros · cons/coverage: Actual Den-host scope is the orr skeleton: its secrets aspect declares policy/order targets but emits no credentials, while remote-builder options are declaration-only (`hosts-den/orr/default.nix:33`, `modules/den/aspects/secrets.nix:91`, `modules/den/aspects/nix-remote-builder.nix:8`). Baseline 2; legacy fleet builders and fixture-only Rosetta checks do not establish a selected Den-derived operational pipeline (`modules/universal/profile/remote-builders/default.nix:198`, `checks/den-mvp/tests.nix:165`). Score **2**; confidence **medium**.

### X

Scope · pros · cons/coverage: A distinct Devenv class evaluates the real upstream top-level module through lib.evalModules, exposes mandatory root/input contracts, and instantiates host-named outputs through a Den policy (`modules/den/classes/devenv.nix:38`, `modules/den/classes/devenv.nix:46`, `modules/den/classes/devenv.nix:92`, `modules/den/classes/devenv.nix:113`, `modules/den/classes/devenv.nix:159`). This meets the 5 evaluated-module integration anchor; OS/HM and ordinary package plumbing receive no extra credit. Score **5**; confidence **high**.

### B

Scope · pros · cons/coverage: Census selection-verified diversity is 7 points: substantive Fish/Zsh/Zellij/Helix/KDE/Sway plus half-point Bash/Tmux availability; source examples include the actual shell selection and explicit aspect imports (`devenv.nix:17`, `modules/den/aspects/program-fish.nix:116`). B_div5. The 20 listed, individually read complete application units establish B_ref9 as a confirmed lower bound, not the entire registry inventory; remaining owners are uncounted. Resolved exports carry generic apps/filter helpers and related included service modules (`modules/den/lib.nix:416`, `modules/den/aspects/apps.nix:73`, `modules/den/aspects/service-zammad.nix:41`). Exclude enable+persist-only PostgreSQL, settings-only KeePass and unprovided-credential Photoprism (`modules/den/aspects/service-postgresql.nix:64`, `modules/den/aspects/program-keepass.nix:8`, `modules/den/aspects/program-photoprism.nix:35`). B=round-half-up((5+9)/2)=7. Score **7**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":7.0,"diversity_grade":5,"reference_grade":9,"reference_units":[{"name":"program-atuin","evidence":"modules/den/aspects/program-atuin.nix:308"},{"name":"program-direnv","evidence":"modules/den/aspects/program-direnv.nix:28"},{"name":"program-fish","evidence":"modules/den/aspects/program-fish.nix:116"},{"name":"program-kdeconnect","evidence":"modules/den/aspects/program-kdeconnect.nix:29"},{"name":"program-nextcloud-client","evidence":"modules/den/aspects/program-nextcloud-client.nix:16"},{"name":"program-nix-index","evidence":"modules/den/aspects/program-nix-index.nix:24"},{"name":"program-obs-studio","evidence":"modules/den/aspects/program-obs-studio.nix:41"},{"name":"program-slack","evidence":"modules/den/aspects/program-slack.nix:22"},{"name":"program-ssh-client","evidence":"modules/den/aspects/program-ssh-client.nix:42"},{"name":"program-tidal","evidence":"modules/den/aspects/program-tidal.nix:21"},{"name":"program-ydotool","evidence":"modules/den/aspects/program-ydotool.nix:32"},{"name":"service-home-assistant","evidence":"modules/den/aspects/service-home-assistant.nix:113"},{"name":"service-iperf3","evidence":"modules/den/aspects/service-iperf3.nix:149"},{"name":"service-coredns","evidence":"modules/den/aspects/service-coredns.nix:99"},{"name":"service-printing","evidence":"modules/den/aspects/service-printing.nix:103"},{"name":"service-samba","evidence":"modules/den/aspects/service-samba.nix:98"},{"name":"service-syncthing","evidence":"modules/den/aspects/service-syncthing.nix:96"},{"name":"service-zammad","evidence":"modules/den/aspects/service-zammad.nix:114"},{"name":"program-handlr","evidence":"modules/den/aspects/program-handlr.nix:89"},{"name":"program-thunderbird","evidence":"modules/den/aspects/program-thunderbird.nix:45"}]}}
```

**Total:** 60.0/100. **Shortlists:** showcase yes; library service-syncthing, den-library-surface; starter no. Strong public composition/export, native portability and negative-consumer tests; custom Devenv integration and confirmed reference breadth. Den routed facts and production operational adoption remain baseline; mixed legacy identity and one credential prerequisite limit portability.

Overall pros:
- Public/private namespace ownership is structural (`modules/den/namespaces.nix:55`).
- An explicit class/aspect import contract supplies owned dependencies (`modules/den/lib.nix:478`).
- Failure cases and bare native consumers are runnable check recipes (`checks/den-mvp/tests.nix:538`, `checks/README.md:31`).

Overall cons / scope limits:
- The real Den host is explicitly an incomplete migration skeleton (`hosts-den/orr/default.nix:23`).
- Legacy shared profiles retain fleet-specific builder records (`modules/universal/profile/remote-builders/default.nix:54`).
- Photoprism leaves an undeclared credential file to the caller (`modules/den/aspects/program-photoprism.nix:35`).
- The status table has stale surface counts (`modules/den/README.md:285`).

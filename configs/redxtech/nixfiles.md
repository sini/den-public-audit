# redxtech/nixfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/redxtech/nixfiles.md)

- Upstream: [redxtech/nixfiles](https://github.com/redxtech/nixfiles)
- Reviewed revision: [`f0611199ba42`](https://github.com/redxtech/nixfiles/commit/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9)
- Author: redxtech
- Score: **51.5 / 100**, rank 43 of 103 ranked configs. D 5 · I 7 · S 5 · R 5 · P 5 · L 5 · V 5 · O 6 · B 5 · X 2. Shortlists: library units (1).
- Summary: D schema/context derivation capped5; I feature ownership with broad CLI; S min(contract7,15-group coverage5); R context bridge B; P honest Linux; L current wiring map; V CI/invariants; O generated deploy/key identities; X standard targets; B strict census/reference inventory.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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

Dendritic flake-file declarations load both modules and packages ([`modules/dendritic.nix:19`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/dendritic.nix#L19)). Three role-oriented hosts share base/workstation/server aspects, with typed per-aspect settings discovered from the aspect tree ([`readme.md:9`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L9), [`modules/schema.nix:8`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L8)).


## 2. Common patterns.

- den.default includes: define-user, hostname, inputs and self plus host settings ([`modules/defaults.nix:6`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/defaults.nix#L6)).
- mutual-provider: user schema enables reciprocal providers ([`modules/defaults.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/defaults.nix#L20)).
- custom schema/classes: recursive settings submodules mirror aspect nesting ([`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34)).
- parametric aspect (fn args): host-settings forwards the current host settings ([`modules/host-settings.nix:3`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L3)).


## 3. Novel patterns.

Typed settings are discovered recursively while class and quirk keys are excluded using den keyClassification internals ([`modules/schema.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L14), [`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34)).


## 4. Library candidates.

- host-settings · [`modules/host-settings.nix:3`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L3) · forwards settings into NixOS and host into HM · den/HM and host.settings schema · fn args · B: requires its surrounding settings convention.


## 5. den friction.

Settings discovery depends on den.lib.aspects.fx.keyClassification, a deep implementation-shaped API ([`modules/schema.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L14)). Explicit argument forwarding fills the host-settings propagation gap ([`modules/host-settings.nix:7`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L7)).


## 6. Docs and complexity.

Docs 4: README explains roles, directories and generated flake inputs ([`readme.md:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L13), [`readme.md:24`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L24), [`readme.md:33`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L33)), while schema comments teach recursive discovery ([`modules/schema.nix:19`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L19)). Complexity 5: dynamic schema discovery plus host-specific monitor/service settings ([`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34), [`modules/hosts/bastion/bastion.nix:12`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/hosts/bastion/bastion.nix#L12)).


## 6a. Defects and scoring notes.

- S · moderate: shared SSH/Git/desktop/secrets/cache bodies embed 15 grouped author-specific adaptation values; exact groups and citations in S card ([`modules/features/base/ssh.nix:26`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/ssh.nix#L26), [`modules/features/base/cli/git.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/git.nix#L20), [`modules/secrets.nix:31`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/secrets.nix#L31), [`modules/nix.nix:56`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/nix.nix#L56)).
Deep key-classification dependency remains a version-coupling observation, not a demonstrated composition defect; former blanket deduction removed. Direct host-output traversal is a D scope ceiling, not an additional S charge.

## 7. Template notes.

Good reference for a large workstation/server split; simplify schema discovery before using as an introductory template ([`readme.md:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L14), [`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34)).

## 8. Scorecard.

### D
Scope: typed host settings, display and audio consumers. Pros: host settings are forwarded into OS/HM ([`modules/host-settings.nix:7`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L7)); declared monitor records render Kanshi outputs with an exactly-one-primary assertion ([`modules/features/workstation/monitors.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L20), [`modules/features/workstation/monitors.nix:114`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L114), [`modules/features/workstation/monitors.nix:150`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L150)); audio records render WirePlumber rules with an empty-list guard ([`modules/features/workstation/audio.nix:61`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/audio.nix#L61), [`modules/features/workstation/audio.nix:72`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/audio.nix#L72)). Cons: these are direct context/schema channels, not policy/pipe routing; host-output SSH traversal is likewise direct ([`modules/features/base/ssh.nix:24`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/ssh.nix#L24)). Literal 5 and capped there; no ceremony credit for schema discovery itself. Score **5**; confidence **medium**.

### I
Scope: feature/host/schema boundaries. Pros: per-app owners, optional providers and role assembly localize settings ([`modules/features/base/cli/editor.nix:48`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/editor.nix#L48), [`modules/features/base/base.nix:62`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/base.nix#L62)). Cons: CLI remains a large multi-application body ([`modules/features/base/cli/cli.nix:314`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/cli.nix#L314)), and deep settings discovery increases maintenance coupling ([`modules/schema.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L14)), without a demonstrated isolation failure. Interpolated 7 between named-feature5 and consistently independent9; old deep-API-as-defect claim is not charged. Score **7**; confidence **medium**.

### S
Scope: settings discovery and shared application bodies. Pros: typed monitor/audio/server options carry real differences and validation ([`modules/schema.nix:46`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L46), [`modules/features/workstation/monitors.nix:114`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L114)). Contract grade7: above5 for reusable typed contracts, below9 because personal assumptions still bypass them. Cons: coverage grade5 for 15 visible adaptation groups: owner identity/account/key; author-home runtime path; checkout root; sucha.foo domain family; super.fish domain family; gabedunn.dev website domain; tailnet domain; three per-host tailnet IPs; personal cache URL+key; household locale; household timezone; two hardware identities ([`modules/features/base/cli/git.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/git.nix#L20), [`modules/features/base/cli/git.nix:83`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/git.nix#L83), [`modules/features/workstation/apps/terminal.nix:134`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/apps/terminal.nix#L134), [`modules/nix.nix:56`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/nix.nix#L56), [`modules/features/base/base.nix:94`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/base.nix#L94), [`modules/features/base/cli/config.nix:9`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/config.nix#L9), [`modules/features/workstation/apps/browser/firefox.nix:102`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/apps/browser/firefox.nix#L102), [`modules/features/base/tailscale.nix:7`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/tailscale.nix#L7), [`modules/features/base/ssh.nix:26`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/ssh.nix#L26), [`modules/nix.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/nix.nix#L20), [`modules/features/base/base.nix:121`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/base.nix#L121), [`modules/features/base/base.nix:16`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/base.nix#L16), [`modules/features/workstation/mouse.nix:68`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/mouse.nix#L68), [`modules/features/workstation/mouse.nix:88`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/mouse.nix#L88)). Domain subpaths/repeated identity occurrences collapse; standard ports/upstream URLs excluded. Final min(7,5)=5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":5,"distinct_leaks":15}}
```

### R
Scope: §4 host-settings unit. Pros: compact context-forwarding bridge has explicit host.settings dependency ([`modules/host-settings.nix:3`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L3)). Cons: it requires the surrounding recursively discovered schema rather than a substantial independent A-unit/minimal external consumer ([`modules/schema.nix:73`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L73)). Literal 5: useful grade B, no extra penalty for the same S identity leaks. Score **5**; confidence **medium**.

### P
Scope: actual NixOS/HM fleet and optional desktop boundaries. Pros: display-related behavior derives from settings instead of assuming every host has a screen ([`modules/features/base/base.nix:6`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/base.nix#L6), [`modules/features/base/security/av.nix:151`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/security/av.nix#L151)); monitor generation is enabled conditionally ([`modules/features/workstation/monitors.nix:110`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L110)). Cons: native Linux tools and x86 database target are the stated implementation scope, with no cross-platform boundary fixtures ([`modules/features/base/cli/nix-index.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/nix-index.nix#L14)). Literal 5 for honest narrow support; no penalty merely for lacking Darwin. Score **5**; confidence **medium**.

### L
Scope: README architecture/commands and schema explanation. Pros: current docs map roles and directories, explain generated flake wiring and provide commands ([`readme.md:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L13), [`readme.md:24`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L24), [`readme.md:33`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L33), [`readme.md:130`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L130)); recursive settings discovery is explained inline ([`modules/schema.nix:19`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L19)). Cons: README says personal deployment is not directly reusable, and does not supply a minimal new-host/settings tutorial ([`readme.md:126`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L126)). Literal 5 reliable wiring map; no score for package-catalog volume. Score **5**; confidence **medium**.

### V
Scope: CI recipe, output builds and local invariants. Pros: GitHub CI invokes local odu recipe and omnix ([`.github/workflows/ci.yml:38`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/.github/workflows/ci.yml#L38), [`.github/workflows/ci.yml:66`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/.github/workflows/ci.yml#L66)); monitor cardinality and Pi version assumptions have assertions ([`modules/features/workstation/monitors.nix:114`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L114), [`modules/features/ai/pi-web.nix:44`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/ai/pi-web.nix#L44)). Cons: inspected workflow has no explicit negative context/collision fixtures ([`.github/workflows/ci.yml:35`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/.github/workflows/ci.yml#L35)). Literal 5: representative invoked verification intent, not passing evidence. Score **5**; confidence **medium**.

### O
Scope: deploy generation and secrets identities. Pros: every generated NixOS configuration becomes a deploy node ([`modules/deploy.nix:6`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/deploy.nix#L6), [`modules/deploy.nix:15`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/deploy.nix#L15)); host SSH key paths derive SOPS identities ([`modules/secrets.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/secrets.nix#L14), [`modules/secrets.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/secrets.nix#L20)). Cons: skipChecks defaults true and no Den-derived install/builder topology was established ([`modules/deploy.nix:11`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/deploy.nix#L11), [`modules/vm.nix:37`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/vm.nix#L37)). Interpolated6: deployment plus provisioning context exceeds one-concern5, short of coordinated bootstrap/builders9; personal secret path charged to S only. Score **6**; confidence **medium**.

### X
Scope: host/home and VM wrapper outputs. Pros: a VMVariant is deliberately configured ([`modules/vm.nix:5`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/vm.nix#L5)). Cons: package wrapper calls an existing NixOS build-vm result, not a guest/non-host class ([`modules/vm.nix:37`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/vm.nix#L37)). Baseline2; deploy generation belongs only to O. Score **2**; confidence **medium**.

### B
Scope: census max-depth family count and strict complete application units. Pros: complete native prompt/image/video/notes and app integrations are enumerated below ([`modules/features/base/cli/prompt.nix:4`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/prompt.nix#L4), [`modules/features/workstation/apps/image-viewer.nix:15`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/apps/image-viewer.nix#L15)). Cons: fleet services rely on self.lib plus externally owned host.settings.server/network/monitoring schema, so are excluded even when substantive ([`modules/features/server/services/adguard.nix:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/server/services/adguard.nix#L13), [`modules/features/server/services/adguard.nix:31`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/server/services/adguard.nix#L31)). Also exclude identity-bound browser/Git/Spotify, multi-app CLI and missing dependency envelopes; backup options are substantial but not one self-contained application unit ([`modules/features/base/backup.nix:25`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/backup.nix#L25)). Nix-index reference scope is explicitly x86 Linux ([`modules/features/base/cli/nix-index.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/nix-index.nix#L14)). Score **5**; confidence **medium**.
B_div: 7.5 points → 5; B_ref: 10 units → 5; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":7.5,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"prompt","evidence":"modules/features/base/cli/prompt.nix:4"},{"name":"image-viewer","evidence":"modules/features/workstation/apps/image-viewer.nix:2"},{"name":"video-player","evidence":"modules/features/workstation/apps/video-player.nix:2"},{"name":"notes","evidence":"modules/features/workstation/apps/notes.nix:2"},{"name":"kde-connect","evidence":"modules/features/workstation/kde-connect.nix:2"},{"name":"screenshot","evidence":"modules/features/workstation/screenshot.nix:4"},{"name":"screen-recorder","evidence":"modules/features/workstation/apps/screen-recorder.nix:2"},{"name":"flatpak","evidence":"modules/features/workstation/flatpak.nix:4"},{"name":"auto-mount","evidence":"modules/features/base/auto-mount.nix:2"},{"name":"nix-index","evidence":"modules/features/base/cli/nix-index.nix:4"}]}}
```

Total: **51.5/100**. Shortlists: showcase false; library_units ['host-settings']; starter false.

Overall pros:
- Typed host variation reaches real display outputs ([`modules/features/workstation/monitors.nix:150`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/monitors.nix#L150)).
- Deploy targets derive from generated host inventory ([`modules/deploy.nix:6`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/deploy.nix#L6)).
- Current README maps features and roles ([`readme.md:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L13)).
- Native reusable application units exist beyond curated nominations ([`modules/features/workstation/screenshot.nix:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/workstation/screenshot.nix#L13)).

Overall cons / limits:
- Shared author identity and endpoints bypass settings (§6a S; [`modules/features/base/cli/git.nix:20`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/base/cli/git.nix#L20)).
- Settings discovery relies on deep framework internals (maintenance scope; [`modules/schema.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L14)).
- Several services require the surrounding fleet envelope ([`modules/features/server/services/adguard.nix:13`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/features/server/services/adguard.nix#L13)).
- No routed cross-scope fact channel verified (anchor limit; [`modules/host-settings.nix:7`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L7)).

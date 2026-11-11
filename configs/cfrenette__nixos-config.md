# cfrenette__nixos-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/cfrenette__nixos-config.md)

- Upstream: [cfrenette/nixos-config](https://github.com/cfrenette/nixos-config)
- Reviewed revision: [`af711691cde3`](https://github.com/cfrenette/nixos-config/commit/af711691cde33c23754da2d6dc81a7ae52bc5e7c)
- Author: cfrenette
- Score: **42.5 / 100**, rank 79 of 103 ranked configs. D 5 · I 6 · S 4 · R 5 · P 5 · L 1 · V 3 · O 5 · B 4 · X 2. Shortlists: —.
- Summary: D entity-derived backups; I Git/mail coupling; S personal constants despite host/user arguments; R independent HM leaves; P honest NixOS scope; L no guide; V one local invariant; O aspect-owned secrets; B eight complete leaves; X standard targets.

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

Feature modules are joined by Den’s flake module (`modules/den.nix:8`); the inventory assigns named users to hosts (`modules/hosts.nix:7`).

## 2. Common patterns

- mutual-provider applies to every user (`modules/den.nix:12`).
- provides tree separates personal and work Git variants (`modules/git.nix:15`, `modules/git.nix:72`).

## 3. Novel patterns

SOPS has separate user-key and host-key variants, matching interactive and headless deployment (`modules/sops.nix:56`, `modules/sops.nix:70`).

## 4. Library candidates

None verified as a useful independent library unit in the reviewed composition.

## 5. den friction

No verified Den-specific friction in the reviewed wiring (`modules/den.nix:8`).

## 6. Docs and complexity

Docs 1: wiring comments explain one mechanism but no README is present; see the inline explanation at `modules/den.nix:13`. Complexity 3: multiple host assignments (`modules/hosts.nix:7`) and distinct signing identities (`modules/git.nix:72`).

## 6a. Defects and scoring notes

- S · moderate: shared SOPS, Git and service aspects embed author identity/domain/network facts; changing consumers requires shared-source edits (`modules/sops.nix:36`, `modules/git.nix:30`, `modules/aspects/server/pihole.nix:26`). The private input is a visible dependency, not proof of an access failure (`modules/sops.nix:9`).
- I · minor: Git personal variant also configures email delivery/account state and secret placement, preventing separate selection of those concerns (`modules/git.nix:48`, `modules/git.nix:64`).

## 7. Template notes

Useful provides-tree example, but identity and secret input are personal (`modules/git.nix:31`, `modules/sops.nix:9`).

## 8. Scorecard

### D (5, high)
Scope: host/user inventory and backups. Pros: host/user names declared at `modules/hosts.nix:7` flow through context arguments (`modules/backups.nix:9`) into per-user/per-host repositories (`modules/backups.nix:23`); consumers include it through the host provider (`modules/hosts/frmwrk.nix:20`). Cons: no custom policy/pipe or conflict contract; this entity-fact channel reaches the explicit cap 5, not cross-scope routing credit. Confidence: high.

### I (6, high)
Scope: feature, host and provider trees. Pros: GUI leaves and host selection are distinct (`modules/aspects/gui.nix:4`, `modules/hosts/frmwrk.nix:15`). Cons: personal Git also owns an email account and secret deployment (`modules/git.nix:48`, `modules/git.nix:64`, §6a). Interpolation: good feature ownership exceeds 5; the unrelated account side effect caps I at 6. Confidence: high.

### S (4, medium)
Scope: shared Git/SOPS/NAS/proxy/editor bodies. Pros: backups derive names and nh exposes overrideable defaults (`modules/backups.nix:23`, `modules/aspects/nh.nix:17`). Cons: §6a fixed account, domains and network facts (`modules/sops.nix:36`, `modules/aspects/server/pihole.nix:26`). Contract 4: between direct personal constants at 2 and mostly explicit variation at 5. Eight grouped leaks: personal identity, work identity, frenette.dev, Pi address, NAS address, LAN network, secrets-repo root, external personal nixvim root (`modules/git.nix:9`, `modules/git.nix:82`, `modules/aspects/server/acme.nix:17`, `modules/aspects/server/nas.nix:18`, `modules/sops.nix:9`, `modules/aspects/tui/nixvim/nixvim.nix:4`). Raw ≥26 distinct literals in these bodies; repeated identity/path and domain variants are grouped. Coverage grade 6 (4–10 groups); min(4,6)=4. Confidence: medium; hidden secret/editor input bodies are uncredited.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":8}}
```

### R (5, medium)
Scope: independent HM leaves. Pros: nh is usable with at most three overrideable checkout values, no author identity (`modules/aspects/nh.nix:11`, `modules/aspects/nh.nix:17`). Cons: no exported substantial unit plus independent consumer example in inspected entry (`flake.nix:4`); the curated §4 list remains empty. Anchor 5: useful light-adaptation leaves, without deducting S identity again. Confidence: medium.

### P (5, high)
Scope: declared x86/ARM NixOS and WSL selection. Pros: platform-specific hardware and WSL input are explicit (`modules/hosts.nix:7`, `modules/hosts/wsl.nix:8`). Cons: no broader boundary contract/check demonstrated by the host wiring (`modules/hosts/solstice.nix:4`). Anchor 5 for honest narrow support; no penalty for not promising Darwin. Confidence: high.

### L (1, high)
Scope: tracked root inventory and entry/wiring comments. Pros: mutual-provider has a brief explanation (`modules/den.nix:13`); backup retry rationale is useful (`modules/backups.nix:57`). Cons: no README/docs or entry-to-feature tutorial in the pinned inventory; the entry teaches only regeneration (`flake.nix:1`). Absence ruling gives 1 rather than placeholder 2. Confidence: high.

### V (3, medium)
Scope: assertions, entry and tracked workflows. Pros: NAS vhost checks that LAN-only access is retained (`modules/aspects/server/nas.nix:32`). Cons: this one local invariant is not a representative enabled/disabled/context suite, and no relevant CI invocation was found in the pinned inventory (`flake.nix:4`). Interpolation 3: some relevant intent above 2, below representative-check 5; no execution claimed. Confidence: medium.

### O (5, medium)
Scope: SOPS variants, per-service credentials and backup lifecycle. Pros: selected service aspects own secret entries/restart environment (`modules/aspects/server/pihole.nix:51`, `modules/aspects/server/pihole.nix:57`); backup location derives host/user facts (`modules/backups.nix:23`). Cons: recipient enrollment and deployment remain manual (`modules/sops.nix:67`, `modules/hosts/pi.nix:3`). Anchor 5 for an aspect-driven secrets concern, without claiming a unified deployment/bootstrap/builder graph. Confidence: medium.

### B (4, medium)
Scope: every authored feature leaf, not just §4. Pros: eight substantive identity-free complete units are enumerated below, each with its NixOS/HM configuration and package/input contract. Cons: personal Git/SOPS/NAS/proxy, asset-dependent Stylix and external-only Nixvim are excluded (`modules/git.nix:9`, `modules/sops.nix:9`, `modules/aspects/stylix.nix:19`, `modules/aspects/tui/nixvim/nixvim.nix:14`); bare enables, installation lists and include bundles count zero. Census arithmetic: Starship 1 + Nixvim .5 + Bash .5 + Cosmic .5 = 2.5 → diversity 2; eight reference units → 5; mean 3.5 rounds up to B4. Confidence: medium.
```score-evidence
{"B":{"diversity_points":2.5,"diversity_grade":2,"reference_grade":5,"reference_units":[{"name":"alacritty","evidence":"modules/aspects/gui/alacritty.nix:6"},{"name":"gtk","evidence":"modules/aspects/gui/gtk.nix:6"},{"name":"starship","evidence":"modules/aspects/tui/starship.nix:4"},{"name":"opencode","evidence":"modules/aspects/tui/opencode.nix:5"},{"name":"nh","evidence":"modules/aspects/nh.nix:11"},{"name":"pipewire","evidence":"modules/aspects/sound.nix:9"},{"name":"steam-gaming","evidence":"modules/aspects/gaming.nix:6"},{"name":"secure-boot","evidence":"modules/aspects/boot/secure-boot.nix:11"}]}}
```

### X (2, high)
Scope: actual host/classes and imports. Pros: NixOS and HM ownership is explicit (`modules/den.nix:10`, `modules/hosts.nix:7`). Cons: no qualifying nonoperational target class in this inspected tree; WSL/ARM are ordinary host support (`modules/hosts/wsl.nix:8`). Baseline 2; operational SOPS remains O-only. Confidence: high.

Total: **42.5/100**. Shortlists: showcase no; library_units none; starter no. Useful direct provider/context composition, but no routed multi-consumer showcase, independent curated library nomination, or short documented starter path.

Overall pros:
- Backups derive storage identity from Den host/user context (`modules/backups.nix:23`).
- Host providers separate headless and GUI use (`modules/hosts/frmwrk.nix:15`, `modules/users/cory.nix:9`).
- SOPS supports interactive-user and headless-host key modes (`modules/sops.nix:56`, `modules/sops.nix:70`).

Overall cons / limits:
- S: shared secret/account settings embed personal identity (`modules/sops.nix:36`).
- I: personal Git selection also owns email delivery (`modules/git.nix:48`).
- L: no root guide accompanies generated-entry comments (`flake.nix:1`).

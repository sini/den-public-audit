---
title: "DJ-Laser/nixos"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/dj-laser/nixos/)

- Upstream: [DJ-Laser/nixos](https://github.com/DJ-Laser/nixos)
- Reviewed revision: [`27e216e2f9d3`](https://github.com/DJ-Laser/nixos/commit/27e216e2f9d3dfdba89177a82535975eb8a89899)
- Author: DJ-Laser
- Score: **34.0 / 100**, rank 95 of 101 ranked configs. D 2 · I 8 · S 3 · R 5 · P 5 · L 2 · V 2 · O 2 · B 3 · X 2. Shortlists: library units (1).
- Summary: Direct class settings and package plumbing; focused features with a personal user bundle; fixed sync peers/checkout; useful filechooser integration needing explicit terminal/package inputs; honest Linux scope, operation-only typo-prone docs, no relevant checks or derived operational pipeline.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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

Den flake module supplies defaults and a custom angle-reference resolver ([`modules/den.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/den.nix#L6), [`modules/den.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/den.nix#L8)). Hosts select feature aspects and declare HM users ([`modules/hosts/nix-desktop/configuration.nix:9`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L9)).

## 2. Common patterns

- den.default includes define-user, hostname, inputs and self ([`modules/den.nix:11`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/den.nix#L11)).
- angle-bracket refs are enabled through __findFile ([`modules/den.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/den.nix#L6)).

## 3. Novel patterns

Hardware Facter data is attached directly to the host aspect while functional concerns remain selected includes ([`modules/hosts/nix-desktop/configuration.nix:16`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L16), [`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26)).

## 4. Library candidates

- ttypicker-yazi portal · [`modules/desktop/tui-file-manager.nix:17`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L17) · Yazi chooser plugin plus XDG portal selection/configuration · inputs: HM, Den, ttypicker and filechooser-yazi packages (owned at [`packages/ttypicker.nix:23`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/ttypicker.nix#L23), [`packages/filechooser-yazi.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/filechooser-yazi.nix#L6)), terminal · parameterization: none currently; grade B, expose terminal command/package and helper package set instead of self'.packages.

## 5. den friction

No verified Den-specific friction in the reviewed wiring ([`modules/den.nix:7`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/den.nix#L7)).

## 6. Docs and complexity

Docs 2: README emphasizes trying the rice ([`README.md:11`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L11)), while host assembly is discoverable in code ([`modules/hosts/nix-desktop/configuration.nix:16`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L16)). Complexity 3: HM class declaration plus hardware and shared feature selection ([`modules/hosts/nix-desktop/configuration.nix:11`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L11), [`modules/hosts/nix-desktop/configuration.nix:27`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L27)).

## 6a. Defects and scoring notes

- S · moderate: reusable nh/Syncthing leaves fix an author checkout and three peer identities instead of receiving variation ([`modules/apps/nh.nix:7`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/nh.nix#L7), [`modules/apps/syncthing.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/syncthing.nix#L8)).
- L · moderate: README installation command is misspelled nixox-rebuild-switch and omits the machine-specific storage/report replacement its broad invitation needs ([`README.md:12`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L12), [`modules/hosts/nix-desktop/fileSystems.nix:3`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/fileSystems.nix#L3)).
- Hardware reports and CPU/GPU choices themselves remain appropriate named-host content ([`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26)).

## 7. Template notes

Useful clear host-aspect selection example; hardware report and personal desktop selections must be replaced ([`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26)).

## 8. Scorecard

### D (2, medium)
Scope: all Den/aspect/output wiring. Pros: host assembly selects named features explicitly ([`modules/hosts/nix-desktop/configuration.nix:16`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L16)). Cons: applications set module options directly; self package references feed a filechooser package, not structured facts ([`modules/desktop/tui-file-manager.nix:20`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L20), [`modules/packages.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/packages.nix#L6)). Baseline 2 under package-plumbing ruling. Confidence: medium.

### I (8, medium)
Scope: complete feature tree and personal user assembly. Pros: OS services, application leaves and concrete hardware are separate ([`modules/apps/steam.nix:2`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/steam.nix#L2), [`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26)). Cons/ceiling: the personal user still owns browser/Git/application policy together ([`modules/users/dj_laser.nix:34`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L34), [`modules/users/dj_laser.nix:47`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L47)). Interpolation 8 above named-feature baseline 5, short of uniformly optional 9; no hardware-scoping defect invented. Confidence: medium.

### S (3, medium)
Scope: shared app/desktop leaves and named user. Pros: identity itself is appropriately scoped to its user ([`modules/users/dj_laser.nix:24`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/users/dj_laser.nix#L24)). Cons: reusable nh fixes a checkout root and Syncthing fixes three peer identities (§6a, [`modules/apps/nh.nix:7`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/nh.nix#L7), [`modules/apps/syncthing.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/syncthing.nix#L8)). Four grouped changes (checkout + three devices), raw 7 including peer names/IDs; repeats of a device count once. Contract 3: native options exist but shared author variation still patches source; between direct 2 and mostly explicit 5. Coverage 6; min(3,6)=3. Confidence: medium.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":6,"distinct_leaks":4,"raw_leaks":7}}
```

### R (5, medium)
Scope: filechooser/Yazi/portal integration and its packaged helpers. Pros: portal selection, chooser configuration and plugin are wired together ([`modules/desktop/tui-file-manager.nix:46`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L46), [`modules/desktop/tui-file-manager.nix:56`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L56), [`packages/ttypicker.nix:23`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/ttypicker.nix#L23)). Cons: terminal is assumed externally and helpers come through this flake self package namespace ([`modules/desktop/tui-file-manager.nix:20`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L20), [`modules/desktop/tui-file-manager.nix:59`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L59)). Grade B needs two explicit inputs: terminal command/package and helper package set. Anchor 5, no substantial independent A-consumer example. Confidence: medium.

### P (5, medium)
Scope: two declared x86 Linux hosts and standalone home. Pros: hardware reports and CPU/GPU modules remain in host owners ([`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26), [`modules/hosts/laser-book/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/laser-book/configuration.nix#L26)). Cons: desktop assumes Linux/Wayland and has no boundary-check fixture ([`modules/desktop/scrolling-wm.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/scrolling-wm.nix#L26)). Honest narrow anchor 5; installation prose error is L-only. Confidence: medium.

### L (2, medium)
Scope: entire short README and feature/host comments. Pros: rice purpose and chosen Niri/base16 stack are stated ([`README.md:9`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L9)). Cons: the only installation command is misspelled nixox-rebuild-switch and promises easy installation despite source requiring hardware adaptation (§6a, [`README.md:12`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L12), [`modules/hosts/nix-desktop/fileSystems.nix:3`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/fileSystems.nix#L3)). Operation-only anchor 2, without a reliable entry-to-feature tutorial. Confidence: medium.

### V (2, medium)
Scope: tracked entry/modules/workflow inventory. Pros: source separates host reports and feature bodies for inspection ([`modules/hosts/nix-desktop/configuration.nix:16`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L16)). Cons: no relevant configuration check/CI definitions were found; the entry merely instantiates imported modules ([`flake.nix:4`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/flake.nix#L4)). Baseline 2; package builds and screenshots do not establish semantic verification. Confidence: medium.

### O (2, medium)
Scope: installation, services and host assembly. Pros: selected hosts declare SSH explicitly ([`modules/hosts/laser-book/configuration.nix:28`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/laser-book/configuration.nix#L28)). Cons: rebuilding is a hand-entered command, sync peers are literal and no deploy/secret/bootstrap/builder target set derives from Den ([`README.md:12`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L12), [`modules/apps/syncthing.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/syncthing.nix#L8)). Baseline 2, not a demand for unnecessary fleet machinery. Confidence: medium.

### B (3, medium)
Scope: every authored aspect plus local integration packages. Pros: Steam, PipeWire, bootloader and VSCode provide coherent identity-free presets ([`modules/apps/steam.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/steam.nix#L8), [`modules/system/audio.nix:3`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/system/audio.nix#L3), [`modules/system/boot.nix:3`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/system/boot.nix#L3), [`modules/apps/vscode.nix:13`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/vscode.nix#L13)). Cons: token btop/lockscreen/notification tweaks, one-unit startup wrappers, personal Syncthing/nh and framework-dependent Niri/idle helpers do not add references ([`modules/apps/btop.nix:13`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/btop.nix#L13), [`modules/desktop/lock-screen.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/lock-screen.nix#L6), [`modules/desktop/scrolling-wm.nix:34`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/scrolling-wm.nix#L34)). Filechooser still needs an external terminal, so is a B nomination rather than a complete reference. Census 2.5→diversity 2; four reference units→4; B3. Confidence: medium.
```score-evidence
{"B":{"diversity_points":2.5,"diversity_grade":2,"reference_grade":4,"reference_units":[{"name":"steam","evidence":"modules/apps/steam.nix:8"},{"name":"pipewire","evidence":"modules/system/audio.nix:3"},{"name":"systemd-boot","evidence":"modules/system/boot.nix:3"},{"name":"vscode","evidence":"modules/apps/vscode.nix:13"}]}}
```

### X (2, medium)
Scope: Den classes, Niri module and custom filechooser packages. Pros: package/portal ownership is explicit ([`modules/packages.nix:6`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/packages.nix#L6), [`packages/ttypicker.nix:23`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/ttypicker.nix#L23)). Cons: standard NixOS/HM and ordinary packages are not distinct target systems ([`modules/hosts/nix-desktop/configuration.nix:9`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L9), [`modules/desktop/tui-file-manager.nix:20`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L20)). Baseline 2; no D/X credit for package plumbing. Confidence: medium.

Total: **34.0/100**. Shortlists: showcase no; library_units ttypicker-yazi portal; starter no. Filechooser integration is independently useful after light parameterization. No routed-fact showcase or documented safe starter path.

Overall pros:
- Host hardware remains local to each declared machine ([`modules/hosts/nix-desktop/configuration.nix:26`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/hosts/nix-desktop/configuration.nix#L26)).
- Yazi is wired into an actual portal backend ([`modules/desktop/tui-file-manager.nix:46`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L46)).
- Steam owns compatible session/firewall/kernel choices together ([`modules/apps/steam.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/steam.nix#L8)).

Overall cons / limits:
- S: shared sync settings fix peer identities ([`modules/apps/syncthing.nix:8`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/syncthing.nix#L8)).
- S: nh fixes the author checkout path ([`modules/apps/nh.nix:7`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/apps/nh.nix#L7)).
- L: the installation command is misspelled ([`README.md:12`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/README.md#L12)).

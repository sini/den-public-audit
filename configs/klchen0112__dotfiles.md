# klchen0112__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/klchen0112__dotfiles.md)

- Upstream: [klchen0112/dotfiles](https://github.com/klchen0112/dotfiles)
- Reviewed revision: [`d47908159f3e`](https://github.com/klchen0112/dotfiles/commit/d47908159f3eb13c9056ce5a0620b875f67f4579)
- Author: klchen0112
- Score: **39.5 / 100**, rank 91 of 103 ranked configs. D 2 · I 7 · S 2 · R 5 · P 5 · L 2 · V 3 · O 5 · B 7 · X 2. Shortlists: library units (2).
- Summary: Library shortlist for the complete Fish preset and small scrub policy; role projection is an I/P example, with no structured-fact or integration bonus. Starter/showcase withheld because native scoping faults, shared constants and installation drift remain.

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
Dendritic module imports wire custom class routing into den’s user schema (`modules/den.nix:49`, `modules/den.nix:53`). OS and HM baselines coexist with role and platform classes (`modules/defaults.nix:10`, `modules/den.nix:8`).

## 2. Common patterns
- forward: role classes are selected from the host/user role intersection (`modules/den.nix:11`, `modules/den.nix:12`).
- mutual-provider joins the same user schema includes (`modules/den.nix:56`).
- angle-bracket refs in den.default includes (`modules/defaults.nix:64`, `modules/defaults.nix:66`).

## 3. Novel patterns
Platform HM classes forward only under the matching host platform and adapt osConfig from the destination context (`modules/den.nix:20`, `modules/den.nix:29`, `modules/den.nix:33`).

## 4. Library candidates
- fish · `modules/shell/fish/default.nix:13` · **A**, self-contained HM Fish/plugin/Tide preset; inputs standard HM lib/pkgs, all plugin sources and macchina supplied by owner (`modules/shell/fish/default.nix:9`, `modules/shell/fish/default.nix:15`); parameterization through native Fish options; activation configures Tide (`modules/shell/fish/default.nix:42`). No minimal external consumer is documented.
- btrfs-scrub · `modules/btrfs.nix:2` · enables weekly automatic filesystem scrubbing · inputs: NixOS/nixpkgs · parameterization: none (`modules/btrfs.nix:4`) · **A**, self-contained storage maintenance policy.

## 5. den friction
No verified den-specific friction in these forwarding/default fragments (`modules/den.nix:11`, `modules/defaults.nix:64`). The custom forwarding is deliberate composition, not by itself evidence of a den defect.

## 6. Docs and complexity
Docs **2**: the overview describes desktop choices and installation, not the role-forward mechanism (`README.org:1`, `README.org:126`). Complexity **5**: role intersection and guarded platform forwards create additional class semantics (`modules/den.nix:12`, `modules/den.nix:25`).

## 6a. Defects and scoring notes

- **S / moderate:** Shared defaults, SSH/network/device configurations retain author identity/endpoints (`modules/defaults.nix:29`, `modules/ssh/default.nix:35`, `modules/sync/default.nix:13`); see grouped inventory on S card.
- **R / moderate:** lib is referenced without a lexical or function-argument binding in native media/keyboard and devshell owners (`modules/media/default.nix:3`, `modules/media/default.nix:62`, `modules/keyboard/default.nix:3`, `modules/keyboard/default.nix:10`, `modules/devshell.nix:18`, `modules/devshell.nix:36`). This is source scoping evidence, not a claimed evaluation result.
- **L / minor:** Installation instructs editing username in flake.nix and running make up (`README.org:142`, `README.org:145`); current identity/rebuild owners differ (`modules/users/klchen.nix:9`, `Justfile:33`). Role-forward complexity itself is a documented-review coverage limit, not an invented defect.

## 7. Template notes
Best as an advanced class-routing example; the weekly scrub aspect is a simpler entry point (`modules/btrfs.nix:2`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Role labels select configuration modules, not a structured facts payload: mbp-m1 repeats aria2 and other roles for host/user (`modules/hosts/mbp-m1/default.nix:12`, `modules/hosts/mbp-m1/default.nix:29`), intersection forwards their classes into HM (`modules/den.nix:11`), and aria2 contains direct native settings (`modules/aria2/default.nix:20`). This is composition/class projection, baseline 2; no credit is added for the forwarding name or fixed build-output lookups (`modules/vm.nix:11`). Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Named app owners and separate host/user selections localize much work (`modules/hosts/mbp-m1/default.nix:48`, `modules/shell/fish/default.nix:13`). The custom role and platform projections are centralized (`modules/den.nix:8`, `modules/den.nix:18`). 7 interpolates that clear ownership with duplicated per-host/per-user role lists and the broad utilities bundle (`modules/hosts/mbp-m1/default.nix:12`, `modules/hosts/mbp-m1/default.nix:29`, `modules/utils/default.nix:5`). Score **7**; confidence **high**.

### S

Scope · pros · cons/coverage: Roles and native standard arguments express some variation, but shared owners directly embed author identity/peer data rather than a small documented settings contract (`modules/defaults.nix:29`, `modules/defaults.nix:61`, `modules/ssh/default.nix:35`, `modules/inputmethod/default.nix:58`): contract 2. The verified change inventory has 29 groups: one author identity, one domain, four local network/peer addresses, a committed credential (reported privately; not located here), personal cache, five Syncthing device IDs, eight VSCode peer aliases, four display selectors, checkout root, Strata data root, model root and weather location (`modules/deploy-rs.nix:11`, `modules/k3s/client.nix:11`, `modules/k8s/master.nix:8`, `modules/nix/caches.nix:35`, `modules/sync/default.nix:11`, `modules/editor/vscode/default.nix:295`, `modules/de/niri/settings.nix:55`, `modules/de/hyprspace/default.nix:21`, `modules/llm/strata.nix:18`, `modules/llm/default.nix:139`, `modules/de/aero-sketchybar/config/items/today/weather.lua:69`). Raw repeated literals exceed this grouped inventory; no deduction uses occurrence count. Coverage cap 5, S=min(2,5). Ordinary public caches, timezone and application defaults are excluded. Score **2**; confidence **medium**.

```score-evidence
{"S":{"contract_design":2,"leak_coverage":5,"distinct_leaks":29}}
```

### R

Scope · pros · cons/coverage: The identity-free Fish preset supplies its own packages/plugins and Tide setup (`modules/shell/fish/default.nix:9`, `modules/shell/fish/default.nix:15`, `modules/shell/fish/default.nix:42`), a useful substantial unit with standard HM inputs. The weekly scrub is independently usable but tiny (`modules/btrfs.nix:4`). 5 reflects useful units without a documented minimal external consumer/platform contract, and concrete unbound lib references elsewhere (`modules/media/default.nix:3`, `modules/media/default.nix:62`, `modules/keyboard/default.nix:3`, `modules/keyboard/default.nix:10`, `modules/devshell.nix:18`, `modules/devshell.nix:36`); importing those owners cannot resolve lib from their ellipsis. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Platform HM forwarding explicitly guards pkgs.stdenv.hostPlatform and adapts osConfig (`modules/den.nix:25`, `modules/den.nix:29`, `modules/den.nix:33`). Aria2 supplies both systemd and launchd implementations (`modules/aria2/default.nix:312`, `modules/aria2/default.nix:331`), and Fish is native HM (`modules/shell/fish/default.nix:13`). Anchor 5: actual Linux/Darwin scope is visible, without representative boundary tests; documentation does not state support for every defined optional desktop (`README.org:4`). Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: The overview lists desktop choices and directory layout (`README.org:4`, `README.org:16`), then installation commands (`README.org:126`). It does not teach the custom role intersection or platform adaptation (`modules/den.nix:8`, `modules/den.nix:18`), baseline 2. Installation still says change username in flake.nix and make up (`README.org:142`, `README.org:145`), while real identity is modules/users/klchen.nix and rebuild recipes are in Justfile (`modules/users/klchen.nix:9`, `Justfile:33`). Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: Treefmt includes shellcheck alongside formatters (`modules/fmt.nix:31`), with a Just check command (`Justfile:19`); perSystem checks is otherwise explicitly empty (`modules/devshell.nix:20`). 3 credits configured static checking above the no-check baseline; no source-visible positive/negative role-routing or representative host fixture is supplied, and deploy explicitly skips checks (`Justfile:72`). Score **3**; confidence **medium**.

### O

Scope · pros · cons/coverage: User/aspect secret entries are consumed by an actual service: klchen declares hermes-env (`modules/users/klchen.nix:74`), its a99r50 provider declares two more (`modules/users/klchen.nix:79`), and Hermes environmentFiles reads their paths (`modules/users/klchen.nix:98`); sops module supplies the decrypting HM integration (`modules/sops/default.nix:14`). This is one live Den-selected operations concern, anchor 5. Deploy targets remain hand-listed and derive DNS from a literal author domain (`modules/deploy-rs.nix:11`, `modules/deploy-rs.nix:22`); builder keys are manually duplicated (`modules/nix/build-machines.nix:12`). Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: Role and hmLinux/hmDarwin classes all project into ordinary native HM (`modules/den.nix:14`, `modules/den.nix:25`). Kubernetes is configured through NixOS services, not an independently evaluated manifest class (`modules/k8s/master.nix:23`); VM wrapper builds an existing host output (`modules/vm.nix:11`). Standard OS/HM baseline 2. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Selected/max-depth census contributes 8.5 points, diversity grade 7; role chains are evidenced by mbp-m1 lists and forwarding (`modules/hosts/mbp-m1/default.nix:12`, `modules/den.nix:12`). Complete visible reference inventory is 11 units below, grade 7 => B7. Native Niri session/Xwayland is counted once; driver and GPU container-runtime integration have distinct owned contracts. Agent-skills supplies source inputs plus OS→HM inputs handoff within its own aspect (`modules/llm/skill.nix:11`, `modules/llm/skill.nix:41`, `modules/llm/skill.nix:54`). Exclude custom-role-only native leaves requiring outside roleClass routing (`modules/aria2/default.nix:2`, `modules/den.nix:11`), author endpoint/data/secret owners, package-only/bare-enable leaves, broad inseparable utils, and Cosmic whose input is not supplied in this source tree (`modules/de/cosmic/default.nix:10`, `flake.nix:4`). Score **7**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":8.5,"diversity_grade":7,"reference_grade":7,"reference_units":[{"name":"flatpak","evidence":"modules/flatpak/default.nix:12"},{"name":"homebrew","evidence":"modules/homebrew/default.nix:17"},{"name":"fish","evidence":"modules/shell/fish/default.nix:15"},{"name":"nix-index","evidence":"modules/nix-index/default.nix:12"},{"name":"nvidia-graphics","evidence":"modules/hardware/nvidia.nix:14"},{"name":"nvidia-container-runtime","evidence":"modules/k3s/k3s-nvidia.nix:42"},{"name":"gnome","evidence":"modules/de/gnome/default.nix:9"},{"name":"fast-nix-gc","evidence":"modules/nix/gc.nix:20"},{"name":"wine-wayland","evidence":"modules/de/niri/wine.nix:5"},{"name":"niri-session-xwayland","evidence":"modules/de/niri/default.nix:30"},{"name":"agent-skills","evidence":"modules/llm/skill.nix:54"}]}}
```

**Total:** 39.5/100. **Shortlists:** showcase no; library fish, btrfs-scrub; starter no. Library shortlist for the complete Fish preset and small scrub policy; role projection is an I/P example, with no structured-fact or integration bonus. Starter/showcase withheld because native scoping faults, shared constants and installation drift remain.

Overall pros:
- Centralized custom role/platform projections keep selection semantics in one owner (`modules/den.nix:8`).
- Native Fish unit owns packages/plugins and activation preset (`modules/shell/fish/default.nix:15`, `modules/shell/fish/default.nix:42`).
- Actual selected secrets reach service environment files (`modules/users/klchen.nix:98`).

Overall cons / scope limits:
- Several module bodies reference unbound lib (`modules/media/default.nix:62`, `modules/keyboard/default.nix:10`, `modules/devshell.nix:36`).
- Shared native files embed author endpoints/device identifiers (`modules/ssh/default.nix:55`, `modules/sync/default.nix:13`).
- Installation entry points are stale and routing is unexplained (`README.org:142`, `README.org:145`, `modules/den.nix:11`).
- Empty explicit checks provide no role/platform regression coverage (`modules/devshell.nix:20`).

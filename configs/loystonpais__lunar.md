# loystonpais__lunar

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/loystonpais__lunar.md)

- Upstream: [loystonpais/lunar](https://github.com/loystonpais/lunar)
- Reviewed revision: [`5f836c9e4a1c`](https://github.com/loystonpais/lunar/commit/5f836c9e4a1c3076e95f7df3969a77da051b6b2e)
- Author: loystonpais
- Score: **51.0 / 100**, rank 46 of 103 ranked configs. D 5 · I 7 · S 3 · R 5 · P 5 · L 5 · V 3 · O 6 · B 6 · X 5. Shortlists: library units (1).
- Summary: Direct context D5; namespace I7; invalid common settings S3/five groups; twelve coherent references R5; bounded architectures P5; README L5; missing workflow script V3; user-derived sync O6; Droidspaces X5.

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

Direct evalModules loads den plus import-tree with a local withSystem adapter (`flake.nix:5`, `flake.nix:11`). A lunar namespace provides shared features across workstation and ARM/Linux server entities (`modules/den.nix:7`, `modules/hosts.nix:7`, `modules/hosts.nix:32`).


## 2. Common patterns.

- namespace: lunar is explicit and private (`modules/den.nix:7`).
- mutual-provider: user and standalone-home schemas include it (`modules/defaults.nix:17`).
- den.default includes: define-user, hostname, inputs and self (`modules/defaults.nix:21`).
- provides tree: audio exposes optional tools (`modules/lunar/audio.nix:17`).


## 3. Novel patterns.

Default package discovery maps files under packages to callPackage results inside the packages class (`modules/defaults.nix:29`). This keeps custom package exposure adjacent to the general den setup.


## 4. Library candidates.

- audio · `modules/lunar/audio.nix:2` · PipeWire ALSA/Pulse/JACK plus audio controls · NixOS/nixpkgs · none · B: lift namespace and separate optional tools from core audio.


## 5. den friction.

Local withSystem manufactures self.packages.hello rather than full self outputs (`flake.nix:5`); this narrows the semantics of scoped self supplied to batteries.


## 6. Docs and complexity.

Docs 3: README describes feature organization, fleet roles and source directories (`README.md:11`, `README.md:35`, `README.md:62`). Complexity 4: x86/ARM host inventory plus namespace, package discovery and custom scope adapter (`modules/hosts.nix:7`, `modules/hosts.nix:32`, `modules/defaults.nix:29`).


## 6a. Defects and scoring notes.

- S · major: global stateVersion is written as nixpkgs.system.stateVersion, not system.stateVersion, producing an invalid common option/type boundary (`modules/defaults.nix:49`, `modules/defaults.nix:55`).
- S · moderate: Plasma HM body binds pkgs only but package lookup interpolates system, an unbound variable (`modules/lunar/plasma.nix:24`, `modules/lunar/plasma.nix:33`).
- S · minor: five shared adaptation groups enumerated in S (`modules/lunar/hm-home-symlinks.nix:29`, `modules/lunar/acme.nix:101`, `modules/lunar/rclone.nix:21`).
- V · moderate: Cachix workflow invokes packages/.cachix-wf-builds.sh, absent from this revision tree (`.github/workflows/cachix.yaml:22`).
Synthetic self is an interface limitation without verified failed consumer; pure duplicate package list entries are not a defect.

## 7. Template notes.

Useful varied-host namespace example; explain the minimal withSystem implementation before copying scoped self usage (`flake.nix:5`).

## 8. Scorecard.

### D
Scope: direct inventory/user derivation and parameterized services. Pros: host metadata defines devices and user context derives service names/ownership; VM autologin consumes current user (`modules/hosts.nix:9`, `modules/lunar/infisical.nix:34`, `modules/lunar/server.nix:95`). Cons: ordinary package discovery/export and manual host walk are plumbing, not routed facts (`modules/defaults.nix:29`, `modules/outputs.nix:12`). Literal5 direct derivation cap; no live independent quirk/policy route. Score **5**; confidence **medium**.

### I
Scope: namespace owners and entity composition. Pros: lunar namespace owns named features, host data and user owner are separate (`modules/den.nix:7`, `modules/hosts.nix:7`, `modules/users/loystonpais/loystonpais.nix:7`). Cons: several large desktop/development bags contain unrelated apps and global adapters (`modules/lunar/dms.nix:9`, `modules/lunar/dev.nix:1`, `flake.nix:5`). Score7 beyond5 feature owners, below9 consistent independent setup. Score **7**; confidence **medium**.

### S
Scope: callable feature interfaces and shared defaults. Pros: Infisical exposes project/environment/cadence and derives user paths; Rclone exposes selected remotes (`modules/lunar/infisical.nix:7`, `modules/lunar/rclone.nix:7`). Cons: global stateVersion is nested under nixpkgs.system rather than system, and Plasma references unbound system (`modules/defaults.nix:49`, `modules/defaults.nix:55`, `modules/lunar/plasma.nix:33`). Contract3 below5 due statically malformed common setting boundary; no evaluation claimed. Four shared adaptation groups: checkout root, secret namespace, ACME author domain, remote catalog plus physical Plasma input identity is fifth (`modules/lunar/hm-home-symlinks.nix:29`, `modules/lunar/sops.nix:34`, `modules/lunar/acme.nix:101`, `modules/lunar/rclone.nix:21`, `modules/lunar/plasma.nix:43`). Coverage6; min3. Score **3**; confidence **medium**.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":6,"distinct_leaks":5}}
```

### R
Scope: complete nonidentity reference envelopes. Pros: VSCode owns profiles/extensions/store-path language tools, Infisical owns timer/user/state/shell consumer, agent constructor owns jail/runtime implementation (`modules/lunar/vscode.nix:175`, `modules/lunar/infisical.nix:35`, `modules/lunar/agents.nix:7`). Cons: Plasma has unbound variable, Zed tasks need unowned language commands, DMS/Niri use outside fleet schema and Minecraft requires self packages/checkout (`modules/lunar/plasma.nix:33`, `modules/lunar/zed.nix:36`, `modules/lunar/niri/niri.nix:39`, `modules/lunar/minecraft/minecraft.nix:21`, `modules/lunar/minecraft/minecraft.nix:36`). Literal5 useful references, below9 polished reusable module library. Score **5**; confidence **medium**.

### P
Scope: x86/ARM Linux hosts and Android-rootfs integration. Pros: architecture inventory explicit; Vili selects Droidspaces rootfs/pinned systemd adapter (`modules/hosts.nix:7`, `modules/hosts.nix:32`, `modules/hosts/vili/vili.nix:16`). Cons: custom scoped self only exposes synthetic hello; no broad self-output interface assumed (`flake.nix:7`). Literal5 bounded configurations; family novelty charged X once. Score **5**; confidence **medium**.

### L
Scope: README architecture and usage. Pros: explains aspects, fleet roles, source directories and rebuild commands (`README.md:11`, `README.md:35`, `README.md:62`, `README.md:78`). Cons: no worked adding-host/new-feature/policy route and documented primary shell differs from current user battery (`README.md:55`, `modules/users/loystonpais/loystonpais.nix:12`). Literal5 useful orientation, below9 complete authoring route. Score **5**; confidence **medium**.

### V
Scope: actual workflow routes. Pros: deploy workflow addresses supplied host output and package workflow is declared (`.github/workflows/deploy-hosts.yaml:55`, `.github/workflows/cachix.yaml:21`). Cons: package job executes packages/.cachix-wf-builds.sh absent at pinned tree; no semantic fixtures for defaults/scoped-self verified (`.github/workflows/cachix.yaml:22`, `modules/defaults.nix:55`). Score3 above2 declared automation but below5 usable structural coverage. Score **3**; confidence **medium**.

### O
Scope: derived secret service and VM lifecycle. Pros: selected user sync derives paths/unit names and shell consumption; VM autologin follows user; CI supplies deployment host manually (`modules/users/loystonpais/loystonpais.nix:252`, `modules/lunar/infisical.nix:35`, `modules/lunar/infisical.nix:103`, `modules/lunar/server.nix:95`). Cons: deployment target selection is not generated from Den inventory and global adapter/common setting issues remain separately charged S (`.github/workflows/deploy-hosts.yaml:19`, `flake.nix:7`). Score6: multiple context-derived operational concerns beyond5, below9 fleet lifecycle. Score **6**; confidence **medium**.

### X
Scope: nonstandard managed target family. Pros: Vili NixOS entity imports working Droidspaces Android rootfs plus systemd compatibility module (`modules/hosts.nix:33`, `modules/hosts/vili/vili.nix:16`). Cons: K8s/Android CLI packages and ordinary package discovery are not further target families (`modules/lunar/android.nix:14`, `modules/defaults.nix:29`). Literal5 one evaluated additional environment family; no runtime success claimed. Score **5**; confidence **medium**.

### B
Scope: twelve complete named app envelopes and census max-depth. Pros: counted units own coherent presets or integration, including callable jail constructor and all its local implementation; Lazyvim counts once with parent module import (`modules/lunar/agents.nix:7`, `modules/lunar/neovim.nix:7`, `modules/lunar/neovim.nix:53`). Cons: package-only/token leaves, include-only bags, mixed browser/dev tools, custom DMS/Niri/Minecraft/self-package/Rclone-secret envelopes excluded (`modules/lunar/browsers.nix:6`, `modules/lunar/dms.nix:9`, `modules/lunar/minecraft/minecraft.nix:21`, `modules/lunar/rclone.nix:62`). Zed tasks omit owned Ruby/Python runtime; Plasma malformed system reference excluded (`modules/lunar/zed.nix:36`, `modules/lunar/plasma.nix:33`). Score **6**; confidence **medium**.
B_div: 7.5 points → 5; B_ref: 12 units → 7; half-up mean → 6.
```score-evidence
{"B":{"diversity_points":7.5,"diversity_grade":5,"reference_grade":7,"reference_units":[{"name":"audio","evidence":"modules/lunar/audio.nix:2"},{"name":"infisical-sync","evidence":"modules/lunar/infisical.nix:7"},{"name":"vscode","evidence":"modules/lunar/vscode.nix:6"},{"name":"android-adb","evidence":"modules/lunar/android.nix:2"},{"name":"devenv","evidence":"modules/lunar/devenv.nix:6"},{"name":"podman","evidence":"modules/lunar/podman.nix:2"},{"name":"ssh","evidence":"modules/lunar/ssh.nix:2"},{"name":"hyprland","evidence":"modules/lunar/hyprland.nix:8"},{"name":"distrobox","evidence":"modules/lunar/distrobox.nix:2"},{"name":"lazyvim","evidence":"modules/lunar/neovim.nix:53"},{"name":"agent-jail","evidence":"modules/lunar/agents.nix:7"},{"name":"asuslinux","evidence":"modules/lunar/asuslinux.nix:2"}]}}
```

Total: **51.0/100**. Shortlists: showcase false; library_units ['audio']; starter false.

Overall pros:
- Feature namespace and fleet metadata are clear (`modules/hosts.nix:7`).
- Infisical unit derives user service and consumers (`modules/lunar/infisical.nix:35`).
- Droidspaces rootfs target is concrete (`modules/hosts/vili/vili.nix:16`).

Overall cons / limits:
- Common stateVersion is under wrong setting scope (§6a S; `modules/defaults.nix:55`).
- Package workflow invokes missing script (§6a V; `.github/workflows/cachix.yaml:22`).
- Plasma references unbound system (§6a S; `modules/lunar/plasma.nix:33`).

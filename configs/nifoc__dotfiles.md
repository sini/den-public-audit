# nifoc__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/nifoc__dotfiles.md)

- Upstream: [nifoc/dotfiles](https://github.com/nifoc/dotfiles)
- Reviewed revision: [`387a13d9abfe`](https://github.com/nifoc/dotfiles/commit/387a13d9abfe831aac5e8b27d9c567d3d4fbe337)
- Author: nifoc
- Score: **45.5 / 100**, rank 69 of 103 ranked configs. D 4 · I 7 · S 4 · R 4 · P 7 · L 1 · V 5 · O 7 · B 4 · X 2. Shortlists: —.
- Summary: Visible literal meta lookup D4; meaningful owners I7; ad hoc settings S4/twelve groups; public-root blocker R4; platform branches P7; URL-only L1; host checks V5; deploy/unlock/backup O7; ordinary targets X2; eight visible independent units.

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

Generated flake-parts/import-tree unconditionally imports public and private module roots (`flake.nix:7`). Public host aspects supply platform/user role bundles, with shared HM scope settings under schema (`modules/hosts/Pallas/default.nix:7`, `modules/dendritic.nix:56`).


## 2. Common patterns.

- mutual-provider: user schema enables reciprocal providers (`modules/dendritic.nix:71`).
- provides tree: host to-users supplies base, client and desktop roles (`modules/hosts/Pallas/default.nix:7`).
- den.default includes: system-scoped inputs are global (`modules/dendritic.nix:54`).


## 3. Novel patterns.

Host aspects carry structured network/firewall/ZFS metadata alongside role composition (`modules/hosts/gallium/default.nix:28`), separating much service configuration from machine facts.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

private is a tracked git submodule using an SSH-only private repository (`.gitmodules:1`); its modules are imported unconditionally (`flake.nix:9`). The public snapshot alone cannot supply that module tree.


## 6. Docs and complexity.

Docs 1: README only identifies main/mirror URLs (`README.md:1`). Complexity 5: multiple platform host bundles and service/network metadata depend on a private overlay of modules (`modules/hosts/Pallas/default.nix:7`, `modules/hosts/gallium/default.nix:28`, `flake.nix:9`).


## 6a. Defects and scoring notes.

- R · major: unconditional private/modules import requires unavailable SSH-authenticated tracked submodule; public snapshot cannot provide module root (`flake.nix:9`, `.gitmodules:1`, `.gitmodules:3`).
- S · moderate: twelve grouped visible adaptations enumerated in S remain outside entity ownership (`modules/audiobookshelf/caddy.nix:10`, `modules/base/networking.nix:9`, `modules/base/msmtp.nix:35`, `modules/geoip-updater/default.nix:25`).
- L · moderate: root README supplies source URLs without architecture/private bootstrap route (`README.md:1`).
Runtime secret availability is distinct from mandatory source import; no unverified private behavior asserted.

## 7. Template notes.

Useful public aspect examples, but private module dependencies prevent a self-contained starter (`flake.nix:9`, `modules/hosts/Pallas/default.nix:20`).

## 8. Scorecard.

### D
Scope: public metadata consumers and providers. Pros: host network metadata drives network naming, DNS interfaces and initrd access; explicit to-users base selection exists (`modules/base/networking.nix:45`, `modules/dns-resolver/blocky.nix:8`, `modules/remote-access/ssh-unlock.nix:8`, `modules/hosts/gallium/default.nix:7`). Cons: consumers perform literal aspect-name lookups, with no routed fact policy or missing/duplicate protocol verified (`modules/base/networking.nix:45`). Score4 literal-peer lookup cap. Private merge may alter selected producers, so visible-code confidence is low. Score **4**; confidence **low**.

### I
Scope: feature directories, host metadata and role composition. Pros: application owners have separate files and host meta separates network/ZFS/access facts (`modules/audiobookshelf/default.nix:2`, `modules/hosts/gallium/default.nix:28`). Cons: base/cli/development are coarse shared addresses and mandatory private overlay obscures final ownership (`modules/base/direnv.nix:8`, `modules/cli/yt-dlp.nix:2`, `flake.nix:9`). Score7 beyond5 meaningful owners, below9 explicit closed scope. Score **7**; confidence **low**.

### S
Scope: visible metadata/settings contracts. Pros: service paths/identity often derive actual context, backup settings follow host meta (`modules/base/agenix.nix:16`, `modules/restic/default.nix:12`). Cons: meta consumers are ad hoc rather than locally typed, and twelve grouped visible adaptations remain: four author domain roots (.network/.io/.email/.li), LAN network, Tailscale network, container network, media storage root, encrypted-secret namespace, checkout root, mail identity, GeoIP account (`modules/audiobookshelf/caddy.nix:10`, `modules/forgejo/default.nix:12`, `modules/mail-security/default.nix:6`, `modules/base/networking.nix:9`, `modules/base/networking.nix:18`, `modules/flaresolverr/default.nix:23`, `modules/audiobookshelf/default.nix:21`, `modules/base/msmtp.nix:16`, `modules/base/shells/zsh.nix:166`, `modules/base/msmtp.nix:35`, `modules/geoip-updater/default.nix:25`). Contract4 below5 typed shared surface; coverage5 capped11–30; min4. Host-owned physical addresses excluded; hidden private settings could move score either direction. Score **4**; confidence **low**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":12}}
```

### R
Scope: visible independently importable app-owner files. Pros: Direnv, Starship and Lazygit are coherent generic presets; Rift and Wezterm own runtime/config assembly (`modules/base/direnv.nix:12`, `modules/base/starship.nix:10`, `modules/development/lazygit.nix:43`, `modules/desktop/macos/rift.nix:224`, `modules/desktop/wezterm.nix:21`). Cons: whole public checkout cannot load unconditional private modules; many service units require fleet schema/identity/assets (`flake.nix:9`, `.gitmodules:3`, `modules/audiobookshelf/default.nix:21`). Score4 below5 self-contained reference collection because mandatory root dependency blocks direct project reuse; visible independent leaves still earn credit, hidden merge unresolved. Score **4**; confidence **low**.

### P
Scope: Linux/Darwin and host-specific service boundaries. Pros: public inventory includes both platforms; shell/editor choose Darwin-only pieces explicitly (`modules/hosts/Pallas/default.nix:4`, `modules/hosts/gallium/default.nix:4`, `modules/base/shells/zsh.nix:148`, `modules/editors/neovim/default.nix:69`). Cons: private source prevents final merged output/platform guarantee and arbitrary host meta is required (`flake.nix:9`, `modules/base/networking.nix:45`). Score7 explicit boundaries beyond5, below9 contract-edge fixtures. Score **7**; confidence **low**.

### L
Scope: root documentation. Pros: README identifies source/mirror (`README.md:1`). Cons: no architecture, private bootstrap or feature/host authoring route (`README.md:1`, `.gitmodules:3`). Literal1 absent teaching route; private-source limit itself is not an invented documentation promise. Score **1**; confidence **low**.

### V
Scope: visible configured checks. Pros: checks build named per-system host toplevels and smoke deploy executable (`modules/flake-parts/checks.nix:15`, `modules/flake-parts/checks.nix:34`, `modules/flake-parts/checks.nix:43`). Cons: literal check inventory omits Styx and cannot be run from public source without private tree (`modules/flake-parts/checks.nix:29`, `modules/hosts/Styx/default.nix:4`, `flake.nix:9`). Literal5 structural checks, low confidence final merge; no run claimed. Score **5**; confidence **low**.

### O
Scope: inventory-derived deploy, unlock and backup lifecycle. Pros: deploy nodes map actual NixOS outputs/system activation; initrd unlock derives host network and authorized keys; Restic derives remote/secret paths (`modules/flake-parts/deploy.nix:33`, `modules/flake-parts/deploy.nix:50`, `modules/remote-access/ssh-unlock.nix:8`, `modules/restic/default.nix:12`). Cons: deployment deliberately disables rollback and uses hostname suffix convention; private overlay required for final target state (`modules/flake-parts/deploy.nix:41`, `modules/flake-parts/deploy.nix:44`, `flake.nix:9`). Score7 multiple derived lifecycle concerns beyond5, below9 validated complete fleet workflow; hidden source could improve or weaken. Score **7**; confidence **low**.

### X
Scope: normal OS/home targets and application containers. Pros: public host variants cover hardware/VM presets (`modules/hosts/gallium/default.nix:20`). Cons: Quadlet/Podman services are application infrastructure, not a distinct evaluated Den target family (`modules/podman/quadlet.nix:12`). Baseline2; private source does not permit null or assumed extra family. Score **2**; confidence **low**.

### B
Scope: eight complete visible app-owner envelopes and census accounting. Pros: independent app-specific files count despite sharing base/cli/development address; native assets belong to Wezterm/Neovim envelope and plugins/config are generated locally (`modules/desktop/wezterm.nix:30`, `modules/editors/neovim/default.nix:89`, `modules/editors/neovim/default.nix:319`). Cons: many services depend on fleet metadata/domain/media roots, so excluded; Bat/Btop/Yazi cosmetic presets and enable-only leaves excluded, FZF needs unowned fd, Zsh includes custom external functions/upa, Bitwarden needs custom user meta (`modules/audiobookshelf/caddy.nix:10`, `modules/dns-resolver/blocky.nix:8`, `modules/cli/btop.nix:10`, `modules/base/fzf.nix:7`, `modules/base/shells/zsh.nix:166`, `modules/bitwarden/cli.nix:46`). Census has no selection-verified enabled row because private merge is unknown: diversity2 is accounting lower bound, not asserted absence of software. Hidden source could change both dimensions. Score **4**; confidence **low**.
B_div: 0 points → 2; B_ref: 8 units → 5; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":0,"diversity_grade":2,"reference_grade":5,"reference_units":[{"name":"direnv","evidence":"modules/base/direnv.nix:8"},{"name":"starship","evidence":"modules/base/starship.nix:2"},{"name":"lazygit","evidence":"modules/development/lazygit.nix:2"},{"name":"yt-dlp","evidence":"modules/cli/yt-dlp.nix:2"},{"name":"openssh","evidence":"modules/remote-access/ssh.nix:2"},{"name":"rift","evidence":"modules/desktop/macos/rift.nix:6"},{"name":"wezterm","evidence":"modules/desktop/wezterm.nix:2"},{"name":"neovim","evidence":"modules/editors/neovim/default.nix:4"}]}}
```

Total: **45.5/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Host metadata feeds real operational consumers (`modules/remote-access/ssh-unlock.nix:8`).
- Deployment nodes follow actual output inventory (`modules/flake-parts/deploy.nix:33`).
- Substantive public app presets remain useful (`modules/development/lazygit.nix:43`).

Overall cons / limits:
- Mandatory private module import blocks public checkout (§6a R; `flake.nix:9`).
- Shared service metadata retains author adaptations (§6a S; `modules/audiobookshelf/caddy.nix:10`).
- No root architecture/bootstrap teaching (§6a L; `README.md:1`).

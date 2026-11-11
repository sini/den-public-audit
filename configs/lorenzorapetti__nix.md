# lorenzorapetti__nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/lorenzorapetti__nix.md)

- Upstream: [lorenzorapetti/nix](https://github.com/lorenzorapetti/nix)
- Reviewed revision: [`e6b3e716d30a`](https://github.com/lorenzorapetti/nix/commit/e6b3e716d30a98a32ee8e76bfafbee6828d40357)
- Author: lorenzorapetti
- Score: **59.0 / 100**, rank 18 of 103 ranked configs. D 7 · I 6 · S 4 · R 7 · P 5 · L 7 · V 6 · O 7 · B 5 · X 2. Shortlists: showcase, library units (1).
- Summary: Four traced quirk channels and an output-inventory-derived cache pipeline distinguish the design; personal global assumptions and custom desktop schema constrain whole-repo adoption despite strong explanatory docs.

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

Den’s flake module supplies common settings while host files declare inventory (`modules/den.nix:8`, `modules/hosts/nyx/default.nix:3`). README explains the flake-parts/import-tree arrangement (`README.md:8`).

## 2. Common patterns

- den.default includes hostname and system-selected inputs/self (`modules/den.nix:13`).
- define-user+primary-user are selected by the user aspect (`modules/users/lorenzo/lorenzo.nix:9`, `modules/users/lorenzo/lorenzo.nix:13`).

## 3. Novel patterns

Shared OS and HM state versions stay together in the global aspect (`modules/den.nix:25`, `modules/den.nix:96`).

## 4. Library candidates

**Managed Flatpak/Flathub** · `modules/desktop/flatpak.nix:2`: owns upstream module import, remote registration and weekly automatic updates (`modules/desktop/flatpak.nix:4`, `modules/desktop/flatpak.nix:10`, `modules/desktop/flatpak.nix:16`). Inputs: Den and explicitly supplied `inputs.nix-flatpak`; ordinary NixOS module context. Parameterization: native Flatpak options; no owner identity required. Reuse **A**: retain the file and declared upstream input, select its aspect on a NixOS host. No independent minimal consumer example is supplied.

## 5. den friction

No verified Den-specific friction in the reviewed wiring (`modules/den.nix:99`).

## 6. Docs and complexity

Docs 4: README teaches recursive imports (`README.md:15`), and wiring explains batteries (`modules/den.nix:17`). Complexity 3: multiple host declarations (`modules/hosts/hades/default.nix:6`, `modules/hosts/nyx/default.nix:3`) share one user schema (`modules/den.nix:100`).

## 6a. Defects and scoring notes

- **S moderate:** globally selected locale/cache defaults require changing personal region/cache trust for a second fleet (`modules/den.nix:27`, `modules/den.nix:69`, `modules/den.nix:78`); grouped with other shared owner assumptions in S, not charged again to P.
- **L minor:** installation guide claims the Sops module declares a specific age.keyFile path, but the referenced module only sets defaultSopsFile (`docs/new-host.md:143`, `modules/secrets/sops.nix:13`). The reader must resolve this stale configuration claim; runtime decryption behavior was not tested.
Co-locating defaults is not itself a verified defect (`modules/den.nix:24`).

## 7. Template notes

Accessible feature-oriented layout; global defaults contain personal locale/cache policy to replace (`modules/den.nix:27`, `modules/den.nix:69`).

## 8. Scorecard

### D (7, high)
Score: 7. Confidence: high. Scope: four live quirk channels. Pros: Technitium emits ports consumed by the firewall (`modules/homelab/technitium.nix:26`, `modules/networking/firewall.nix:10`); app MIME entries reach XDG defaults (`modules/desktop/applications/base.nix:92`, `modules/base/xdg.nix:3`); homelab routes reach generated proxy routers/services (`modules/homelab/glance.nix:3`, `modules/homelab/traefik.nix:9`); embedded triples extend the Rust toolchain (`modules/development/embedded.nix:7`, `modules/development/rust.nix:16`). Cons: MIME conversion silently uses listToAttrs and proxy routes recursively overwrite keys (`modules/base/xdg.nix:4`, `modules/homelab/traefik.nix:9`), with no stated collision contract there. Interpolation 7: actual multiple channels; no 8–9 cross-scope policy/duplicate guarantees.

### I (6, high)
Score: 6. Confidence: high. Scope: feature composition. Pros: features own ordinary native imports and dependencies, including Flatpak and Steam overlays/modules (`modules/desktop/flatpak.nix:4`, `modules/desktop/gaming/steam.nix:4`); context-specific 1Password policy derives its owner (`modules/desktop/applications/1password.nix:5`, `modules/desktop/applications/1password.nix:13`). Cons / limit: desktop bodies depend on separate font/terminal schema and feature profiles (`modules/desktop/applications/terminals.nix:53`, `modules/desktop/hyprland/default.nix:71`, `modules/desktop/hyprland/default.nix:83`). Interpolation 6: coherent integration beyond 5, with tighter cross-feature coupling than 9; no additional defect charged for that choice.

### S (4, medium)
Score: 4. Confidence: medium. Scope: shared configuration, excluding correctly scoped host hardware and user Git identity. Pros: host files own their disk/driver facts and personal Git has a user envelope (`modules/hosts/hades/default.nix:35`, `modules/hosts/zagreus/disko.nix:8`, `modules/users/lorenzo/lorenzo.nix:68`). Cons: shared defaults fix region and private cache/key (`modules/den.nix:27`, `modules/den.nix:69`, `modules/den.nix:78`); AI/editor settings require an owner checkout (`modules/ai/default.nix:9`, `modules/desktop/applications/coding.nix:47`); shared GPG trusts/signs one identity (`modules/security/gpg.nix:29`, `modules/security/gpg.nix:69`). Proxy domains, three device addresses and LAN range are personal (`modules/homelab/traefik.nix:66`, `modules/homelab/traefik.nix:91`, `modules/homelab/traefik.nix:100`, `modules/homelab/traefik.nix:120`, `modules/homelab/traefik.nix:125`, `modules/homelab/traefik.nix:130`); five audio-device rules include a serial identity (`modules/desktop/sound.nix:23`, `modules/desktop/sound.nix:32`, `modules/desktop/sound.nix:45`, `modules/desktop/sound.nix:67`, `modules/desktop/sound.nix:148`). Builder origin/identity, work calendar and notes/code roots add choices (`modules/homelab/atticd-builder.nix:2`, `modules/homelab/atticd-builder.nix:37`, `modules/desktop/noctalia.nix:62`, `modules/shell/default.nix:8`, `modules/shell/default.nix:78`). Twenty grouped changes, at least 35 raw sites: coverage cap 5, contract 4 controls S.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":20,"raw_leaks":35}}
```

### R (7, high)
Score: 7. Confidence: high. Scope: independently adoptable app envelopes. Pros: Flatpak owns its upstream import, Flathub URL and automatic update schedule (`modules/desktop/flatpak.nix:1`, `modules/desktop/flatpak.nix:4`, `modules/desktop/flatpak.nix:10`, `modules/desktop/flatpak.nix:16`); Tailscale derives interface/port from native options (`modules/networking/tailscale.nix:3`). Cons: docs show whole-host addition rather than an independent app consumer (`docs/new-host.md:102`), and major desktop presets need outside custom schema (`modules/desktop/noctalia.nix:197`). Interpolation 7: genuine closed A integrations, without a minimal independent app example for 9.

### P (5, high)
Score: 5. Confidence: high. Scope: supported NixOS consumers. Pros: laptop, desktop, VM and server select different hardware/services through their own envelopes (`README.md:63`, `modules/hosts/hades/default.nix:31`, `modules/hosts/nyx/default.nix:15`). Cons / limit: the shared interactive stack requires NixOS osConfig and custom OS fields (`modules/shell/fish.nix:26`, `modules/desktop/applications/terminals.nix:53`); no additional platform consumer is shown by the declared inventory (`README.md:63`). Anchor 5 for honest Linux support, without penalizing the support boundary itself.

### L (7, high)
Score: 7. Confidence: high. Scope: explanatory docs and owner workflows. Pros: README teaches import-tree and entity/aspect composition (`README.md:15`, `README.md:28`) and includes a concrete host inventory (`README.md:61`); host-addition guide supplies Disko/entity examples and installation commands (`docs/new-host.md:56`, `docs/new-host.md:102`, `docs/new-host.md:149`). Cons: guide attributes an age.keyFile setting to a module that does not declare it (`docs/new-host.md:143`, `modules/secrets/sops.nix:13`). Interpolation 7: substantial instructions, short of a fully matching independent adoption guide.

### V (6, high)
Score: 6. Confidence: high. Scope: declared checks and scheduled builds. Pros: statix/deadnix checks are real flake outputs (`modules/checks.nix:7`, `modules/checks.nix:13`); the selected cache job builds generated host outputs, records failures and refuses publication after any failure (`modules/hosts/nyx/default.nix:18`, `modules/homelab/atticd-builder.nix:68`, `modules/homelab/atticd-builder.nix:74`, `modules/homelab/atticd-builder.nix:80`). Cons / limit: VM is explicitly omitted and the job updates the remote checkout rather than testing a fixed independent consumer (`modules/homelab/atticd-builder.nix:62`, `modules/homelab/atticd-builder.nix:65`, `modules/homelab/atticd-builder.nix:69`). Interpolation 6 for declared broader integration builds plus lint; no passing run was executed or inferred.

### O (7, high)
Score: 7. Confidence: high. Scope: inventory-derived maintenance and secrets. Pros: cache builder enumerates actual generated NixOS configurations, builds each and publishes only after collective success (`modules/homelab/atticd-builder.nix:68`, `modules/homelab/atticd-builder.nix:74`, `modules/homelab/atticd-builder.nix:80`, `modules/homelab/atticd-builder.nix:85`); per-aspect secret templates feed service environments (`modules/homelab/traefik.nix:11`, `modules/homelab/traefik.nix:17`). Cons: checkout origin and skipped VM remain literal policy (`modules/homelab/atticd-builder.nix:2`, `modules/homelab/atticd-builder.nix:69`), while remote switch is a fixed recipe (`justfile:17`). Interpolation 7 for two derived lifecycle concerns, below broad fleet provisioning at 9.

### B (5, medium)
Score: 5. Confidence: medium. Scope: full visible native application-reference inventory. Pros: 14 coherent units cover native search/desktop, gaming, networking, hardware maintenance and a collected Rust toolchain (`modules/base/nix.nix:7`, `modules/desktop/gaming/steam.nix:4`, `modules/development/rust.nix:16`). Cons: broad multi-app shell/default profiles are not split (`modules/shell/default.nix:40`); desktop sound/GPG contain personal devices or identity (`modules/desktop/sound.nix:67`, `modules/security/gpg.nix:29`); desktop theme/terminal/Noctalia files need fleet font/aspect schema (`modules/themes/catppuccin.nix:8`, `modules/desktop/applications/terminals.nix:67`, `modules/desktop/noctalia.nix:197`). Packaging-only AppImage and CLI outputs do not create reference aspects (`modules/_lib/appimage.nix:29`, `modules/shell/linear.nix:26`). Standard resource-quirk collector dependencies are allowed; no custom-schema dependency is waved through. Census 5→3, reference 14→7; B=5.
```score-evidence
{"B":{"diversity_points":5.0,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"Nix-index/comma integration","evidence":"modules/base/nix.nix:7"},{"name":"XDG desktop policy","evidence":"modules/base/xdg.nix:12"},{"name":"Plymouth quiet boot","evidence":"modules/boot/plymouth.nix:4"},{"name":"1Password desktop integration","evidence":"modules/desktop/applications/1password.nix:9"},{"name":"Managed Flatpak/Flathub","evidence":"modules/desktop/flatpak.nix:4"},{"name":"Ananicy scheduling integration","evidence":"modules/desktop/gaming/ananicy.nix:4"},{"name":"Steam Proton/Gamescope integration","evidence":"modules/desktop/gaming/steam.nix:4"},{"name":"Nix daemon resource policy","evidence":"modules/desktop/nix-daemon.nix:9"},{"name":"Bluetooth policy","evidence":"modules/hardware/bluetooth.nix:4"},{"name":"BTRFS maintenance/snapshots","evidence":"modules/hardware/btrfs.nix:4"},{"name":"AMD graphics policy","evidence":"modules/hardware/igpu-amd.nix:4"},{"name":"NetworkManager/resolved","evidence":"modules/networking/networkmanager.nix:8"},{"name":"Tailscale firewall integration","evidence":"modules/networking/tailscale.nix:4"},{"name":"Rust target toolchain","evidence":"modules/development/rust.nix:9"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: output families. Pros / limit: embedded targets configure a native host toolchain, not firmware artifacts evaluated as a separate Den class (`modules/development/embedded.nix:7`, `modules/development/rust.nix:16`). Cons: ordinary app package outputs and Den nh wrappers add no non-host family (`modules/packages/zellij-sesh.nix:3`, `modules/nh.nix:3`). Baseline 2.

Total: **59.0/100**. Shortlists: showcase yes; library_units Managed Flatpak/Flathub; starter no. Useful showcase of actual quirk collection and derived cache maintenance; managed Flatpak is independently reusable. Personal checkout/secret prerequisites prevent a starter shortlist.

Overall pros:
- Four actual emitter/consumer channels (`modules/networking/firewall.nix:10`, `modules/base/xdg.nix:3`, `modules/homelab/traefik.nix:9`, `modules/development/rust.nix:16`).
- Generated host enumeration drives guarded cache publication (`modules/homelab/atticd-builder.nix:68`, `modules/homelab/atticd-builder.nix:80`).
- Closed managed Flatpak envelope (`modules/desktop/flatpak.nix:4`, `modules/desktop/flatpak.nix:16`).
- Substantial architecture and host-addition explanations (`README.md:28`, `docs/new-host.md:102`).

Overall cons / limits:
- Shared cache, checkout and identity assumptions (`modules/den.nix:69`, `modules/ai/default.nix:9`, `modules/security/gpg.nix:69`).
- No stated quirk collision contract at overwrite sites (`modules/base/xdg.nix:4`, `modules/homelab/traefik.nix:9`).
- Desktop presets require external custom font/terminal schema (`modules/desktop/applications/terminals.nix:53`, `modules/desktop/noctalia.nix:197`).
- Bootstrap guide cites an age.keyFile declaration absent from its referenced module (`docs/new-host.md:143`, `modules/secrets/sops.nix:13`).

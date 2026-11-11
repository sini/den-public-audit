# eldios__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/eldios__dotfiles.md)

- Upstream: [eldios/dotfiles](https://github.com/eldios/dotfiles)
- Reviewed revision: [`ce9d9573891e`](https://github.com/eldios/dotfiles/commit/ce9d9573891ec0460a23da535166ab6455c0586e)
- Author: eldios
- Score: **51.5 / 100**, rank 43 of 103 ranked configs. D 5 · I 6 · S 4 · R 5 · P 5 · L 7 · V 5 · O 6 · B 5 · X 2. Shortlists: library units (1).
- Summary: D5 context-only cap; S4 visible shared variation contract and sixteen grouped changes; R5 small closed presets; L7 explicit composition guides; B5 both census/reference grades5.

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

A fleet inventory states entities while separate host aspects select roles (`modules/hosts.nix:1`). Den wiring overrides host instantiation to provide an explicit common argument set (`modules/den.nix:10`, `modules/den.nix:21`).

## 2. Common patterns

- define-user+primary-user and host-aspects are user includes (`modules/users/eldios.nix:14`, `modules/users/eldios.nix:19`).
- den.default includes hostname and HM integration (`modules/den.nix:24`).

## 3. Novel patterns

Password configuration inspects cleartext SOPS key names before deciding whether to create a password-backed account (`modules/users/eldios.nix:31`, `modules/users/eldios.nix:35`).

## 4. Library candidates

- AMD GPU integration · `modules/aspects/hardware/gpu-amd.nix:4` · owns common hardware import, driver/compute tools and home VA/VDPAU settings · inputs: nixos-hardware, nixpkgs, Den · native Linux GPU options; no author parameters · A; select the aspect on a compatible AMD host and retain its declared input (`modules/aspects/hardware/gpu-amd.nix:7`, `modules/aspects/hardware/gpu-amd.nix:23`, `modules/aspects/hardware/gpu-amd.nix:32`).

## 5. den friction

Host instantiate and HM extraSpecialArgs are wired manually to preserve the argument API expected by modules (`modules/den.nix:8`, `modules/den.nix:21`, `modules/den.nix:33`); no explicit upstream defect is established.

## 6. Docs and complexity

Docs 4: README teaches model and links further docs (`README.md:65`, `README.md:87`); source describes fleet and argument boundaries (`modules/hosts.nix:1`, `modules/den.nix:8`). Complexity 4: custom instantiation and secret-dependent account logic (`modules/den.nix:21`, `modules/users/eldios.nix:35`).

## 6a. Defects and scoring notes

- S · moderate: hasPassword only searches for a top-level YAML passwords key, then requests `passwords/<host>/<user>`; an unrelated passwords mapping can select an absent account secret, while alternative valid YAML formatting can miss the gate (`modules/users/eldios.nix:32`, `modules/users/eldios.nix:35`, `modules/users/eldios.nix:37`). Private data unavailable; no current-fleet failure asserted.
- Explicit OS/HM argument propagation serves two module boundaries and is not inherently a defect (`modules/den.nix:21`, `modules/den.nix:33`). No additional verified defect in the scoped reading.

## 7. Template notes

Good migration/integration reference; module argument injection and secrets conventions need adaptation (`modules/den.nix:10`, `modules/users/eldios.nix:31`).

## 8. Scorecard

### D (5, high)
Score: 5. Confidence: high. Scope: actual host/user facts. Pros: selected user aspect derives secret file/key from host.name and user.userName; Clevis derives mapper/device/IP from host/native config (`modules/users/eldios.nix:31`, `modules/aspects/services/_clevis-unlock.nix:28`, `modules/aspects/services/_clevis-unlock.nix:32`). Cons: these are context/native-config derivations, with no policy/quirk route; backup peers remain a fixed list (`modules/aspects/services/_backup-server.nix:20`). Context-only cap 5 applies.

### I (6, high)
Score: 6. Confidence: high. Scope: source ownership/composition. Pros: underscore files hold owned native modules, host selectors choose features, and user-specific host overrides use provides (`modules/aspects/desktop/hyprland.nix:13`, `modules/hosts/lele8845ace.nix:4`, `modules/hosts/lele8845ace.nix:48`). Cons: base/CLI/desktop bundles combine many capabilities and shared overlays supply hidden package assumptions (`modules/aspects/_base/system.nix:86`, `modules/aspects/dev/cli.nix:6`, `modules/aspects/overlays.nix:5`). Coherent ownership earns 6, below isolated 9.

### S (4, medium)
Score: 4. Confidence: medium. Scope: visible shared code; private network/secrets bodies unavailable, scored visible code with medium confidence. Pros: host hardware is properly scoped and monitor settings are an explicit option (`modules/hosts/lele8845ace.nix:28`, `modules/aspects/desktop/_hyprland/omarchy-shell.nix:291`). Cons: sixteen grouped changes remain: owner identity; checkout root; private-repo local root; LAN; Docker DNS address; cache policy; locale; three DAC selectors; two backup peers; backup storage root; Clevis interface and driver; local MCP endpoint (`modules/aspects/_base/system.nix:8`, `modules/aspects/_base/system.nix:148`, `scripts/prebuild-dispatch.sh:16`, `modules/aspects/_base/system.nix:95`, `modules/aspects/_dns.nix:25`, `modules/aspects/_nix-cache.nix:47`, `modules/aspects/_locale.nix:2`, `modules/aspects/desktop/_audio/audio.nix:90`, `modules/aspects/desktop/_audio/audio.nix:117`, `modules/aspects/desktop/_audio/audio.nix:149`, `modules/aspects/services/_backup-server.nix:8`, `modules/aspects/services/_backup-server.nix:20`, `modules/aspects/services/_clevis-unlock.nix:100`, `modules/aspects/services/_clevis-unlock.nix:108`, `modules/aspects/dev/_ai-tools/mcp-servers.nix:45`). Coverage capped 5; contract 4 because shared identity/topology and secret-shape assumptions remain; S=4.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":16}}
```

### R (5, high)
Score: 5. Confidence: high. Scope: complete native feature modules. Pros: GPU AMD owns its declared hardware-module import, native settings and tools; Ghostty needs only native HM config (`modules/aspects/hardware/gpu-amd.nix:4`, `modules/aspects/hardware/gpu-amd.nix:23`, `modules/aspects/desktop/_terminals/ghostty.nix:1`). Cons: most larger integrations depend on global overlays, private data or runtime Riso assets (`modules/aspects/neovim.nix:7`, `modules/aspects/desktop/_hyprland/omarchy-shell.nix:307`, `modules/aspects/_dns.nix:13`). Useful preset/light-parametrization level 5; no substantial independently demonstrated consumer for 9.

### P (5, high)
Score: 5. Confidence: high. Scope: declared x86_64 Linux fleet, separate from two-architecture tooling. Pros: hosts select Intel/AMD/laptop-specific modules, and packaged CLI rejects unsupported systems explicitly (`modules/hosts/lele9iyoga.nix:23`, `modules/hosts/lele8845ace.nix:23`, `modules/aspects/_overlays/antigravity-cli.nix:19`). Cons: host instantiate always uses nixosSystem and only x86_64 hosts exist; aarch64 formatter/devshell is not host support (`modules/den.nix:21`, `modules/hosts.nix:4`, `modules/flake-outputs.nix:7`). Honest narrow scope fits 5.

### L (7, high)
Score: 7. Confidence: high. Scope: composition and operating guides. Pros: README explains both classes, user propagation and provides; new-host guide gives complete selector/module steps; theme guide describes runtime ownership/fallback (`README.md:67`, `docs/new-host.md:25`, `docs/new-host.md:73`, `docs/theming.md:71`). Cons: private secret schema/enrollment is not reproduced and the example retains the author user (`README.md:76`, `docs/new-host.md:13`). Strong explicit path earns 7, below self-contained prerequisites/independent examples for 9.

### V (5, high)
Score: 5. Confidence: high. Scope: declared trusted checking workflow, not results. Pros: eval-all derives actual nixosConfigurations names and forces every host toplevel; ci combines format, shell lint and that evaluation (`Justfile:21`, `Justfile:45`). Cons: no focused enable/disable, missing-key or routing regression checks are declared; prebuild workflow body is remote/private to this source (`modules/flake-outputs.nix:12`, `scripts/prebuild-dispatch.sh:29`). Representative output coverage fits 5; nothing was executed.

### O (6, medium)
Score: 6. Confidence: medium. Scope: visible host/user operations. Pros: selected aspects emit secrets/templates, and Clevis derives host JWE/mapper/native addresses for initrd unlock (`modules/users/eldios.nix:31`, `modules/aspects/dev/_ai-tools/mcp-servers.nix:54`, `modules/aspects/services/_clevis-unlock.nix:28`). Cons: backup peers and signing identities are maintained separately; prebuild dispatch has fixed repo/private local path (`modules/aspects/services/_backup-server.nix:20`, `modules/aspects/_nix-cache.nix:52`, `scripts/prebuild-dispatch.sh:14`). Multiple derived concerns place 6 above per-aspect secrets 5, but manual registries and unavailable provisioning semantics prevent upper-band credit.

### B (5, medium)
Score: 5. Confidence: medium. Scope: full visible substantive complete app-unit inventory. Pros: nine native units below own usable presets; Ghostty optional theme include is deliberately nonfatal (`modules/aspects/desktop/_terminals/ghostty.nix:29`, `modules/aspects/hardware/gpu-amd.nix:7`). Cons: bare enable/package, broad multi-app bundles, author-identity Git/Zsh/Nu, nonoptional Riso-dependent terminals/lock, global-overlay Neovim, and private/fleet-dependent backup/Clevis/DNS/cache/MCP integrations are excluded (`modules/aspects/desktop/_terminals/alacritty.nix:16`, `modules/aspects/desktop/_terminals/nushell.nix:4`, `modules/aspects/neovim.nix:7`, `modules/aspects/services/_clevis-unlock.nix:32`). Audio/Tang require rebinding three DAC selectors/one LAN; no hidden/private units invented. Census 7.5→5; reference 9→5; B=5.
```score-evidence
{"B":{"diversity_points":7.5,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"PipeWire DAC/rate preset","evidence":"modules/aspects/desktop/_audio/audio.nix:7"},{"name":"Ghostty native terminal preset","evidence":"modules/aspects/desktop/_terminals/ghostty.nix:3"},{"name":"WezTerm tab/window preset","evidence":"modules/aspects/desktop/_terminals/wezterm.nix:3"},{"name":"Yazi plugin/tool integration","evidence":"modules/aspects/dev/_cli/yazi.nix:5"},{"name":"AMD GPU driver/compute integration","evidence":"modules/aspects/hardware/gpu-amd.nix:7"},{"name":"Intel GPU media/compute integration","evidence":"modules/aspects/hardware/gpu-intel.nix:8"},{"name":"Nvidia offload preset","evidence":"modules/aspects/hardware/gpu-nvidia.nix:6"},{"name":"Suspend policy module","evidence":"modules/aspects/_base/suspend.nix:10"},{"name":"Tang access/firewall preset","evidence":"modules/aspects/services/_tang-server.nix:7"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: distinct non-host Den module targets. Pros: virtual machines and several desktop shells are configured operationally (`modules/hosts/_mininixos/libvirt-vms.nix:6`, `modules/aspects/desktop/_hyprland/omarchy-shell.nix:316`). Cons: these are native NixOS/HM settings and runtime app packages, not other module systems driven as Den classes (`modules/aspects/virtualisation.nix:4`, `modules/aspects/desktop/hyprland.nix:13`). Baseline 2.

Total: **51.5/100**. Shortlists: showcase no; library_units AMD GPU integration; starter no. A readable migration/composition example with useful small native presets; larger app envelopes remain personal or private. Library shortlist credits the closed AMD integration, not hidden runtime infrastructure.

Overall pros:
- README/new-host guide explain actual entry, classes and per-user provides (`README.md:67`, `docs/new-host.md:25`).
- Host/user identity drives secret references and initrd unlock inputs (`modules/users/eldios.nix:31`, `modules/aspects/services/_clevis-unlock.nix:28`).
- All declared host outputs are enumerated by the verification recipe (`Justfile:21`).

Overall cons / limits:
- Shared native modules still assume the author account, checkout and hardware (`modules/aspects/_base/system.nix:8`, `modules/aspects/_base/system.nix:148`, `modules/aspects/desktop/_audio/audio.nix:90`).
- Password presence heuristic does not validate the requested nested account key (`modules/users/eldios.nix:32`, `modules/users/eldios.nix:35`).
- Private secrets/network input prevents verification of its contents; no runtime or evaluation success claimed (`flake.nix:40`, `modules/aspects/_dns.nix:13`).

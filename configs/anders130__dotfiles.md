# anders130__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/anders130__dotfiles.md)

- Upstream: [anders130/dotfiles](https://github.com/anders130/dotfiles)
- Reviewed revision: [`470c551356c8`](https://github.com/anders130/dotfiles/commit/470c551356c8ccc92421f2d863cc0c15058df035)
- Author: anders130
- Score: **52.5 / 100**, rank 39 of 103 ranked configs. D 5 · I 6 · S 5 · R 7 · P 5 · L 4 · V 5 · O 7 · B 5 · X 2. Shortlists: showcase, library units (1).
- Summary: D5 one traced readme route; O7 host-derived install/docs plus per-aspect secrets; R7 audio/client contracts; S5 eleven grouped changes; B5 census3/reference7.

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

Personal dots namespace wraps shared feature modules (`modules/flake/namespace.nix:2`). Host declarations remain in a distinct hosts tree (`hosts/wsl/default.nix:9`, `README.md:5`).

## 2. Common patterns

- namespace dots is exported (`modules/flake/namespace.nix:2`).
- host-aspects integrates host HM features (`modules/default/homeManager.nix:25`).

## 3. Novel patterns

Audio devices are expressed through an option schema then translated into WirePlumber device/node rules (`modules/hardware/audio.nix:23`, `modules/hardware/audio.nix:71`).

## 4. Library candidates

- audio · `modules/hardware/audio.nix:2` · generates device naming/profile/disable rules · inputs: nixpkgs lib/packages · parameterization: options my.audio.devices · B; document profile string grammar.

## 5. den friction

No verified Den-specific friction in the reviewed namespace import (`modules/flake/namespace.nix:2`).

## 6. Docs and complexity

Docs 4: README maps directories (`README.md:5`) and host source contributes detailed install guidance and maintenance caveat (`hosts/wsl/default.nix:16`, `hosts/wsl/default.nix:19`). Complexity 4: namespace composition plus substantial configurable device-rule generation (`modules/flake/namespace.nix:2`, `modules/hardware/audio.nix:37`).

## 6a. Defects and scoring notes

- P · minor: selected WSL VPN service spells systemd KillMode as KillMde; the intended kill behavior is not configured by that key (`hosts/wsl/vpn.nix:16`). Runtime impact untested.
- I · minor: Nextcloud declares startInBackground but the complete config renderer never consumes it (`modules/apps/nextcloud/options.nix:7`, `modules/apps/nextcloud/config.nix:13`); setting it does not arrange startup.
- The WSL maintenance warning and documented audio grammar are support/contract limits, not verified defects (`hosts/wsl/default.nix:16`, `modules/hardware/audio.nix:86`).

## 7. Template notes

Useful option-based reuse and colocated host documentation; WSL target explicitly lacks current maintenance assurance (`hosts/wsl/default.nix:16`).

## 8. Scorecard

### D (5, high)
Score: 5. Confidence: high. Scope: actual Den contribution routing, distinct from native option transforms. Pros: aspects emit readme contributions, a host-class-guarded policy routes them to native host options, then actual nixosConfigurations generate README files (`modules/apps/winapps/default.nix:5`, `modules/default/readme.nix:43`, `hosts/readme.nix:6`, `hosts/readme.nix:24`). Cons: this is one live channel; audio/keyboard/monitor transformations are native option data rather than further policy channels (`modules/hardware/audio.nix:23`, `modules/default/keyboard.nix:10`). Fits 5, without multiple routed fact concerns for 7–9.

### I (6, high)
Score: 6. Confidence: high. Scope: feature ownership. Pros: namespaces and includes localize app definitions, and native schemas sit with their renderers (`modules/flake/namespace.nix:2`, `modules/apps/nextcloud/options.nix:5`, `modules/apps/nextcloud/config.nix:13`). Cons: desktop combines unrelated apps and theme-dependent wrappers consume a shared flake helper (`modules/desktop/desktop.nix:14`, `modules/apps/kitty.nix:6`). Above 5 for coherent ownership, below 9 for broad bundles/global coupling.

### S (5, medium)
Score: 5. Confidence: medium. Scope: shared second-consumer changes, excluding correct host hardware/user facts. Pros: audio and Nextcloud take typed settings, while hardware remains host-scoped (`modules/hardware/audio.nix:71`, `modules/apps/nextcloud/options.nix:5`, `hosts/jesse-desktop/peripherals.nix:11`). Cons: eleven groups remain: owner identity, cache URL/key, repo root/clone identity, locale, work path, search endpoint, local browser endpoint, music window geometry, OpenRGB motherboard, audio card default, monitor fallback (`modules/dev/git/package.nix:15`, `modules/apps/winapps/default.nix:35`, `modules/shell/nix/nix.nix:54`, `modules/flake/readme.nix:13`, `modules/default/locale.nix:3`, `modules/work.nix:14`, `modules/apps/browsers/browser.nix:53`, `modules/apps/browsers/zen-browser/extensions/vimium.nix:58`, `modules/apps/youtube-music.nix:29`, `modules/hardware/openrgb.nix:10`, `modules/hardware/audio.nix:121`, `modules/desktop/display/monitors.nix:15`). Contract 6, grouped coverage cap 5.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":5,"distinct_leaks":11,"raw_leaks":12}}
```

### R (7, high)
Score: 7. Confidence: high. Scope: closed app options/helpers. Pros: audio owns schema, rule generation and enablement; Nextcloud owns client settings and declares its initial-file helper (`modules/hardware/audio.nix:71`, `modules/hardware/audio.nix:102`, `modules/apps/nextcloud/deps.nix:2`, `modules/helpers/initial-files.nix:9`). Cons: profile grammar needs care and reusable client has no minimal independent adoption example (`modules/hardware/audio.nix:46`, `modules/apps/nextcloud/options.nix:24`). Substantial A/B units earn 7, not 9.

### P (5, high)
Score: 5. Confidence: high. Scope: declared x86 Linux desktop/laptop/WSL. Pros: WSL imports its platform module separately and documents reduced maintenance assurance (`hosts/wsl/default.nix:58`, `hosts/wsl/README.md:5`). Cons: only x86_64-linux is declared, HM expects osConfig, and native user-file inclusion assumes /home (`modules/flake/systems.nix:2`, `modules/default/homeManager.nix:18`, `modules/shell/nix/nix.nix:63`). Honest narrow support fits 5; the maintenance disclaimer itself is not a defect.

### L (4, high)
Score: 4. Confidence: high. Scope: entry, operational prerequisites and reuse explanation. Pros: directory map, rebuild commands and generated per-host installation/secure-boot instructions are concrete (`README.md:5`, `README.md:35`, `hosts/workstation/README.md:16`, `hosts/workstation/README.md:36`). Cons: README does not teach adding/selecting a feature or explain the readme policy (`README.md:5`, `README.md:35`, `modules/default/readme.nix:43`). Useful operations docs justify 4, below composition-onboarding 5.

### V (5, high)
Score: 5. Confidence: high. Scope: declared checks only. Pros: shellcheck/statix/secrets hooks and formatting are wired, and host build closure includes syntax checking generated effective Hyprland Lua (`modules/dev/git/hooks.nix:9`, `modules/flake/treefmt.nix:23`, `modules/desktop/hyprland/lua-check.nix:10`, `modules/desktop/hyprland/lua-check.nix:18`). Cons: luac checks syntax, not compositor behavior or missing/colliding contribution variants (`modules/desktop/hyprland/lua-check.nix:14`). Representative checks fit 5; no checks were run.

### O (7, high)
Score: 7. Confidence: high. Scope: host operations. Pros: native disk configuration drives per-host install instructions; aspect notes and actual output inventory drive generated READMEs; per-owner secrets and rebuild host identity are selected through Den (`modules/hardware/disko.nix:12`, `modules/hardware/disko.nix:35`, `hosts/readme.nix:6`, `hosts/workstation/wireguard/default.nix:3`, `modules/default/rebuild.nix:109`). Cons: recipient/key enrollment is manual and rebuild expects ambient NH_FLAKE (`modules/default/sops.nix:5`, `modules/default/rebuild.nix:67`). Several derived concerns justify 7, below automated provisioning 9.

### B (5, medium)
Score: 5. Confidence: medium. Scope: all visible complete app/native presets. Pros: sixteen units below retain app activation/settings and declared helpers (`modules/apps/nextcloud/deps.nix:2`, `modules/apps/nautilus.nix:9`, `modules/hardware/audio.nix:102`). Cons: theme/fleet-schema-dependent Kitty, Tmux, Atuin, Zen, Discord, Element, Hyprland/Caelestia and AI registry consumers are excluded; package-only, token cosmetic and one-resource leaves are excluded too (`modules/apps/kitty.nix:6`, `modules/shell/atuin.nix:3`, `modules/apps/browsers/zen-browser/default.nix:19`, `modules/dev/ai/agents/claude/default.nix:22`). Native DisplayLink preset excludes readme-class additions; OpenRGB motherboard needs light parameterization. Census 4.5→3 and reference 16→7 average to 5.
```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"WirePlumber device/profile rules","evidence":"modules/hardware/audio.nix:23"},{"name":"Nextcloud declarative client","evidence":"modules/apps/nextcloud/config.nix:13"},{"name":"ZapZap initial settings","evidence":"modules/apps/messengers/zapzap.nix:11"},{"name":"YouTube Music desktop preset","evidence":"modules/apps/youtube-music.nix:23"},{"name":"OBS virtual camera","evidence":"modules/apps/obs.nix:4"},{"name":"Direnv Fish completions","evidence":"modules/dev/direnv.nix:19"},{"name":"Btop ROCm/view preset","evidence":"modules/shell/btop.nix:8"},{"name":"Steam gaming integration","evidence":"modules/gaming/steam/default.nix:3"},{"name":"DisplayLink native driver integration","evidence":"modules/hardware/displaylink.nix:9"},{"name":"Nautilus extension integration","evidence":"modules/apps/nautilus.nix:9"},{"name":"KDE Connect firewall/agent","evidence":"modules/apps/kdeconnect.nix:4"},{"name":"Fastfetch wrapper preset","evidence":"modules/shell/fastfetch/default.nix:19"},{"name":"Lethal Company mod loader","evidence":"modules/gaming/lethal-company.nix:5"},{"name":"OpenRGB daemon/user integration","evidence":"modules/hardware/openrgb.nix:8"},{"name":"Lsd hidden-file integration","evidence":"modules/shell/lsd.nix:9"},{"name":"Yazi opener integration","evidence":"modules/shell/yazi.nix:6"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: non-host module/output targets. Pros: configured wrapper-module packages and a readme class are visible (`modules/flake/wrappers.nix:3`, `modules/default/readme.nix:10`). Cons: wrappers are configured alongside Den; readme is operational O, and ESPHome-named host file only installs Chromium/dialout access (`modules/apps/kitty.nix:13`, `hosts/jesse-desktop/esphome.nix:7`). No distinct non-operational Den target class; baseline 2.

Total: **52.5/100**. Shortlists: showcase yes; library_units audio; starter no. Showcase the host-derived installation documentation; audio is a useful extraction. Operational instructions do not yet make this an independent starter.

Overall pros:
- Readme class contributions become actual host-specific documentation (`modules/default/readme.nix:43`, `hosts/readme.nix:24`).
- Audio and Nextcloud expose meaningful typed app contracts (`modules/hardware/audio.nix:71`, `modules/apps/nextcloud/options.nix:5`).
- Effective generated Lua receives syntax validation in the host closure (`modules/desktop/hyprland/lua-check.nix:12`).

Overall cons / limits:
- Many desktop leaves require the shared theme/schema envelope (`modules/apps/kitty.nix:6`, `modules/desktop/caelestia/config.nix:46`).
- Shared WinApps/Git identity and cache defaults need rebinding (`modules/apps/winapps/default.nix:35`, `modules/dev/git/package.nix:15`, `modules/shell/nix/nix.nix:54`).
- WSL service has a misspelled systemd field; runtime impact is untested (`hosts/wsl/vpn.nix:16`).

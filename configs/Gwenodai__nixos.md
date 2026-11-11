# Gwenodai__nixos

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/Gwenodai__nixos.md)

- Upstream: [Gwenodai/nixos](https://github.com/Gwenodai/nixos)
- Reviewed revision: [`ab05d3c6e156`](https://github.com/Gwenodai/nixos/commit/ab05d3c6e156b7651a1ec6ee874c553f71979734)
- Author: Gwenodai
- Score: **56.0 / 100**, rank 28 of 103 ranked configs. D 7 · I 7 · S 6 · R 7 · P 5 · L 2 · V 2 · O 7 · B 6 · X 2. Shortlists: showcase, library units (1).
- Summary: D7 live cross-host provenance routing capped by head semantics; S6 five grouped changes; R7 real helpers; B6 census3/reference9; L2 and V2 limit onboarding confidence.

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

Entity schemas carry hardware information and shared batteries (`modules/hosts/stacy-pc/hardware.nix:6`, `modules/schema/defaults.nix:12`). Policies collect host metadata and schemas expose derived aspect inventories (`modules/policies/network-backends.nix:10`, `modules/schema/activeAspects.nix:39`).

## 2. Common patterns

- policies collect quirks with provenance (`modules/policies/network-backends.nix:16`).
- define-user and user-shell are global defaults (`modules/schema/defaults.nix:16`).

## 3. Novel patterns

A host emits backend hostname/IP/key (`modules/hosts/gwen-t1/main.nix:19`), pipe.collect retains provenance (`modules/policies/network-backends.nix:16`), and SSH turns collected entries into knownHosts (`modules/aspects/services/ssh.nix:22`). Derived read-only activeAspects and category groups let consumers inspect entity composition (`modules/schema/activeAspects.nix:11`, `modules/schema/activeAspects.nix:29`).

## 4. Library candidates

- activeAspects schema · `modules/schema/activeAspects.nix:3` · exposes names and category groups for host/user aspects · inputs: Den, nixpkgs lib · parameterization: fn args entity/typeName · B; document top-level traversal limits.

## 5. den friction

The shared SSH data consumer temporarily excludes a named host, weakening generic policy composition (`modules/aspects/services/ssh.nix:34`). Custom enumeration assumes aspects are discoverable through den.aspects values (`modules/schema/activeAspects.nix:11`).

## 6. Docs and complexity

Docs 2: source comments describe schema semantics (`modules/schema/activeAspects.nix:10`, `modules/schema/defaults.nix:22`); a two-sentence purpose/example README exists (`readme.md:1`, `readme.md:3`). Complexity 5: custom hardware schema, metadata policies and derived introspection (`modules/hosts/stacy-pc/hardware.nix:7`, `modules/policies/network-backends.nix:10`, `modules/schema/activeAspects.nix:39`).

## 6a. Defects and scoring notes

- S · moderate: schema-wide authorizedKeys installs Gwen's two literal keys for every user, including Stacy; consumer identity must be rebound (`modules/schema/defaults.nix:25`, `modules/aspects/services/ssh.nix:101`).
- D · minor: CIFS uses head over backend matches without missing/duplicate diagnostics; an absent target fails without a domain-specific message (`modules/aspects/batteries/mount-cifs.nix:26`). No runtime failure is claimed for the current matching hosts.

## 7. Template notes

Good advanced metadata/policy reference, requiring prior understanding of entity predicates and policy collection (`modules/schema/activeAspects.nix:11`, `modules/policies/network-backends.nix:17`).

## 8. Scorecard

### D (7, high)
Score: 7. Confidence: high. Scope: host/user facts and live routes. Pros: all three hosts emit connection facts; provenance-preserving policy feeds SSH and CIFS (`modules/hosts/gwen-t1/main.nix:19`, `modules/policies/network-backends.nix:16`, `modules/aspects/services/ssh.nix:22`, `modules/aspects/batteries/mount-cifs.nix:26`); preservation forwards six classes into host/user state (`modules/aspects/core/preservation/class/classes.nix:78`). Cons: CIFS silently takes the first matching backend and has no missing-match guard (`modules/aspects/batteries/mount-cifs.nix:26`), capping otherwise cross-scope routing at 7.

### I (7, high)
Score: 7. Confidence: high. Scope: ownership and composition. Pros: app owners declare their upstream modules/inputs, and class adapters stay in explicit bridges (`modules/aspects/window-managers/shells/noctalia/noctalia.nix:9`, `modules/aspects/window-managers/niri/niri.nix:19`); host-specific user profiles select app/config separately (`modules/hosts/gwen-t1/main.nix:53`). Cons: consumers know shared category/schema contracts and global user defaults (`modules/aspects/window-managers/niri/config/keybinds.nix:20`, `modules/schema/defaults.nix:25`). Above 5 for explicit ownership and adapters, below 9 without a demonstrated external consumer.

### S (6, medium)
Score: 6. Confidence: medium. Scope: visible shared presets, excluding correct per-host IP/device facts and named-user identities. Pros: hardware choices are typed host facts and Git secrets remain user-scoped (`modules/schema/hardware.nix:22`, `modules/users/stacy/git.nix:8`). Cons: five grouped second-consumer changes remain: global authorized-key identity, ymir exception, checkout root, locale, and x86 cache-path assumption (`modules/aspects/services/ssh.nix:101`, `modules/aspects/services/ssh.nix:37`, `modules/aspects/programs/cli-tools/nh.nix:8`, `modules/aspects/core/preservation/minimal.nix:95`, `modules/aspects/system/locale.nix:4`, `modules/aspects/core/preservation/minimal.nix:108`). Contract 7; coverage capped at 6 by five groups; raw six occurrences (NH/preserved checkout share one root).
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":5,"raw_leaks":6}}
```

### R (7, high)
Score: 7. Confidence: high. Scope: reusable closures. Pros: active-aspect schema takes entity/type/lib; CIFS helper explicitly accepts mount identity/options (`modules/schema/activeAspects.nix:3`, `modules/aspects/batteries/mount-cifs.nix:3`). Kitty owns useful native integration without author identity (`modules/aspects/programs/terminals/kitty.nix:14`). Cons: category consumers require this schema and CIFS requires retained policy/emissions (`modules/aspects/window-managers/niri/config/keybinds.nix:20`, `modules/policies/network-backends.nix:22`). Substantial A/B units justify 7; no minimal independent consumer for 9.

### P (5, high)
Score: 5. Confidence: high. Scope: declared Linux fleet. Pros: hardware facts select AMD CPU/GPU behavior and optional display settings (`modules/aspects/system/hardware/amdcpu.nix:23`, `modules/aspects/system/hardware/amdgpu.nix:46`, `modules/schema/hardware.nix:72`). Cons: only x86_64-linux is declared and editor tooling assumes system Nix path (`modules/schema/defaults.nix:6`, `modules/aspects/programs/vscode/optional/config/languages/nix.nix:32`). Coherent narrow platform boundary earns 5; no wider target claim.

### L (2, high)
Score: 2. Confidence: high. Scope: repository onboarding. Pros: README identifies Den and links a concrete host example (`readme.md:1`, `readme.md:3`); schema has option descriptions (`modules/schema/hardware.nix:24`). Cons: two-sentence README does not document setup, route contracts or independent adoption (`readme.md:1`, `readme.md:3`). Purpose/example-only documentation fits 2.

### V (2, high)
Score: 2. Confidence: high. Scope: visible verification declarations. Pros: flake assembles pinned input-backed modules (`flake.nix:4`, `modules/aspects/core/inputs.nix:4`). Cons: that assembly declares no checks/tests; helpers are operational tools, not regression oracles (`flake.nix:4`, `modules/aspects/core/preservation/pkgs/find-ephemeral.nix:60`). Baseline 2; no evaluation or runtime checks were performed.

### O (7, high)
Score: 7. Confidence: high. Scope: host/home lifecycle. Pros: per-owner secret emissions feed password/Git wiring, persistence derives effective state, and find-ephemeral reads that effective configuration (`modules/users/gwen/gwen.nix:12`, `modules/users/gwen/git.nix:22`, `modules/aspects/core/preservation/class/transformers.nix:40`, `modules/aspects/core/preservation/pkgs/find-ephemeral.nix:24`). Cons: encryption recipients remain manual and no deployment/bootstrap validation is declared (`.sops.yaml:16`, `flake.nix:4`). Multiple derived concerns justify 7, below 9 for manual registry/limited lifecycle evidence.

### B (6, medium)
Score: 6. Confidence: medium. Scope: all visible complete native app presets; custom persistence additions uncredited. Pros: 20 closed native app units below cover shell, desktop integration, login, audio and hardware policy (`modules/aspects/programs/gnome-calendar.nix:5`, `modules/aspects/services/audio.nix:6`, `modules/aspects/system/hardware/amdgpu.nix:33`). Cons: Steam/MangoHud/Nemo/VSCode/Sty­lix/Niri depend on caller schema; bare enable, package+MIME, package+custom-persist and cosmetic Starship toggles are excluded (`modules/aspects/games/tools/mangohud.nix:40`, `modules/aspects/programs/file-managers/nemo.nix:75`, `modules/aspects/programs/vscode/optional/config/settings.nix:97`, `modules/aspects/programs/shells/starship.nix:11`). Census 4.5→3; reference 20→9; half-up mean 6.
```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":9,"reference_units":[{"name":"Heroic native launcher preset","evidence":"modules/aspects/games/launchers/heroic/optional/config.nix:21"},{"name":"Halo Wars camera/input preset","evidence":"modules/aspects/games/mods/halo-wars/cameraZoom.nix:11"},{"name":"Bat pager integration","evidence":"modules/aspects/programs/cli-tools/bat.nix:7"},{"name":"Eza listing preset","evidence":"modules/aspects/programs/cli-tools/eza.nix:5"},{"name":"Caprine desktop integration","evidence":"modules/aspects/programs/communication/caprine.nix:12"},{"name":"Vesktop/Vencord native preset","evidence":"modules/aspects/programs/communication/vesktop/optional/config.nix:11"},{"name":"Zsh interactive preset","evidence":"modules/aspects/programs/shells/zsh.nix:6"},{"name":"Spotify desktop/player integration","evidence":"modules/aspects/programs/spotify.nix:12"},{"name":"Kitty terminal integration","evidence":"modules/aspects/programs/terminals/kitty.nix:14"},{"name":"GNOME Calendar account integration","evidence":"modules/aspects/programs/gnome-calendar.nix:5"},{"name":"PipeWire audio","evidence":"modules/aspects/services/audio.nix:6"},{"name":"CoolerControl managed-config integration","evidence":"modules/aspects/services/coolercontrol.nix:19"},{"name":"Greetd/Tuigreet session","evidence":"modules/aspects/services/display-managers/greetd.nix:6"},{"name":"Ly login preset","evidence":"modules/aspects/services/display-managers/ly.nix:9"},{"name":"GNOME keyring portal","evidence":"modules/aspects/services/keyrings/gnome-keyring.nix:6"},{"name":"Polkit session agent","evidence":"modules/aspects/services/polkits/polkit-gnome.nix:17"},{"name":"AMD CPU power policy","evidence":"modules/aspects/system/hardware/amdcpu.nix:8"},{"name":"AMD GPU tuning","evidence":"modules/aspects/system/hardware/amdgpu.nix:33"},{"name":"Nix garbage collection/optimization","evidence":"modules/aspects/system/garbage-collection.nix:4"},{"name":"KDE Connect desktop integration","evidence":"modules/aspects/services/kde-connect/kde-connect.nix:9"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: distinct non-host output contracts. Pros: custom Niri/Noctalia contribution classes have explicit routes (`modules/aspects/window-managers/niri/niri.nix:19`, `modules/aspects/window-managers/shells/noctalia/noctalia.nix:23`). Cons: both merely project into native HM app options; no distinct module system/output is evaluated (`modules/aspects/window-managers/niri/niri.nix:22`, `modules/aspects/window-managers/shells/noctalia/noctalia.nix:26`). X stays 2.

Total: **56.0/100**. Shortlists: showcase yes; library_units activeAspects schema; starter no. Showcase the real provenance-aware host network channel and persistence adapters; useful library material, but not a documented starter.

Overall pros:
- Host facts reach two actual consumers through a provenance-preserving policy (`modules/policies/network-backends.nix:16`, `modules/aspects/batteries/mount-cifs.nix:26`).
- Persistence adapters and effective-state inspection have real consumers (`modules/aspects/core/preservation/class/classes.nix:78`, `modules/aspects/core/preservation/pkgs/find-ephemeral.nix:24`).
- Twenty native app presets remain reusable after excluding fleet-dependent envelopes (`modules/aspects/programs/gnome-calendar.nix:5`, `modules/aspects/programs/terminals/kitty.nix:14`).

Overall cons / limits:
- CIFS takes the first backend without missing/duplicate diagnostics (`modules/aspects/batteries/mount-cifs.nix:26`).
- Shared user keys and checkout assumptions require second-consumer changes (`modules/aspects/services/ssh.nix:101`, `modules/aspects/programs/cli-tools/nh.nix:8`).
- README is purpose/example-only and no regression checks are declared (`readme.md:1`, `flake.nix:4`).

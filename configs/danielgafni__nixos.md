# danielgafni__nixos

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/danielgafni__nixos.md)

- Upstream: [danielgafni/nixos](https://github.com/danielgafni/nixos)
- Reviewed revision: [`26f03bc416ad`](https://github.com/danielgafni/nixos/commit/26f03bc416ad2535ff4cdf52a1d8cb9ead4b8fd6)
- Author: danielgafni
- Score: **50.5 / 100**, rank 48 of 103 ranked configs. D 5 · I 5 · S 4 · R 7 · P 7 · L 4 · V 5 · O 5 · B 5 · X 2. Shortlists: library units (1).
- Summary: D home-name table projection into native consumers cap5; I named features/broad base/global imports; S untyped data and actual second-user Git identity fallback plus13 grouped shared facts; R self-contained Colima A unit with real host consumer but no minimal independent example; P explicit OS-role selection plus both-platform outputs; L usage/layout docs; V representative output CI without boundary fixtures; O selected per-aspect secrets; B7 clean units/census8; X standard classes only.

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

Den hosts and standalone homes deliberately activate separately (`modules/den.nix:97`, `modules/den.nix:114`). Global host/user lookup tables inject personal data through home-name dispatch (`modules/den.nix:80`).

## 2. Common patterns

- homes (standalone HM) covers Linux and Darwin (`modules/den.nix:114`).
- custom schema disables automatic user HM class (`modules/den.nix:21`).

## 3. Novel patterns

The home name user@host is parsed into two lookup keys, then injected as HM options (`modules/den.nix:83`, `modules/den.nix:89`). This is explicit table dispatch rather than verified quirk collection.

## 4. Library candidates

**Colima Darwin service** · `modules/aspects/features/darwin/docker.nix:8`: Docker/Compose/Colima packages, primaryUser-derived socket and launch agent. Inputs: standard Darwin config/pkgs with primaryUser, no author data or fleet schema (`modules/aspects/features/darwin/docker.nix:15`). **A**: import the definition and include den.aspects.docker-mac; existing MacBook consumer demonstrates inclusion and native primaryUser (`modules/aspects/hosts/MacBook.nix:10`, `modules/aspects/hosts/MacBook.nix:17`). CPU/memory/disk are coherent preset policy, optional future parameters (`modules/aspects/features/darwin/docker.nix:18`).

## 5. den friction

Embedded HM projection is forcibly removed (`modules/den.nix:98`), and the source documents excluding Stylix HM because its overlay caused recursion (`modules/den.nix:28`).

## 6. Docs and complexity

Docs 4: README explains multi-host/Dendritic goals and CI cache rationale (`README.md:3`, `README.md:7`, `README.md:9`). Source explains standalone versus embedded HM choices (`modules/den.nix:97`). Complexity 5: custom home dispatch, host/user tables and dual OS environments (`modules/den.nix:80`, `modules/den.nix:101`).

## 6a. Defects and scoring notes

- S · moderate: actual underdel user data has email/fullName but no git subtree; shared Git therefore uses Daniel's hardcoded name/email rather than the second user's values (`modules/den.nix:237`, `modules/aspects/features/dev/git.nix:28`, `modules/aspects/features/shared-hm.nix:33`, `modules/den.nix:118`). Static selected-consumer mismatch; not evaluated.
- S · moderate: permissive attrs and unvalidated user@host parsing defer missing/shape errors to consumers; shared fallback/endpoint/path facts remain outside those tables (`modules/den.nix:10`, `modules/den.nix:83`, `modules/aspects/features/editors/zed.nix:73`, `modules/aspects/features/shell/default.nix:192`).
- O · moderate: initial creation of the privileged dan account uses a committed credential (reported privately; not located here); current runtime access is not inferred.
- Global definition/import bookkeeping is an ownership tradeoff, not independently demonstrated breakage (`modules/den.nix:31`, `modules/den.nix:125`).

## 7. Template notes

Useful reference for intentionally separate HM activation; context overrides and documented recursion workaround make it an advanced example (`modules/den.nix:28`, `modules/den.nix:98`).

## 8. Scorecard

### D (5, medium)
Scope: standalone home entity → user/host tables → native feature consumers. Pros: declared dan/underdel homes resolve their lookup keys; host display settings and shared keymap reach Hyprland and AeroSpace (`modules/den.nix:83`, `modules/den.nix:89`, `modules/den.nix:118`, `modules/aspects/features/linux/wayland/hyprland.nix:61`, `modules/aspects/features/darwin/aerospace.nix:98`). Cons: fixed-table/context projection has no independent quirk/policy routing or checked missing/duplicate semantics (`modules/den.nix:85`, `modules/den.nix:90`). Non-routing cap5; native package selection earns nothing. Confidence: medium.

### I (5, medium)
Scope: features, host/user variants and common imports. Pros: named aspects isolate most app/native resources and platform variants are explicit (`modules/aspects/features/darwin/docker.nix:2`, `modules/aspects/features/shared-hm.nix:40`). Cons: shared-hm and nixos-system remain broad platform bundles; global Den defaults import every third-party program module and custom data schema (`modules/aspects/features/shared-hm.nix:29`, `modules/aspects/features/nixos/system.nix:95`, `modules/den.nix:31`). Anchor5: readable concern ownership with broad baseline coupling; file count itself earns nothing. Confidence: medium.

### S (4, medium)
Scope: all visible shared native/feature bodies and actual table consumers. Pros: real host/user inventories centralize display/identity values (`modules/den.nix:125`, `modules/den.nix:207`). Cons: tables and my options are untyped attrs; underdel supplies flat email/fullName, but Git reads nested git.user fields and falls back to Daniel (§6a). Shared facts remain in fallback identity/GPG, personal cache, three checkout roots (nixos/dotfiles/nixpkgs), devbox hostname, four remote project roots, EC2 instance, weather and vault (`modules/den.nix:237`, `modules/aspects/features/dev/git.nix:28`, `modules/aspects/features/security/gpg.nix:9`, `modules/aspects/features/nixos/system.nix:20`, `modules/aspects/features/nixos/system.nix:295`, `modules/aspects/features/shell/default.nix:88`, `modules/aspects/features/shell/default.nix:91`, `modules/aspects/features/editors/zed.nix:73`, `modules/aspects/features/editors/zed.nix:75`, `modules/aspects/features/shell/default.nix:192`, `modules/aspects/features/linux/wayland/hyprpanel.nix:62`, `modules/aspects/features/linux/wayland/hyprland.nix:183`). Thirteen grouped changes, raw at least20; repeated Daniel identity and instance/region pairs count once, correctly scoped hardware/user variants are excluded. Contract4/coverage5 (11–30 cap), min4. Confidence: medium.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":13,"raw_leaks":20}}
```

### R (7, medium)
Scope: §4 Colima unit and other visible consumer contracts. Pros: Colima owns Docker/Compose/Colima packages, derives socket user from standard Darwin primaryUser, and owns the foreground launch agent; the actual MacBook includes it and supplies primaryUser (`modules/aspects/features/darwin/docker.nix:8`, `modules/aspects/features/darwin/docker.nix:15`, `modules/aspects/features/darwin/docker.nix:17`, `modules/aspects/hosts/MacBook.nix:10`, `modules/aspects/hosts/MacBook.nix:17`). Cons: no minimal independent consumer guide/export test, while many other features require fleet my.* data (`modules/aspects/features/editors/zed.nix:13`). Interpolation7: one substantial closed grade-A service beyond B5, below A-plus-minimal-independent-consumer9. Confidence: medium.

### P (7, medium)
Scope: Linux/Darwin standalone homes and intentionally separate OS activation. Pros: explicit user/platform variant lists select appropriate terminal packages, pinentry and native services; CI builds actual Linux/Darwin host/home outputs (`modules/aspects/features/shared-hm.nix:3`, `modules/aspects/features/shared-hm.nix:10`, `modules/aspects/features/shell/terminals.nix:45`, `modules/aspects/features/security/gpg.nix:35`, `.github/workflows/build.yml:50`, `.github/workflows/build.yml:61`, `.github/workflows/build.yml:95`). Cons: some boundaries remain manual role composition and no isolated unsupported-platform checks were found (`modules/den.nix:98`, `modules/aspects/users/linux/dan.nix:23`). Interpolation7 above manual-platform5 through actual clean variant selection and representative both-platform builds, below boundary-fixture9. Intentional separate activation is not itself a defect. Confidence: medium.

### L (4, medium)
Scope: README and architecture comments. Pros: README explains separate OS/home activation and concern directories; source explains why HM projection is disabled and Stylix excluded (`README.md:40`, `README.md:50`, `README.md:65`, `modules/den.nix:28`, `modules/den.nix:97`). Cons: no concrete add-host/add-user/table-shape walkthrough or independent aspect consumer example (`modules/den.nix:83`, `README.md:65`). Interpolation4 above operation-only2 through ownership explanation, below complete adaptation5. Confidence: medium.

### V (5, medium)
Scope: authored checks and CI invocation. Pros: pre-commit check is exported, and CI builds both Linux host outputs, Darwin and three standalone homes (`modules/dev.nix:7`, `.github/workflows/build.yml:24`, `.github/workflows/build.yml:50`, `.github/workflows/build.yml:61`, `.github/workflows/build.yml:95`). Cons: underdel home is absent from the build-home matrix; no authored assertions/fixtures for missing @, user-data shape or per-feature disabled/context cases (`modules/den.nix:118`, `.github/workflows/build.yml:67`). Anchor5 for traceable representative outputs, without claiming successful execution. Confidence: medium.

### O (5, medium)
Scope: selected secrets and maintenance. Pros: selected dan-linux includes a SOPS-emitting aspect with three actual secret definitions; Waystt consumes the API-key file (`modules/aspects/users/linux/dan.nix:29`, `modules/aspects/features/security/dan-sops/default.nix:7`, `modules/aspects/users/linux/dan.nix:53`). Cons: no Den-derived deploy/install fleet pipeline found, and account creation uses a committed credential (reported privately; not located here) (§6a); scheduled cleanup and manual nh activation add no second derived concern (`README.md:41`, `modules/aspects/features/nixos/system.nix:291`). Anchor5 for per-aspect secret emission. Confidence: medium.

### B (5, medium)
Scope: complete visible aspects/native app-module helpers and assets, not custom package files or each installed app. Pros: seven complete integration/preset units below; Helix owns its substantive TOML, Colima owns service/packages, and CommandShift/Waystt have explicit app-module parameter contracts (`modules/aspects/features/editors/helix.nix:5`, `modules/aspects/features/editors/helix-config.toml:3`, `modules/_packages/commandshift.nix:9`, `modules/_packages/waystt.nix:10`). Cons: exclude broad multi-app CLI/system/shell bodies, token leaves, personal GPG assets/Git fallback, external native Claude installation and my.*-dependent WM/editor/terminal features (`modules/aspects/features/shell/cli.nix:34`, `modules/aspects/features/dev/git.nix:28`, `modules/aspects/features/security/gpg.nix:9`, `modules/aspects/features/editors/claude-code/claude-code.nix:64`, `modules/aspects/features/linux/wayland/hyprland.nix:9`). App-specific helpers count with their package/feature closure; no ordinary package-file credit. Census8→diversity5; references7→5; B5. Confidence: medium.
```score-evidence
{"B":{"diversity_points":8.0,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"Colima Darwin service","evidence":"modules/aspects/features/darwin/docker.nix:8"},{"name":"CommandShift integration","evidence":"modules/_packages/commandshift.nix:24"},{"name":"Jankyborders","evidence":"modules/aspects/features/darwin/jankyborders.nix:4"},{"name":"Krewfile plugin preset","evidence":"modules/aspects/features/dev/krewfile.nix:8"},{"name":"Bluetooth audio","evidence":"modules/aspects/features/nixos/bluetooth.nix:4"},{"name":"Helix","evidence":"modules/aspects/features/editors/helix.nix:4"},{"name":"Waystt environment integration","evidence":"modules/_packages/waystt.nix:31"}]}}
```

### X (2, medium)
Scope: Den classes and imported editor/agent modules. Pros: same concern structure reaches native NixOS/Darwin/HM outputs (`modules/den.nix:101`, `modules/den.nix:114`). Cons: Nixvim is an ordinary HM module import, not a distinct Den target class; cloud/Kubernetes CLI packages are installation, not generated target configuration (`modules/den.nix:33`, `modules/aspects/users/dan.nix:57`). Baseline2. Confidence: medium.

Total: **50.5/100**. Shortlists: showcase no; library_units Colima Darwin service; starter no. Colima is a drop-in service reference with standard primaryUser input. No routed showcase; untyped table dispatch and a real second-user identity mismatch prevent a starter nomination.

Overall pros:
- Actual host/user data reaches display and identity consumers (`modules/den.nix:89`, `modules/aspects/features/linux/wayland/hyprland.nix:61`).
- Colima owns packages, socket and launch-agent lifecycle (`modules/aspects/features/darwin/docker.nix:8`, `modules/aspects/features/darwin/docker.nix:17`).
- CI covers real host/home outputs on both OS platforms (`.github/workflows/build.yml:50`, `.github/workflows/build.yml:61`, `.github/workflows/build.yml:95`).

Overall cons / limits:
- S: underdel Git falls back to Daniel despite separate user-data values (`modules/den.nix:237`, `modules/aspects/features/dev/git.nix:28`).
- S: shared feature bodies retain personal cache/checkout/cloud instance settings (`modules/aspects/features/nixos/system.nix:20`, `modules/aspects/features/nixos/system.nix:295`, `modules/aspects/features/shell/default.nix:192`).
- O: initial creation of the privileged account uses a committed credential (reported privately; not located here).
- V limit: second-user home is not in CI matrix (`modules/den.nix:118`, `.github/workflows/build.yml:67`).

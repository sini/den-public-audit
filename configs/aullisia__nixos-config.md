# aullisia__nixos-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/aullisia__nixos-config.md)

- Upstream: [aullisia/nixos-config](https://github.com/aullisia/nixos-config)
- Reviewed revision: [`233eb5e4cfaf`](https://github.com/aullisia/nixos-config/commit/233eb5e4cfaf27a454f3b27b5a496c7f7eb2f1e8)
- Author: aullisia
- Score: **46.0 / 100**, rank 67 of 103 ranked configs. D 5 · I 6 · S 5 · R 7 · P 3 · L 2 · V 4 · O 5 · B 5 · X 2. Shortlists: library units (3).
- Summary: Direct schema facts and inventory-derived NH helpers are useful, with closed terminal/editor/integration presets. Missing test-host prerequisites, personal shared settings and local bundle input limit portability; manual persistence tests and operation-only guidance give partial maintenance support.

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

Den and flake-file dendritic modules supply the module framework (`modules/den.nix:14`). Host inventory and feature aspects use shared HM defaults (`modules/hosts.nix:10`, `modules/den.nix:25`).

## 2. Common patterns

- mutual-provider is included for every user (`modules/den.nix:21`).
- den.default includes define-user, primary-user and user-shell (`modules/den.nix:45`).

## 3. Novel patterns

The shared default makes every user primary, a strong personal-machine policy rather than a neutral multi-user default (`modules/den.nix:49`).

## 4. Library candidates

- ghostty · `modules/programs/ghostty.nix:10` · **A**, standalone HM terminal preset with owned fallback palette; requires standard Den registration and ordinary HM/nixpkgs, optional Stylix colors, no author identity; adjust through native Ghostty settings (`modules/programs/ghostty.nix:6`, `modules/programs/ghostty.nix:31`).
- helix · `modules/programs/helix.nix:9` · **A**, HM editor with Nix LSP/formatter and cursor/UI preset; standard Den registration and ordinary HM/nixpkgs, optional theme data with an owned fallback; native settings/languages are the parameter surface (`modules/programs/helix.nix:44`, `modules/programs/helix.nix:57`).
- direnv · `modules/shell/direnv.nix:6` · **A**, NixOS Direnv/Nix-direnv integration; standard Den registration and ordinary nixpkgs/NixOS, native Direnv options, no extra assets or identity (`modules/shell/direnv.nix:10`, `modules/shell/direnv.nix:12`).

## 5. den friction

Den input is forced because flake-file contributes a conflicting mkDefault URL; the comment records the exact conflict (`modules/den.nix:10`, `modules/den.nix:13`).

## 6. Docs and complexity

Docs 2: no README found; source teaches battery purposes and a compatibility workaround (`modules/den.nix:10`, `modules/den.nix:46`). Complexity 3: multi-host inventory and cross-class features such as Flatpak (`modules/hosts.nix:10`, `modules/programs/flatpak.nix:6`, `modules/programs/flatpak.nix:22`).

## 6a. Defects and scoring notes

- **S · moderate:** eight grouped personal adaptations remain in shared policy, disk/display selectors, identity settings and checkout/bundle roots (`modules/system/boot.nix:24`, `modules/programs/nemo.nix:14`, `modules/programs/nemo.nix:29`, `modules/shell/zsh.nix:73`, `modules/desktop/niri/_parts/settings.nix:31`). The Helios local input is additionally unavailable and its generated/declaration/locked paths disagree; score visible source, not a reduced denominator (`flake.nix:12`, `modules/flake-inputs.nix:51`, `flake.lock:309`).
- **P · major:** registered test has an absent imported hardware file and is selected into a Niri configuration whose required host maps omit test (`modules/hosts/test/default.nix:32`, `modules/users/aul/aul.nix:8`, `modules/desktop/niri/_parts/settings.nix:90`). The installer can generate hardware later, but the committed output remains incomplete (`installer/03-validate.sh:84`).
- **I · minor:** enabling Tailscale also disables global and initrd network-online waits (`modules/programs/tailscale.nix:33`, `modules/programs/tailscale.nix:34`).
- **R · minor:** the Yazi preset dispatches to unprovided application executables, supplied by the personal profile rather than its own module (`modules/programs/yazi.nix:48`, `modules/programs/yazi.nix:56`, `modules/programs/yazi.nix:80`, `modules/users/aul/aul.nix:65`). Excluded from B_ref.
- **V · minor:** persistence canary inventories omit currently declared state, limiting the advertised round-trip coverage (`installer/test-impermanence.sh:37`, `installer/test-impermanence.sh:66`, `modules/system/impermanence.nix:135`, `modules/system/impermanence.nix:207`).
- Withdraw the earlier primary-user and forced-input deductions: all registered identities are aul, and mkForce resolves the documented URL collision; these are explicit policy/workaround boundaries, not verified current failures (`modules/hosts.nix:12`, `modules/den.nix:13`, `modules/den.nix:49`).

## 7. Template notes

Readable wiring comments help, but global primary-user policy and forced upstream URL should be reconsidered when copying (`modules/den.nix:49`, `modules/den.nix:13`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Host registrations emit timezone and user Git fields, read directly through Den context arguments by Locale/Git (`modules/hosts.nix:3`, `modules/hosts.nix:14`, `modules/system/locale.nix:4`, `modules/system/locale.nix:11`, `modules/shell/git.nix:4`, `modules/shell/git.nix:17`). This is the 5 schema/context anchor; no additional routed fact policy/pipe is verified. The theme interface is an ordinary native option graph, not Den routing (`modules/themes/_theme/options.nix:7`). Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: Named feature owners and host/user include lists localize application changes and keep hardware overrides on named hosts (`modules/users/aul/aul.nix:4`, `modules/hosts/auronix/default.nix:4`, `modules/programs/ghostty.nix:3`). Interpolate 6 above the named-feature baseline, capped at 6 by Tailscale disabling unrelated global/early-boot network waits (`modules/programs/tailscale.nix:33`). The global primary-user battery is an intentional single-identity policy, not a verified current defect (`modules/hosts.nix:12`, `modules/den.nix:49`). Score **6**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract design 5: Git identity/timezone vary through entity fields, and app theming has optional fallbacks, but shared modules still require source edits for personal facts (`modules/hosts.nix:3`, `modules/system/locale.nix:11`, `modules/programs/ghostty.nix:6`). Eight grouped adaptations: aul identity across browser/operator/persistence/polkit (`modules/programs/librewolf.nix:61`, `modules/programs/tailscale.nix:14`, `modules/system/impermanence.nix:166`, `modules/programs/nemo.nix:14`); b660 and auronix named boot policy, the latter also package selection (`modules/system/boot.nix:24`, `modules/system/boot.nix:25`, `modules/nix/overlays.nix:25`); checkout root (`modules/shell/zsh.nix:73`, `modules/system/impermanence.nix:176`); one Helios asset-root contract with conflicting source/lock locations (`flake.nix:12`, `modules/flake-inputs.nix:51`, `flake.lock:309`); one disk UUID and two serial-bearing monitor IDs (`modules/programs/nemo.nix:29`, `modules/desktop/niri/_parts/settings.nix:31`, `modules/desktop/niri/_parts/settings.nix:55`). At least 14 cited raw occurrences group to eight; coverage6 capped, S=min(5,6)=5. Named entity identity/hardware files and ordinary locale/vendor presets are excluded. The retained local bundle is unavailable here; its actual contents could move portability assessment, never justify null. Score **5**; confidence **low**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":8}}
```

### R

Scope · pros · cons/coverage: Ghostty and Helix are substantial identity-free modules with native settings and optional fallback palettes; Direnv owns the complete native integration (`modules/programs/ghostty.nix:10`, `modules/programs/helix.nix:44`, `modules/shell/direnv.nix:6`). Interpolate 7 above light adaptation because these are usable as written, below 9 because there is no minimal adopter example and several richer units depend on unowned prerequisites: Yazi openers expect other apps on PATH (`modules/programs/yazi.nix:48`, `modules/programs/yazi.nix:56`, `modules/programs/yazi.nix:80`). Personal include lists show actual use, not a minimal standalone contract (`modules/users/aul/aul.nix:4`). Score **7**; confidence **high**.

### P

Scope · pros · cons/coverage: The declared scope is three x86_64-linux NixOS hosts, with host-specific hardware kept separate (`modules/hosts.nix:10`, `modules/hosts/b660/default.nix:35`). Interpolate 3 below honest-narrow 5: the registered test host imports an absent hardware file, and its selected Niri user has no test entry in either required map (`modules/hosts/test/default.nix:32`, `modules/hosts.nix:12`, `modules/users/aul/aul.nix:8`, `modules/desktop/niri/_parts/settings.nix:90`, `modules/desktop/niri/_parts/settings.nix:94`). No evaluation was run; the assessment is static missing-path/explicit-throw evidence. Score **3**; confidence **medium**.

### L

Scope · pros · cons/coverage: Operation-only guidance is substantive: installer usage stages and password/bootstrap comments explain deployment prerequisites (`installer/install.sh:4`, `installer/install.sh:16`, `modules/users/aul/aul.nix:112`). Battery comments and theme docs give local navigation, but there is no repository README or composition/adopter guide (`modules/den.nix:46`, `modules/themes/_theme/options.nix:1`). This fits 2 rather than the 5 wiring tutorial anchor. Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: Manual recipes check actual persistence across reboot, including negative ephemeral canaries, and the installer can force a selected host’s toplevel (`installer/test-impermanence.sh:4`, `installer/test-impermanence.sh:157`, `installer/test-impermanence.sh:200`, `installer/03-validate.sh:307`). Interpolate 4 below 5 because the hand-maintained mirror already omits declared Tailscale persistence and newer user paths (`installer/test-impermanence.sh:37`, `installer/test-impermanence.sh:66`, `modules/system/impermanence.nix:135`, `modules/system/impermanence.nix:207`). No broad context/collision checks are verified and the only workflow is entirely commented out (`.github/workflows/main.yml:1`). No test execution is asserted. Score **4**; confidence **high**.

### O

Scope · pros · cons/coverage: NH packages are generated from the Den inventory (`modules/nh.nix:9`, `modules/nh.nix:12`). Exact pinned Den f1d16b… enumerates den.hosts/den.homes then renders NH commands from each entity’s class/intoAttr/name ([immutable helper](https://raw.githubusercontent.com/vic/den/f1d16b177de42088ede5ad911a39c7f068877a7f/nix/lib/nh.nix#L56); local pin `flake.lock:97`). This meets one derived operational concern at 5. The installer also reads source registrations to choose user/host, but relies on text parsing and manually mirrored persistence rather than a complete evaluated operational projection (`installer/lib.sh:192`, `installer/lib.sh:251`, `installer/test-impermanence.sh:15`). Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: Only ordinary NixOS/HM targets are driven by Den; WinBoat creates packages and host runtime configuration, not a separately evaluated guest class/output contract (`modules/den.nix:25`, `modules/programs/winboat.nix:31`, `modules/programs/winboat.nix:46`). Baseline 2; package wrapping is credited as packaging/reuse where warranted, not another target family. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census diversity is five substantive selected families: Zsh, Starship, Helix, VSCode and Niri, hence B_div3; native owners and the selected user include list show that scope (`modules/shell/zsh.nix:22`, `modules/shell/zsh.nix:102`, `modules/programs/helix.nix:9`, `modules/programs/vscode.nix:6`, `modules/users/aul/aul.nix:8`). Fourteen individually read complete units listed below establish B_ref7, so B=5. Fastfetch’s fallback icon is owned (`modules/shell/fastfetch.nix:9`); Unity’s desktop wrapper and Vesktop’s RPC daemon are owned integrations (`modules/programs/unity3d.nix:34`, `modules/programs/vesktop.nix:291`). Exclude identity-bearing LibreWolf/Nemo/Tailscale, bare enable/package leaves, Yazi’s unprovided opener apps, Spicetify’s missing local module import, and Stylix/Plasma/Zsh/Git/Lsd units needing globally supplied modules/custom packages/colors (`modules/programs/librewolf.nix:61`, `modules/programs/nemo.nix:14`, `modules/programs/yazi.nix:56`, `modules/den.nix:35`, `modules/desktop/stylix.nix:56`, `modules/shell/zsh.nix:19`). No partial app fragment or settings-only preset is counted. Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"ghostty","evidence":"modules/programs/ghostty.nix:10"},{"name":"helix","evidence":"modules/programs/helix.nix:9"},{"name":"direnv","evidence":"modules/shell/direnv.nix:6"},{"name":"heroic","evidence":"modules/gaming/heroic.nix:10"},{"name":"steam","evidence":"modules/gaming/steam.nix:9"},{"name":"mangohud","evidence":"modules/gaming/mangohud.nix:15"},{"name":"virt-manager","evidence":"modules/programs/virt-manager.nix:9"},{"name":"unity3d","evidence":"modules/programs/unity3d.nix:8"},{"name":"vesktop","evidence":"modules/programs/vesktop.nix:16"},{"name":"fastfetch","evidence":"modules/shell/fastfetch.nix:13"},{"name":"openrgb","evidence":"modules/hardware/openrgb.nix:47"},{"name":"audio","evidence":"modules/system/audio.nix:6"},{"name":"ssh","evidence":"modules/system/ssh.nix:5"},{"name":"nixsettings","evidence":"modules/nix/settings.nix:11"}]}}
```

**Total:** 46.0/100. **Shortlists:** showcase no; library ghostty, helix, direnv; starter no. Direct schema facts and inventory-derived NH helpers are useful, with closed terminal/editor/integration presets. Missing test-host prerequisites, personal shared settings and local bundle input limit portability; manual persistence tests and operation-only guidance give partial maintenance support.

Overall pros:
- Timezone and Git identity consume explicit entity facts (`modules/system/locale.nix:11`, `modules/shell/git.nix:17`).
- Ghostty and Helix own useful fallback presets (`modules/programs/ghostty.nix:31`, `modules/programs/helix.nix:44`).
- NH commands derive from Den inventory (`modules/nh.nix:12`).

Overall cons / scope limits:
- The committed test host imports missing hardware and lacks Niri map entries (`modules/hosts/test/default.nix:32`, `modules/desktop/niri/_parts/settings.nix:90`).
- A global input assumes an unavailable local bundle (`flake.nix:12`).
- Shared policy still selects personal identity and devices (`modules/programs/tailscale.nix:14`, `modules/programs/nemo.nix:29`).
- Manual persistence coverage can drift from the configuration (`installer/test-impermanence.sh:15`).

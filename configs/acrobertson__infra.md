# acrobertson__infra

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/acrobertson__infra.md)

- Upstream: [acrobertson/infra](https://github.com/acrobertson/infra)
- Reviewed revision: [`05a8582100fb`](https://github.com/acrobertson/infra/commit/05a8582100fb93d1de94b5119cc5dddc86f4ba45)
- Author: acrobertson
- Score: **46.0 / 100**, rank 67 of 103 ranked configs. D 3 · I 5 · S 4 · R 5 · P 9 · L 5 · V 6 · O 5 · B 3 · X 2. Shortlists: library units (1).
- Summary: Direct shared account facts and carefully guarded Darwin/WSL integrated homes; checks uninvoked, personal values remain in shared owners, app settings bundled and unseen external editor uncredited.

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

Den’s flake module uses a default user+HM class pairing (`modules/den.nix:8`, `modules/den.nix:14`). README explains automatic flake-parts imports and names Darwin/WSL hosts (`README.md:9`, `README.md:17`).

## 2. Common patterns

- define-user initializes the user (`modules/users/alecrobertson.nix:19`).
- custom schema/classes defaults user to both user and homeManager (`modules/den.nix:14`).

## 3. Novel patterns

Wiring explicitly documents how a host may opt out of integrated HM by selecting user only (`modules/den.nix:10`).

## 4. Library candidates

- **1password-shell-integration · B:** owns Darwin GUI plus CLI/plugin integration for gh; explicit input module and unfree battery (`modules/features/authentication.nix:5`, `modules/features/authentication.nix:12`, `modules/features/authentication.nix:24`). Isolate the unrelated optional sudo TouchID policy and expose plugin selection. Exact locked shell-plugins10c9ede3f5a39fe09da5ca8df8da12ae497c6ab6 [package/wrapper implementation](https://github.com/1Password/shell-plugins/blob/10c9ede3f5a39fe09da5ca8df8da12ae497c6ab6/nix/shell-plugins.nix#L133) installs CLI/plugin packages and shell wrappers; GUI is supplied by this aspect, not a missing companion.

## 5. den friction

Integrated HM needs an explicit unfree allowlist mirror: the author explains that the battery emits to the OS class in host-user context and the independently constructed home package set does not inherit it (`modules/features/darwin-home.nix:17`, `modules/hosts/hodor.nix:28`). Regression checks preserve this workaround (`modules/flake/checks.nix:100`); no evaluation failure asserted.

## 6. Docs and complexity

Docs 3: host table, layout and rebuild instructions are explicit (`README.md:5`, `README.md:13`, `README.md:27`). Complexity 3: Darwin and WSL targets share class wiring (`README.md:9`, `modules/den.nix:14`).

## 6a. Defects and scoring notes
- moderate · **S**: shared home/Darwin/Git owners repeat the personal account, signing key/GitHub identity and Windows profile path rather than consuming the existing userConfig contract (`modules/features/darwin-home.nix:14`, `modules/features/darwin-homebrew.nix:12`, `modules/features/git.nix:42`, `modules/features/git.nix:74`, `modules/features/git.nix:121`). Agent credential references also assume particular vault entries (`modules/features/development.nix:41`, `modules/features/development.nix:116`).
- minor · **I**: the two Darwin host owners duplicate account, input-device defaults and dock policy (`modules/hosts/pequod.nix:21`, `modules/hosts/dragula.nix:21`). Multi-app shell/terminal owners have broad change boundaries (`modules/features/shell.nix:17`, `modules/features/shell.nix:93`, `modules/features/terminal/default.nix:8`, `modules/features/terminal/default.nix:42`).
No class-opt-out or documented WSL terminal exception is charged as a defect (`modules/den.nix:10`, `modules/hosts/hodor.nix:41`).

## 7. Template notes

Good moderate cross-platform example with an explained HM opt-out (`modules/den.nix:10`).

## 8. Scorecard

### D (3, high)
Scope: Pros: the user aspect factors identity into a static record, injects it through native HM _module.args, and Git/home construction consume it (`modules/users/alecrobertson.nix:8`, `modules/users/alecrobertson.nix:33`, `modules/features/git.nix:106`). Cons: this is ordinary class-module argument factoring, not facts read from Den host/user entity attributes or a quirk/policy route. Three recognizes the explicit shared record above direct literal2, but it does not reach live Den entity-channel5. The previous5 conflated native _module.args with Den entity context; corrected after independent audit. Confidence: high.

### I (5, high)
Scope: Pros: named feature owners separate platform, authentication, shell and Git (`modules/users/alecrobertson.nix:18`, `modules/features/git.nix:4`). Cons: host policy is copied and shell/terminal owners cover several apps (§6a; `modules/hosts/dragula.nix:21`, `modules/features/terminal/default.nix:42`). Literal5 localizes most changes with some broad/repeated bundles. Confidence: high.

### S (4, low)
Scope: Pros: shared userConfig carries account/name/email (`modules/users/alecrobertson.nix:8`, `modules/features/git.nix:106`). Cons: four grouped adaptations escape it: Alec/GitHub/signing identity, Windows user-profile root, OpenCode agent vault entry and Claude vault entry (§6a; `modules/features/git.nix:42`, `modules/features/git.nix:74`, `modules/features/git.nix:121`, `modules/features/development.nix:41`, `modules/features/development.nix:116`). Repeated Darwin account references and signing identity group once; generic macOS app paths/vendor endpoints are not extra leaks. Contract4 below mostly explicit5; coverage6 for4groups; min4. Personal neovim-config input body is not inspected here (`flake.nix:39`): hidden variation could improve its own contract or add leaks, so score visible code with low confidence, never null. Confidence: low.
```score-evidence
{"S": {"contract_design": 4, "leak_coverage": 6, "distinct_leaks": 4}}
```

### R (5, low)
Scope: Pros: lightweight nh cleanup policy is independently importable (`modules/features/nix-tools.nix:4`). Cons: larger owners depend on userConfig, unstable overlay, external personal editor, or companion application bundles (`modules/features/git.nix:8`, `modules/features/development.nix:25`, `modules/features/terminal/default.nix:25`). Literal5 useful light-adaptation modules, without claiming a substantial grade-A exported app contract. Unseen personal editor might supply a reusable unit or additional coupling; it is uncredited, low confidence. Confidence: low.

### P (9, high)
Scope: Pros: Darwin-only files/services and WSL behavior are explicitly guarded (`modules/features/desktop/default.nix:34`, `modules/features/authentication.nix:29`, `modules/features/containers.nix:7`, `modules/hosts/hodor.nix:44`); positive/negative platform checks verify that WSL excludes Darwin assets and each Darwin home includes its intended environment (`modules/flake/checks.nix:37`, `modules/flake/checks.nix:65`). Cons/limit: only declared ARM Darwin and x86 WSL supported (`modules/flake/systems.nix:4`); no wider claim. Literal9 for implemented platform boundaries plus concrete fixtures, not number of platforms. Confidence: high.

### L (5, high)
Scope: Pros: README explains automatic imports, per-feature class ownership, host/user locations and rebuild route (`README.md:17`, `README.md:21`, `README.md:27`); class opt-out and cross-class workaround are explained in source (`modules/den.nix:10`, `modules/features/darwin-home.nix:17`). Cons: no fuller minimal second-user settings/feature tutorial (`README.md:42`). Literal5 wiring explanation, below composition/routing tutorial9. Confidence: high.

### V (6, high)
Scope: Pros: focused assertions cover integrated-home identity, absent Darwin leakage, per-host app selection and builder/tarball output boundaries (`modules/flake/checks.nix:21`, `modules/flake/checks.nix:37`, `modules/flake/checks.nix:81`, `modules/flake/checks.nix:91`). Cons: tracked inventory has no CI workflow invoking them; they are only exported checks (`modules/flake/checks.nix:110`). Explicit uninvoked-check cap6, no passing-status claim. Confidence: high.

### O (5, medium)
Scope: Pros: WSL install packaging reads the actual Den-instantiated Hodor configuration's system.build.tarballBuilder and exports that runnable operational artifact (`modules/flake/tarball.nix:6`, `modules/flake/tarball.nix:12`). This is the configuration output of the selected Den host, a single install/packaging concern, under the configuration-output ruling. Cons: fixed Darwin linux-builder enable/systems are not another derived inventory (`modules/features/platform-defaults.nix:34`); no derived secrets/deploy/bootstrap fleet inventory and the tarball is manually run (`modules/flake/tarball.nix:4`, `README.md:29`). Literal5 for the one derived host artifact, not generic builder/tool installation. Confidence: medium.

### X (2, high)
Scope: Pros: Darwin/WSL and HM classes are explicit (`modules/den.nix:14`, `modules/hosts/hodor.nix:8`). Cons: builder and tarball are operational outputs, not a distinct non-host Den class (`modules/flake/tarball.nix:12`). Baseline2; O is not counted twice. Confidence: high.

### B (3, low)
Scope: Census max-depth: Fish1 + Starship1 + Tmux1 + Nushell.5 + Neovim.5 + Zsh.5 =4.5→diversity3. One complete independently owned integration is counted→reference2; mean2.5 rounds up3. Pros: substantial actual shell/terminal settings are present (`modules/features/shell.nix:17`, `modules/features/terminal/default.nix:42`). Cons: shell/terminal/desktop are inseparable multi-app owners, Git has personal identity, nh cleanup is a thin enable/retention leaf (`modules/features/shell.nix:93`, `modules/features/git.nix:42`, `modules/features/nix-tools.nix:4`). External editor body unavailable to this pass could add complete units; visible reference count remains1, low confidence, not null. Confidence: low.
```score-evidence
{"B": {"diversity_points": 4.5, "diversity_grade": 3, "reference_grade": 2, "reference_units": [{"name":"1password-shell-integration","evidence":"modules/features/authentication.nix:12"}]}}
```

Total: **46.0/100**. Shortlists: showcase no; library_units 1password-shell-integration; starter no. Notable for concrete positive/negative integrated-home platform assertions and documented cross-class allowlist workaround, not a routed-data showcase.

Overall pros:
- Platform-specific state is explicitly guarded and checked (`modules/flake/checks.nix:37`).
- Account data already has a shared argument contract (`modules/users/alecrobertson.nix:33`).
- Cross-class allowlist workaround and opt-out are explained (`modules/features/darwin-home.nix:17`, `modules/den.nix:10`).

Overall cons / limits:
- Shared Git/platform fragments still assume personal account details (`modules/features/git.nix:121`, `modules/features/darwin-homebrew.nix:12`).
- Shell/terminal files bundle several application concerns (`modules/features/shell.nix:93`, `modules/features/terminal/default.nix:42`).
- Focused checks have no tracked CI invocation (`modules/flake/checks.nix:110`).

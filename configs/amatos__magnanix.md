# amatos__magnanix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/amatos__magnanix.md)

- Upstream: [amatos/magnanix](https://github.com/amatos/magnanix)
- Reviewed revision: [`7675475f0509`](https://github.com/amatos/magnanix/commit/7675475f050939b2606e5c4d0d0205c25ac18cfd)
- Author: amatos
- Score: **64.0 / 100**, rank 7 of 103 ranked configs. D 5 · I 8 · S 6 · R 5 · P 9 · L 9 · V 6 · O 6 · B 7 · X 2. Shortlists: starter, library units (1).
- Summary: Strong composition teaching, explicit OS boundaries and concrete failure tests; ordinary entity-derived settings constrain D, while author service defaults constrain S and project schemas constrain independent reuse.

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
Generated flake/import-tree organization is documented, with separate host files and shared den modules (`README.md:29`, `README.md:123`). A common base includes OS-specific and HM features together (`modules/den/base.nix:8`).

## 2. Common patterns
- den.default includes the base bundle (`modules/den/base.nix:57`).
- os-class: an explicit OS target sits beside darwin/nixos targets (`modules/den/base.nix:39`, `modules/den/base.nix:44`, `modules/den/base.nix:48`).

## 3. Novel patterns
Two architecture-specific hosts intentionally share one hostname and aspect, separating inventory identity from OS hostname (`README.md:22`). A single repoDir option centralizes writable checkout paths (`modules/den/repo-dir.nix:2`).

## 4. Library candidates
- repo-dir · `modules/den/repo-dir.nix:6` · HM option for the live checkout used by out-of-store links · inputs: HM, lib · parameterization: options magnanix.repoDir (`modules/den/repo-dir.nix:9`) · **B**, rename prefix and parameterize the fallback directory (`modules/den/repo-dir.nix:11`).

## 5. den friction
No verified den-specific friction in the base or checkout option; immutable account requirements are NixOS behavior, explicitly explained separately (`modules/den/base.nix:49`).

## 6. Docs and complexity
Docs **5**: platform semantics, hostname exceptions and module map are explained (`README.md:22`, `README.md:52`, `modules/den/base.nix:39`). Complexity **3**: a shared feature bundle spans OS classes with one overrideable checkout option (`modules/den/base.nix:8`, `modules/den/repo-dir.nix:9`).

## 6a. Defects and scoring notes

- **S · moderate:** six grouped author adaptations remain in shared application/operation code: domain, cache pair, mail identity, private network, APFS container, and encrypted common credential asset (`modules/packages/mail.nix:19`, `modules/packages/mail.nix:38`, `modules/packages/attic.nix:18`, `modules/packages/orbstack.nix:6`, `modules/packages/certbot.nix:121`).
No additional concrete functional defect verified. Non-9 routing/reuse/operations scores describe anchor coverage rather than extra charged defects.

## 7. Template notes
A clear cross-platform baseline example, especially the explanation of class-specific contributions and immutable-account prerequisites (`modules/den/base.nix:39`, `modules/den/base.nix:49`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Den host/user facts determine secret filenames (`modules/den/sops.nix:37`, `modules/den/sops.nix:51`), and user metadata determines Git identity (`modules/packages/git.nix:9`, `modules/packages/git.nix:25`). These are actual fact-derived settings at5, not routed policy/quirk channels. The theme usedBy accumulator is an HM option (`modules/den/dracula-pro.nix:44`), not a Den data-flow primitive. Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: Optional application aspects and explicit base inclusion separate fleet defaults from features (`modules/den/base.nix:8`, `README.md:148`); checkout and licensed theme configuration have centralized option contracts (`modules/den/repo-dir.nix:9`, `modules/den/dracula-pro.nix:23`). Eight interpolates toward9 for these clear boundaries; some native application presets remain coupled to project option schemas, such as Ghostty to magnanix.draculaPro (`modules/packages/ghostty.nix:27`). Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Checkout and theme paths are overrideable, with the latter opt-in and failed clone only warning (`modules/den/repo-dir.nix:9`, `modules/den/dracula-pro.nix:24`, `modules/den/dracula-pro.nix:69`), contract7. Six adaptation groups remain: matos domain/subdomains (`modules/packages/mail.nix:24`, `modules/packages/tailscale.nix:13`); cache URL/key (`modules/packages/attic.nix:12`, `modules/packages/attic.nix:18`); mail identity (`modules/packages/mail.nix:19`); private relay network (`modules/packages/mail.nix:38`); APFS disk3 container (`modules/packages/orbstack.nix:6`); author-encrypted common credential asset (`modules/packages/certbot.nix:121`, `secrets/common.yaml:13`). Raw hostname/domain references are grouped by one adaptation, not occurrences. Coverage6 cap gives min6; overrideable repoDir default is not charged as a leak. Score **6**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":6}}
```

### R

Scope · pros · cons/coverage: The checkout module exposes a documented HM option and one fallback directory (`modules/den/repo-dir.nix:5`, `modules/den/repo-dir.nix:9`), a light rename/parameterization5. Larger presets are useful but often consume the project theme/schema (`modules/packages/neovim.nix:23`, `modules/packages/ghostty.nix:27`); those dependencies prevent treating every leaf as an independent A library unit. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Shared baseline documents os/darwin/nixos selection and NixOS account prerequisites (`modules/den/base.nix:39`, `modules/den/base.nix:49`). Darwin and Linux application differences are implemented explicitly (`modules/packages/openssh.nix:7`, `modules/packages/openssh.nix:19`), with architecture-specific Linux test configurations/checks (`modules/hosts/nixostron.nix:40`, `modules/flake/outputs.nix:63`) and CI builds on both OS families (`.github/workflows/build.yml:70`, `.github/workflows/build.yml:121`). These satisfy clear boundaries/examples9 within the declared scope. Score **9**; confidence **high**.

### L

Scope · pros · cons/coverage: README teaches where to include a feature, distinguishes host and user delivery, and supplies minimal include examples (`README.md:148`, `README.md:162`, `README.md:165`, `README.md:171`). It documents metadata prerequisites and absent-key behavior (`README.md:179`, `README.md:193`) and separates Determinate platform settings (`README.md:204`). This is composition teaching9; its domain/secret examples still require adapting to another fleet. Score **9**; confidence **high**.

### V

Scope · pros · cons/coverage: CI builds actual Darwin/Linux OS outputs and the ARM devShell (`.github/workflows/build.yml:72`, `.github/workflows/build.yml:123`, `.github/workflows/build.yml:168`). Fastfetch executes focused wrapper tests inside package postBuild (`modules/packages/fastfetch/fastfetch.nix:34`), covering empty input, crashes, silent output and hangs (`modules/packages/fastfetch/test_fastfetch_wrapper.py:72`, `modules/packages/fastfetch/test_fastfetch_wrapper.py:152`, `modules/packages/fastfetch/test_fastfetch_wrapper.py:168`). Generated-flake consistency and nixostron checks are defined separately (`modules/flake/outputs.nix:58`) but no visible CI recipe invokes that checks set. 6 credits representative OS builds plus exercised native failure tests, not the full context/platform check coverage of anchor9. No checks were executed during this static audit. Score **6**; confidence **high**.

### O

Scope · pros · cons/coverage: NH wrappers derive from Den outputs (`modules/flake/outputs.nix:50`), and host/user secret defaults derive from entity names (`modules/den/sops.nix:37`, `modules/den/sops.nix:51`). Two real concerns support6, slightly above single-concern5. The CI target list is manually named (`.github/workflows/build.yml:70`, `.github/workflows/build.yml:121`); the evidence does not reach9 for deploy/install/builders all generated from one inventory. Score **6**; confidence **high**.

### X

Scope · pros · cons/coverage: Darwin, NixOS and embedded HM are ordinary host/home outputs (`modules/flake/outputs.nix:35`, `modules/den/home-manager.nix:23`); the disposable VM remains a NixOS host variant (`modules/hosts/nixostron.nix:118`). Baseline2; secret/NH operation generation is credited only under O. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Enabled selection-verified census contributes9points, diversity7. The 13 complete application units below include native Finder/clock/screenshot presets, installed browser integrations and tested Fastfetch. Helium is an include/cask bundle whose native bridge is supplied by another aspect, so it is excluded rather than counted alongside the 1Password unit (`modules/packages/browsers/helium.nix:4`, `modules/packages/1password/1password-for-helium.nix:18`). App Store/cask-only leaves are excluded (`modules/packages/appstore/acorn.nix:7`); token Nushell/Tealdeer/Zellij preferences are excluded (`modules/packages/nushell.nix:11`, `modules/packages/tealdeer.nix:7`, `modules/packages/zellij.nix:12`). Ghostty/Neovim/Zed require project option schemas (`modules/packages/ghostty.nix:27`, `modules/packages/neovim.nix:23`, `modules/packages/zed/zed.nix:29`); Git/GPG require the fleet metadata convention (`modules/packages/git.nix:9`, `modules/packages/gpg.nix:31`); OrbStack and Attic retain author hardware/endpoints (`modules/packages/orbstack.nix:6`, `modules/packages/attic.nix:6`). They are not counted as self-contained references. Reference7 and diversity7 yield B7. Score **7**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":9,"diversity_grade":7,"reference_grade":7,"reference_units":[{"name":"_1password","evidence":"modules/packages/1password/1password.nix:2"},{"name":"tui.atuin","evidence":"modules/packages/atuin.nix:2"},{"name":"browsers.firefox","evidence":"modules/packages/browsers/firefox.nix:2"},{"name":"browsers.zen","evidence":"modules/packages/browsers/zen.nix:10"},{"name":"claude","evidence":"modules/packages/claude.nix:2"},{"name":"darwin.controlCenter","evidence":"modules/packages/darwin/controlCenter.nix:2"},{"name":"darwin.finder","evidence":"modules/packages/darwin/finder.nix:2"},{"name":"darwin.menuExtraClock","evidence":"modules/packages/darwin/menuExtraClock.nix:2"},{"name":"darwin.screencapture","evidence":"modules/packages/darwin/screencapture.nix:2"},{"name":"tui.fastfetch","evidence":"modules/packages/fastfetch/fastfetch.nix:17"},{"name":"openssh","evidence":"modules/packages/openssh.nix:4"},{"name":"shell.starship","evidence":"modules/packages/shells/starship.nix:4"},{"name":"tui.zoxide","evidence":"modules/packages/zoxide.nix:2"}]}}
```

**Total:** 64.0/100. **Shortlists:** showcase no; library repo-dir; starter yes. Strong composition teaching, explicit OS boundaries and concrete failure tests; ordinary entity-derived settings constrain D, while author service defaults constrain S and project schemas constrain independent reuse.

Overall pros:
- Feature placement and host-to-user delivery are taught with examples (`README.md:148`, `README.md:165`).
- Secret paths derive from host and user identities (`modules/den/sops.nix:37`, `modules/den/sops.nix:51`).
- Native wrapper tests cover crashes and hangs (`modules/packages/fastfetch/test_fastfetch_wrapper.py:152`, `modules/packages/fastfetch/test_fastfetch_wrapper.py:168`).

Overall cons / scope limits:
- Shared mail configuration retains the author address/network (`modules/packages/mail.nix:19`, `modules/packages/mail.nix:38`).
- OrbStack volume setup selects disk3 (`modules/packages/orbstack.nix:6`).
- Larger editor presets require the project theme/checkout schema (`modules/packages/neovim.nix:23`, `modules/packages/zed/zed.nix:29`).
- CI builds representative OS outputs but does not invoke the separately defined checks set (`.github/workflows/build.yml:72`, `.github/workflows/build.yml:123`, `modules/flake/outputs.nix:58`).

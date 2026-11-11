# raphaelladinig/dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/raphaelladinig/dotfiles.md)

- Upstream: [raphaelladinig/dotfiles](https://github.com/raphaelladinig/dotfiles)
- Reviewed revision: [`f29658d31d04`](https://github.com/raphaelladinig/dotfiles/commit/f29658d31d046b1dc155bb57d00f8d7155a59a2d)
- Author: raphaelladinig
- Score: **53.0 / 100**, rank 37 of 103 ranked configs. D 5 · I 8 · S 8 · R 6 · P 5 · L 2 · V 8 · O 6 · B 3 · X 2. Shortlists: showcase, library units (1).
- Summary: Direct membership/config projection D5; ownership I8; typed guarded preferences S8/two adaptations; generic extraction R6; honest Darwin P5; brief docs L2; generated behavioral fixture suite V8; native lifecycle O6; ordinary target family X2.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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

Generated flake-parts/import-tree maps one Darwin host/user to explicitly named aspects ([`flake.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/flake.nix#L4), [`modules/hosts/default.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L3)). Cross-aspect options are centralized and gated by actual aspect membership ([`modules/defaults.nix:16`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L16)).


## 2. Common patterns.

- den.default includes: nix-settings and nixpkgs aspects ([`modules/defaults.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L3)).
- custom classes selection: users default to HM ([`modules/defaults.nix:43`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L43)).
- host-aspects: host/user aspect identities are overridden explicitly ([`modules/hosts/default.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L4)).


## 3. Novel patterns.

Cross-feature enable flags only remain effective while the corresponding HM aspect is included ([`modules/defaults.nix:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L20)). Typed application preferences are applied only if the target application is closed ([`modules/app-preferences.nix:84`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L84), [`modules/app-preferences.nix:138`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L138)).


## 4. Library candidates.

- app-preferences · [`modules/app-preferences.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L3) · typed macOS preference activation with running-app guard · nix-darwin/nixpkgs plus warning helper · options · B: bundle helper and document primaryUser requirement.


## 5. den friction.

Central cross-aspect flags explicitly solve option tests when another aspect is absent ([`modules/defaults.nix:24`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L24)); a concrete integration seam rather than quirk-based data routing.


## 6. Docs and complexity.

Docs 2: README states platform and fixed checkout expectation ([`README.md:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L3), [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)); implementation comments explain guarded membership and preference writes ([`modules/defaults.nix:24`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L24), [`modules/app-preferences.nix:61`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L61)). Complexity 4: one host with fine-grained editor aspects and custom typed activation ([`modules/defaults.nix:30`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L30), [`modules/app-preferences.nix:138`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L138)).


## 6a. Defects and scoring notes.

- S · moderate: reusable Git app embeds personal email/signing key, and root docs fix checkout root; two grouped adaptations ([`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3), [`modules/apps/git.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L4), [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)).
- L · minor: six-line README omits authoring/custom activation architecture route ([`README.md:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L3), [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)).
No additional verified defect in guarded application writes.

## 7. Template notes.

Useful activation-safety and aspect-membership examples; parameterize personal Git identity and checkout assumptions ([`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3), [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)).

## 8. Scorecard.

### D
Scope: membership-derived effective flags and app payload collection. Pros: each flag is masked by actual included aspect; core collects per-feature config files/parsers and writes effective feature table ([`modules/defaults.nix:16`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L16), [`modules/apps/neovim/default.nix:37`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L37), [`modules/apps/neovim/default.nix:65`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L65)). Cons: ordinary module option merging/direct context queries, no independent quirk/policy fact route verified ([`modules/defaults.nix:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L20)). Literal5 direct derivation cap. Score **5**; confidence **medium**.

### I
Scope: app owners, native helpers and personal entity. Pros: host/user aspects explicitly separate target identity from application includes; each editor contribution owns files ([`modules/hosts/default.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L4), [`modules/users/raphaelladinig.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/users/raphaelladinig.nix#L4), [`modules/apps/neovim/default.nix:42`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L42)). Cons: central flags require defaults helper envelope, and Git identity remains inside reusable app owner ([`modules/defaults.nix:27`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L27), [`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3)). Score8 strong ownership beyond5, below9 consistently entity-owned identity. Score **8**; confidence **medium**.

### S
Scope: owned typed preference interface and effective flags. Pros: preference domain/process/scalars typed, scalar types preserved during read/write, no write while app running; feature flags cannot outlive selection ([`modules/app-preferences.nix:107`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L107), [`modules/app-preferences.nix:26`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L26), [`modules/app-preferences.nix:84`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L84), [`modules/defaults.nix:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L20)). Contract8 beyond5 useful knobs toward9 explicit interface with error/type behavior, but no arbitrary-app/context fixture completeness claim. Cons: two adaptation groups: Git email/signing identity and checkout-root convention ([`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3), [`modules/apps/git.nix:4`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L4), [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)). Coverage8; min8. Score **8**; confidence **medium**.
```score-evidence
{"S":{"contract_design":8,"leak_coverage":8,"distinct_leaks":2}}
```

### R
Scope: generic app preferences and complete app owners. Pros: §4 preference constructor owns type/activation implementation and bundled warning helper; Fish and Lazygit own runtime integrations ([`modules/app-preferences.nix:11`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L11), [`modules/_lib/app-preferences-warning.nix:1`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/_lib/app-preferences-warning.nix#L1), [`modules/apps/fish/default.nix:37`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/fish/default.nix#L37), [`modules/apps/lazygit.nix:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/lazygit.nix#L6)). Cons: generic constructor is not exported as a polished external module; Nvim/Helium/KeePassXC depend on central dotfiles flags ([`modules/apps/neovim/default.nix:67`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L67), [`modules/apps/helium/default.nix:81`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/helium/default.nix#L81), [`modules/apps/keepassxc.nix:23`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/keepassxc.nix#L23)). Score6 beyond5 meaningful typed extraction, below9 standalone public API/examples. Score **6**; confidence **medium**.

### P
Scope: one ARM Darwin host and native account/application interfaces. Pros: source explicitly scopes native settings to Darwin and guards application process writes ([`modules/hosts/default.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L3), [`modules/app-preferences.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L3), [`modules/app-preferences.nix:85`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L85)). Cons: no non-Darwin target/claim or negative target fixture ([`README.md:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L3)). Literal5 honest narrow scope, no platform-count penalty. Score **5**; confidence **medium**.

### L
Scope: brief root docs and source comments. Pros: README states platform/path; comments explain cross-aspect enable semantics and existing-account shell limitation ([`README.md:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L3), [`modules/defaults.nix:24`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L24), [`modules/hosts/caelum.nix:18`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/caelum.nix#L18)). Cons: no worked adding-host/aspect/native-preference authoring route ([`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)). Score2 above1 unexplained URL-only source, below5 authoring orientation. Score **2**; confidence **medium**.

### V
Scope: actual activation/type/runtime regression suite. Pros: just check connects syntax/runtime/Python/editor checks to CI; tests extract actual generated preference shell and inject app-open/failure cases, KeePass tests use generated activation with partial-write failures ([`justfile:12`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/justfile#L12), [`.github/workflows/check.yml:31`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/.github/workflows/check.yml#L31), [`tests/test_app_preferences_types.py:55`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/tests/test_app_preferences_types.py#L55), [`tests/test_keepassxc_activation.py:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/tests/test_keepassxc_activation.py#L20), [`tests/test_keepassxc_activation.py:80`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/tests/test_keepassxc_activation.py#L80)). Cons: no verified negative fixture for every aspect-membership flag/context ([`modules/defaults.nix:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L20)). Score8 strong behavioral regression beyond5, below9 complete routing/contract-edge coverage; nothing run here. Score **8**; confidence **medium**.

### O
Scope: context-derived native activation lifecycle. Pros: app-preference map uses actual primary user and process-aware writes; host reconciles existing account shell from actual enabled Fish ([`modules/app-preferences.nix:138`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L138), [`modules/app-preferences.nix:144`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L144), [`modules/hosts/caelum.nix:21`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/caelum.nix#L21)). Cons: no inventory-derived deployment/recovery/secrets tooling; just defaults to one literal host ([`justfile:1`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/justfile#L1)). Score6 two concrete derived activation concerns beyond5, below9 fleet lifecycle. Score **6**; confidence **medium**.

### X
Scope: standard Darwin/HM plus app configuration helpers. Pros: native application preferences have owned module implementation ([`modules/app-preferences.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L3)). Cons: no distinct evaluated Den nonhost class/target; standard app activation remains OS/home ([`modules/hosts/default.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L3)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: five complete app-owner envelopes and selected census max-depth. Pros: Homebrew owns pins/taps/activation, Fish owns native config/tools, Lazygit owns Delta, Cmux owns palette/font include closure, Alcove explicitly includes generic preference helper and Homebrew ([`modules/homebrew.nix:13`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/homebrew.nix#L13), [`modules/apps/fish/default.nix:49`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/fish/default.nix#L49), [`modules/apps/lazygit.nix:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/lazygit.nix#L6), [`modules/apps/cmux.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/cmux.nix#L3), [`modules/apps/alcove.nix:24`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/alcove.nix#L24)). Cons: generic app-preferences is a constructor rather than another single-app unit; Git identity excluded; Neovim/Helium/KeePassXC require central fleet flags outside unit, so no silently extracted core counted ([`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3), [`modules/apps/neovim/default.nix:67`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L67), [`modules/apps/helium/default.nix:81`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/helium/default.nix#L81), [`modules/apps/keepassxc.nix:23`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/keepassxc.nix#L23)). Include-only template/profile and package bags excluded. Score **3**; confidence **medium**.
B_div: 2 points → 2; B_ref: 5 units → 4; half-up mean → 3.
```score-evidence
{"B":{"diversity_points":2,"diversity_grade":2,"reference_grade":4,"reference_units":[{"name":"homebrew","evidence":"modules/homebrew.nix:13"},{"name":"fish","evidence":"modules/apps/fish/default.nix:3"},{"name":"lazygit","evidence":"modules/apps/lazygit.nix:3"},{"name":"cmux","evidence":"modules/apps/cmux.nix:3"},{"name":"alcove","evidence":"modules/apps/alcove.nix:23"}]}}
```

Total: **53.0/100**. Shortlists: showcase true; library_units ['app-preferences']; starter false.

Overall pros:
- Flags reflect actual included aspects ([`modules/defaults.nix:20`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/defaults.nix#L20)).
- Typed native preferences preserve values and skip running apps ([`modules/app-preferences.nix:84`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L84)).
- Behavioral fixtures inspect generated activation and failures ([`tests/test_keepassxc_activation.py:80`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/tests/test_keepassxc_activation.py#L80)).

Overall cons / limits:
- Git identity is not entity-owned (§6a S; [`modules/apps/git.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/git.nix#L3)).
- Root authoring guidance is minimal (§6a L; [`README.md:6`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/README.md#L6)).
- Editor/browser units require shared flags envelope ([`modules/apps/neovim/default.nix:67`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/apps/neovim/default.nix#L67)).

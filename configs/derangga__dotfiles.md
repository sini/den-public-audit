# derangga__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/derangga__dotfiles.md)

- Upstream: [derangga/dotfiles](https://github.com/derangga/dotfiles)
- Reviewed revision: [`c43c24f8b7f7`](https://github.com/derangga/dotfiles/commit/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f)
- Author: derangga
- Score: **46.5 / 100**, rank 65 of 103 ranked configs. D 5 · I 5 · S 4 · R 5 · P 5 · L 7 · V 5 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: D shared host terminal/context reaches native consumers without routing; I native per-app files inside common user baseline; S small constructor contract but closed Git host map and fixed checkout/Chrome installation; R OmniWM B closure; P honest one-user aarch64-Darwin scope; L detailed real wiring guide; V both-host evaluation CI plus native watcher selfcheck; O manual activation; B4 complete app-file units/census7; X ordinary Darwin/HM.

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

Native evalModules exports Darwin configurations from Den (`flake.nix:40`). A mapAttrs host constructor centralizes per-machine user/terminal data and custom Darwin instantiation (`den.nix:31`, `den.nix:96`).

## 2. Common patterns

- define-user+primary-user live in the user aspect (`den.nix:103`).
- parametric aspect (fn args) injects host-specific HM arguments (`den.nix:62`).

## 3. Novel patterns

One terminal selector is threaded into host attributes, system builder and HM context (`den.nix:38`, `den.nix:40`, `den.nix:84`). No structured Den quirk route is verified.

## 4. Library candidates

**OmniWM writable preset** · `modules/omniwm/default.nix:13` · pinned native package + substantial workspace/keybindings + writable main/shell TOML activation. Inputs: standard HM config/lib/pkgs with OmniWM support; retain settings.nix and shell.nix (`modules/omniwm/default.nix:20`, `modules/omniwm/default.nix:32`). **B**: wrap as a named Den HM aspect or retain native module import; expose workspace/monitor policy if varied (`modules/omniwm/settings.nix:79`). No host identity/schema dependency.

## 5. den friction

Comments explain needing custom specialArgs and the input-name mismatch nix-darwin versus darwin (`den.nix:8`). Host construction duplicates context because instantiate cannot access its owning host (`den.nix:29`).

## 6. Docs and complexity

Docs 4: README diagrams Den/evalModules and explains adding hosts (`README.md:39`, `README.md:135`). Source documents integration constraints (`den.nix:8`, `den.nix:56`). Complexity 3: two Darwin hosts with shared terminal and account routing (`den.nix:96`).

## 6a. Defects and scoring notes

- S · moderate: README adds an arbitrary host but shared Git identity lookup is closed to maclop/worklop; the new target needs an extra table edit or fails when programs.git.settings.user is forced (`README.md:141`, `modules/git/default.nix:3`, `modules/git/default.nix:12`). Static consumer mismatch; not evaluated.
- S · minor: common rebuild abbreviation fixes the checkout root (`modules/default.nix:72`).
- R · moderate: Presenterm wires Mermaid rendering to an external Chrome path without owning its installation (`modules/presenterm/default.nix:22`, `darwin/homebrew/default.nix:17`).
- Constructor projections share one input source, and one-user-per-host is documented scope; neither is independently demonstrated breakage (`den.nix:31`, `den.nix:59`).

## 7. Template notes

Good migration case for Darwin integration constraints; the explicit one-user-per-host assumption limits generalization (`den.nix:59`).

## 8. Scorecard

### D (5, medium)
Scope: host constructor → native Darwin/HM consumers. Pros: terminal is one constructor value, stored on the host and passed to the builder/HM; Homebrew cask and HM program conditions both consume it (`den.nix:35`, `den.nix:38`, `den.nix:40`, `den.nix:84`, `darwin/terminal.nix:3`, `modules/terminal/ghostty.nix:7`). Cons: direct context/specialArgs propagation, without routed facts/quirks/policies. Non-routing cap5; duplicating projections of the same constructor value is not a second independent source of truth. Confidence: medium.

### I (5, medium)
Scope: Den account aspects and native per-app module imports. Pros: individual programs have app-specific module boundaries and actual user overrides span Darwin/HM (`modules/default.nix:9`, `den.nix:107`, `den.nix:123`). Cons: every user imports a broad common app/toolchain baseline, while feature selection remains mostly native module structure rather than named independent Den features (`den.nix:93`, `modules/default.nix:25`). Anchor5 for readable but coarse common ownership. Confidence: medium.

### S (4, medium)
Scope: constructor/user data and shared native modules. Pros: constructor accepts username/terminal, define-user owns account projection, and OmniWM resources derive from configHome (`den.nix:34`, `den.nix:103`, `modules/omniwm/default.nix:30`). Cons: shared Git only accepts two existing host identity records; new host from README therefore needs an undocumented table change. Rebuild abbreviation fixes ~/nix; Presenterm fixes an externally installed Chrome executable (`modules/git/default.nix:3`, `modules/git/default.nix:12`, `README.md:141`, `modules/default.nix:72`, `modules/presenterm/default.nix:22`). Four grouped changes: two host identity records, checkout root, Chrome installation; at least5 raw literals. Contract4 below5 because adding a constructor-supported host still breaks an implicit consumer; coverage6 (four-group cap), min4. Logical OmniWM workspace IDs are stable preset keys, not inferred machine identities (`modules/omniwm/settings.nix:68`). Confidence: medium.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":4,"raw_leaks":5}}
```

### R (5, medium)
Scope: §4 OmniWM native HM closure. Pros: module owns pinned package, generated main/shell TOML and writable installation at activation; settings contain a substantial complete workspace/keybinding preset (`modules/omniwm/default.nix:13`, `modules/omniwm/default.nix:31`, `modules/omniwm/default.nix:34`, `modules/omniwm/settings.nix:18`). Cons: retain all three files/native HM OmniWM support and decide whether to expose workspace/monitor policy; no independent exported consumer test (`modules/omniwm/default.nix:20`, `modules/omniwm/settings.nix:79`). Grade B anchor5 for a light-adaptation closure, without claiming a new module system. Confidence: medium.

### P (5, medium)
Scope: two declared aarch64-Darwin machines, each with one configured user. Pros: scope is explicit in host registry/platform and upstream binary wrappers reject unsupported systems (`den.nix:96`, `darwin/configuration.nix:58`, `modules/llm-agents/herdr-review.nix:21`). Cons: it is a native Darwin configuration rather than a wider portability contract, and one-user extraSpecialArgs is explicitly documented (`den.nix:59`). Anchor5 for honest narrow support. The documented one-user limit and builder argument restoration are not platform defects. Confidence: medium.

### L (7, medium)
Scope: README/source integration guidance. Pros: diagram shows evalModules→Den→Darwin/HM ownership; detailed host/user example explains constructor arguments, batteries and activation (`README.md:39`, `README.md:135`, `README.md:148`, `README.md:168`, `README.md:174`). Cons: no isolated app consumer tutorial or exact bounded-context test examples; manual adaptation still crosses the common native entry module (`modules/default.nix:9`). Interpolation7 above complete practical wiring5 through integration rationale/examples, below independent minimal/failure-oriented teaching9. The Git lookup mismatch is charged once to S. Confidence: medium.

### V (5, medium)
Scope: CI output checks and owned native watcher checks. Pros: CI evaluates both actual host outputs; Ghost build verifies shader substitution and runs canned watcher-state selfchecks, including unknown agent/status and missing focus (`.github/workflows/check.yml:21`, `modules/ghost/default.nix:44`, `modules/ghost/default.nix:58`, `modules/ghost/script/main.go:420`). Cons: CI evaluation does not build/run those native checks, and no authored added-host, terminal-switch or one-user boundary fixture was found (`.github/workflows/check.yml:23`, `den.nix:35`). Anchor5 for representative host evaluation plus authored integration checks; no execution/pass inferred. Confidence: medium.

### O (2, medium)
Scope: activation/rebuild/cleanup. Pros: native Darwin activation owns login-shell setup and scheduled Nix cleanup (`darwin/configuration.nix:26`, `darwin/configuration.nix:49`). Cons: deployment remains the manual rebuild abbreviation/README command; ordinary app activation hooks and the graphical agent watcher do not derive machine lifecycle targets from Den (`modules/default.nix:72`, `README.md:174`, `modules/ghost/default.nix:68`). Baseline2. Confidence: medium.

### B (5, medium)
Scope: complete visible native app-file closures reached by Den plus alternate definitions, not package names or individual editor plugins. Pros: four complete presets below; OmniWM owns settings/install behavior and terminals retain their common Darwin cask selector (`modules/omniwm/default.nix:34`, `darwin/terminal.nix:3`). Cons: exclude multi-app default/toolchain bodies, token btop/no-version toggles, Presenterm missing external Chrome, and integration fragments requiring outside app suites (Nixvim Rust/Xcode/agent tools; Ghost watcher Herdr; AeroSpace Sketchybar) (`modules/default.nix:54`, `modules/presenterm/default.nix:22`, `modules/nixvim/plugins/lsp.nix:60`, `modules/nixvim/plugins/ai.nix:18`, `modules/aerospace/default.nix:36`). Starship alternatives count once; own powerline preset is substantive (`modules/starship/powerline.nix:8`). Census7→diversity5; references4→4; half-up B5. Confidence: medium.
```score-evidence
{"B":{"diversity_points":7.0,"diversity_grade":5,"reference_grade":4,"reference_units":[{"name":"OmniWM writable preset","evidence":"modules/omniwm/default.nix:13"},{"name":"Ghostty terminal","evidence":"modules/terminal/ghostty.nix:8"},{"name":"Kitty terminal","evidence":"modules/terminal/kitty.nix:3"},{"name":"Starship powerline","evidence":"modules/starship/powerline.nix:4"}]}}
```

### X (2, medium)
Scope: native Darwin/HM modules and editor/shader/package helpers. Pros: substantial Nixvim/native shader work is actually imported (`modules/default.nix:18`, `modules/ghost/default.nix:42`). Cons: Nixvim remains an ordinary HM import, and helper derivations do not establish another Den target class (`modules/default.nix:11`, `den.nix:46`). Baseline2. Confidence: medium.

Total: **46.5/100**. Shortlists: showcase no; library_units OmniWM writable preset; starter no. OmniWM is a worthwhile library closure. No routed showcase; the otherwise useful host-adaptation guide misses a shared Git table requirement, so no starter nomination.

Overall pros:
- One constructor terminal value reaches both package and program selection (`den.nix:35`, `darwin/terminal.nix:3`, `modules/terminal/ghostty.nix:7`).
- OmniWM owns native writable-config installation (`modules/omniwm/default.nix:34`).
- Both real host outputs are checked in CI (`.github/workflows/check.yml:21`).
- README explains account batteries and constructor integration (`README.md:135`, `README.md:168`).

Overall cons / limits:
- S: documented new hosts are absent from the shared Git identity lookup (`modules/git/default.nix:3`, `README.md:141`).
- S: rebuild helper assumes a fixed checkout root (`modules/default.nix:72`).
- R: Presenterm Mermaid rendering assumes an external Chrome installation (`modules/presenterm/default.nix:22`).

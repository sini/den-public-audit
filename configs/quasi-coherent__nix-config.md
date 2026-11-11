# quasi-coherent__nix-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/quasi-coherent__nix-config.md)

- Upstream: [quasi-coherent/nix-config](https://github.com/quasi-coherent/nix-config)
- Reviewed revision: [`52971feef21f`](https://github.com/quasi-coherent/nix-config/commit/52971feef21f5769354ae2359dbc598d2623aab4)
- Author: quasi-coherent
- Score: **43.5 / 100**, rank 76 of 103 ranked configs. D 2 · I 9 · S 6 · R 5 · P 5 · L 1 · V 5 · O 5 · B 5 · X 2. Shortlists: —.
- Summary: D no selected routed facts; I clear namespace ownership; S typed instances with dropped field/three adaptations; R twelve independent files; P Darwin/home scope; L title only; V imported CI/lint; O NH wrappers; X no new class; B counted app owners.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

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

Namespaced a/our/my modules separate reusable features, shared opinion and personal topology (`modules/den.nix:8`). A Darwin host and standalone home are declared independently (`modules/my/configurations.nix:3`), with host features composing shared platform setup (`modules/my/hosts.nix:4`).


## 2. Common patterns.

- namespace: three roots have different visibility settings (`modules/den.nix:9`).
- homes (standalone HM): daniel@hemlock is explicit alongside the host user (`modules/my/configurations.nix:3`).
- mutual-provider: user schema includes the battery (`modules/den.nix:33`).
- forward: synthetic nixpkgs content is forwarded into the current class path (`modules/a/cls.nix:16`).


## 3. Novel patterns.

The a/our/my split distinguishes feature vocabulary from organization policy and personal entity data (`modules/den.nix:9`, `modules/my/configurations.nix:3`).


The overlay route remains unverified: nixpkgs-overlays is declared and consumed, while inspected language features set nixpkgs.overlays directly (`modules/den.nix:26`, `modules/our/home.nix:20`, `modules/a/development/language/rs.nix:37`). This earns no end-to-end dataflow credit and is not treated as a confirmed dead declaration.

## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

No verified den-specific defect in the inspected namespace and forwarding integration (`modules/den.nix:9`, `modules/a/cls.nix:16`).


## 6. Docs and complexity.

Docs 1: root readme only names the project (`readme.md:1`). Complexity 4: three namespaces, class forwarding, Darwin host and separate standalone home (`modules/den.nix:9`, `modules/a/cls.nix:16`, `modules/my/configurations.nix:3`).


## 6a. Defects and scoring notes.

- S · moderate: effortLevel option is declared and supplied by preset but absent from assembled settings, so selecting it cannot change emitted JSON (`modules/a/development/_claude/default.nix:56`, `modules/a/development/_claude/default.nix:143`, `modules/a/development/claude.nix:24`).
- S · minor: three shared adaptation groups remain, enumerated in S (`modules/our/nix-settings.nix:75`, `modules/our/darwin-system.nix:110`, `modules/a/applications/aerospace.nix:54`).
- R · minor: kgew alias contains a trailing unmatched quote (`modules/a/virtualization/k8s.nix:28`); Tmux native copy commands require unowned reattach-to-user-namespace (`modules/a/terminal/_files/tmux/tmux.common.conf:45`).
- L · moderate: title-only readme does not explain namespaces/authoring (`readme.md:1`).
Unverified overlay/forward chain remains no-credit coverage, not a confirmed dead declaration.

## 7. Template notes.

Worth studying for namespace boundaries and standalone homes, but a beginner needs explanatory documentation and a verified overlay route (`modules/den.nix:9`, `modules/our/home.nix:20`).

## 8. Scorecard.

### D
Scope: namespaces, selected direct settings and unused-looking forward declaration. Pros: personal host/user selections are explicit and ordinary inputs/self context drives packages (`modules/my/configurations.nix:3`, `modules/a/applications/spotify.nix:19`). Cons: package lookup/build plumbing earns no D credit; neither overlay quirk nor synthetic class forward has a verified selected producer→consumer chain (`modules/a/cls.nix:16`, `modules/den.nix:26`, `modules/our/home.nix:20`). Baseline2; no-emitter coverage observation is not a confirmed defect. Score **2**; confidence **medium**.

### I
Scope: vocabulary/organization/personal ownership. Pros: a/our/my namespaces separate reusable definitions, shared policy and identity; user composes those concerns (`modules/den.nix:9`, `modules/my/users.nix:14`, `modules/my/gitconfig.nix:18`). Cons: no additional concrete isolation defect verified. Literal9 ownership, not namespace count. Score **9**; confidence **medium**.

### S
Scope: Claude instance contract and shared defaults. Pros: typed multi-instance settings expose package/configDir, modes and environment, with generated wrapper/settings consumer (`modules/a/development/_claude/default.nix:28`, `modules/a/development/_claude/default.nix:166`, `modules/a/development/_claude/package.nix:13`). Contract6 beyond5 useful interface but effortLevel is declared/set yet omitted from serialized settings (`modules/a/development/_claude/default.nix:56`, `modules/a/development/_claude/default.nix:143`). Cons: three shared adaptation groups: author cache URL/key, household locale/timezone, Aerospace physical workspace-monitor topology (`modules/our/nix-settings.nix:75`, `modules/our/darwin-system.nix:36`, `modules/our/darwin-system.nix:110`, `modules/a/applications/aerospace.nix:54`). Personal my identity is intentionally entity-owned, excluded. Coverage8; min(6,8)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":6,"leak_coverage":8,"distinct_leaks":3}}
```

### R
Scope: independently owned nonidentity app presets. Pros: Zsh and SSH are complete coherent definitions; Claude constructor owns its wrapper (`modules/a/terminal/zsh.nix:6`, `modules/a/trusted/ssh.nix:5`, `modules/a/development/_claude/package.nix:8`). Cons: no §4 polished A/B nomination/consumer guide; Emacs depends on repository package outputs and native config, Tmux native commands need external helper (`modules/a/development/emacs.nix:49`, `modules/a/terminal/_files/tmux/tmux.common.conf:45`). Literal5 useful references, not9 packaged extraction. Score **5**; confidence **medium**.

### P
Scope: Darwin host plus explicit standalone HM target. Pros: both contexts declared; generic HM home directories have platform branch (`modules/my/configurations.nix:3`, `modules/our/home.nix:31`). Cons: no Linux managed target/boundary claim or negative-context tests (`modules/my/configurations.nix:4`). Literal5 honest scope, no platform-count bonus. Score **5**; confidence **medium**.

### L
Scope: root teaching material. Pros: source separates ownership clearly (`modules/den.nix:9`). Cons: readme contains only project name with no host/feature/context authoring route (`readme.md:1`). Literal1 root documentation absence; no source-namespace bonus. Score **1**; confidence **medium**.

### V
Scope: imported generated CI and linters. Pros: explicit _ci import enables workflow flake check, and perSystem enables deadnix/statix/typos (`nix/perSystem.nix:114`, `nix/_ci/workflows.nix:62`, `nix/perSystem.nix:58`, `nix/perSystem.nix:90`). Cons: no fixture for Claude option-to-JSON completeness or forward behavior (`modules/a/development/_claude/default.nix:143`). Literal5 structural checks, no run claimed. Score **5**; confidence **medium**.

### O
Scope: inventory-derived activation tools and builder integration. Pros: NH denPackages derives host/home wrappers exported and installed in devshell; host selects on-demand Linux builder (`nix/perSystem.nix:17`, `nix/perSystem.nix:51`, `nix/perSystem.nix:53`, `modules/our/linux-builder.nix:4`). Cons: builder is configured directly, secrets need existing runtime key, no generalized secret/deploy inventory (`modules/our/secrets.nix:25`). Literal5 useful derived activation, not9 fully automated fleet lifecycle. Score **5**; confidence **medium**.

### X
Scope: ordinary OS/HM plus developer package tools. Pros: custom Claude wrapper creates real packages (`modules/a/development/_claude/package.nix:8`). Cons: package plumbing and installed kubectl tools are not new evaluated Den target classes (`modules/a/virtualization/k8s.nix:6`); forward declaration alone earns no extension credit (`modules/a/cls.nix:16`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: all complete independent application owners and census enabled max-depth. Pros: listed app presets have multiple related settings or owned runtime integration; Claude includes full typed module/wrapper (`modules/a/development/claude.nix:18`, `modules/a/terminal/alacritty.nix:38`). Cons: enable/package-only leaves, language tool bags, Emacs repository package dependency, Tmux unowned reattach helper, k8s broken alias and physical Aerospace preset excluded (`modules/a/applications/obsidian.nix:14`, `modules/a/development/emacs.nix:49`, `modules/a/terminal/_files/tmux/tmux.common.conf:45`, `modules/a/virtualization/k8s.nix:28`, `modules/a/applications/aerospace.nix:54`). Git/Delta/JJ integrated VCS file counted once, not once per inner program. Score **5**; confidence **medium**.
B_div: 4 points → 3; B_ref: 12 units → 7; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":4,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"vesktop","evidence":"modules/a/applications/discord.nix:14"},{"name":"homebrew","evidence":"modules/a/applications/homebrew.nix:10"},{"name":"rectangle","evidence":"modules/a/applications/rectangle.nix:23"},{"name":"spicetify","evidence":"modules/a/applications/spotify.nix:22"},{"name":"claude","evidence":"modules/a/development/claude.nix:18"},{"name":"git-vcs","evidence":"modules/a/development/vcs.nix:20"},{"name":"starship","evidence":"modules/a/terminal/starship.nix:13"},{"name":"zsh","evidence":"modules/a/terminal/zsh.nix:6"},{"name":"ssh","evidence":"modules/a/trusted/ssh.nix:5"},{"name":"alacritty","evidence":"modules/a/terminal/alacritty.nix:7"},{"name":"stylix","evidence":"modules/our/theme.nix:13"},{"name":"docker-cli","evidence":"modules/a/virtualization/docker.nix:6"}]}}
```

Total: **43.5/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Clear reusable/shared/personal ownership (`modules/den.nix:9`).
- Typed multi-instance app constructor (`modules/a/development/_claude/default.nix:166`).
- Host/home wrappers follow inventory (`nix/perSystem.nix:17`).

Overall cons / limits:
- Declared effort setting is not serialized (§6a S; `modules/a/development/_claude/default.nix:143`).
- No root authoring docs (§6a L; `readme.md:1`).
- Some references need external helper closure (§6a R; `modules/a/terminal/_files/tmux/tmux.common.conf:45`).

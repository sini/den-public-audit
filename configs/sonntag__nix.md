# sonntag__nix

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/sonntag__nix.md)

- Upstream: [sonntag/nix](https://github.com/sonntag/nix)
- Reviewed revision: [`816947c6a270`](https://github.com/sonntag/nix/commit/816947c6a2707def93b5f5070e5420a6abac7bb1)
- Author: sonntag
- Score: **57.0 / 100**, rank 24 of 103 ranked configs. D 5 · I 6 · S 5 · R 5 · P 7 · L 8 · V 4 · O 7 · B 6 · X 2. Shortlists: library units (2).
- Summary: D direct target enumeration/context graph cap5; I coherent named integrations/custom playbook enable contract within broad personal/default ownership; S typed options plus four grouped installation assumptions; R Nixible/Kanata B closures; P explicit Darwin/Linux-home boundaries; L detailed setup/fork/enrollment docs; V one-host update CI without bridge tests; O actual per-Den-target playbooks and secrets setup with masked evaluation failure; B19 complete units/census7; X operational class only.

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

Den imports host and home outputs and an exported sonntag namespace (`modules/den.nix:6`). A custom nixible class extends host/user composition into imperative playbooks (`modules/den.nix:17`, `modules/nixible/playbooks.nix:42`).

## 2. Common patterns

- namespace explicitly exports reusable aspects (`modules/den.nix:11`).
- host-aspects follows the primary user (`modules/users/justin/default.nix:4`).

## 3. Novel patterns

A target enumerator resolves user/home entities and emits per-target Nixible apps (`modules/nixible/playbooks.nix:15`, `modules/nixible/playbooks.nix:87`).

## 4. Library candidates

- **nixible playbook bridge** · `modules/nixible/playbooks.nix:42` · Den entities → typed enabled playbook modules → per-target CLI. Inputs: Den, nixible, lib/pkgs; contract: declared dependencies/collections/playbook and target context (`modules/nixible/playbooks.nix:51`, `modules/nixible/playbooks.nix:80`). **B**: retain generic enumeration/manual host projection and register the user class (`modules/den.nix:17`).
- **Kanata Darwin integration** · `modules/services/kanata/default.nix:25` · driver, signed app, keyboard config, privileged/user launchd and diagnostics. Inputs: lib/pkgs plus owned kanata-app package/native helper/assets (`pkgs/kanata-app.nix:17`, `pkgs/kanata-app/setup.m:168`). **B**: package that closure, move den.default to a named aspect and expose the keyboard-config path (`modules/services/kanata/default.nix:274`); generic platform paths/signing identity are deliberate app resources.

## 5. den friction

A resolved user output lacks the parent host walk, so concrete host.aspect is appended explicitly (`modules/nixible/playbooks.nix:17`, `modules/nixible/playbooks.nix:23`).

## 6. Docs and complexity

Docs 4: README teaches bootstrap/setup (`README.md:3`, `README.md:20`), and bridge comments explain resolution limitations (`modules/nixible/playbooks.nix:17`). Complexity 5: custom class, evaluation and target-specific app generation (`modules/nixible/playbooks.nix:42`, `modules/nixible/playbooks.nix:67`).

## 6a. Defects and scoring notes

- O · moderate: run_nixible silently skips any app evaluation error, then setup records success; a malformed selected playbook can therefore leave imperative configuration unapplied without surfacing its evaluation failure (`scripts/nixctl:431`, `scripts/nixctl:467`). Static control-flow finding; not executed.
- S · moderate: shared wallpaper/auto-update/trusted-user, cache, repository and monitor assumptions encode installation facts (`modules/system/wallpaper.nix:34`, `modules/system/auto-update.nix:13`, `modules/nix.nix:14`, `modules/nix.nix:34`, `modules/nixible/nix-flake-checkout.nix:25`, `modules/services/aerospace/default.nix:41`).
- Documented explicit host.aspect projection is a workaround/adoption dependency, not independently demonstrated breakage (`modules/nixible/playbooks.nix:17`, `modules/nixible/playbooks.nix:23`).

## 7. Template notes

Strong advanced extension reference; the custom class and imperative tooling make it a demanding first example (`modules/nixible/playbooks.nix:49`).

## 8. Scorecard

### D (5, medium)
Scope: Den entity enumeration, resolution and graph consumers. Pros: host user/home entities determine playbook target names, systems and aspect chains; diagram capture consumes the actual resolved host context (`modules/nixible/playbooks.nix:12`, `modules/nixible/playbooks.nix:34`, `modules/flake/diagrams.nix:15`). Cons: these are direct registry traversal/context derivation, without policies/pipes or structured quirk routing; target attrs use listToAttrs without an authored collision check (`modules/nixible/playbooks.nix:87`). Non-routing cap5. Confidence: medium.

### I (6, medium)
Scope: named profiles/app integrations and default class ownership. Pros: MacWhisper owns package/license template; playbooks have typed independent enable flags, and a host can override one (`modules/programs/macwhisper/macwhisper.nix:3`, `modules/nixible/playbooks.nix:55`, `README.md:136`). Cons: many unrelated apps merge into justin/default, and the personal role includes several installation profiles (`modules/shell/helix.nix:2`, `modules/programs/homebrew/casks.nix:2`, `modules/profiles/personal.nix:4`). Interpolation6 above workable mixed ownership5 through real optional playbook/app boundaries, below narrow dependency ownership9. Confidence: medium.

### S (5, medium)
Scope: shared defaults, playbooks and personal/host boundaries. Pros: playbook enable/dependencies and wallpaper image are explicit contracts; fork/bootstrap has documented source overrides (`modules/nixible/playbooks.nix:55`, `modules/system/wallpaper.nix:10`, `README.md:58`). Cons: global trusted-user and wallpaper logs/auto-update fix justin, default automation fixes the repository, Nix fixes its personal cache, and AeroSpace fixes Dell/built-in monitor policy (`modules/nix.nix:14`, `modules/system/wallpaper.nix:34`, `modules/system/auto-update.nix:13`, `modules/nixible/nix-flake-checkout.nix:25`, `modules/nix.nix:34`, `modules/services/aerospace/default.nix:41`, `modules/services/aerospace/default.nix:185`). Four grouped changes: identity/home-root, repository origin, cache pair, monitor layout; raw at least10 literals. Correctly user-scoped Git/JJ identity and host dock paths are not additional leaks (`modules/shell/git.nix:2`, `modules/hosts/wrath/dock.nix:2`). Contract5/coverage6 (four-group cap), min5. Confidence: medium.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":4,"raw_leaks":10}}
```

### R (5, medium)
Scope: §4 Nixible and Kanata closures. Pros: bridge declares its own module/enable contract and combines declared dependencies; Kanata owns app packaging, launch services, driver/signing and recovery docs (`modules/nixible/playbooks.nix:51`, `modules/nixible/playbooks.nix:80`, `pkgs/kanata-app.nix:17`, `modules/services/kanata/README.md:26`). Cons: consumer must retain target enumeration/context projection and the nixible input, or package the Kanata app/assets and expose its keyboard config; no independent external consumer fixture (`modules/nixible/playbooks.nix:23`, `modules/services/kanata/default.nix:274`). Verified grade B anchor5. Confidence: medium.

### P (7, medium)
Scope: Darwin host, three standalone homes and exported Linux desktop definition. Pros: home instantiation supplies platform packages; Ghostty, SOPS paths and SSH keychain settings have explicit platform guards; nixctl rejects unsupported platforms (`modules/flake/homes.nix:15`, `modules/programs/ghostty/default.nix:10`, `modules/secrets/secrets.nix:17`, `modules/ssh/personal.nix:19`, `scripts/nixctl:55`). Cons: default Darwin platform remains fixed to aarch64 and CI only builds wrath; huginn is explicitly an exported consumer module, not a declared operational host (`modules/defaults.nix:20`, `.github/workflows/weekly-flake-update.yaml:46`, `README.md:53`). Interpolation7 for multiple implemented native boundaries, below checked independent boundary contracts9. Confidence: medium.

### L (8, medium)
Scope: README and Kanata operator guide. Pros: explains source overrides, target selection, secret enrollment stop/recovery, declarative-versus-imperative activation and permission/signing ownership (`README.md:58`, `README.md:99`, `README.md:126`, `modules/services/kanata/README.md:13`). Cons: a new generic user still needs to discover the justin-owned feature composition; no minimal independent bridge import example alongside the producer example (`modules/users/justin/default.nix:2`, `README.md:130`). Interpolation8: comprehensive actual failure/adaptation guidance beyond5, short of complete independent wiring9. Confidence: medium.

### V (4, medium)
Scope: update CI, scaffold validation and operational diagnostics. Pros: update jobs build the declared Darwin host before committing; new scaffolds validate an output, Kanata verifies signing, and enrollment checks decrypt the actual required secret (`.github/workflows/weekly-flake-update.yaml:68`, `scripts/nixctl:400`, `modules/services/kanata/default.nix:372`, `modules/flake/identities.nix:131`). Cons: no authored bridge merge/disable/collision or standalone-home consumer tests; CI covers wrath only (`.github/workflows/weekly-flake-update.yaml:46`). Interpolation4: meaningful output/operational checks above3, incomplete representative semantic coverage below5; no runtime pass claimed. Confidence: medium.

### O (7, medium)
Scope: derived target playbooks, selected secrets and setup lifecycle. Pros: enumerates Den host/users and homes, resolves and evaluates their nixible fragments, filters enable, builds matching-system apps, and setup executes the matching target after activation/enrollment (`modules/nixible/playbooks.nix:7`, `modules/nixible/playbooks.nix:29`, `modules/nixible/playbooks.nix:66`, `modules/nixible/playbooks.nix:76`, `scripts/nixctl:427`, `scripts/nixctl:461`). MacWhisper owns its secret/template and identities are local (`modules/programs/macwhisper/macwhisper.nix:17`, `modules/secrets/secrets.nix:16`). Cons: any app evaluation failure is silently handled like absence, after which setup writes completion (§6a); collection merge is implicit last-write-wins (`scripts/nixctl:431`, `scripts/nixctl:467`, `modules/nixible/playbooks.nix:81`). Interpolation7 for multiple real derived operational concerns above5, below robust checked enrollment/failure/merge semantics9. Fixed Comin remote is not an extra derived concern. Confidence: medium.

### B (6, medium)
Scope: all visible aspects, native theme/shader/keymap assets and package helper closure. Pros: 19 complete app presets/integrations below, including owned Kanata app/driver/signing and MacWhisper secret-to-plist wiring (`pkgs/kanata-app.nix:17`, `modules/services/kanata/default.nix:230`, `modules/programs/macwhisper/macwhisper.nix:22`). Cons: exclude bare packages, one fetched Bat theme, external NVim package, installer-only playbooks, include profiles and Fish fragments whose enablement comes from the broad user role (`modules/shell/bat.nix:5`, `modules/shell/nvim.nix:7`, `modules/users/justin/default.nix:7`). Git/JJ personal identities exclude both bodies from reference credit (`modules/shell/git.nix:7`, `modules/shell/jj.nix:12`). Count each app once; native color presets are fully authored settings rather than a single upstream theme preference (`modules/shell/starship/rose-pine.toml:26`). Census7→diversity5; 19 references→7; B6. Confidence: medium.
```score-evidence
{"B":{"diversity_points":7.0,"diversity_grade":5,"reference_grade":7,"reference_units":[{"name":"Atuin Fish integration","evidence":"modules/shell/atuin.nix:2"},{"name":"Difftastic Git integration","evidence":"modules/shell/difftastic.nix:2"},{"name":"Fzf","evidence":"modules/shell/fzf.nix:2"},{"name":"Tmux","evidence":"modules/shell/tmux.nix:3"},{"name":"Helix","evidence":"modules/shell/helix.nix:7"},{"name":"Lazygit","evidence":"modules/shell/lazygit.nix:3"},{"name":"Starship","evidence":"modules/shell/starship/default.nix:3"},{"name":"K9s","evidence":"modules/shell/k9s/k9s.nix:3"},{"name":"Zellij","evidence":"modules/shell/zellij/zellij.nix:3"},{"name":"Ghostty","evidence":"modules/programs/ghostty/default.nix:23"},{"name":"MacWhisper","evidence":"modules/programs/macwhisper/macwhisper.nix:17"},{"name":"Spotify Spicetify","evidence":"modules/programs/spotify.nix:20"},{"name":"VoiceInk","evidence":"modules/programs/voiceink.nix:5"},{"name":"AeroSpace","evidence":"modules/services/aerospace/default.nix:2"},{"name":"Hyprland","evidence":"modules/services/hyprland/default.nix:6"},{"name":"Kanata","evidence":"modules/services/kanata/default.nix:25"},{"name":"nix-homebrew","evidence":"modules/profiles/nix-homebrew.nix:5"},{"name":"SSH keychain client","evidence":"modules/ssh/personal.nix:7"},{"name":"wallpaper launch agent","evidence":"modules/system/wallpaper.nix:10"}]}}
```

### X (2, medium)
Scope: nixible custom class and generated diagrams. Pros: real custom-class resolution/evaluation feeds operational app generation (`modules/nixible/playbooks.nix:42`, `modules/nixible/playbooks.nix:67`). Cons: this class exclusively handles bootstrap/install/checkout lifecycle; coordinator ruling assigns that credit to O only. Diagrams are package/render outputs, not another distinct Den module-system target (`modules/flake/diagrams.nix:95`). Baseline2; original interpretation as an X extension is ruled out. Confidence: medium.

Total: **57.0/100**. Shortlists: showcase no; library_units nixible playbook bridge, Kanata Darwin integration; starter no. Two worthwhile B-grade library closures and strong operational teaching. Direct registry/context flow does not establish a routed showcase; broad personal defaults and advanced setup machinery make it unsuitable as a short starter.

Overall pros:
- Per-target playbooks derive from real Den entities (`modules/nixible/playbooks.nix:7`, `modules/nixible/playbooks.nix:29`).
- Enrollment boundary and recovery are explained concretely (`README.md:99`, `README.md:110`).
- Kanata owns driver/signing/service integration and diagnostics (`modules/services/kanata/default.nix:230`, `modules/services/kanata/README.md:83`).
- OS/HM-specific identity paths are explicit (`modules/secrets/secrets.nix:17`).

Overall cons / limits:
- O: failed app evaluation can be skipped and setup marked complete (`scripts/nixctl:431`, `scripts/nixctl:467`).
- S: global identity/cache/repository assumptions need consumer edits (`modules/nix.nix:14`, `modules/nix.nix:34`, `modules/nixible/nix-flake-checkout.nix:25`).
- V limit: update CI covers the Darwin host, not standalone homes or bridge boundaries (`.github/workflows/weekly-flake-update.yaml:46`).

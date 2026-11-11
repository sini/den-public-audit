# eugencowie__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/eugencowie__dotfiles.md)

- Upstream: [eugencowie/dotfiles](https://github.com/eugencowie/dotfiles)
- Reviewed revision: [`64dbfad5d9ca`](https://github.com/eugencowie/dotfiles/commit/64dbfad5d9ca500edd0043e51502172bac37d7d7)
- Author: eugencowie
- Score: **44.5 / 100**, rank 72 of 103 ranked configs. D 5 · I 6 · S 5 · R 5 · P 7 · L 3 · V 3 · O 2 · B 4 · X 2. Shortlists: library units (1).
- Summary: D user-context service projection; I feature ownership capped by global license side effects; S explicit Git/context contracts with fixed remote/MCP installation facts; R Git/Meld B unit; P portable class branches; L generation guide only; V static lint plus check recipe; O manual activation; B complete presets and integrations; X ordinary packages/HM.

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

Den’s dendritic module and flake-file centralize class/default setup (`modules/den.nix:22`, `README.md:7`). User aspects select nested feature provides across Darwin and Linux/WSL hosts (`modules/users/eugen.nix:4`, `modules/hosts/inspiron-16.nix:4`).

## 2. Common patterns

- den.default includes hostname and define-user (`modules/den.nix:25`).
- parametric aspect (fn args) configures Git identity (`modules/aspects/vcs/git.nix:3`).

## 3. Novel patterns

Git bundles a Meld merge tool and git-absorb while leaving identity at each call site (`modules/aspects/vcs/git.nix:6`, `modules/users/eugen.nix:25`).

## 4. Library candidates

- vcs.git · `modules/aspects/vcs/git.nix:3` · enables Git, identity, Meld merge and git-absorb · inputs: nixpkgs plus local diff._.meld aspect, Den · parameterization: fn args name/email · B; package the Meld companion too.

## 5. den friction

No verified Den-specific friction in the reviewed defaults (`modules/den.nix:25`).

## 6. Docs and complexity

Docs 3: README explains generated flake/input ownership (`README.md:7`); source comments explain state-version policy (`modules/den.nix:34`). Complexity 3: multiple users and Darwin/WSL targets (`modules/users/echo.nix:4`, `modules/hosts/macbook-air-m1.nix:13`, `modules/hosts/inspiron-16.nix:4`).

## 6a. Defects and scoring notes

- I · moderate: selecting Claude globally permits unfree packages, extending the feature into unrelated host package policy (`modules/aspects/ai/claude.nix:8`).
- S · moderate: shared Sunshine/MCP aspects fix operator endpoint, display/NIC policy and a connection UUID rather than taking consumer variation (`modules/aspects/remote/sunshine.nix:13`, `modules/aspects/remote/sunshine.nix:27`, `modules/aspects/remote/sunshine.nix:48`, `modules/aspects/ai/agent-mcps.nix:9`).
- Git/Meld companion ownership remains an explicit extraction dependency, not another defect (`modules/aspects/vcs/git.nix:6`).

## 7. Template notes

Useful parametric feature example; avoid copying generated flake directly (`README.md:7`).

## 8. Scorecard

### D (5, medium)
Scope: user/host contexts and generated service consumers. Pros: declared user context (`modules/users/echo.nix:41`) drives T3 runtime User, operator selection and the integrated HM package path (`modules/aspects/ai/t3code.nix:9`, `modules/aspects/ai/t3code.nix:26`, `modules/aspects/ai/t3code.nix:42`). Cons: direct context access has no quirk/policy route or collision protocol. The explicit non-quirk cap gives 5; ordinary input-package selection earns nothing. Confidence: medium.

### I (6, medium)
Scope: complete feature/provides tree and user/host assemblies. Pros: independent named owners and parametric Git separate identity from feature logic (`modules/aspects/vcs/git.nix:3`, `modules/users/eugen.nix:25`). Cons: enabling Claude also globally permits unfree packages (§6a, `modules/aspects/ai/claude.nix:8`). Interpolation/ruling: otherwise strong optional boundaries exceed 5, but unrelated global policy caps I at 6. Confidence: medium.

### S (5, medium)
Scope: all shared feature bodies and literal/context variation. Pros: Git name/email are real arguments and user/host facts derive service/scheduling variants (`modules/aspects/vcs/git.nix:3`, `modules/aspects/nix/gc.nix:10`). Cons: Sunshine fixes a LAN endpoint, NIC and display-mode assumptions; MCP fixes an account-specific connection (§6a, `modules/aspects/remote/sunshine.nix:13`, `modules/aspects/remote/sunshine.nix:27`, `modules/aspects/remote/sunshine.nix:48`, `modules/aspects/ai/agent-mcps.nix:9`). Four grouped installation changes, raw ≥5 literals; repeated display modes share one display-policy group. Contract5: identity/context variation is real, but the shared remote/MCP installation settings lack consumer contracts. The previous interpolation6 overstated that coverage. Coverage6; min(5,6)=5. Confidence: medium.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":4}}
```

### R (5, medium)
Scope: §4 Git/Meld integration and consumer call sites. Pros: identity is supplied at the consumer and Meld/git-absorb ship with the feature (`modules/aspects/vcs/git.nix:6`, `modules/aspects/vcs/git.nix:17`, `modules/users/eugen.nix:25`). Cons: adoption must take the local Meld companion and namespace registration; there is no substantial independently exported A-unit tutorial. Anchor 5 for the verified grade B, without recharging S constants elsewhere. Confidence: medium.

### P (7, medium)
Scope: real Darwin, WSL and NixOS declarations plus shared feature boundaries. Pros: GC distinguishes platform schedules, Stylix imports by host.class and Ghostty selects its Darwin package (`modules/aspects/nix/gc.nix:10`, `modules/aspects/theme/stylix.nix:13`, `modules/aspects/term/ghostty.nix:14`). Cons: no authored cross-platform boundary fixtures found; Linux-heavy GPU/ComfyUI stay consumer-selected (`modules/users/echo.nix:42`). Interpolation 7: explicit multiple-platform ownership beyond manual-exception 5, below checked boundaries 9. Confidence: medium.

### L (3, medium)
Scope: README, Den comments and mise tasks. Pros: generated flake/input ownership and regeneration are explained (`README.md:7`, `README.md:9`); user class/state-version policy is commented (`modules/den.nix:28`). Cons: README ends after regeneration rather than showing host/user/feature adaptation (`README.md:12`). Interpolation 3 above operations-only 2 through useful ownership explanation, below a complete wiring path 5. Confidence: medium.

### V (3, medium)
Scope: lint workflow and task recipes. Pros: CI invokes deadnix/workflow/shell lint, and a check task regenerates then invokes flake check (`.github/workflows/lint.yml:32`, `mise.toml:3`, `mise.toml:14`). Cons: no authored enabled/disabled/context/consumer assertions found; CI itself runs lint only (`.github/workflows/lint.yml:31`). Interpolation 3 for the check recipe above absent intent 2, below representative semantic CI 5; no pass inferred. Confidence: medium.

### O (2, medium)
Scope: apply/maintenance/service setup. Pros: activation recipe distinguishes OS rebuild commands (`mise.toml:35`). Cons: it chooses from uname rather than deriving deployment/provisioning targets from Den; service package ownership and local GC do not create a fleet operational pipeline (`mise.toml:39`, `modules/aspects/nix/gc.nix:6`). Baseline 2 for manual personal deployment; runtime application services are not relabeled as machine orchestration. Confidence: medium.

### B (4, medium)
Scope: all visible aspects, including unselected definitions and helper dependencies. Pros: ten coherent complete units are listed below; Mise wires toolchain/OpenSSL/nix-ld and T3 couples a real user-context service with Tailscale (`modules/aspects/env/mise.nix:26`, `modules/aspects/ai/t3code.nix:31`). Cons: token toggles, bare packages, default editor descriptors and cosmetic GNOME preferences are excluded; agent consumers inherit the personal MCP endpoint, and Sunshine has installation constants (`modules/aspects/desktop/gnome.nix:16`, `modules/aspects/ai/agent-mcps.nix:9`, `modules/aspects/remote/sunshine.nix:13`). Census maximum-depth 5→diversity 3; ten references→5; B4. Confidence: medium.
```score-evidence
{"B":{"diversity_points":5.0,"diversity_grade":3,"reference_grade":5,"reference_units":[{"name":"vcs.git","evidence":"modules/aspects/vcs/git.nix:3"},{"name":"gc-maintenance","evidence":"modules/aspects/nix/gc.nix:6"},{"name":"mise-toolchain","evidence":"modules/aspects/env/mise.nix:11"},{"name":"comfyui","evidence":"modules/aspects/ai/comfyui.nix:15"},{"name":"t3code-service","evidence":"modules/aspects/ai/t3code.nix:34"},{"name":"ghostty","evidence":"modules/aspects/term/ghostty.nix:11"},{"name":"zsh","evidence":"modules/aspects/shell/zsh.nix:6"},{"name":"stylix","evidence":"modules/aspects/theme/stylix.nix:13"},{"name":"pipewire","evidence":"modules/aspects/sound/pipewire.nix:6"},{"name":"nvidia","evidence":"modules/aspects/gpu/nvidia.nix:6"}]}}
```

### X (2, medium)
Scope: Den classes and editor/agent imports. Pros: ordinary OS/HM boundaries and third-party modules are explicit (`modules/den.nix:22`, `modules/aspects/editor/lazyvim.nix:11`). Cons: LazyVim remains an ordinary HM module, not its own Den target class; input package selection is build plumbing (`modules/aspects/ai/t3code.nix:10`). Baseline 2. Confidence: medium.

Total: **44.5/100**. Shortlists: showcase no; library_units vcs.git; starter no. Git/Meld is a useful parameterized library unit. No routed multi-consumer showcase or short complete starter path; custom program data and services remain source-level intermediate material.

Overall pros:
- Git identity is supplied at its call site (`modules/users/eugen.nix:25`).
- User context consistently determines T3 service identity (`modules/aspects/ai/t3code.nix:42`).
- GC and terminal implementation distinguish Darwin/Linux explicitly (`modules/aspects/nix/gc.nix:10`, `modules/aspects/term/ghostty.nix:14`).

Overall cons / limits:
- I: one AI feature changes global unfree policy (`modules/aspects/ai/claude.nix:8`).
- S: remote-desktop feature fixes LAN/display/device details (`modules/aspects/remote/sunshine.nix:13`, `modules/aspects/remote/sunshine.nix:48`).
- S: shared MCP carries a fixed connection identifier (`modules/aspects/ai/agent-mcps.nix:9`).

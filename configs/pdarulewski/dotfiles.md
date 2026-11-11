# pdarulewski/dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/pdarulewski/dotfiles.md)

- Upstream: [pdarulewski/dotfiles](https://github.com/pdarulewski/dotfiles)
- Reviewed revision: [`97a47bb048ad`](https://github.com/pdarulewski/dotfiles/commit/97a47bb048adbc576160d1ee04de55698a0064a0)
- Author: pdarulewski
- Score: **31.0 / 100**, rank 101 of 103 ranked configs. D 2 · I 6 · S 3 · R 5 · P 3 · L 2 · V 2 · O 2 · B 4 · X 2. Shortlists: library units (1).
- Summary: D direct settings; I mutable CLI side effect caps6; S source-edit identity contract; R independent leaf; P incomplete Linux envelope; L placeholder; V no semantic checks; O manual switch; X standard classes; B census and seven complete application references.

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

Den is evaluated through nixpkgs evalModules and import-tree; conventional output constructors then consume each den host mainModule ([`flake.nix:38`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L38), [`flake.nix:77`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L77)). Shared features cover two Darwin architectures and a Linux host ([`flake.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L44)).


## 2. Common patterns.

- host-aspect selection: each Darwin host includes hostname and shared Darwin/font/Homebrew features ([`modules/hosts/akari/default.nix:5`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/akari/default.nix#L5)).
- os-class: fonts are expressed once through the os class ([`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2)).
- den.default includes/state: HM classes and stateVersion are shared centrally ([`modules/den.nix:8`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/den.nix#L8)).


## 3. Novel patterns.

Manual output wrapping retains conventional darwinSystem/nixosSystem entrypoints around den mainModule ([`flake.nix:78`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L78), [`flake.nix:92`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L92)); useful when migrating an existing flake.


## 4. Library candidates.

- fonts · [`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2) · cross-OS font package set · nixpkgs · none · A: small self-contained os-class feature.


## 5. den friction.

Manual output plumbing repeats host wiring instead of using generated outputs ([`flake.nix:77`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L77)); migration signal, with no explicit den complaint verified.


## 6. Docs and complexity.

Docs 1: root README is only a title and image ([`README.md:1`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/README.md#L1)). Complexity 3: three architecture-specific entities and manual output composition share feature aspects ([`flake.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L44), [`modules/hosts/akari/default.nix:5`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/akari/default.nix#L5)).


## 6a. Defects and scoring notes.

- L · moderate: README title/image provides no entry-to-feature or new-host instructions ([`README.md:1`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/README.md#L1)).
- I · minor: broad CLI package bundle also creates mutable vault directories and bookmarks state ([`modules/features/cli.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L44), [`modules/features/cli.nix:49`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L49)); I cap6 applies.
- S · moderate: shared Git/GitHub/Darwin settings inline the author/account identity group; shared Linux timezone is a second group ([`modules/features/git/default.nix:73`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/git/default.nix#L73), [`modules/features/gh/default.nix:16`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/gh/default.nix#L16), [`modules/darwin/darwin.nix:9`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/darwin/darwin.nix#L9), [`modules/nixos/configuration.nix:11`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/configuration.nix#L11)).
- P · moderate: selected Linux NixOS settings lack the nixos class envelope; Ghostty also relies on Darwin-only installation outside its shared unit ([`modules/nixos/configuration.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/configuration.nix#L2), [`modules/nixos/hardware-configuration.nix:6`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/hardware-configuration.nix#L6), [`modules/features/ghostty/default.nix:10`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/ghostty/default.nix#L10)).
Manual output constructors are an explicit migration choice, not independently a defect; former blanket duplication deduction removed.

## 7. Template notes.

Teaches incremental adoption and os-class reuse, but a beginner must already understand evalModules and platform output constructors ([`flake.nix:38`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L38), [`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2)).

## 8. Scorecard.

### D
Scope: user/host feature selection and output constructors. Pros: named user context chooses a reusable feature bundle ([`modules/users/pd.nix:8`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/users/pd.nix#L8)). Cons: inspected feature bodies directly set application options, without a shared fact channel or policy-routed consumer ([`modules/features/atuin/default.nix:3`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/atuin/default.nix#L3)); manual mainModule wrapping is construction, not data flow ([`flake.nix:78`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L78)). Literal 2, not a correctness judgment. Score **2**; confidence **medium**.

### I
Scope: feature owners, CLI bundle and platform assembly. Pros: named application units localize changes ([`modules/features/atuin/default.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/atuin/default.nix#L2), [`modules/features/features.nix:6`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/features.nix#L6)). Cons: broad CLI installation also creates mutable vault directories and publishes a bookmarks path ([`modules/features/cli.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L44)). Calibration cap 6 for unrelated mutable state in a shared bundle; otherwise near 9 boundaries. Score **6**; confidence **medium**.

### S
Scope: shared user/app/Darwin bodies. Pros: home paths generally derive from config ([`modules/features/cli.nix:45`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L45), [`modules/features/zsh/default.nix:51`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/zsh/default.nix#L51)). Cons: contract grade 3: variation is mostly source edits; shared Git fixes author name/email and GitHub fixes account ([`modules/features/git/default.nix:73`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/git/default.nix#L73), [`modules/features/gh/default.nix:16`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/gh/default.nix#L16)), while Darwin trust fixes pd ([`modules/darwin/darwin.nix:9`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/darwin/darwin.nix#L9)). Grouped leak coverage grade 8: two groups—author identity/accounts and household timezone ([`modules/nixos/configuration.nix:11`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/configuration.nix#L11)); standard XDG paths and upstream theme pins excluded. Below contract5 despite low grouped leak count; min(3,8)=3. Score **3**; confidence **medium**.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":8,"distinct_leaks":2}}
```

### R
Scope: existing §4 fonts and independent application leaves. Pros: fonts is a drop-in os-class preset selected by real Darwin consumers ([`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2), [`modules/hosts/akari/default.nix:9`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/akari/default.nix#L9)); substantive Atuin is also independently scoped ([`modules/features/atuin/default.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/atuin/default.nix#L2)). Cons: existing nomination is tiny and lacks a documented minimal external adoption example ([`README.md:1`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/README.md#L1)). Literal 5 for readily adoptable leaves; substantial documented A-unit anchor9 unmet. Score **5**; confidence **medium**.

### P
Scope: two Darwin architectures, declared Linux route and shared terminal. Pros: Darwin class owns its OS options and fonts uses os ([`modules/darwin/darwin.nix:3`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/darwin/darwin.nix#L3), [`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2)). Cons: selected Linux configuration/hardware settings sit directly at aspect root rather than within nixos ([`modules/nixos/configuration.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/configuration.nix#L2), [`modules/nixos/hardware-configuration.nix:6`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/hardware-configuration.nix#L6)); shared Ghostty installs a mock package and depends on Darwin Homebrew for the actual app ([`modules/features/ghostty/default.nix:4`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/ghostty/default.nix#L4), [`modules/darwin/homebrew.nix:14`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/darwin/homebrew.nix#L14)). Interpolated 3: useful Darwin separation but declared Linux path lacks corresponding OS class contributions; no evaluation-failure claim. Score **3**; confidence **medium**.

### L
Scope: root documentation and inline explanations. Pros: source comments explain specific integration workarounds ([`modules/features/zoxide/default.nix:7`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/zoxide/default.nix#L7)). Cons: README title/image supplies no wiring or new-host path ([`README.md:1`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/README.md#L1)). Literal 2 placeholder anchor, despite useful local comments. Score **2**; confidence **medium**.

### V
Scope: flake outputs and module tree. Pros: devShell contains formatter/Lua tools ([`flake.nix:64`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L64)). Cons: output construction supplies no relevant semantic check definitions or invoked CI in inspected tree ([`flake.nix:77`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L77)); tools installed is not checks run. Literal 2, passing status unknown. Score **2**; confidence **medium**.

### O
Scope: rebuild/activation script. Pros: switch wrapper chooses platform-appropriate commands ([`flake.nix:53`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L53)). Cons: names are separately hard-coded rather than derived from Den inventory ([`flake.nix:54`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L54), [`flake.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L44)). Literal 2 for manual operation; no fleet requirement invented. Score **2**; confidence **medium**.

### X
Scope: os/home target classes and conventional constructors. Pros: standard Darwin/NixOS mainModules compose through existing entrypoints ([`flake.nix:78`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L78), [`flake.nix:92`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L92)). Cons: no non-host artifact class instantiated by this wiring ([`flake.nix:77`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/flake.nix#L77)). Baseline 2; Darwin belongs under P. Score **2**; confidence **medium**.

### B
Scope: census max-depth families and every complete app reference. Pros: native prompt configuration is supplied and independently enabled ([`modules/features/oh-my-posh/config.yaml:16`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/oh-my-posh/config.yaml#L16)). Cons: bare gh-dash/lazydocker leaves and package bundles excluded; Git/gh embed identity, Ghostty depends on a separate Homebrew install, Tmux uses an undeclared dev shell function and fzf, and Neovim bootstraps plugins through an undeclared Git runtime ([`modules/features/tmux/sessionizer:17`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/tmux/sessionizer#L17), [`modules/features/tmux/sessionizer:28`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/tmux/sessionizer#L28), [`modules/features/neovim/nvim/init.lua:9`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/neovim/nvim/init.lua#L9)). FZF explicitly wires Zsh integration ([`modules/features/fzf/default.nix:5`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fzf/default.nix#L5)), and Zoxide supplies ordered native initialization ([`modules/features/zoxide/default.nix:9`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/zoxide/default.nix#L9)); exact HM bd868f769a69d3b6091a1da68a75cb83a181033c modules/programs/fzf.nix line221 consumes the FZF switch. Fonts is reusable but package selection alone is not a substantive application reference. Score **4**; confidence **medium**.
B_div: 4 points → 3; B_ref: 7 units → 5; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":4,"diversity_grade":3,"reference_grade":5,"reference_units":[{"name":"atuin","evidence":"modules/features/atuin/default.nix:2"},{"name":"btop","evidence":"modules/features/btop/default.nix:2"},{"name":"eza","evidence":"modules/features/eza/default.nix:2"},{"name":"oh-my-posh","evidence":"modules/features/oh-my-posh/default.nix:2"},{"name":"ripgrep","evidence":"modules/features/ripgrep/default.nix:2"},{"name":"fzf","evidence":"modules/features/fzf/default.nix:2"},{"name":"zoxide","evidence":"modules/features/zoxide/default.nix:2"}]}}
```

Total: **31.0/100**. Shortlists: showcase false; library_units ['fonts']; starter false.

Overall pros:
- App concerns live in named feature aspects ([`modules/features/features.nix:6`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/features.nix#L6)).
- Cross-OS font preset is concise ([`modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2)).
- Native prompt format and segments are bundled ([`modules/features/oh-my-posh/config.yaml:16`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/oh-my-posh/config.yaml#L16)).

Overall cons / limits:
- Linux settings lack NixOS class envelope (§6a P; [`modules/nixos/configuration.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/nixos/configuration.nix#L2)).
- Shared author identity needs a setting (§6a S; [`modules/features/git/default.nix:73`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/git/default.nix#L73)).
- CLI bundle owns unrelated mutable directories (§6a I; [`modules/features/cli.nix:44`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L44)).
- No authoring guide (§6a L; [`README.md:1`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/README.md#L1)).

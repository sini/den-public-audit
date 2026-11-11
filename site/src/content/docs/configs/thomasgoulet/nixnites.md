---
title: "thomasgoulet/nixnites"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/thomasgoulet/nixnites/)

- Upstream: [thomasgoulet/nixnites](https://github.com/thomasgoulet/nixnites)
- Reviewed revision: [`54d53d7979ed`](https://github.com/thomasgoulet/nixnites/commit/54d53d7979ed9e712aa725c5ca06dfce98398691)
- Author: thomasgoulet
- Score: **40.0 / 100**, rank 88 of 101 ranked configs. D 3 · I 7 · S 5 · R 5 · P 5 · L 3 · V 2 · O 3 · B 4 · X 2. Shortlists: —.
- Summary: Direct context D3; feature boundary I7; ordinary validated settings S5/four adaptations; useful four references R5; WSL boundary P5; usage docs L3; assertions V2; bootstrap O3; package plumbing X2.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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

Flake-parts uses a regex-limited import-tree pass so only top-level feature/host/user modules enter the flake scope ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)). Nested files remain class-specific module trees, such as editor modules imported within HM ([`nix/features/editor.nix:8`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor.nix#L8)).


## 2. Common patterns.

- den.default includes: user/hostname and scoped input/self batteries are shared ([`nix/defaults.nix:14`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/defaults.nix#L14)).
- host-aspects composition: WSL host imports a dedicated OS subtree ([`nix/hosts/oric.nix:12`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric.nix#L12)).
- custom classes selection: user explicitly carries user and homeManager classes ([`nix/hosts/oric.nix:6`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric.nix#L6)).


## 3. Novel patterns.

Regex-limited discovery preserves a distinction between flake feature declarations and nested class modules ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44), [`nix/features/editor.nix:10`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor.nix#L10)).


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Explicit moduleFiles filtering is a scope-management technique rather than a verified den defect ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)). NH_FLAKE uses getEnv, so initial activation depends on the stated environment setup ([`nix/defaults.nix:24`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/defaults.nix#L24)).


## 6. Docs and complexity.

Docs 2: README gives installation and packaged-editor commands ([`README.md:9`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/README.md#L9), [`README.md:16`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/README.md#L16)), while flake comments explain discovery ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)). Complexity 3: shared features, separate user classes and a WSL subtree ([`nix/defaults.nix:14`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/defaults.nix#L14), [`nix/hosts/oric.nix:6`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric.nix#L6)).


## 6a. Defects and scoring notes.

- S · moderate: the shared Searx service carries a committed credential (reported privately; not located here); three further adaptation groups enumerated in S ([`nix/hosts/oric/wsl.nix:23`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric/wsl.nix#L23), [`nix/packages.nix:82`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L82), [`nix/features/headful/niri.nix:35`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/headful/niri.nix#L35)).
- P · minor: shared Lazygit openLink unconditionally uses wsl-open even for non-WSL user selection ([`nix/features/terminal/lazygit.nix:58`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/lazygit.nix#L58), [`nix/users/thom.nix:13`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/users/thom.nix#L13)).
- R · minor: wrapped editor packages retain custom herdr.nu/nix.nu command bindings without owning their installation ([`nix/packages.nix:31`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L31), [`nix/features/editor/settings.nix:151`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor/settings.nix#L151)).

## 7. Template notes.

Good module-scope teaching example; replace a committed credential (reported privately; not located here) in the bundled privacy service before extracting it ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)).

## 8. Scorecard.

### D
Scope: ordinary feature composition and host context. Pros: WSL NH_HOST consumes config hostname and batteries provide scoped inputs/self ([`nix/hosts/oric/wsl.nix:16`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric/wsl.nix#L16), [`nix/defaults.nix:14`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/defaults.nix#L14)). Cons: no selected quirk/policy fact pipeline verified; configured editor export is package plumbing ([`nix/packages.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L44)). Score3: small direct derivation above2 ordinary lists, below5 substantial shared domain. Score **3**; confidence **medium**.

### I
Scope: shallow feature discovery plus nested class modules. Pros: root regex preserves flake/class boundary and editor owns its nested module tree ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44), [`nix/features/editor.nix:8`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor.nix#L8)). Cons: terminal is a coarse multiapp bag and headful combines compositor/music/browser packages ([`nix/features/terminal.nix:24`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal.nix#L24), [`nix/features/headful.nix:33`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/headful.nix#L33)). Score7: intentional feature owners beyond5, below9 granular independence. Score **7**; confidence **medium**.

### S
Scope: native module settings and checkout precondition. Pros: dotfile path is checked for absolute checkout and required directories with actionable assertions ([`nix/features/dotfiles.nix:17`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/dotfiles.nix#L17), [`nix/features/dotfiles.nix:39`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/dotfiles.nix#L39)). Cons: no typed common feature parameter interface; four shared adaptation groups: a committed credential (reported privately; not located here), WSL trusted identity, installer repository URL, Niri keyboard/physical display topology ([`nix/hosts/oric/wsl.nix:23`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric/wsl.nix#L23), [`nix/packages.nix:82`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L82), [`nix/features/headful/niri.nix:17`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/headful/niri.nix#L17), [`nix/features/headful/niri.nix:35`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/headful/niri.nix#L35)). Contract5 ordinary settings with checked prerequisite, coverage6, min5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":4}}
```

### R
Scope: independently owned reference presets. Pros: Bat and Starship coherent settings; ExcaliDash owns Docker dependency and network/container ordering ([`nix/features/terminal/bat.nix:4`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/bat.nix#L4), [`nix/features/terminal/starship.nix:4`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/starship.nix#L4), [`nix/features/excalidash.nix:8`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/excalidash.nix#L8), [`nix/features/excalidash/network.nix:7`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/excalidash/network.nix#L7)). Cons: editor/Broot/Lazygit/Drydock/Leaf depend on unowned herdr.nu/hx/workspace tools, so not independently complete ([`nix/features/editor/settings.nix:150`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor/settings.nix#L150), [`nix/features/terminal/broot.nix:181`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/broot.nix#L181), [`nix/features/terminal/lazygit.nix:57`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/lazygit.nix#L57), [`nix/features/terminal/drydock.nix:86`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/drydock.nix#L86), [`nix/features/terminal/leaf.nix:11`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/leaf.nix#L11)). Literal5 reference material, below9 packaged library. Score **5**; confidence **medium**.

### P
Scope: WSL and graphical Linux host separation. Pros: WSL imports dedicated module and only graphical user selects headful ([`nix/hosts/oric.nix:12`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric.nix#L12), [`nix/users/thom.nix:9`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/users/thom.nix#L9), [`nix/features/headful.nix:17`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/headful.nix#L17)). Cons: global terminal native tools include WSL-specific opener in Lazygit without a host guard ([`nix/features/terminal/lazygit.nix:58`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/lazygit.nix#L58)). Literal5 explicit basic boundaries, no platform-count credit for four package keys. Score **5**; confidence **medium**.

### L
Scope: installation and editor usage. Pros: README gives concrete install/editor commands, discovery comment explains relative regex ([`README.md:9`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/README.md#L9), [`README.md:16`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/README.md#L16), [`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)). Cons: no worked new-feature/host/context route ([`README.md:19`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/README.md#L19)). Score3 above2 links-only orientation, below5 authoring walkthrough. Score **3**; confidence **medium**.

### V
Scope: declarative checkout assertions. Pros: invalid checkout is rejected with specific messages ([`nix/features/dotfiles.nix:39`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/dotfiles.nix#L39)). Cons: no test/check/CI fixture verified for discovery, platform guards or package helper closure ([`flake.nix:48`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L48), [`nix/packages.nix:43`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L43)). Baseline2 assertions alone, no run claimed. Score **2**; confidence **medium**.

### O
Scope: user-directed bootstrap and host variable. Pros: installer validates arguments/existing directory and carries NH_FLAKE into activation; WSL NH_HOST follows hostname ([`nix/packages.nix:67`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L67), [`nix/packages.nix:77`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L77), [`nix/packages.nix:83`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L83), [`nix/hosts/oric/wsl.nix:16`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric/wsl.nix#L16)). Cons: installer target is supplied manually and checkout/impure environment is an explicit prerequisite, not inventory-generated lifecycle ([`nix/defaults.nix:24`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/defaults.nix#L24), [`nix/packages.nix:72`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L72)). Score3: modest derived activation context, below5 inventory tooling. Score **3**; confidence **medium**.

### X
Scope: ordinary OS/HM plus wrapped editor package. Pros: Helix gets generated settings/language files and PATH ([`nix/packages.nix:35`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L35), [`nix/packages.nix:50`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L50)). Cons: wrapper is ordinary HM/package plumbing, not a distinct evaluated Den nonhost class ([`nix/packages.nix:11`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/packages.nix#L11)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: four complete independent owners and census max-depth. Pros: Bat, Starship, Docker and ExcaliDash own substantive preset or runtime wiring ([`nix/features/terminal/bat.nix:6`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/bat.nix#L6), [`nix/features/terminal/starship.nix:30`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/starship.nix#L30), [`nix/features/docker.nix:13`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/docker.nix#L13), [`nix/features/excalidash/systemd.nix:7`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/excalidash/systemd.nix#L7)). Cons: mixed notes/privacy/headful bodies cannot split into inner apps; editor and many terminal files require external custom script envelope; settings-only hl does not own installation ([`nix/features/notes.nix:13`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/notes.nix#L13), [`nix/features/privacy.nix:11`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/privacy.nix#L11), [`nix/features/editor/settings.nix:151`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor/settings.nix#L151), [`nix/features/infra/hl.nix:3`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/infra/hl.nix#L3)). Difftastic integration lacks independently owned Git activation ([`nix/features/terminal/difftastic.nix:6`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/difftastic.nix#L6)). Score **4**; confidence **medium**.
B_div: 4.0 points → 3; B_ref: 4 units → 4; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":4.0,"diversity_grade":3,"reference_grade":4,"reference_units":[{"name":"bat","evidence":"nix/features/terminal/bat.nix:4"},{"name":"starship","evidence":"nix/features/terminal/starship.nix:4"},{"name":"docker","evidence":"nix/features/docker.nix:3"},{"name":"excalidash","evidence":"nix/features/excalidash.nix:7"}]}}
```

Total: **40.0/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Flake and nested class imports have explicit scope boundary ([`flake.nix:44`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/flake.nix#L44)).
- Checkout failure has actionable assertions ([`nix/features/dotfiles.nix:39`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/dotfiles.nix#L39)).
- ExcaliDash owns network and ordering envelope ([`nix/features/excalidash/network.nix:7`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/excalidash/network.nix#L7)).

Overall cons / limits:
- A shared service carries a committed credential (reported privately; not located here) (§6a S).
- Generic Lazygit opener is WSL-specific (§6a P; [`nix/features/terminal/lazygit.nix:58`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/terminal/lazygit.nix#L58)).
- Editor package retains unowned custom keymap commands (§6a R; [`nix/features/editor/settings.nix:151`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/editor/settings.nix#L151)).

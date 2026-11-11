# phucisstupid__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/phucisstupid__dotfiles.md)

- Upstream: [phucisstupid/dotfiles](https://github.com/phucisstupid/dotfiles)
- Reviewed revision: [`0e80243bb07b`](https://github.com/phucisstupid/dotfiles/commit/0e80243bb07bb53e2cb1d118d8dfc7f127ea0b6c)
- Author: phucisstupid
- Score: **42.5 / 100**, rank 79 of 103 ranked configs. D 3 · I 8 · S 4 · R 5 · P 5 · L 3 · V 5 · O 2 · B 6 · X 2. Shortlists: library units (1).
- Summary: Small direct context D3; app-family ownership I8; untyped identity S4/one root adaptation; useful references R5; intended OS branches P5; usage docs L3; formatter V5; generic NH wrapper O2; normal module families X2.

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

Dendritic flake-parts/import-tree groups small tools under feature families (`flake.nix:4`, `modules/core/dendritic.nix:7`, `modules/aspects/clis/fd-ripgrep.nix:2`). Shared OS/HM policy serves both Linux and Darwin entity declarations (`modules/core/os-default.nix:19`, `modules/hosts/linux/main.nix:7`, `modules/hosts/phucs-MacBook-Air/main.nix:7`).


## 2. Common patterns.

- os-class: shared HM package/backup policy sits under os (`modules/core/os-default.nix:25`).
- den.default includes: define-user and hostname (`modules/core/os-default.nix:34`).
- provides tree: cli contains separately selectable fd and ripgrep children (`modules/aspects/clis/fd-ripgrep.nix:2`).


## 3. Novel patterns.

Ripgrep integrates batgrep and replaces the rg shell command as one search-tool opinion (`modules/aspects/clis/fd-ripgrep.nix:28`); users should know this affects command behavior.


## 4. Library candidates.

- cli.fd · `modules/aspects/clis/fd-ripgrep.nix:3` · fd with hidden-file search and .git exclusion · HM/nixpkgs · none · A: independent small tool preference.


## 5. den friction.

No verified den-specific workaround in inspected dendritic or shared class configuration (`modules/core/dendritic.nix:7`, `modules/core/os-default.nix:19`).


## 6. Docs and complexity.

Docs 2: README teaches wrapper commands but little architecture (`README.md:3`, `README.md:15`). Complexity 3: cross-platform entities and layered tool families share a concise OS default (`modules/hosts/linux/main.nix:7`, `modules/core/os-default.nix:19`).


## 6a. Defects and scoring notes.

- R · minor: ripgrep aliases rg to batgrep but adds batgrep only through Bat extraPackages without enabling Bat in the unit, so independent selection lacks the wrapper envelope (`modules/aspects/clis/fd-ripgrep.nix:28`, `modules/aspects/clis/fd-ripgrep.nix:33`).
- L · minor: wrapper commands have no worked entity/preset authoring route (`README.md:3`, `README.md:27`).
Shared checkout-root assumption is noted in S (`modules/aspects/shells/zsh-fish-nushell.nix:6`); platform coverage uncertainty is not a confirmed defect.

## 7. Template notes.

Approachable small features, though explain role activation and command aliases before borrowing the CLI bundle (`modules/aspects/clis/fd-ripgrep.nix:32`, `README.md:3`).

## 8. Scorecard.

### D
Scope: identity/context and ordinary presets. Pros: Git consumes selected user fullName/email; Ghostty chooses package by platform (`modules/aspects/clis/git.nix:8`, `modules/aspects/terminals.nix:38`). Cons: no independent shared fact emitter/collector/policy route verified (`modules/core/os-default.nix:34`). Score3 small direct context above2 lists, below5 substantial shared model. Score **3**; confidence **medium**.

### I
Scope: app families, named variants and entity values. Pros: user owner explicitly composes named leaves, identities remain in host user records (`modules/users/wow.nix:3`, `modules/hosts/linux/main.nix:8`, `modules/aspects/clis/fd-ripgrep.nix:3`). Cons: Delta/Lazygit/Atuin write settings for another separately activated tool (`modules/aspects/clis/delta.nix:15`, `modules/aspects/clis/lazygit.nix:15`, `modules/aspects/clis/atuin.nix:12`). Score8 strong selectable ownership beyond5, below9 consistently closed feature envelopes. Score **8**; confidence **medium**.

### S
Scope: native settings and custom identity fields. Pros: identity values come from current user and app presets expose normal HM settings (`modules/aspects/clis/git.nix:8`, `modules/aspects/clis/clock-rs.nix:6`). Cons: fullName/email have no local typed interface and checkout directory is assumed in shared shell PATH (`modules/hosts/linux/main.nix:9`, `modules/aspects/shells/zsh-fish-nushell.nix:6`). Contract4 below5 explicit local domain surface; coverage8 one grouped checkout-root adaptation; min4. Fonts/themes are ordinary defaults, not author leaks. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":8,"distinct_leaks":1}}
```

### R
Scope: independently selectable complete app presets. Pros: Lazyvim owns import/extras, Yazi owns plugins/keymaps and Spotify owns upstream integration (`modules/aspects/editors/lazyvim.nix:9`, `modules/aspects/clis/yazi.nix:6`, `modules/aspects/apps/spotify.nix:21`). Cons: many §4-grade tiny leaves are below substantive B threshold; ripgrep alias needs separately enabled Bat for batgrep (`modules/aspects/clis/fd-ripgrep.nix:28`). Literal5 useful references, below9 polished standalone library. Score **5**; confidence **medium**.

### P
Scope: declared Linux and Darwin users. Pros: shared os policy plus Ghostty Darwin package branch demonstrate boundaries (`modules/core/os-default.nix:25`, `modules/aspects/terminals.nix:38`). Cons: same user includes Darwin Aerospace for Linux too, with no source platform guard; final Linux support is unverified (`modules/users/wow.nix:7`, `modules/hosts/linux/main.nix:8`, `modules/aspects/window-managers/aerospace.nix:8`). Literal5 basic intended boundary, not a proved unsupported-platform failure. Score **5**; confidence **medium**.

### L
Scope: wrapper usage documentation. Pros: README supplies switch/update/generator/bootstrap commands and wrapper resolves repository cwd (`README.md:3`, `README.md:15`, `dotfiles:5`). Cons: no worked preset/entity/new-feature authoring route (`README.md:27`, `modules/users/wow.nix:3`). Score3 above2 links-only orientation, below5 authoring guide. Score **3**; confidence **medium**.

### V
Scope: formatter and workflow. Pros: treefmt enables deadnix/statix/shfmt and CI actually formats (`modules/core/formatters.nix:12`, `.github/workflows/ci.yml:24`). Cons: CI updates/commits lockfile rather than testing host/policy contexts; no negative-context fixture (`.github/workflows/ci.yml:34`). Literal5 ordinary structural tools, no run claimed. Score **5**; confidence **medium**.

### O
Scope: wrapper activation. Pros: wrapper selects OS command and actual hostname (`dotfiles:12`). Cons: this is uname/hostname-driven NH usage, not Den-inventory operational generation (`dotfiles:13`, `modules/aspects/clis/nh.nix:4`). Baseline2. Score **2**; confidence **medium**.

### X
Scope: standard OS/HM app modules. Pros: Lazyvim upstream module is actually imported (`modules/aspects/editors/lazyvim.nix:9`). Cons: no separate evaluated Den editor class; Nvf settings file lacks owned upstream module import (`modules/aspects/editors/nvf.nix:3`). Baseline2; package/module integration alone not new family. Score **2**; confidence **medium**.

### B
Scope: twenty-one complete named app presets and selected census max-depth. Pros: coherent presets include browser extensions, native editor plugins, named shell variants, terminal settings, prompt/theme and actual Bat man alias (`modules/aspects/apps/browser.nix:7`, `modules/aspects/editors/lazyvim.nix:19`, `modules/aspects/shells/zsh-fish-nushell.nix:14`, `modules/aspects/clis/bat.nix:11`). Cons: tiny fd/Helix/Btop/Zellij/Oh-my-posh and enable-only leaves excluded; Delta/Lazygit unowned secondary-app settings, Nvf missing import, Niri unowned launcher/module envelope and Wezterm undeclared local config excluded (`modules/aspects/clis/btop.nix:6`, `modules/aspects/editors/helix.nix:7`, `modules/aspects/clis/lazygit.nix:15`, `modules/aspects/editors/nvf.nix:3`, `modules/aspects/window-managers/niri.nix:76`, `modules/aspects/terminals.nix:8`). Fastfetch counts once via self-contained ml4w variant; hyde unowned hyprctl variant excluded (`modules/aspects/clis/fastfetch.nix:15`, `modules/aspects/clis/fastfetch.nix:328`). Score **6**; confidence **medium**.
B_div: 5 points → 3; B_ref: 21 units → 9; half-up mean → 6.
```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":9,"reference_units":[{"name":"bat","evidence":"modules/aspects/clis/bat.nix:2"},{"name":"clock-rs","evidence":"modules/aspects/clis/clock-rs.nix:2"},{"name":"eza","evidence":"modules/aspects/clis/ls.nix:2"},{"name":"fzf","evidence":"modules/aspects/clis/fzf.nix:2"},{"name":"direnv","evidence":"modules/aspects/clis/direnv.nix:2"},{"name":"fastfetch","evidence":"modules/aspects/clis/fastfetch.nix:328"},{"name":"yazi","evidence":"modules/aspects/clis/yazi.nix:2"},{"name":"tmux","evidence":"modules/aspects/multiplexers.nix:3"},{"name":"kitty","evidence":"modules/aspects/terminals.nix:18"},{"name":"ghostty","evidence":"modules/aspects/terminals.nix:34"},{"name":"lazyvim","evidence":"modules/aspects/editors/lazyvim.nix:7"},{"name":"zed","evidence":"modules/aspects/editors/zed-editor.nix:2"},{"name":"zsh","evidence":"modules/aspects/shells/zsh-fish-nushell.nix:14"},{"name":"fish","evidence":"modules/aspects/shells/zsh-fish-nushell.nix:33"},{"name":"nushell","evidence":"modules/aspects/shells/zsh-fish-nushell.nix:50"},{"name":"starship","evidence":"modules/aspects/shells/prompts.nix:3"},{"name":"chromium","evidence":"modules/aspects/apps/browser.nix:3"},{"name":"brave","evidence":"modules/aspects/apps/browser.nix:22"},{"name":"spotify","evidence":"modules/aspects/apps/spotify.nix:12"},{"name":"aerospace","evidence":"modules/aspects/window-managers/aerospace.nix:2"},{"name":"catppuccin","evidence":"modules/aspects/styles/themes.nix:7"}]}}
```

Total: **42.5/100**. Shortlists: showcase false; library_units ['cli.fd']; starter false.

Overall pros:
- Named app leaves are easy to compose (`modules/users/wow.nix:3`).
- Identity values remain on current entity (`modules/aspects/clis/git.nix:8`).
- Substantive editor and browser presets own their configuration (`modules/aspects/editors/lazyvim.nix:19`).

Overall cons / limits:
- Some app units need separately activated tools (§6a R; `modules/aspects/clis/fd-ripgrep.nix:28`).
- README teaches usage without authoring (§6a L; `README.md:27`).
- Linux use of Darwin WM remains unverified (`modules/users/wow.nix:7`).

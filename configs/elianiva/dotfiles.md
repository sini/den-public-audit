# elianiva/dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/elianiva/dotfiles.md)

- Upstream: [elianiva/dotfiles](https://github.com/elianiva/dotfiles)
- Reviewed revision: [`44d6d212ab1d`](https://github.com/elianiva/dotfiles/commit/44d6d212ab1deb2b7285a83244ff15aa20e32869)
- Author: elianiva
- Score: **45.0 / 100**, rank 70 of 101 ranked configs. D 3 · I 8 · S 5 · R 5 · P 5 · L 7 · V 2 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: D small host-context projection; I clear feature owners with a broad pure-tool bundle; S centralized identity but fixed native paths; R standalone GPG leaf; P native Ghostty Linux path contradiction; L strong guide with stale fields; V no relevant checks; O manual activation; B eight diversity points and three complete references; X standard Darwin/HM.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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

Native evalModules imports the module tree and passes inputs ([`flake.nix:58`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/flake.nix#L58)). Den then supplies global defaults and platform-aware host/home composition ([`modules/den.nix:23`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L23), [`modules/hosts.nix:20`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L20)).

## 2. Common patterns

- den.default includes shared fonts/packages and hostname ([`modules/den.nix:27`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L27)).
- define-user+primary-user live in the user aspect ([`modules/user.nix:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L8), [`modules/user.nix:10`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L10)).

## 3. Novel patterns

Identity data is deliberately a plain helper, separating platform home-directory calculation from modules ([`modules/_lib/identity.nix:1`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L1)).

## 4. Library candidates

- gpg · [`modules/aspects/gpg.nix:34`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L34) · GPG/agent/pass preset with OS-specific pinentry and cache policy · inputs: Den, HM, nixpkgs; no personal key asset · parameterization: none beyond native HM options · grade B: extract its aspect/input/platform contract and document key provisioning; it does not configure the author identity.

## 5. den friction

The identity helper mirrors define-user’s platform mapping, a small duplicated convention that must track Den ([`modules/_lib/identity.nix:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L18)).

## 6. Docs and complexity

Docs 5: README states platform coverage ([`README.md:3`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L3)), and entry/wiring comments teach import and class behavior ([`flake.nix:53`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/flake.nix#L53), [`modules/den.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L15)). Complexity 3: Darwin host plus standalone Linux homes are explicitly described ([`README.md:3`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L3), [`modules/hosts.nix:20`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L20)).

## 6a. Defects and scoring notes

- S · moderate: shared native prompt/config paths retain the original user and checkout/notes roots despite the central helper ([`nushell/starship.nu:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nushell/starship.nu#L8), [`modules/aspects/fish.nix:7`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/fish.nix#L7), [`qmd/index.yml:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/qmd/index.yml#L8)).
- P · moderate: selected Ghostty config always launches /run/current-system/sw/bin/nu although Linux outputs are explicitly foreign-distro standalone homes; those homes install Nushell in their home profile, not this system path ([`ghostty/config:12`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/ghostty/config#L12), [`modules/hosts.nix:22`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L22), [`modules/aspects/packages.nix:108`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L108)). Runtime impact is untested; consumers need an external path or native-config repair.
- L · minor: README says edit identity.dotfiles, which the helper does not export, and retains a removed Rust/fenix row ([`README.md:309`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L309), [`modules/_lib/identity.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L15), [`README.md:57`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L57)).
- Final pass drops the prior duplicate home-mapping/overlay notes as deductions: the supported mapping matches both OSes, and separate nixpkgs instances explain repeated overlays ([`modules/_lib/identity.nix:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L18), [`modules/hosts.nix:5`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L5)).

## 7. Template notes

Strong teaching example for classes and defaults ([`modules/den.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L15)); replace personal identity ([`modules/_lib/identity.nix:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L8)).

## 8. Scorecard

### D (3, high)
Scope: identity helper, host projection and module wiring. Pros: declared host context ([`modules/hosts.nix:20`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L20)) supplies host.system to the helper and home-derived Dock path ([`modules/aspects/host-darwin.nix:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/host-darwin.nix#L18), [`modules/aspects/host-darwin.nix:52`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/host-darwin.nix#L52), [`modules/_lib/identity.nix:20`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L20)). Cons: only a simple platform/name projection, not an application-fact channel or policy/pipe. Interpolation 3: a visible context-derived consumer exceeds direct-settings 2, but is much narrower than the useful application-data channel at 5; the no-policy cap remains 5. Confidence: high.

### I (8, high)
Scope: complete module/aspect inventory and user/platform selections. Pros: each native config directory has its own feature owner and Linux plumbing is an explicit variant ([`modules/user.nix:21`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L21), [`modules/user.nix:44`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/user.nix#L44)). Cons/ceiling: small pure-program settings share a broad bundle by deliberate design ([`modules/aspects/programs.nix:1`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/programs.nix#L1), [`modules/aspects/programs.nix:29`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/programs.nix#L29)). Interpolation 8: clearer optional ownership than 5, short of uniformly independent concerns at 9; no unrelated mutable-state defect charged. Confidence: high.

### S (5, medium)
Scope: identity helper, native shell/editor/notes settings and linked checkout roots. Pros: identity is centralized and home paths usually derive config.home.homeDirectory ([`modules/_lib/identity.nix:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L8), [`modules/aspects/git.nix:37`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/git.nix#L37)). Cons: §6a native identity/checkout/notes paths bypass that helper ([`nushell/starship.nu:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nushell/starship.nu#L8), [`modules/aspects/fish.nix:7`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/fish.nix#L7), [`qmd/index.yml:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/qmd/index.yml#L8)). Four grouped changes: user identity (including fixed prompt/plugin/credential paths), .dotfiles checkout root, personal notes root, herdr worktree root ([`fish/fish_variables:39`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/fish/fish_variables#L39), [`nushell/ai.nu:6`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nushell/ai.nu#L6), [`nvim/lua/plugins/obsidian.lua:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nvim/lua/plugins/obsidian.lua#L18), [`herdr/config.toml:56`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/herdr/config.toml#L56)). Raw ≥15 literals in this inspected subset; repeated username paths and both notes variants are grouped. Contract 5 (central identity and context-aware options, incomplete native path contract); coverage 6; min(5,6)=5. Confidence: medium.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":4}}
```

### R (5, medium)
Scope: GPG leaf and its adoption prerequisites. Pros: GPG, agent, pinentry selection and password-store are declared together without personal keys or names ([`modules/aspects/gpg.nix:34`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L34), [`modules/aspects/gpg.nix:43`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L43), [`modules/aspects/gpg.nix:58`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L58)). Cons: §4 grade B needs namespace/input/platform contract extraction and lacks a minimal independent consumer example; other links rely on external checkout/package selection ([`modules/aspects/nvim.nix:10`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/nvim.nix#L10), [`modules/aspects/packages.nix:51`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L51)). Anchor 5; S path costs are not deducted again. Confidence: medium.

### P (5, high)
Scope: Darwin host plus three standalone Linux homes and linked native entry files. Pros: class-specific package placement and Linux ARM/nixGL exceptions are explicit ([`modules/aspects/packages.nix:91`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L91), [`modules/aspects/packages.nix:108`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L108), [`modules/aspects/ghostty.nix:35`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/ghostty.nix#L35)). Cons: Ghostty always launches /run/current-system/sw/bin/nu even for foreign-Linux homes (§6a, [`ghostty/config:12`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/ghostty/config#L12), [`modules/hosts.nix:22`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L22)); no declared home provides that system path. Anchor 5: useful explicit boundaries with an unresolved native exception, not full feature parity or verified runtime failure. Confidence: high.

### L (7, high)
Scope: entire README, entry comments and justfile. Pros: README maps ownership, prerequisites, bootstrap and adding a feature/host ([`README.md:19`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L19), [`README.md:72`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L72), [`README.md:287`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L287)); Den class comments teach account ownership ([`modules/den.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L15)). Cons: §6a README instructs changing a nonexistent identity.dotfiles field and still describes a removed Rust/fenix source ([`README.md:309`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L309), [`README.md:57`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L57), [`modules/_lib/identity.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L15)). Interpolation 7: substantial teaching beyond 5, drift prevents 9 reliable navigation. Confidence: high.

### V (2, high)
Scope: tracked root/module checks, justfile and relevant workflow inventory. Pros: post-bootstrap commands are documented ([`README.md:181`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L181)). Cons: no authored configuration behavior/boundary checks or CI were found in the pinned tree; justfile provides switches/updates, not assertions ([`justfile:3`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/justfile#L3), [`justfile:14`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/justfile#L14)). Baseline 2; vendored agent tooling tests are outside configuration verification and no passing status is claimed. Confidence: high.

### O (2, medium)
Scope: actual targets, bootstrap guide and activation helpers. Pros: rebuild recipes identify standalone home and Darwin outputs ([`justfile:3`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/justfile#L3), [`justfile:14`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/justfile#L14)). Cons: OS install and activation are imperative rather than generated from Den host facts ([`README.md:85`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L85), [`README.md:227`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L227)); global vp installation is a local package list, not fleet data ([`modules/aspects/vp-global-packages.nix:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/vp-global-packages.nix#L18)). Baseline 2 for manual personal setup, without inventing a fleet defect. Confidence: medium.

### B (5, medium)
Scope: all current aspect/native-entry bodies, excluding legacy config and vendored agent implementations. Pros: census max-depth credit is 1 each for Neovim, Helix, Fish, Nushell, Zellij, Bash and Starship plus .5 Tmux + .5 Zed = 8 → diversity 5. Three complete identity-free references below → reference 4; mean 4.5 rounds up to B5. Cons: native symlink leaves do not install all their applications independently ([`modules/aspects/nvim.nix:10`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/nvim.nix#L10), [`modules/aspects/packages.nix:51`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/packages.nix#L51)); broad programs/profile bundles and package-only Go/Bazel are not separately counted ([`modules/aspects/programs.nix:1`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/programs.nix#L1), [`modules/aspects/go.nix:14`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/go.nix#L14)). GPG, Linux Nix management and fontconfig include substantive bodies with their package/input dependencies ([`modules/aspects/gpg.nix:34`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L34), [`modules/aspects/home-linux.nix:22`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/home-linux.nix#L22), [`modules/aspects/fonts.nix:32`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/fonts.nix#L32)). Confidence: medium.
```score-evidence
{"B":{"diversity_points":8.0,"diversity_grade":5,"reference_grade":4,"reference_units":[{"name":"gpg","evidence":"modules/aspects/gpg.nix:34"},{"name":"linux-nix-management","evidence":"modules/aspects/home-linux.nix:22"},{"name":"fontconfig","evidence":"modules/aspects/fonts.nix:32"}]}}
```

### X (2, high)
Scope: Den schemas, host/home inventory and package outputs. Pros: standard OS/home classes are explicit ([`modules/den.nix:17`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L17), [`modules/hosts.nix:20`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L20)). Cons: native Neovim/Lua and agent packages are payloads, not additional Den target classes ([`modules/aspects/nvim.nix:9`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/nvim.nix#L9), [`modules/aspects/agents.nix:13`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/agents.nix#L13)). Baseline 2; Darwin and standalone HM receive P credit only. Confidence: high.

Total: **45.0/100**. Shortlists: showcase no; library_units gpg; starter no. The GPG leaf merits a library nomination. No routed-fact showcase; not a starter recommendation while native portability and documentation mismatches require source repair.

Overall pros:
- Concern ownership and class selection are taught directly ([`README.md:19`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L19), [`modules/den.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/den.nix#L15)).
- Linux versus Darwin package/GL handling is localized ([`modules/aspects/ghostty.nix:35`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/ghostty.nix#L35)).
- GPG has a complete identity-free program/agent body ([`modules/aspects/gpg.nix:34`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L34)).

Overall cons / limits:
- S: prompt/native paths still embed the original user ([`nushell/starship.nu:8`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/nushell/starship.nu#L8)).
- P: foreign Linux inherits a system-profile-only Ghostty command ([`ghostty/config:12`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/ghostty/config#L12)).
- L: checkout adaptation guidance names a field absent from its helper ([`README.md:309`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/README.md#L309), [`modules/_lib/identity.nix:15`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L15)).

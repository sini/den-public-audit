---
title: "voidlily/dotfiles"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/voidlily/dotfiles/)

- Upstream: [voidlily/dotfiles](https://github.com/voidlily/dotfiles)
- Reviewed revision: [`ef20abb997bd`](https://github.com/voidlily/dotfiles/commit/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc)
- Author: voidlily
- Score: **47.5 / 100**, rank 61 of 101 ranked configs. D 4 · I 8 · S 5 · R 5 · P 6 · L 2 · V 5 · O 5 · B 5 · X 2. Shortlists: library units (1).
- Summary: Direct context D4; app ownership I8; ordinary settings S5/six adaptations; eleven complete references; null OS boundary P6; stale bootstrap L2; treefmt V5; derived rekey ops O5; ordinary targets X2.

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

Generated flake-parts/import-tree outputs load numerous application and role aspects ([`flake.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/flake.nix#L4), [`modules/minimal.nix:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L9)). Host and user schemas carry hostname/host-aspects and mutual-provider while scoped inputs/self are global ([`modules/den.nix:17`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L17), [`modules/den.nix:24`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L24)).


## 2. Common patterns.

- mutual-provider: enabled on the user schema ([`modules/den.nix:29`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L29)).
- host-aspects: selected for all hosts alongside hostname ([`modules/den.nix:24`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L24)).
- os-class: minimal uses one OS package/certificate policy for multiple platforms ([`modules/minimal.nix:21`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L21)).
- den.default includes: inputs and self are system-scoped batteries ([`modules/den.nix:17`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L17)).


## 3. Novel patterns.

Agenix-rekey config computes local secret-storage directories differently for OS and HM and handles a null osConfig ([`modules/agenix.nix:59`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L59), [`modules/agenix.nix:67`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L67)). This supports reuse of secret plumbing across nested and standalone contexts.


## 4. Library candidates.

- direnv · [`modules/direnv.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L15) · direnv-instant plus explicit nix-direnv support · direnv-instant, HM/nixpkgs · none · B: bundle the default import at line 11 with the opt-in aspect.


## 5. den friction.

The secret module explicitly questions whether hostPubkey belongs in host metadata or concrete host age.rekey settings ([`modules/agenix.nix:39`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L39)); an unresolved modeling choice, not a verified den bug.


## 6. Docs and complexity.

Docs 2: README gives a Mac bootstrap recipe pointing at systems/aarch64-darwin ([`README.md:3`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L3), [`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9)), while current wiring is under modules ([`flake.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/flake.nix#L4)). Complexity 4: shared OS/HM roles and secret rekey storage boundaries add to the feature breadth ([`modules/minimal.nix:21`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L21), [`modules/agenix.nix:59`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L59)).


## 6a. Defects and scoring notes.

- L · moderate: bootstrap requires copying systems/aarch64-darwin, absent from current module-based host inventory ([`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9), [`modules/hosts/homu/homu.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/homu/homu.nix#L4)).
- S · moderate: six grouped shared adaptations enumerated in S, including rekey master identities and printer endpoint ([`modules/agenix.nix:49`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L49), [`modules/hardware/printing.nix:35`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hardware/printing.nix#L35), [`modules/shell/git.nix:19`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/git.nix#L19)).

## 7. Template notes.

Teaches schema-wide batteries and cross-platform role classes, but update the bootstrap paths and separate personal rekey identities before reuse ([`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9), [`modules/agenix.nix:49`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L49)).

## 8. Scorecard.

### D
Scope: named provider delivery and direct resource context. Pros: host aspects reach users and secret storage keys derive current OS/user hostname, including null osConfig ([`modules/den.nix:24`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L24), [`modules/agenix.nix:64`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L64), [`modules/agenix.nix:74`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L74)). Cons: explicit provider/class delivery and direct config lookup dominate; no selected independent routed fact collector verified ([`modules/desktop/scanner.nix:11`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/scanner.nix#L11), [`modules/containers.nix:48`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/containers.nix#L48)). Score4 beyond2 ordinary lists, below5 rich typed shared model; no declaration-only route credit. Score **4**; confidence **medium**.

### I
Scope: many feature owners and personal host composition. Pros: applications have individual files, host composes roles, identity lives in dedicated user owner ([`modules/hosts/homu/homu.nix:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/homu/homu.nix#L9), [`modules/hosts/users.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/users.nix#L4), [`modules/direnv.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L15)). Cons: broad Steam game presets and global module-import defaults impose larger envelopes ([`modules/games/steam.nix:97`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/games/steam.nix#L97), [`modules/direnv.nix:11`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L11)). Score8 strong ownership beyond5, below9 consistently independent setup. Score **8**; confidence **medium**.

### S
Scope: ordinary settings and secret context boundary. Pros: OS/HM storage paths follow context and handle standalone null osConfig ([`modules/agenix.nix:59`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L59), [`modules/agenix.nix:74`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L74)). Cons: no richer local typed feature schema; six adaptation groups remain: shared identity/signing, rekey identity material, checkout root, Syncthing peer, printer/network endpoint, repository secret namespace ([`modules/shell/git.nix:19`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/git.nix#L19), [`modules/gpg.nix:10`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/gpg.nix#L10), [`modules/agenix.nix:49`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L49), [`modules/minimal.nix:47`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L47), [`modules/desktop/syncthing.nix:22`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/syncthing.nix#L22), [`modules/hardware/printing.nix:35`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hardware/printing.nix#L35), [`modules/ddns.nix:13`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/ddns.nix#L13)). Physical host settings are entity-owned, excluded. Contract5 ordinary option surface, coverage6, min5. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":6}}
```

### R
Scope: meaningful independent app presets. Pros: Direnv owns upstream default import plus opt-in instant/nix-direnv; Reaper owns extension/preferences and runtime libraries; Starship wires store-path jj helper ([`modules/direnv.nix:11`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L11), [`modules/direnv.nix:23`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L23), [`modules/reaper.nix:38`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/reaper.nix#L38), [`modules/shell/starship.nix:127`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/starship.nix#L127)). Cons: Git/JJ identity, MPV self package, mixed K8s/linters and Emacs extra command dependency envelopes excluded ([`modules/shell/git.nix:19`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/git.nix#L19), [`modules/shell/jj.nix:43`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/jj.nix#L43), [`modules/desktop/mpv.nix:16`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/mpv.nix#L16), [`modules/dev/k8s.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/dev/k8s.nix#L15), [`doom.d/config.el:83`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/doom.d/config.el#L83)). Literal5 useful references, not9 packaged/documented exports. Score **5**; confidence **medium**.

### P
Scope: Linux fleet with explicit Darwin/standalone module boundaries. Pros: shared os policy and separate rekey imports cover OS classes; HM secret path handles null osConfig ([`modules/minimal.nix:21`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L21), [`modules/agenix.nix:21`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L21), [`modules/agenix.nix:26`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L26), [`modules/agenix.nix:75`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L75)). Cons: current host inventory is one Linux machine; README Mac instructions are stale ([`modules/hosts/homu/homu.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/homu/homu.nix#L4), [`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9)). Score6: explicit cross-context boundary beyond5, no unsupported target success claimed. Score **6**; confidence **medium**.

### L
Scope: bootstrap guidance. Pros: README gives ordered bootstrap steps and module comments explain rekey context ([`README.md:3`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L3), [`modules/agenix.nix:39`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L39)). Cons: bootstrap tells readers to copy nonexistent systems/aarch64-darwin instead of current module inventory, and no current feature-authoring walkthrough ([`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9), [`modules/hosts/homu/homu.nix:4`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/homu/homu.nix#L4)). Score2: actionable intent but stale route below5. Score **2**; confidence **medium**.

### V
Scope: generated formatter check. Pros: imported treefmt module enables nixfmt with project-root contract ([`modules/treefmt.nix:14`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/treefmt.nix#L14), [`modules/treefmt.nix:16`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/treefmt.nix#L16)). Cons: no targeted provider/null-context/rekey fixture or actual build workflow verified ([`modules/agenix.nix:75`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L75), [`modules/den.nix:29`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/den.nix#L29)). Literal5 ordinary generated structural check, static only. Score **5**; confidence **medium**.

### O
Scope: inventory-context secret rekey outputs and VM convenience. Pros: secret storage derives hostname/user context; rekey devshell package follows config; VM wrapper resolves actual host build output ([`modules/agenix.nix:64`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L64), [`modules/agenix.nix:74`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L74), [`modules/devshell.nix:10`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/devshell.nix#L10), [`modules/vm.nix:13`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/vm.nix#L13)). Cons: VM host is literal and NH checkout fixed; not full fleet deployment/recovery automation ([`modules/vm.nix:13`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/vm.nix#L13), [`modules/minimal.nix:47`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L47)). Literal5 useful derived operational paths. Score **5**; confidence **medium**.

### X
Scope: ordinary OS/HM apps and developer tools. Pros: shared classes reach OS/home; K8s tools are installed ([`modules/minimal.nix:21`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/minimal.nix#L21), [`modules/dev/k8s.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/dev/k8s.nix#L15)). Cons: tools do not define evaluated Kubernetes/nonhost Den targets; VM wrapper is ordinary host build plumbing ([`modules/vm.nix:13`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/vm.nix#L13)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: eleven complete app-owner envelopes and selected census max-depth. Pros: owned runtime integrations include Ghostty theme input, Starship jj command, OBS virtual camera/plugin, Podman compatibility/socket, Monado/OpenXR and Reaper extension/preferences ([`modules/desktop/ghostty.nix:29`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/ghostty.nix#L29), [`modules/shell/starship.nix:127`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/starship.nix#L127), [`modules/desktop/obs-studio.nix:10`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/obs-studio.nix#L10), [`modules/containers.nix:18`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/containers.nix#L18), [`modules/games/vr.nix:13`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/games/vr.nix#L13), [`modules/reaper.nix:48`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/reaper.nix#L48)). Cons: package/enable/token preference leaves, include-only profiles and comments excluded; author-specific Steam/Git/JJ/Syncthing/rekey excluded; MPV/Retroarch self packages and Doom external Rust/Tofu tools break independent envelopes ([`modules/games/steam.nix:311`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/games/steam.nix#L311), [`modules/desktop/mpv.nix:16`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/mpv.nix#L16), [`modules/games/retroarch.nix:17`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/games/retroarch.nix#L17), [`doom.d/config.el:83`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/doom.d/config.el#L83), [`doom.d/config.el:108`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/doom.d/config.el#L108)). Multiapp K8s/notes bundles not split per inner attr. Score **5**; confidence **medium**.
B_div: 4.5 points → 3; B_ref: 11 units → 7; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"direnv","evidence":"modules/direnv.nix:15"},{"name":"starship","evidence":"modules/shell/starship.nix:3"},{"name":"bat","evidence":"modules/shell/bat.nix:6"},{"name":"pipewire","evidence":"modules/desktop/pipewire.nix:7"},{"name":"libreoffice","evidence":"modules/desktop/libreoffice.nix:7"},{"name":"obs-studio","evidence":"modules/desktop/obs-studio.nix:6"},{"name":"ghostty","evidence":"modules/desktop/ghostty.nix:14"},{"name":"podman","evidence":"modules/containers.nix:7"},{"name":"libvirt","evidence":"modules/libvirt.nix:7"},{"name":"vr-monado","evidence":"modules/games/vr.nix:9"},{"name":"reaper","evidence":"modules/reaper.nix:12"}]}}
```

Total: **47.5/100**. Shortlists: showcase false; library_units ['direnv']; starter false.

Overall pros:
- Many app owners support explicit selection ([`modules/hosts/homu/homu.nix:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/hosts/homu/homu.nix#L9)).
- Secret storage distinguishes OS and standalone-home contexts ([`modules/agenix.nix:75`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L75)).
- Real prompt and DAW runtime integrations are available ([`modules/shell/starship.nix:127`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/shell/starship.nix#L127), [`modules/reaper.nix:48`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/reaper.nix#L48)).

Overall cons / limits:
- Bootstrap path is stale (§6a L; [`README.md:9`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/README.md#L9)).
- Shared secret/identity data needs adaptation (§6a S; [`modules/agenix.nix:49`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L49)).
- Several rich definitions require repository-specific package closure ([`modules/desktop/mpv.nix:16`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/desktop/mpv.nix#L16)).

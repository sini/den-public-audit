---
title: "mrbandler/nix"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/mrbandler/nix/)

- Upstream: [mrbandler/nix](https://github.com/mrbandler/nix)
- Reviewed revision: [`6869a203c3fc`](https://github.com/mrbandler/nix/commit/6869a203c3fc4e605eaebefc2c760b7096b8fc66)
- Author: mrbandler
- Score: **59.5 / 100**, rank 15 of 101 ranked configs. D 5 · I 7 · S 6 · R 5 · P 7 · L 7 · V 5 · O 6 · B 8 · X 2. Shortlists: showcase.
- Summary: D shared typed config capped5; I coarse selectable bags; S real contracts with five adaptations; R independent app files; P explicit platform branches; L worked ownership; V closure checks; O derived installer/NH; X standard; B full file-owned unit inventory.

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

Dendritic modules organize concerns into aspect families with fleet defaults for Darwin/NixOS/HM ([`modules/dendritic.nix:3`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/dendritic.nix#L3), [`modules/fleet/defaults.nix:15`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/defaults.nix#L15)). The README explicitly distinguishes the active Darwin host from the not-yet-ported Linux system ([`README.md:13`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L13)).


## 2. Common patterns.

- den.default includes/classes: platform defaults and HM user classes live under fleet ([`modules/fleet/defaults.nix:16`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/defaults.nix#L16), [`modules/fleet/defaults.nix:47`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/defaults.nix#L47)).
- host-aspects: every host schema includes core centrally ([`modules/fleet/schema.nix:8`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/schema.nix#L8)).
- provides tree + parametric aspect (fn args): hermes gives its users a host-specific browser device label ([`modules/hosts/hermes.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L20)).


## 3. Novel patterns.

Host-bound browser identity is delivered through to-users instead of being attached to the travelling user ([`modules/hosts/hermes.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L20)); the README explains this ownership rule ([`README.md:61`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L61)).


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

No verified den-specific workaround in inspected fleet and host boundary code ([`modules/fleet/schema.nix:8`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/schema.nix#L8), [`modules/hosts/hermes.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L20)).


## 6. Docs and complexity.

Docs 4: README explains layout, generated inputs and aspect/value ownership conventions ([`README.md:16`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L16), [`README.md:49`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L49), [`README.md:55`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L55)). Complexity 4: multi-platform defaults, grouped feature families and user-boundary projections ([`modules/fleet/defaults.nix:17`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/fleet/defaults.nix#L17), [`modules/hosts/hermes.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L20)).


## 6a. Defects and scoring notes.

- I · minor: cli/development/apps aspect bags bind independent file-owned app choices together ([`modules/aspects/cli/tools/tools.nix:3`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/tools.nix#L3), [`modules/aspects/apps/comms/comms.nix:2`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/comms/comms.nix#L2), [`modules/users/mrbandler/mrbandler.nix:7`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/users/mrbandler/mrbandler.nix#L7)).
- S · moderate: five grouped shared adaptations remain, enumerated in S ([`modules/aspects/development/vcs/_identity.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/vcs/_identity.nix#L5), [`modules/aspects/security/onepassword.nix:101`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/security/onepassword.nix#L101)).
- O · minor: installer takes first HM user and chowns home to fixed 1000:100, constraining otherwise parameterized host/address flow ([`modules/tools/install.nix:75`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L75), [`modules/tools/install.nix:168`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L168)).
Disclosed unported Linux status is a limit, not a defect.

## 7. Template notes.

Useful example of ownership and migration status, but do not imply Linux is already operational ([`README.md:14`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L14)).

## 8. Scorecard.

### D
Scope: typed keybindings shared by compositor backends. Pros: one typed binding contract is consumed by AeroSpace chord translation and Niri key translation ([`modules/aspects/desktop/core/_keybindings.nix:12`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/core/_keybindings.nix#L12), [`modules/aspects/desktop/compositors/aerospace.nix:12`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/compositors/aerospace.nix#L12), [`modules/aspects/desktop/compositors/niri.nix:23`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/compositors/niri.nix#L23)). Cons: direct HM config/schema calculations, not emitted/routed Den facts; host browser label uses direct provider value ([`modules/hosts/hermes.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L20)). Literal5 useful shared data model capped5. Score **5**; confidence **medium**.

### I
Scope: file ownership versus selectable aspect scope. Pros: per-app files own integrations and platform-specific bodies ([`modules/aspects/cli/tools/posting.nix:18`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/posting.nix#L18), [`modules/aspects/cli/terminals/ghostty.nix:19`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/terminals/ghostty.nix#L19)). Cons: unrelated apps merge into cli/development/apps bags, so selecting one bag selects all contributions rather than composing apps independently ([`modules/aspects/cli/tools/tools.nix:3`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/tools.nix#L3), [`modules/aspects/apps/comms/comms.nix:2`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/comms/comms.nix#L2), [`modules/users/mrbandler/mrbandler.nix:7`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/users/mrbandler/mrbandler.nix#L7)). Interpolated7 for strong file ownership below9 aspect-level isolation; deliberate bag itself is not a runtime bug. Score **7**; confidence **medium**.

### S
Scope: local option modules versus personal shared integrations. Pros: typed keybindings/devDir/disk.device have defaults and real consumers ([`modules/aspects/desktop/core/_keybindings.nix:4`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/core/_keybindings.nix#L4), [`modules/aspects/development/core/_devdir.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/core/_devdir.nix#L5), [`modules/aspects/core/disk.nix:39`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/core/disk.nix#L39)). Contract7 above5 useful coherent surfaces, below9 consistently parameterized apps. Cons: five grouped adaptations: owner identities/signing, config repository/root, Opnix vault/item namespace, private Obsidian vault repository set, household locale/keyboard ([`modules/aspects/development/vcs/_identity.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/vcs/_identity.nix#L5), [`modules/aspects/core/comin.nix:15`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/core/comin.nix#L15), [`modules/aspects/security/onepassword.nix:101`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/security/onepassword.nix#L101), [`modules/aspects/apps/knowledge/obsidian.nix:13`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/knowledge/obsidian.nix#L13), [`modules/aspects/core/locale.nix:3`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/core/locale.nix#L3), [`modules/aspects/desktop/shells/noctalia.nix:35`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/shells/noctalia.nix#L35)). Coverage6; business identity variants grouped with owner. min(7,6)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":5}}
```

### R
Scope: independently importable app owner files despite shared aspect addresses. Pros: coherent Posting/MPV/terminal presets and Stylix import/assets can be copied independently ([`modules/aspects/cli/tools/posting.nix:18`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/posting.nix#L18), [`modules/aspects/apps/media/mpv.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/media/mpv.nix#L5), [`modules/aspects/theme/stylix.nix:11`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/theme/stylix.nix#L11)). Cons: §4 nominates no polished standalone Den package; personal identity/secret/desktop schema units require wider envelope ([`modules/aspects/development/vcs/git.nix:10`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/vcs/git.nix#L10), [`modules/aspects/apps/storage/rclone.nix:13`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/storage/rclone.nix#L13)). Literal5 useful independent files, not9 documented A-aspect extraction. Score **5**; confidence **medium**.

### P
Scope: active Darwin and explicitly migrating Linux. Pros: class/provider boundaries and package/service guards are intentional; Nu PATH and Ghostty package differ by platform ([`modules/aspects/cli/shells/nushell.nix:15`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/shells/nushell.nix#L15), [`modules/aspects/cli/terminals/ghostty.nix:24`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/terminals/ghostty.nix#L24), [`modules/aspects/apps/creative/creative.nix:30`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/creative/creative.nix#L30)). Cons: Linux is explicitly not yet ported, and there are no negative-context boundary fixtures ([`README.md:14`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L14)). Interpolated7 for concrete multi-platform guards beyond5, not9 verified complete platform boundary suite. Score **7**; confidence **medium**.

### L
Scope: conventions, authoring and operations README. Pros: explains file versus aspect unit, ownership, provider wrappers and gives worked Comin include ([`README.md:55`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L55), [`README.md:68`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L68), [`README.md:143`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L143)). Cons: not a comprehensive clean new-app/target walkthrough for custom desktop contracts ([`README.md:72`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L72)). Interpolated7 beyond5 useful worked conventions, below9 end-to-end teaching. Score **7**; confidence **medium**.

### V
Scope: checks generated from actual host closures. Pros: host configs map to architecture-grouped flake checks ([`modules/tools/checks.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/checks.nix#L5), [`modules/tools/checks.nix:11`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/checks.nix#L11)). Cons: these are closure builds, not targeted provider/boundary assertions; no run claimed. Literal5 structural validation. Score **5**; confidence **medium**.

### O
Scope: inventory-derived NH/check artifacts and installer facts. Pros: NH packages derive entities; installer reads target user/disk, checks installer environment and requires typed hostname confirmation ([`modules/tools/nh.nix:7`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/nh.nix#L7), [`modules/tools/install.nix:74`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L74), [`modules/tools/install.nix:85`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L85), [`modules/tools/install.nix:134`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L134)). Cons: repository and first-user/UID ownership assumptions remain ([`modules/tools/install.nix:20`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L20), [`modules/tools/install.nix:75`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L75), [`modules/tools/install.nix:168`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L168)). Interpolated6 beyond5 two concrete operational integrations, below9 reusable failure-handled fleet pipeline. Score **6**; confidence **medium**.

### X
Scope: ordinary OS/home, installer ISO and package outputs. Pros: installer ISO owns install helper ([`modules/tools/iso.nix:28`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/iso.nix#L28)). Cons: ordinary nixosSystem/package export is build plumbing, not a new evaluated Den target class ([`modules/tools/iso.nix:19`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/iso.nix#L19), [`modules/tools/iso.nix:35`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/iso.nix#L35)). Baseline2, no duplicate O credit. Score **2**; confidence **medium**.

### B
Scope: source-read independent app owner files, even when sharing an aspect address. Pros: listed files own complete coherent presets/integration; same app counted once ([`modules/aspects/cli/tools/posting.nix:18`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/posting.nix#L18), [`modules/aspects/cli/tools/yazi.nix:7`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/yazi.nix#L7)). Cons: token Btop/K9s/Fd/Ripgrep/Tealdeer, external-runtime Television, identity VCS/mail/Obsidian, Stylix-dependent Nb/Firefox/Neovim and fleet keybinding/compositor envelopes excluded ([`modules/aspects/cli/tools/btop.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/btop.nix#L5), [`modules/aspects/cli/tools/television.nix:15`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/television.nix#L15), [`modules/aspects/development/vcs/_identity.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/vcs/_identity.nix#L5), [`modules/aspects/apps/knowledge/nb.nix:10`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/apps/knowledge/nb.nix#L10)). Mixed bag bodies are not counted once per every inner program; complete single-app files are. Score **8**; confidence **medium**.
B_div: 10.5 points → 7; B_ref: 25 units → 9; half-up mean → 8.
```score-evidence
{"B":{"diversity_points":10.5,"diversity_grade":7,"reference_grade":9,"reference_units":[{"name":"starship","evidence":"modules/aspects/cli/prompts/starship.nix:2"},{"name":"bash","evidence":"modules/aspects/cli/shells/bash.nix:2"},{"name":"nushell","evidence":"modules/aspects/cli/shells/nushell.nix:18"},{"name":"zsh","evidence":"modules/aspects/cli/shells/zsh.nix:8"},{"name":"ghostty","evidence":"modules/aspects/cli/terminals/ghostty.nix:19"},{"name":"aerc","evidence":"modules/aspects/cli/tools/aerc.nix:2"},{"name":"atuin","evidence":"modules/aspects/cli/tools/atuin.nix:5"},{"name":"carapace","evidence":"modules/aspects/cli/tools/carapace.nix:5"},{"name":"direnv","evidence":"modules/aspects/cli/tools/direnv.nix:7"},{"name":"eza","evidence":"modules/aspects/cli/tools/eza.nix:5"},{"name":"fastfetch","evidence":"modules/aspects/cli/tools/fastfetch.nix:14"},{"name":"fzf","evidence":"modules/aspects/cli/tools/fzf.nix:5"},{"name":"glow","evidence":"modules/aspects/cli/tools/glow.nix:15"},{"name":"harlequin","evidence":"modules/aspects/cli/tools/harlequin.nix:15"},{"name":"khal","evidence":"modules/aspects/cli/tools/khal.nix:2"},{"name":"lazygit","evidence":"modules/aspects/cli/tools/lazygit.nix:5"},{"name":"posting","evidence":"modules/aspects/cli/tools/posting.nix:18"},{"name":"tailspin","evidence":"modules/aspects/cli/tools/tailspin.nix:8"},{"name":"yazi","evidence":"modules/aspects/cli/tools/yazi.nix:5"},{"name":"zoxide","evidence":"modules/aspects/cli/tools/zoxide.nix:5"},{"name":"mpv","evidence":"modules/aspects/apps/media/mpv.nix:5"},{"name":"diffnav","evidence":"modules/aspects/development/tools/diffnav.nix:8"},{"name":"delta","evidence":"modules/aspects/development/tools/delta.nix:2"},{"name":"nautilus","evidence":"modules/aspects/desktop/fileManagers/nautilus.nix:5"},{"name":"stylix","evidence":"modules/aspects/theme/stylix.nix:11"}]}}
```

Total: **59.5/100**. Shortlists: showcase true; library_units []; starter false.

Overall pros:
- Meaningful typed desktop binding contract ([`modules/aspects/desktop/core/_keybindings.nix:12`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/desktop/core/_keybindings.nix#L12)).
- Explicit platform guards and ownership conventions ([`README.md:61`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L61)).
- Useful independent app presets ([`modules/aspects/cli/tools/posting.nix:18`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/cli/tools/posting.nix#L18)).

Overall cons / limits:
- Coarse selectable app bags (§6a I; [`modules/users/mrbandler/mrbandler.nix:7`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/users/mrbandler/mrbandler.nix#L7)).
- Shared personal settings remain (§6a S; [`modules/aspects/development/vcs/_identity.nix:5`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/aspects/development/vcs/_identity.nix#L5)).
- Installer chooses first user/fixed IDs (§6a O; [`modules/tools/install.nix:75`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/tools/install.nix#L75)).
- Linux remains a declared migration limit ([`README.md:14`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L14)).

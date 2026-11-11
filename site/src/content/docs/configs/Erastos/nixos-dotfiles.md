---
title: "Erastos/nixos-dotfiles"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/erastos/nixos-dotfiles/)

- Upstream: [Erastos/nixos-dotfiles](https://github.com/Erastos/nixos-dotfiles)
- Reviewed revision: [`f2336347f41d`](https://github.com/Erastos/nixos-dotfiles/commit/f2336347f41da991f4e371e10cd01864109b4687)
- Author: Erastos
- Score: **34.0 / 100**, rank 95 of 101 ranked configs. D 2 · I 7 · S 4 · R 5 · P 5 · L 2 · V 2 · O 2 · B 3 · X 2. Shortlists: library units (1).
- Summary: Useful incremental wrapping of an existing native module tree; direct selection dominates Den composition, and native schemas coexist with author-specific shared settings.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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
Flake-parts/import-tree loads parts, whose den aspects wrap existing ordinary NixOS/HM modules ([`flake.nix:30`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/flake.nix#L30), [`parts/aspects/features/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L3)). Two host users and two standalone home outputs share the same identities ([`parts/hosts.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L2), [`parts/hosts.nix:8`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L8)).

## 2. Common patterns
- define-user+primary-user belong to netscape ([`parts/aspects/netscape.nix:4`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/netscape.nix#L4)).
- homes (standalone HM): host-qualified keys select matching user aspects ([`parts/hosts.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L7)).
- includes compose shared-nixos from feature wrappers ([`parts/aspects/features/shared.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L3)).

## 3. Novel patterns
Host-qualified standalone aspects select different compositor/color profiles while retaining the same feature module tree ([`parts/aspects/netscape.nix:12`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/netscape.nix#L12), [`parts/aspects/netscape.nix:20`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/netscape.nix#L20)).

## 4. Library candidates
- audio · [`parts/aspects/features/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L2) · imports a small PipeWire/PulseAudio-compatible server policy · inputs: NixOS/nixpkgs and local module ([`modules/system/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L2)) · parameterization: none · **B**, inline or bundle the six-line target module.

## 5. den friction
No verified den-specific friction in the reviewed wrappers/inventory ([`parts/aspects/features/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L3), [`parts/hosts.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L2)). The two module systems coexist intentionally; this is not itself a failure.

## 6. Docs and complexity
Docs **2**: host-qualified output intent is explained inline ([`parts/hosts.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L7)) but feature wrappers mostly delegate without teaching the underlying enable schema ([`parts/aspects/features/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L3)). Complexity **3**: shared feature wrappers and per-machine HM specializations across two hosts ([`parts/aspects/features/shared.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L3), [`parts/aspects/netscape.nix:12`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/netscape.nix#L12)).

## 6a. Defects and scoring notes

- **S · moderate:** seven grouped author adaptations remain in shared native modules: account, checkout, two wallpaper roots, printer address, output selector, encrypted credential asset ([`modules/system/users.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/users.nix#L3), [`modules/system/core/nix-settings.nix:13`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/core/nix-settings.nix#L13), [`modules/home/wm/niri.nix:80`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L80), [`modules/home/wm/niri.nix:501`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L501), [`modules/system/services.nix:54`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L54), [`modules/home/wm/niri.nix:223`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L223), [`modules/system/htb.nix:187`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/htb.nix#L187)).
Shared baseline HTTP/HTB/Docker choices are explicit feature options, not an additional forced isolation defect ([`parts/aspects/features/shared.nix:19`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L19)). Wrapper/import hops and honest narrow scope are not defects; non-9 limits above describe coverage.

## 7. Template notes
Useful for incremental den wrapping of existing module trees; the shared baseline includes more personal security tooling than a general template should ([`parts/aspects/features/shared.nix:20`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L20)).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Named hosts select shared wrappers and native feature flags directly ([`parts/aspects/Trinity.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/Trinity.nix#L3), [`parts/aspects/Trinity.nix:9`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/Trinity.nix#L9)); host-qualified home aspects choose ordinary profile settings ([`parts/aspects/netscape.nix:20`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/netscape.nix#L20)). Baseline2: this is useful selection, but no custom Den producer→policy/pipe→consumer channel is established by those definitions. Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Feature wrappers localize native module ownership ([`parts/aspects/features/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L3), [`parts/aspects/features/desktop.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/desktop.nix#L3)); native feature schemas keep optional services explicit ([`modules/system/services.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L7)). Seven interpolates between named-feature5 and isolated9 because the main shared host/home bundles aggregate many concerns ([`parts/aspects/features/shared.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L3), [`modules/home/default.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/default.nix#L2)). Deliberate overrideable baseline toggles are not charged as defects. Score **7**; confidence **high**.

### S

Scope · pros · cons/coverage: Native enable/theme/service options expose substantial variation ([`modules/home/editors.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/editors.nix#L7), [`modules/system/bloodhound-ce.nix:23`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L23)), but shared account and filesystem behavior still needs source edits ([`modules/system/users.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/users.nix#L3), [`modules/home/shell.nix:101`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/shell.nix#L101)), contract4 between embedded-author2 and mostly explicit5. Seven grouped adaptations: account identity ([`modules/system/security-extras.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/security-extras.nix#L3)); checkout root ([`modules/system/core/nix-settings.nix:13`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/core/nix-settings.nix#L13)); Pictures and Dropbox wallpaper roots ([`modules/home/wm/niri.nix:80`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L80), [`modules/home/wm/niri.nix:501`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L501)); printer address set ([`modules/system/services.nix:54`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L54), [`modules/system/services.nix:69`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L69)); DP-2 output ([`modules/home/wm/niri.nix:223`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L223)); encrypted HTB asset ([`modules/system/htb.nix:187`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/htb.nix#L187)). Repeated raw usernames/path occurrences group once; coverage6 cap gives min4. Overrideable Git name/email defaults are not hardcoded-contract defects ([`modules/home/git.nix:9`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/git.nix#L9)). Score **4**; confidence **medium**.

```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":7}}
```

### R

Scope · pros · cons/coverage: The nominated audio unit is a wrapper plus a six-line native module, requiring only bundling/inlining ([`parts/aspects/features/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L3), [`modules/system/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L2)), grade5. More substantial BloodHound has useful typed settings, but depends on another project-specific services schema ([`modules/system/bloodhound-ce.nix:10`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L10), [`modules/system/bloodhound-ce.nix:70`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L70)); it does not establish the independent A+minimal-consumer9 anchor. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Systems and actual host/home inventories explicitly limit scope to x86_64 Linux ([`parts/systems.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/systems.nix#L2), [`parts/hosts.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L2), [`parts/hosts.nix:8`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L8)). Honest narrow support5; architecture-specific kernel selection is consistent with that scope ([`parts/aspects/features/kernel-cachyos.nix:5`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/kernel-cachyos.nix#L5)) and is not an extra portability defect. Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: The SOPS guide provides concrete setup, editing and host-addition procedures ([`docs/SOPS-SETUP.md:13`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/docs/SOPS-SETUP.md#L13), [`docs/SOPS-SETUP.md:197`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/docs/SOPS-SETUP.md#L197)). It teaches that operational concern rather than Den feature selection, while topology intent is only an inline comment ([`parts/hosts.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L7)). Operation-focused2; an extra import hop itself is not a documentation defect. Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: BloodHound asserts its required runtime and services reject simultaneous Docker/Podman ([`modules/system/bloodhound-ce.nix:68`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L68), [`modules/system/services.nix:36`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L36)). These are useful configuration guards, but the flake entry only imports parts ([`flake.nix:30`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/flake.nix#L30)) and the reviewed parts declare no test fixture/check invocation. Baseline2; guards are not claimed as executed tests. Score **2**; confidence **high**.

### O

Scope · pros · cons/coverage: HTB keys are selected by the native OS hostname ([`modules/system/htb.nix:188`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/htb.nix#L188), [`modules/system/htb.nix:243`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/htb.nix#L243)), while secrets and NH retain a fixed file/checkout ([`modules/system/secrets.nix:4`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/secrets.nix#L4), [`modules/system/core/nix-settings.nix:13`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/core/nix-settings.nix#L13)). These operations are configured beside Den rather than generated from Den inventory, baseline2; the SOPS guide uses hand-named hosts ([`docs/SOPS-SETUP.md:17`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/docs/SOPS-SETUP.md#L17)). Score **2**; confidence **high**.

### X

Scope · pros · cons/coverage: Den outputs are ordinary Linux hosts and standalone homes ([`parts/hosts.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L2), [`parts/hosts.nix:8`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L8)); devShells are independently imported ([`parts/devshells.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/devshells.nix#L3)). Standard OS/home scope is2, with no separate first-class integration class established. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census enabled verified breadth is4.5points, diversity3. No complete substantive nonidentity application aspect qualifies: audio is only enable flags ([`modules/system/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L3)); osdev is installation-only ([`parts/aspects/features/osdev.nix:4`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/osdev.nix#L4)); BloodHound requires the external fleet services schema ([`modules/system/bloodhound-ce.nix:10`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L10)); services and desktop wrappers aggregate multiple applications ([`modules/system/services.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L7), [`modules/system/desktop/default.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/desktop/default.nix#L2)), while shared-hm is an import-only bundle ([`parts/aspects/features/shared.nix:26`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/shared.nix#L26)). Native editor/Tmux settings remain inside that broad home import, not independently exported application aspects ([`modules/home/default.nix:6`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/default.nix#L6)). Reference2 and diversity3 round to B3. Score **3**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":2,"reference_units":[]}}
```

**Total:** 34.0/100. **Shortlists:** showcase no; library audio; starter no. Useful incremental wrapping of an existing native module tree; direct selection dominates Den composition, and native schemas coexist with author-specific shared settings.

Overall pros:
- Native feature schemas make optional behavior explicit ([`modules/system/services.nix:7`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/services.nix#L7)).
- BloodHound validates its required container backend ([`modules/system/bloodhound-ce.nix:68`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/bloodhound-ce.nix#L68)).
- SOPS setup and adding recipients are documented ([`docs/SOPS-SETUP.md:197`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/docs/SOPS-SETUP.md#L197)).

Overall cons / scope limits:
- Shared account settings fix netscape ([`modules/system/users.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/users.nix#L3)).
- Shell helpers and NH assume the author checkout ([`modules/home/shell.nix:101`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/shell.nix#L101), [`modules/system/core/nix-settings.nix:13`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/core/nix-settings.nix#L13)).
- Wallpaper paths are fixed inside compositor code ([`modules/home/wm/niri.nix:80`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L80), [`modules/home/wm/niri.nix:501`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/home/wm/niri.nix#L501)).

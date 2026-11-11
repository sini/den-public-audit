---
title: "moxie0420/dotfiles"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/moxie0420/dotfiles/)

- Upstream: [moxie0420/dotfiles](https://github.com/moxie0420/dotfiles)
- Reviewed revision: [`42df6003db8c`](https://github.com/moxie0420/dotfiles/commit/42df6003db8cf97408656e9fef28d66459c3c8eb)
- Author: moxie0420
- Score: **44.5 / 100**, rank 72 of 101 ranked configs. D 6 · I 8 · S 3 · R 5 · P 4 · L 2 · V 3 · O 2 · B 6 · X 2. Shortlists: library units (1).
- Summary: D routed address chain; I feature ownership; S limited validation and 14 grouped leaks; R small B leaf; P HM typo; L stale map; V uninvo­ked topology checks; O manual deployment; X standard targets; B census plus complete app-unit inventory.

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

An import-tree flake loads dendritic modules and a sizeable desktop/server feature tree ([`flake.nix:141`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/flake.nix#L141), [`modules/dendritic.nix:7`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/dendritic.nix#L7)). Host metadata feeds service aggregation policies rather than only selecting static includes ([`modules/policies/pipes.nix:6`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L6)).


## 2. Common patterns.

- namespace: six namespaces expose desktop, class, hardware, program, service and system aspects ([`modules/namespaces.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/namespaces.nix#L10)).
- policies + quirks: collect HTTP backends and host addresses through policy pipes ([`modules/policies/pipes.nix:6`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L6)).
- custom schema/classes: address/domain/tailnet fields extend the host schema ([`modules/schema.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/schema.nix#L3)).


## 3. Novel patterns.

hostfile emits address/name data ([`modules/aspects/system/hostfile.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/hostfile.nix#L3)), collect-host-addrs routes it ([`modules/policies/pipes.nix:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L12)), and the NixOS consumer renders extraHosts ([`modules/aspects/system/hostfile.nix:17`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/hostfile.nix#L17)). HTTP backends are emitted ([`modules/aspects/services/networking/caddy/caddy.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/networking/caddy/caddy.nix#L3)) but no HTTP backend consumer was verified; do not infer one from the declaration alone.


## 4. Library candidates.

- ripgrep · [`modules/aspects/programs/ripgrep.nix:2`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ripgrep.nix#L2) · system package and HM enablement · nixpkgs/HM plus a `programs` namespace · none · B: replace namespace binding or package as a namespaced aspect.


## 5. den friction.

No verified den-specific workaround in the inspected namespace and policy modules ([`modules/namespaces.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/namespaces.nix#L10), [`modules/policies/pipes.nix:29`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L29)).


## 6. Docs and complexity.

Docs 2: README has a contents map but still describes modules as only a theme and asks for documentation ([`README.md:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L12), [`README.md:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L27)). Complexity 5: custom schema, namespace and policy aggregation coexist with three live host records ([`modules/hosts.nix:29`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L29), [`modules/schema.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/schema.nix#L3), [`modules/policies/pipes.nix:6`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L6)).


## 6a. Defects and scoring notes.

- L · moderate: README modules description contradicts the live tree ([`README.md:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L27), [`modules/namespaces.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/namespaces.nix#L10)).
- S · moderate: 14 grouped author-specific adaptation values remain in shared application/default bodies; enumerated with citations in S card ([`modules/aspects/system/nix.nix:104`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/nix.nix#L104), [`modules/aspects/services/vaultwarden.nix:17`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/vaultwarden.nix#L17)).
- P · moderate: homeManger misspelling prevents the Zoxide arm from being a homeManager contribution ([`modules/aspects/system/shell/zoxide.nix:24`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/shell/zoxide.nix#L24)).
- O · minor: deploy duplicates theHub endpoint rather than deriving its target from host metadata ([`modules/deploy-rs.nix:14`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L14), [`modules/hosts.nix:46`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L46)).
The former namespace-only ripgrep portability note is an adaptation prerequisite, not a defect; removed without a deduction.

## 7. Template notes.

Useful advanced policy example; update the README and remove personal address/domain fields before presenting it as a starter ([`README.md:25`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L25), [`modules/hosts.nix:35`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L35)).

## 8. Scorecard.

### D
Scope: host-address channel and class routes. Pros: address/name emission ([`modules/aspects/system/hostfile.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/hostfile.nix#L3)) → schema-attached collect pipe ([`modules/policies/pipes.nix:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L12), [`modules/policies/pipes.nix:29`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L29)) → extraHosts ([`modules/aspects/system/hostfile.nix:17`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/hostfile.nix#L17)), selected by two addressed hosts ([`modules/aspects/hosts/nixUwU/nixUwU.nix:22`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/hosts/nixUwU/nixUwU.nix#L22), [`modules/aspects/hosts/theHub/theHub.nix:13`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/hosts/theHub/theHub.nix#L13)). Cons: no explicit null-address or duplicate-name checks at consumer; unselected laptop does not emit. Above 5 for live routed collection; below 9 for single-consumer/implicit merge semantics. HTTP backend consumer remains unknown, earning no extra credit ([`modules/policies/pipes.nix:6`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L6)). Score **6**; confidence **medium**.

### I
Scope: namespaces, defaults and service boundaries. Pros: independent application owners and optional Caddy children ([`modules/aspects/services/multimedia/immich.nix:11`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/immich.nix#L11)). Cons: broad baseline includes printing and desktop-oriented shell choices on every host ([`modules/aspects/defaults.nix:45`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/defaults.nix#L45), [`modules/aspects/defaults.nix:57`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/defaults.nix#L57)); scope ceiling rather than a second S deduction. Near 9 ownership, interpolated 8 for the broad mandatory baseline. Score **8**; confidence **medium**.

### S
Scope: host schema and inspected shared application bodies. Pros: host domain/storage/address facts are consumed contextually ([`modules/hosts.nix:39`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L39), [`modules/aspects/services/multimedia/muxarr.nix:28`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/muxarr.nix#L28)). Cons: contract grade 3: metadata has null defaults without types/validation ([`modules/schema.nix:5`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/schema.nix#L5)), while shared bodies retain personal values. Grouped coverage grade 5: 14 adaptation groups, not raw occurrences: owner identity; checkout root; CA asset; timezone; router address; Hub address; storage root; NixUwU label; moxiege.com domain family; tailnet domain family; tunnel UUID; SSO client ID; immich.lan alias; thehub.lan alias ([`modules/aspects/system/nix.nix:91`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/nix.nix#L91), [`modules/aspects/system/nix.nix:104`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/nix.nix#L104), [`modules/aspects/defaults.nix:24`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/defaults.nix#L24), [`modules/aspects/defaults.nix:32`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/defaults.nix#L32), [`modules/aspects/programs/ssh.nix:21`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ssh.nix#L21), [`modules/aspects/programs/ssh.nix:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ssh.nix#L27), [`modules/aspects/services/multimedia/aurral.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/aurral.nix#L10), [`modules/aspects/programs/hyfetch.nix:178`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/hyfetch.nix#L178), [`modules/aspects/services/forgejo.nix:84`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/forgejo.nix#L84), [`modules/aspects/services/vaultwarden.nix:17`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/vaultwarden.nix#L17), [`modules/aspects/services/cloudflare.nix:16`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/cloudflare.nix#L16), [`modules/aspects/services/vaultwarden.nix:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/vaultwarden.nix#L27), [`modules/aspects/services/blocky.nix:47`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/blocky.nix#L47), [`modules/aspects/services/blocky.nix:49`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/blocky.nix#L49)). Subpaths/subdomains collapse into these groups; min(3,5)=3. Score **3**; confidence **medium**.
```score-evidence
{"S":{"contract_design":3,"leak_coverage":5,"distinct_leaks":14}}
```

### R
Scope: existing §4 ripgrep contract. Pros: stock package/HM feature can be extracted by rebinding one namespace ([`modules/aspects/programs/ripgrep.nix:1`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ripgrep.nix#L1)). Cons: this small grade-B leaf supplies enablement, not a substantial documented A-unit consumer package ([`modules/aspects/programs/ripgrep.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ripgrep.nix#L3)). Literal 5; namespace binding is adoption work, not itself a defect. Score **5**; confidence **medium**.

### P
Scope: actual Linux hosts and OS/HM arms. Pros: NixOS versus home ownership is explicit ([`modules/aspects/programs/kitty.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/kitty.nix#L3), [`modules/aspects/programs/kitty.nix:39`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/kitty.nix#L39)). Cons: Zoxide home arm is misspelled homeManger and therefore is not the homeManager contribution ([`modules/aspects/system/shell/zoxide.nix:24`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/shell/zoxide.nix#L24)). Below honest-narrow 5 for this concrete boundary defect; ARM listed output systems alone do not prove ARM host support ([`modules/hosts.nix:85`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L85)). Score **4**; confidence **medium**.

### L
Scope: README and feature entry. Pros: contents links offer a starting map ([`README.md:23`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L23)). Cons: README says modules contain only a theme, contradicting current tree ([`README.md:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L27), [`modules/namespaces.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/namespaces.nix#L10)). Literal 2: operation/placeholder-level authoring guidance. Score **2**; confidence **medium**.

### V
Scope: deploy checks, generated config validation, CI. Pros: deployChecks defined ([`modules/deploy-rs.nix:7`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L7)) and greeter config gets a native validator ([`modules/aspects/programs/regreet.nix:26`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/regreet.nix#L26)). Cons: CI builds a fixed theme-package list, not these topology checks ([`.github/workflows/cache.yml:18`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/.github/workflows/cache.yml#L18)). Interpolated 3 above absence for meaningful definitions, below representative invoked host checks; passing unknown. Score **3**; confidence **medium**.

### O
Scope: deployment and bootstrap. Pros: deploy path consumes the generated host output ([`modules/deploy-rs.nix:18`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L18)). Cons: target/IP are hand-maintained and only cover theHub ([`modules/deploy-rs.nix:14`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L14), [`modules/hosts.nix:46`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/hosts.nix#L46)); PXE also fixes its operator key ([`modules/aspects/services/pixiecore.nix:26`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/pixiecore.nix#L26)). Literal 2: no operational target inventory derived from Den facts. Score **2**; confidence **medium**.

### X
Scope: custom Niri settings route. Pros: class fragment is deliberately routed into HM programs.niri.settings ([`modules/classes/niri.nix:9`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/classes/niri.nix#L9)). Cons: consumer remains a standard OS/home configuration, with no independent non-host target family ([`modules/classes/niri.nix:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/classes/niri.nix#L12)). Baseline 2; wrapper mechanism is not credited again as a new target. Score **2**; confidence **medium**.

### B
Scope: census max-depth families plus complete inspected application units. Pros: required-family settings are substantive; list below enumerates every counted self-contained unit, counting multi-file apps once ([`modules/aspects/programs/starship.nix:22`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/starship.nix#L22)). Cons: enable-only leaves such as ripgrep and tealdeer, include-only arrstack, personal service/storage leaves, and units requiring unrelated fleet packaging are excluded ([`modules/aspects/programs/ripgrep.nix:3`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ripgrep.nix#L3), [`modules/aspects/services/arrstack.nix:7`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/arrstack.nix#L7)). Also excluded: Immich/Jellyfin/Lidarr/Tdarr require external fleet aspect/schema names; Snapcast presumes an externally produced /tmp/snapfifo stream ([`modules/aspects/services/multimedia/jellyfin.nix:9`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/jellyfin.nix#L9), [`modules/aspects/services/multimedia/tdarr.nix:18`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/tdarr.nix#L18), [`modules/aspects/services/multimedia/snapcast.nix:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/snapcast.nix#L27)). FZF explicitly enables completion and keybindings ([`modules/aspects/programs/fzf.nix:10`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/fzf.nix#L10)); exact root nixpkgs31ecbaca1bdefa45dffc409f0250bd8039ea0010 nixos/modules/programs/fzf.nix consumes both switches into shell initialization. B arithmetic follows the census and enumerated list. Score **6**; confidence **medium**.
B_div: 4 points → 3; B_ref: 20 units → 9; half-up mean → 6.
```score-evidence
{"B":{"diversity_points":4,"diversity_grade":3,"reference_grade":9,"reference_units":[{"name":"direnv","evidence":"modules/aspects/programs/direnv.nix:11"},{"name":"discord","evidence":"modules/aspects/programs/discord.nix:15"},{"name":"firefox","evidence":"modules/aspects/programs/firefox.nix:6"},{"name":"gamescope","evidence":"modules/aspects/programs/gamescope.nix:2"},{"name":"git","evidence":"modules/aspects/programs/git.nix:2"},{"name":"kitty","evidence":"modules/aspects/programs/kitty.nix:2"},{"name":"mpv","evidence":"modules/aspects/programs/mpv.nix:2"},{"name":"nautilus","evidence":"modules/aspects/programs/nautilus.nix:2"},{"name":"obs-studio","evidence":"modules/aspects/programs/obs-studio.nix:2"},{"name":"starship","evidence":"modules/aspects/programs/starship.nix:2"},{"name":"waydroid","evidence":"modules/aspects/programs/waydroid.nix:2"},{"name":"openssh","evidence":"modules/aspects/services/openssh.nix:2"},{"name":"printing","evidence":"modules/aspects/services/hardware/printing.nix:2"},{"name":"bat","evidence":"modules/aspects/system/shell/bat.nix:2"},{"name":"eza","evidence":"modules/aspects/system/shell/eza.nix:11"},{"name":"mako","evidence":"modules/aspects/desktop/notifications.nix:2"},{"name":"cliphist","evidence":"modules/aspects/desktop/wayland.nix:3"},{"name":"pipewire","evidence":"modules/aspects/desktop/audio.nix:2"},{"name":"polkit","evidence":"modules/aspects/desktop/polkit.nix:2"},{"name":"fzf","evidence":"modules/aspects/programs/fzf.nix:2"}]}}
```

Total: **44.5/100**. Shortlists: showcase false; library_units ['ripgrep']; starter false.

Overall pros:
- Real routed host-address rendering ([`modules/policies/pipes.nix:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/policies/pipes.nix#L12)).
- Optional service integrations stay with their service owner ([`modules/aspects/services/multimedia/jellyfin.nix:12`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/services/multimedia/jellyfin.nix#L12)).
- Substantive independent application presets ([`modules/aspects/programs/firefox.nix:114`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/firefox.nix#L114)).

Overall cons / limits:
- Personal variation leaks remain in shared implementation (§6a S; [`modules/aspects/system/nix.nix:104`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/nix.nix#L104)).
- Zoxide HM arm misspelling (§6a P; [`modules/aspects/system/shell/zoxide.nix:24`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/system/shell/zoxide.nix#L24)).
- README wiring map is stale (§6a L; [`README.md:27`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/README.md#L27)).
- Operations keep a separate host/IP declaration (§6a O; [`modules/deploy-rs.nix:14`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L14)).

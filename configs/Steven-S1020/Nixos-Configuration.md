# Steven-S1020/Nixos-Configuration

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/Steven-S1020/Nixos-Configuration.md)

- Upstream: [Steven-S1020/Nixos-Configuration](https://github.com/Steven-S1020/Nixos-Configuration)
- Reviewed revision: [`89fd086f61a5`](https://github.com/Steven-S1020/Nixos-Configuration/commit/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c)
- Author: Steven-S1020
- Score: **36.0 / 100**, rank 92 of 101 ranked configs. D 3 · I 7 · S 2 · R 5 · P 5 · L 3 · V 2 · O 2 · B 4 · X 2. Shortlists: library units (1).
- Summary: D literal context branch; I copied composition; S personal settings without contract; R independent audio; P honest Linux; L stale framework text; V no checks; O manual; X baseline; B nine coherent presets.

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

Flake-parts/import-tree loads two NixOS hosts and nested system/program/desktop aspects ([`flake.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/flake.nix#L2), [`modules/hosts/deimos/deimos.nix:6`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L6)). Angle references and provides.to-users separate user desktop features from system services ([`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9)).


## 2. Common patterns.

- angle-bracket refs: den __findFile backs feature paths ([`modules/den.nix:3`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/den.nix#L3), [`modules/hosts/deimos/deimos.nix:11`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L11)).
- define-user+primary-user: defaults define users and the steven aspect selects primary-user ([`modules/defaults.nix:22`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/defaults.nix#L22), [`modules/users/steven.nix:5`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/users/steven.nix#L5)).
- provides tree: host-specific to-users includes carry desktop and graphical applications ([`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9)).


## 3. Novel patterns.

Host-specific Stylix font sizes coexist with a shared desktop provider set ([`modules/hosts/azami/azami.nix:43`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L43), [`modules/hosts/deimos/deimos.nix:47`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L47)).


## 4. Library candidates.

- system/audio · [`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2) · PipeWire, ALSA/Pulse/JACK and rtkit · NixOS/nixpkgs · none · A: self-contained audio feature after lifting the namespace.


## 5. den friction.

No verified den-specific workaround in the inspected defaults and user provider wiring ([`modules/defaults.nix:21`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/defaults.nix#L21), [`modules/users/steven.nix:3`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/users/steven.nix#L3)).


## 6. Docs and complexity.

Docs 3: README introduces the daily-use hosts and copying expectations ([`README.md:11`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L11)); source labels user and system feature groups ([`modules/hosts/deimos/deimos.nix:10`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L10), [`modules/hosts/deimos/deimos.nix:23`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L23)). Complexity 3: two hosts share nested user/system features with local hardware/application overrides ([`modules/hosts/azami/azami.nix:6`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L6), [`modules/hosts/deimos/deimos.nix:36`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L36)).


## 6a. Defects and scoring notes.

- I · moderate: copied host selection lists require parallel edits ([`modules/hosts/azami/azami.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L9), [`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9)).
- S · moderate: nine grouped personal/environment adaptation values lack a local contract, listed in S ([`modules/system/syncthing.nix:13`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/syncthing.nix#L13), [`modules/desktop/hyprland.nix:26`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/hyprland.nix#L26)).
- R · moderate: generated Empty-Flake references system and pkgs without binding either ([`modules/programs/configs/mkdev.nix:53`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/mkdev.nix#L53), [`modules/programs/configs/mkdev.nix:56`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/mkdev.nix#L56)). Fastfetch references capital Assets but tracked directory is assets ([`modules/programs/configs/fastfetch.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/fastfetch.nix#L9)).
- L · moderate: README explains outdated parametric/take API and wrong HM class alias ([`README.md:120`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L120), [`README.md:125`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L125)).
Commented debug scaffolding is inactive explanation, not independently a defect.

## 7. Template notes.

Good example of host-to-user provisioning; explain the provider route before copying the nearly identical host lists ([`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9), [`modules/hosts/azami/azami.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L9)).

## 8. Scorecard.

### D
Scope: host context used by desktop. Pros: Hyprland generates local monitor settings from host.hostName ([`modules/desktop/hyprland.nix:26`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/hyprland.nix#L26)). Cons: literal Deimos branch and direct settings, no routed fact channel ([`modules/desktop/noctalia.nix:56`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/noctalia.nix#L56)). Interpolated3 for live context selection above2, literal peer/hostname branches cannot justify6. Score **3**; confidence **medium**.

### I
Scope: feature owners and host composition. Pros: audio, desktop and app concerns are localized ([`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2), [`modules/programs/cli.nix:4`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/cli.nix#L4)). Cons: nearly identical graphical and system lists are maintained separately per host ([`modules/hosts/azami/azami.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L9), [`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9)). Interpolated7: useful ownership above5, avoidable parallel composition below9. Score **7**; confidence **medium**.

### S
Scope: personal presets. Pros: host context separates a monitor branch ([`modules/desktop/hyprland.nix:26`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/hyprland.nix#L26)); ordinary module overrides remain available. Cons: no purposeful local option surface; contract2. Nine adaptation groups: owner identity/home/key paths, checkout root, Azami Syncthing ID, Deimos Syncthing ID, Vigil address, Deimos hostname branch, monitor topology, IR camera, household locale ([`modules/programs/configs/git.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/git.nix#L9), [`modules/programs/configs/zsh.nix:11`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/zsh.nix#L11), [`modules/system/syncthing.nix:13`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/syncthing.nix#L13), [`modules/system/syncthing.nix:16`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/syncthing.nix#L16), [`modules/system/networking.nix:20`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/networking.nix#L20), [`modules/desktop/hyprland.nix:26`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/hyprland.nix#L26), [`modules/desktop/hyprland.nix:31`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/desktop/hyprland.nix#L31), [`modules/system/howdy.nix:30`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/howdy.nix#L30), [`modules/system/locale.nix:3`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/locale.nix#L3)). Coverage6; repeated identity/domain occurrences grouped. min(2,6)=2. Score **2**; confidence **medium**.
```score-evidence
{"S":{"contract_design":2,"leak_coverage":6,"distinct_leaks":9}}
```

### R
Scope: independent audio and app definitions. Pros: audio owns its PipeWire compatibility/rtkit settings with no personal values ([`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2)). Cons: no extraction guide or second consumer, and several native configurations rely on /etc/nixos ([`modules/programs/configs/neovim.nix:47`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/neovim.nix#L47)). Literal5 useful A leaf, not9 documented substantial package. Score **5**; confidence **medium**.

### P
Scope: honest two-host Linux/HM support. Pros: OS audio and HM terminal classes are separated ([`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2), [`modules/programs/configs/kitty.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/kitty.nix#L2)). Cons: no Darwin/standalone-home boundary claims or tests; fixed IR device is charged S, not twice ([`modules/system/howdy.nix:30`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/howdy.nix#L30)). Literal5 for narrow scope, no platform-count bonus. Score **5**; confidence **medium**.

### L
Scope: README installation and framework explanation. Pros: host roles, inputs and install route are described ([`README.md:28`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L28), [`README.md:133`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L133)). Cons: explains old parametric API and misidentifies homeManager as users.users; mentions NVF absent from current imports ([`README.md:120`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L120), [`README.md:125`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L125), [`README.md:76`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L76)). Interpolated3 for useful operator context above2 but misleading authoring guidance below5. Score **3**; confidence **medium**.

### V
Scope: flake and operator commands. Pros: reproducible import-tree entry ([`flake.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/flake.nix#L2)). Cons: just validate only authenticates sudo, not composition; no relevant checks verified ([`justfile:51`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/justfile#L51)). Literal2, static inspection is not a successful check run. Score **2**; confidence **medium**.

### O
Scope: operator activation. Pros: just wraps nh rebuild/update ([`justfile:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/justfile#L9), [`justfile:26`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/justfile#L26)). Cons: wrappers do not derive operational artifacts or deployment inventory from Den ([`modules/den.nix:5`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/den.nix#L5)). Literal2 manual operation; keyring is desktop credential service, not Den secret inventory. Score **2**; confidence **medium**.

### X
Scope: NixOS/HM desktop. Pros: ordinary input packages are architecture-selected through inputs prime ([`modules/programs/graphical.nix:18`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/graphical.nix#L18)). Cons: no non-host target class at root ([`flake.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/flake.nix#L2)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: all coherent independent presets plus enabled census diversity. Pros: Kitty, Starship, audio and Ly have several related settings; FZF explicitly wires Zsh integration and Direnv wires nix-direnv ([`modules/programs/configs/kitty.nix:7`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/kitty.nix#L7), [`modules/programs/configs/starship.nix:8`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/starship.nix#L8), [`modules/programs/configs/fzf.nix:7`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/fzf.nix#L7), [`modules/programs/configs/nix-direnv.nix:5`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/nix-direnv.nix#L5)). Cons: Git/Syncthing/Hyprland are identity/topology-bound; shells call unowned commands; Btop launches unowned Kitty; Fastfetch path case differs from tracked assets; MKdev recipe has undefined variables ([`modules/programs/configs/git.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/git.nix#L9), [`modules/programs/configs/bash.nix:7`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/bash.nix#L7), [`modules/programs/configs/btop.nix:19`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/btop.nix#L19), [`modules/programs/configs/fastfetch.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/fastfetch.nix#L9), [`modules/programs/configs/mkdev.nix:56`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/mkdev.nix#L56)). No extracted cores counted. Score **4**; confidence **medium**.
B_div: 5 points → 3; B_ref: 9 units → 5; half-up mean → 4.
```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":5,"reference_units":[{"name":"pipewire","evidence":"modules/system/audio.nix:2"},{"name":"ly","evidence":"modules/system/dm.nix:3"},{"name":"kitty","evidence":"modules/programs/configs/kitty.nix:5"},{"name":"starship","evidence":"modules/programs/configs/starship.nix:5"},{"name":"direnv","evidence":"modules/programs/configs/nix-direnv.nix:3"},{"name":"fzf","evidence":"modules/programs/configs/fzf.nix:5"},{"name":"wireshark","evidence":"modules/programs/configs/wireshark.nix:9"},{"name":"tailscale","evidence":"modules/system/tailscale.nix:5"},{"name":"stylix","evidence":"modules/system/stylix.nix:8"}]}}
```

Total: **36.0/100**. Shortlists: showcase false; library_units ['system/audio']; starter false.

Overall pros:
- Clear audio unit ([`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2)).
- Host-to-user desktop selection ([`modules/hosts/deimos/deimos.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L9)).
- Tracked native editor configuration ([`modules/programs/configs/_neovim/init.lua:3`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/_neovim/init.lua#L3)).

Overall cons / limits:
- Copied host composition (§6a I; [`modules/hosts/azami/azami.nix:9`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/azami/azami.nix#L9)).
- Personal values lack configuration surface (§6a S; [`modules/system/syncthing.nix:13`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/syncthing.nix#L13)).
- Framework explanation is stale (§6a L; [`README.md:125`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/README.md#L125)).
- Generated Empty-Flake references undefined variables (§6a R; [`modules/programs/configs/mkdev.nix:56`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/programs/configs/mkdev.nix#L56)).

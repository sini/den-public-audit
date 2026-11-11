# jkopano/nixiak

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/jkopano/nixiak.md)

- Upstream: [jkopano/nixiak](https://github.com/jkopano/nixiak)
- Reviewed revision: [`97bf0689bb4d`](https://github.com/jkopano/nixiak/commit/97bf0689bb4d587a51199058a7ee2c89f5d4c204)
- Author: jkopano
- Score: **47.5 / 100**, rank 61 of 101 ranked configs. D 5 · I 6 · S 4 · R 7 · P 5 · L 5 · V 5 · O 2 · B 5 · X 2. Shortlists: library units (1).
- Summary: Context-derived outputs and useful closed application presets coexist with shared owner assumptions and a real declared CI workflow. Repeated remap literal sets have disjoint children and merge legally.

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

Den’s flake module derives systems from declared hosts ([`modules/den.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L8)). Shared defaults and personal desktop features are separate ([`modules/defaults.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L8)).

## 2. Common patterns

- angle-bracket refs select define-user ([`modules/defaults.nix:70`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L70)).
- den.default includes installs shared behavior ([`modules/defaults.nix:68`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L68)).

## 3. Novel patterns

Deriving systems directly from host inventory keeps output platform selection synchronized ([`modules/den.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L8)).

## 4. Library candidates

**OpenSSH client/agent** — [`modules/services/ssh.nix:3`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L3): configures the agent plus native client keepalive/multiplexing policy ([`modules/services/ssh.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L6), [`modules/services/ssh.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L9)). Inputs: Den and ordinary Home Manager; no private settings or app-specific flake input. Parameterization: none required, native SSH options remain available. Reuse **A**: retain the aspect’s native module body and select it from a new home; no author identity replacement is needed.

## 5. den friction

No verified Den-specific friction in the reviewed entry module ([`modules/den.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L9)).

## 6. Docs and complexity

Docs 3: README names targets and usage ([`README.md:5`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L5), [`README.md:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L11)) and clearly limits reuse ([`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)). Complexity 3: multiple named targets ([`README.md:7`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L7)) with shared defaults ([`modules/defaults.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L8)).

## 6a. Defects and scoring notes

**P moderate:** the shared Helix C# formatter uses an owner absolute executable path ([`modules/tui/helix/default.nix:258`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/helix/default.nix#L258)), so another home lacks that formatter unless it recreates the path. Explicit Linux-only support is an honest limit ([`README.md:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L9)).

## 7. Template notes

Good concise angle-reference example; author explicitly describes it as machine-specific ([`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)).

## 8. Scorecard

### D (5, high)
Score: 5. Confidence: high. Scope: context and output facts. Pros: host inventory determines systems ([`modules/den.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L8)), and host context sets the native hostname ([`modules/defaults.nix:73`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L73)). Cons: this is entity/context derivation, with explicit feature selection rather than policy/pipe routing ([`modules/hosts/jkopano/default.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/hosts/jkopano/default.nix#L9)); cap 5.

### I (6, high)
Score: 6. Confidence: high. Scope: feature integration. Pros: Niri owns its upstream module import and local settings/binds/theme closure ([`modules/wayland/niri/default.nix:10`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/niri/default.nix#L10), [`modules/wayland/niri/default.nix:24`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/niri/default.nix#L24)). Cons / limit: broad host profiles and global defaults still determine much of composition ([`modules/hosts/jkopano/default.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/hosts/jkopano/default.nix#L9), [`modules/defaults.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L8)). Interpolation 6 for coherent local ownership beyond 5, without the stronger optional isolation of 9. The repeated remap literal sets have disjoint children and merge legally ([`modules/hardware/keyboard.nix:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/hardware/keyboard.nix#L26), [`modules/hardware/keyboard.nix:29`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/hardware/keyboard.nix#L29)); no parse deduction applies.

### S (4, medium)
Score: 4. Confidence: medium. Scope: shared settings, not correctly scoped host hardware. Pros: personal machine details have an explicit host envelope ([`modules/hosts/jkopano/default.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/hosts/jkopano/default.nix#L9)). Cons: shared vars hardcode identity, checkout and vault layout ([`modules/vars.nix:14`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L14), [`modules/vars.nix:17`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L17), [`modules/vars.nix:29`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L29)), Rclone fixes a peer/account/root ([`modules/services/rclone.nix:15`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/rclone.nix#L15), [`modules/services/rclone.nix:16`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/rclone.nix#L16), [`modules/services/rclone.nix:20`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/rclone.nix#L20)), and shared desktop/scripts assume a monitor arrangement, backlight and wallpaper ([`modules/wayland/shikane.nix:14`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/shikane.nix#L14), [`modules/cli/scripts/_brightness-control.nix:4`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/cli/scripts/_brightness-control.nix#L4), [`modules/wayland/noctalia.nix:191`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/noctalia.nix#L191)); Git identity and weather/locale add scope work ([`modules/services/git.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/git.nix#L6), [`modules/vars.nix:19`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L19)). Ten grouped changes (at least 15 raw sites) cap coverage at 6; contract 4 controls S.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":6,"distinct_leaks":10,"raw_leaks":15}}
```

### R (7, high)
Score: 7. Confidence: high. Scope: best independent units. Pros: OpenSSH client/agent is a complete ordinary Home Manager envelope without caller fleet fields ([`modules/services/ssh.nix:3`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L3), [`modules/services/ssh.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L6)); Picom is similarly closed ([`modules/x11/picom.nix:4`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/x11/picom.nix#L4)). Cons: no independent consumer example is documented, and the author explicitly recommends snippets rather than whole-repo reuse ([`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)). Interpolation 7: useful A units, short of the documented consumer required for 9.

### P (5, high)
Score: 5. Confidence: high. Scope: declared Linux consumers. Pros: native host and standalone home share feature selection ([`modules/den.nix:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L11), [`modules/users/kuba.nix:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/users/kuba.nix#L9)). Cons / limit: shared Helix invokes an absolute owner tool path ([`modules/tui/helix/default.nix:258`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/helix/default.nix#L258)); no portable alternative is supplied there. The explicitly Linux-only support promise is not itself a defect ([`README.md:9`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L9)).

### L (5, high)
Score: 5. Confidence: high. Scope: onboarding. Pros: README identifies targets and gives rebuild/switch/update commands ([`README.md:7`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L7), [`README.md:14`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L14), [`README.md:17`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L17), [`README.md:20`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L20)). Cons: it explicitly limits reuse to snippets and supplies no independent app consumer walkthrough ([`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)). Usable owner instructions meet the 5 anchor.

### V (5, high)
Score: 5. Confidence: high. Scope: declared validation. Pros: CI evaluates the current and updated host output and runs a build dry-run ([`.github/workflows/flake-update-check.yml:36`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L36), [`.github/workflows/flake-update-check.yml:51`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L51), [`.github/workflows/flake-update-check.yml:56`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L56)). Cons / limit: those commands target one named host rather than an independent consumer matrix ([`.github/workflows/flake-update-check.yml:36`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L36)); their success has not been observed.

### O (2, high)
Score: 2. Confidence: high. Scope: lifecycle derivation. Pros: a fixed WSL deployment/check definition exists ([`modules/wsl.nix:41`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L41), [`modules/wsl.nix:58`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L58)). Cons: it is a separate literal node list, not operations derived from Den host facts ([`modules/wsl.nix:41`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L41)); auto-upgrade is disabled ([`modules/base.nix:12`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/base.nix#L12)). Baseline 2.

### B (5, medium)
Score: 5. Confidence: medium. Scope: all visible substantive app envelopes, not package/profile counts. Pros: ten complete units are inventoried below, including theme, shell, network, audio and X11 presets ([`modules/stylix.nix:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/stylix.nix#L11), [`modules/services/tailscale.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/tailscale.nix#L6), [`modules/x11/rofi.nix:21`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/x11/rofi.nix#L21)). Cons / limits: Nvim/Helix require outside Stylix/fleet settings ([`modules/tui/nvim/default.nix:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/nvim/default.nix#L11), [`modules/tui/helix/default.nix:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/helix/default.nix#L11)); Firefox also requires fleet PWA data ([`modules/gui/browser/default.nix:7`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/gui/browser/default.nix#L7)); personal Git and Rclone are excluded ([`modules/services/git.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/git.nix#L6), [`modules/services/rclone.nix:15`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/rclone.nix#L15)). Broad multi-app terminal/profile bodies and helper scripts are not split into artificial units ([`modules/gui/terminal.nix:34`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/gui/terminal.nix#L34), [`modules/cli/scripts/default.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/cli/scripts/default.nix#L6)); Tmux/Yazi commands require tools outside their own envelope ([`modules/tui/tmux/sesh.nix:19`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/tmux/sesh.nix#L19), [`modules/tui/yazi/_yazi.nix:130`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/yazi/_yazi.nix#L130)). Census diversity 7 points→5; reference 10→5; B=5.
```score-evidence
{"B":{"diversity_points":7.0,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"Plymouth/systemd boot preset","evidence":"modules/bootloader.nix:9"},{"name":"PipeWire audio","evidence":"modules/hardware/audio.nix:18"},{"name":"Bluez desktop preset","evidence":"modules/hardware/bluetooth.nix:8"},{"name":"OpenSSH client/agent","evidence":"modules/services/ssh.nix:6"},{"name":"Tailscale networking","evidence":"modules/services/tailscale.nix:6"},{"name":"Stylix desktop theme","evidence":"modules/stylix.nix:11"},{"name":"Starship prompt","evidence":"modules/cli/starship.nix:6"},{"name":"Zsh credential/shell integration","evidence":"modules/cli/zsh/default.nix:22"},{"name":"Picom compositor preset","evidence":"modules/x11/picom.nix:7"},{"name":"Rofi launcher preset","evidence":"modules/x11/rofi.nix:21"}]}}
```

### X (2, high)
Score: 2. Confidence: high. Scope: non-host classes. Pros / limit: WSL still builds an ordinary NixOS target ([`modules/wsl.nix:24`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L24)); the app classes shown are native Home Manager ([`modules/gui/terminal.nix:3`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/gui/terminal.nix#L3)). Cons: no additional non-operational target kind is demonstrated by these outputs ([`modules/den.nix:11`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L11), [`modules/wsl.nix:24`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L24)). Baseline 2.

Total: **47.5/100**. Shortlists: showcase no; library_units OpenSSH client/agent; starter no. The OpenSSH client/agent merits a library shortlist; shared owner settings and limited independent adoption instructions do not support a starter or showcase shortlist ([`modules/vars.nix:17`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L17), [`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)).

Overall pros:
- Inventory-derived systems and hostname ([`modules/den.nix:8`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/den.nix#L8), [`modules/defaults.nix:73`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/defaults.nix#L73)).
- Closed OpenSSH client/agent and Picom units ([`modules/services/ssh.nix:3`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L3), [`modules/x11/picom.nix:4`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/x11/picom.nix#L4)).
- Niri owns upstream import and local feature closure ([`modules/wayland/niri/default.nix:10`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/niri/default.nix#L10), [`modules/wayland/niri/default.nix:24`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wayland/niri/default.nix#L24)).
- Meaningful current/updated output checks are declared ([`.github/workflows/flake-update-check.yml:36`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L36), [`.github/workflows/flake-update-check.yml:51`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/.github/workflows/flake-update-check.yml#L51)).

Overall cons / limits:
- Shared owner checkout and identity require replacement ([`modules/vars.nix:14`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L14), [`modules/vars.nix:17`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/vars.nix#L17), [`modules/services/git.nix:6`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/git.nix#L6)).
- Helix formatter assumes an owner absolute tool path ([`modules/tui/helix/default.nix:258`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/tui/helix/default.nix#L258)).
- Explicit snippet-only onboarding has no independent consumer example ([`README.md:26`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/README.md#L26)).

# EzT32__nixos

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/EzT32__nixos.md)

- Upstream: [EzT32/nixos](https://github.com/EzT32/nixos)
- Reviewed revision: [`aa287213a56e`](https://github.com/EzT32/nixos/commit/aa287213a56e8bf8b4229f233ad8d7e240449319)
- Author: EzT32
- Score: **42.0 / 100**, rank 82 of 103 ranked configs. D 3 · I 9 · S 5 · R 5 · P 4 · L 4 · V 2 · O 2 · B 5 · X 2. Shortlists: —.
- Summary: D simple host-system selector; I clear ownership; S typed app options limited by six grouped assumptions/helper shape; R usable leaves; P HM-context error; L partially accurate guide; V no checks; O manual; X baseline; B census+eleven complete units.

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

Flake-parts/import-tree imports a small-feature desktop configuration with two entities declared centrally (`flake.nix:30`, `modules/den.nix:14`). Most software is selected in a common default, leaving hardware-specific host files (`modules/hosts/defaults.nix:15`, `README.md:23`).


## 2. Common patterns.

- define-user+primary-user: the user aspect includes both batteries (`modules/users.nix:5`).
- host-aspects: defaults allow host features to reach HM (`modules/hosts/defaults.nix:16`).
- den.default includes: CLI, development, GUI and services share a single feature list (`modules/hosts/defaults.nix:15`).


## 3. Novel patterns.

Audio policy includes a device-specific Razer profile and a Firefox stream volume rule (`modules/services/pipewire.nix:15`, `modules/services/pipewire.nix:26`), demonstrating where general audio and personal tuning currently mix.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

No verified den-specific workaround in the inspected entity and defaults modules (`modules/den.nix:9`, `modules/hosts/defaults.nix:15`).


## 6. Docs and complexity.

Docs 3: README explains import-tree exclusions and shows the directory structure (`README.md:3`, `README.md:13`). Complexity 3: two hosts share a fairly broad desktop default plus user setup (`modules/den.nix:14`, `modules/hosts/defaults.nix:15`).


## 6a. Defects and scoring notes.

- S · moderate: shared SSH/headset/monitor/wallpaper/locale bodies retain six grouped adaptation values, enumerated in S card (`modules/cli/ssh.nix:18`, `modules/services/pipewire.nix:18`, `modules/gui/hyprland/hyprland.nix:60`). Firefox volume is ordinary preference, not a defect.
- S · moderate: unselected Hypridle helper declares options while leaving services outside config, unlike the correctly wrapped Git/Kitty modules (`modules/gui/hyprland/hypridle.nix:8`, `modules/gui/hyprland/hypridle.nix:22`, `modules/cli/git.nix:24`).
- P · minor: unselected Hyprlock helper uses OS config.home-manager.users inside its HM configuration (`modules/gui/hyprland/hyprlock.nix:13`).
- L · minor: README describes host-file-driven discovery while entry imports all modules (`README.md:4`, `flake.nix:34`).
Broad graphical defaults match both intended desktop targets and are not an isolation defect merely because a hypothetical server would exclude them.

## 7. Template notes.

Approachable feature decomposition; split generic PipeWire enablement from headset and Firefox preferences for reuse (`modules/services/pipewire.nix:15`, `modules/services/pipewire.nix:26`).

## 8. Scorecard.

### D
Scope: inventory/default selection and editor package resolution. Pros: declared host.system selects the external Neovim package architecture (`modules/den.nix:14`, `modules/dev/nvim.nix:9`), reached through defaults (`modules/hosts/defaults.nix:28`). Cons: only this simple context fact is traced; the rest is direct module settings (`modules/programs/kitty.nix:53`). Interpolated3 above direct-only2 for one live architecture selector, below5 a useful shared data contract; no policies/pipes verified. Score **3**; confidence **medium**.

### I
Scope: feature files and hardware-only host imports. Pros: app owners and keybinding pieces remain localized (`modules/hosts/desktop/configuration.nix:7`, `modules/gui/hyprland/hyprland.nix:5`); defaults compose the intended two desktop hosts (`modules/hosts/defaults.nix:15`). Cons: no additional concrete isolation defect verified; broad desktop default is deliberate scope, not a promised headless interface. Literal9, no host-count bonus. Score **9**; confidence **medium**.

### S
Scope: app options versus shared personal presets. Pros: Git identity is explicitly supplied by user, Kitty font/theme and Discord client have types (`modules/cli/git.nix:12`, `modules/users.nix:11`, `modules/programs/kitty.nix:16`, `modules/programs/discord.nix:15`). Contract5: useful variation exists, but incomplete helpers and personal constants remain. Cons: coverage6 for six adaptation groups: owner/account/home-key identity, uio.no institution endpoints, checkout/wallpaper root, Razer headset, monitor topology, household locale/timezone (`modules/cli/ssh.nix:19`, `modules/cli/ssh.nix:18`, `modules/gui/hyprland/hyprlock.nix:13`, `modules/services/pipewire.nix:18`, `modules/gui/hyprland/hyprland.nix:60`, `modules/system/locale.nix:5`). Related subdomains/identity aliases and monitor occurrences grouped. min(5,6)=5; Firefox volume is ordinary preference and excluded from leaks. Score **5**; confidence **medium**.
```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":6}}
```

### R
Scope: visible independent application units, despite conservative old §4. Pros: Git takes two identity options, consumed by existing user config; Kitty exposes a parameterized preset (`modules/cli/git.nix:13`, `modules/users.nix:11`, `modules/programs/kitty.nix:16`). Cons: no independent consumer/adoption guide and §4 nominates no polished package (`README.md:13`). Literal5 for useful units changing at most two identified values, not9 a documented substantial A-unit example. No shortlist unit invented beyond existing §4. Score **5**; confidence **medium**.

### P
Scope: NixOS/HM boundaries and unselected lock helper. Pros: host hardware remains OS-specific while app settings live in HM (`modules/hosts/laptop/configuration.nix:5`, `modules/dev/vscode.nix:5`). Cons: Hyprlock HM body defaults to an OS-level config.home-manager.users.ezt path, unavailable in its HM config context (`modules/gui/hyprland/hyprlock.nix:13`). Interpolated4 below honest-narrow5 for this helper boundary defect; it is an unselected definition, not evidence current hosts fail. Score **4**; confidence **medium**.

### L
Scope: README discovery/structure explanation. Pros: describes exclusion prefix, output concept and directory map (`README.md:7`, `README.md:9`, `README.md:13`). Cons: discovery description points at host configuration files, whereas flake imports the entire modules tree (`README.md:4`, `flake.nix:34`); no worked new-host/user route. Interpolated4: useful architecture beyond2, not fully reliable authoring5. Score **4**; confidence **medium**.

### V
Scope: entry/output and authored modules. Pros: x86 Linux evaluation entry is explicit (`flake.nix:31`). Cons: no relevant composition checks or CI invocation found in inspected tree; hardware files are configuration, not tests (`modules/hosts/laptop/configuration.nix:8`). Literal2; no evaluation was attempted. Score **2**; confidence **medium**.

### O
Scope: rebuild path and host/user provisioning. Pros: README explains standard host rebuild entry (`README.md:9`). Cons: no deployment, builder or secret/bootstrap outputs derived from Den inventory in the root constructor (`flake.nix:30`, `modules/den.nix:14`). Literal2 manual activation, without inventing a fleet requirement. Score **2**; confidence **medium**.

### X
Scope: OS/HM aspects and external package selection. Pros: package system follows host metadata (`modules/dev/nvim.nix:9`). Cons: it installs a standard application package into HM, not a non-host Den target class (`modules/dev/nvim.nix:5`). Baseline2. Score **2**; confidence **medium**.

### B
Scope: census max-depth applications and strict reference list. Pros: Git/Kitty/VSCode expose complete settings and plugin/runtime closure (`modules/cli/git.nix:24`, `modules/dev/vscode.nix:69`). Cons: package-only leaves, Firefox single-volume preference, identity-bound SSH/PipeWire/OnlyOffice/Hyprland and incomplete helpers excluded (`modules/programs/firefox.nix:9`, `modules/programs/onlyoffice.nix:12`). Waybar references unowned pavucontrol; Hyprsunset toggle relies on external hyprctl, so neither whole leaf counts independently (`modules/gui/waybar/audio.nix:7`, `modules/gui/hyprland/hyprsunset.nix:19`). Multiple files of one app count once; disabled _minecraft excluded. Score **5**; confidence **medium**.
B_div: 3.0 points → 2; B_ref: 11 units → 7; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":3.0,"diversity_grade":2,"reference_grade":7,"reference_units":[{"name":"git","evidence":"modules/cli/git.nix:3"},{"name":"vscode","evidence":"modules/dev/vscode.nix:3"},{"name":"discord","evidence":"modules/programs/discord.nix:3"},{"name":"kitty","evidence":"modules/programs/kitty.nix:3"},{"name":"obs","evidence":"modules/programs/obs.nix:3"},{"name":"steam","evidence":"modules/programs/steam.nix:3"},{"name":"bluetooth","evidence":"modules/services/bluetooth.nix:3"},{"name":"rofi","evidence":"modules/gui/rofi.nix:3"},{"name":"hyprpaper","evidence":"modules/gui/hyprland/hyprpaper.nix:3"},{"name":"lact","evidence":"modules/programs/lact.nix:3"},{"name":"nix","evidence":"modules/system/nix.nix:3"}]}}
```

Total: **42.0/100**. Shortlists: showcase false; library_units []; starter false.

Overall pros:
- Explicit Git identity contract (`modules/cli/git.nix:12`).
- Application concerns have feature owners (`modules/programs/kitty.nix:3`).
- Desktop/laptop hardware stays in host imports (`modules/hosts/laptop/configuration.nix:8`).

Overall cons / limits:
- Shared physical topology/identity assumptions (§6a S; `modules/gui/hyprland/hyprland.nix:60`).
- Hypridle module shape violates its options/config envelope (§6a S; `modules/gui/hyprland/hypridle.nix:8`).
- Hyprlock confuses OS and home config (§6a P; `modules/gui/hyprland/hyprlock.nix:13`).
- Discovery explanation needs correction (§6a L; `README.md:4`).

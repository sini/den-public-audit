# scoiatael__dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/scoiatael__dotfiles.md)

- Upstream: [scoiatael/dotfiles](https://github.com/scoiatael/dotfiles)
- Reviewed revision: [`b1b3cc10eef1`](https://github.com/scoiatael/dotfiles/commit/b1b3cc10eef10161c924085b6946b7a9b1d32ad4)
- Author: scoiatael
- Score: **48.0 / 100**, rank 57 of 103 ranked configs. D 2 · I 7 · S 4 · R 7 · P 8 · L 2 · V 4 · O 6 · B 7 · X 2. Shortlists: library units (3).
- Summary: Library shortlist for the typed native SSH key generator, complete MPV integration and small comma/database unit. Showcase withheld because composition/source indexing is not structured-fact flow; starter withheld for shared environment constants, cold broken units and stale entry-point docs.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

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
Den defaults and user classes are centralized; host aspects extend an identity through provides (`modules/den.nix:15`, `modules/aspects/lsair.nix:10`). Feature files declare their own inputs alongside aspect definitions (`modules/aspects/comma.nix:4`).

## 2. Common patterns
- define-user+primary-user are grouped in the identity aspect (`modules/aspects/lukaszczaplinski.nix:9`).
- provides tree specializes a Darwin user for LsAir (`modules/aspects/lsair.nix:7`, `modules/aspects/lsair.nix:11`).
- The user schema defaults to HM (`modules/den.nix:19`).

## 3. Novel patterns
The comma aspect co-locates the external module input declaration with the HM import and enable flag, making its dependency easy to copy (`modules/aspects/comma.nix:4`, `modules/aspects/comma.nix:8`).

## 4. Library candidates
- openssh-host-keys · `modules/_darwin/modules/openssh-host-keys.nix:85` · **A**, standalone nix-darwin module; inputs config/lib/pkgs; hostKeys list parameterizes type/path/bits/comment, writes sshd config and generates missing keys in activation (`modules/_darwin/modules/openssh-host-keys.nix:11`, `modules/_darwin/modules/openssh-host-keys.nix:113`); caller imports it at `modules/aspects/lsair.nix:50`. No identity/assets required.
- mpv-uosc · `modules/aspects/mpv.nix:10` · **A**, inputs standard HM/nixpkgs plus owned config/mpv/uosc.conf; owns uosc/thumbfast settings, fonts and preview tools (`modules/aspects/mpv.nix:27`, `modules/aspects/mpv.nix:50`); native MPV options remain overrideable; caller selects it at `modules/aspects/lsair.nix:17`.
- comma · `modules/aspects/comma.nix:5` · enables nix-index-database comma integration in HM · inputs: nix-index-database, HM (input declared at `modules/aspects/comma.nix:4`) · parameterization: none · **A**, self-contained input/module/enable bundle (`modules/aspects/comma.nix:8`, `modules/aspects/comma.nix:10`).

## 5. den friction
The local dotfiles battery explicitly guards synthetic classless host/home contexts before selecting native classes (`modules/batteries/dotfiles.nix:20`, `modules/batteries/dotfiles.nix:38`). This is an author-documented context/API accommodation, not an independently reproduced Den defect.
No verified den-specific friction in reviewed host/user/provider wiring (`modules/aspects/lsair.nix:11`, `modules/aspects/lukaszczaplinski.nix:9`).

## 6. Docs and complexity
Docs **2**: README focuses on HM invocation and macOS setup (`README.md:3`, `README.md:10`), whereas provider behavior is visible mainly in source (`modules/aspects/lsair.nix:11`). Complexity **3**: shared identity plus host-specific provider choices (`modules/aspects/lukaszczaplinski.nix:7`, `modules/aspects/lsair.nix:11`).

## 6a. Defects and scoring notes

- **S / moderate:** Shared shell/service/editor bodies retain identity, checkout, private domain/address and backup destination constants (`modules/_home/modules/zsh.nix:166`, `modules/_nixos/modules/services/blocky.nix:39`, `modules/_nixos/modules/services/mail.nix:29`, `modules/aspects/doomemacs.nix:83`); grouped S inventory excludes overrideable Git defaults and named-host facts.
- **R / moderate:** FastAnime references ../config assets from modules/_home/modules, resolving to an absent modules/_home/config tree rather than supplied root config (`modules/_home/modules/fastanime.nix:24`, `modules/_home/modules/fastanime.nix:25`, `config/FastAnime/config.ini:1`). This is a cold native-unit defect, not an asserted selected-host evaluation failure.
- **R / minor:** Pry vterm prompt reads ENV[pwd] instead of the standard uppercase PWD (`modules/_home/modules/pry.nix:13`), so normal environments emit an empty cwd segment (`modules/_home/modules/pry.nix:14`).
- **L / minor:** README output names predate the visible inventory (`README.md:7`, `README.md:17`, `README.md:20`, `modules/aspects/lsair.nix:8`, `modules/aspects/lsframework.nix:3`).

## 7. Template notes
Good small dependency-owning aspect example; a newcomer needs to inspect source to understand host/user specialization (`modules/aspects/comma.nix:4`, `modules/aspects/lsair.nix:11`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: The dotfiles battery projects a static source index into native class arguments (`modules/den.nix:23`, `modules/batteries/dotfiles.nix:8`), while host providers select configuration fragments (`modules/aspects/lsair.nix:11`). Those are source lookup/composition, not a domain-fact payload or routed structured-data channel; host.name only labels the backup-command aspect (`modules/batteries/mkBackupCommand.nix:21`). Baseline 2. NH output generation is credited under O (`modules/nh.nix:16`), not also D. Score **2**; confidence **high**.

### I

Scope · pros · cons/coverage: Named Den features own dependencies and host/user providers select optional capabilities (`modules/aspects/comma.nix:4`, `modules/aspects/lsair.nix:11`, `modules/aspects/lsframework.nix:10`). Native modules are indexed separately for reuse (`modules/den.nix:38`). 7 interpolates clear new aspect boundaries with a broad identity baseline and substantial remaining host-local configuration (`modules/aspects/lukaszczaplinski.nix:8`, `modules/aspects/lsframework.nix:42`, `modules/_home/modules/default.nix:59`); tree size alone is not a penalty. Score **7**; confidence **high**.

### S

Scope · pros · cons/coverage: Actual second identity overrides Git name/email/signing in its provider (`modules/aspects/lswootingmbp.nix:61`), using overrideable native defaults (`modules/_home/modules/git.nix:233`, `modules/_home/modules/git.nix:260`). Contract 4: useful native option variation exists, but shared shell/editor/services retain checkout/identity/environment constants. Grouped inventory 21: shared identity1, public/private domain roots2, server address/name1, SMB network1, FontAwesome account key1, B2 account1 plus three backup destinations, checkout1, Drive Desktop1, GDrive1, NFS1, Org1, two Sway displays, Niri display1, Gemma project1, Documents/Git1, worktree root1 (`modules/_home/modules/zsh.nix:166`, `config/doom/modules/scoiatael/system/config.el:4`, `modules/_nixos/modules/services/blocky.nix:39`, `modules/_nixos/modules/services/smb.nix:76`, `modules/_nixos/modules/services/dashy.nix:11`, `modules/_nixos/modules/services/mail.nix:29`, `modules/_nixos/modules/services/restic.nix:41`, `modules/_nixos/modules/services/valheim.nix:83`, `modules/aspects/doomemacs.nix:83`, `modules/_home/modules/sway.nix:57`, `modules/_home/modules/terminals/rio.nix:49`, `config/doom/modules/scoiatael/system/autoload.el:54`, `modules/aspects/claude.nix:72`). Raw repeated literals exceed the grouped count; coverage cap5, S=min(4,5). Native mkDefault identity options, named-host facts and the Wezterm test fixture path are excluded (`config/wezterm/config.lua:184`). Score **4**; confidence **medium**.

```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":21}}
```

### R

Scope · pros · cons/coverage: Darwin SSH host-key provisioning is a substantial A unit: typed type/path/bits/comment inputs, native config output and activation generation are owned together (`modules/_darwin/modules/openssh-host-keys.nix:11`, `modules/_darwin/modules/openssh-host-keys.nix:54`, `modules/_darwin/modules/openssh-host-keys.nix:85`, `modules/_darwin/modules/openssh-host-keys.nix:113`). LsAir actually imports it (`modules/aspects/lsair.nix:50`); MPV independently owns plugin/font/assets (`modules/aspects/mpv.nix:12`, `modules/aspects/mpv.nix:27`). 7 credits those closed contracts without an isolated minimal external recipe, alongside incomplete legacy harvests: FastAnime paths resolve under modules/_home/config rather than root config (`modules/_home/modules/fastanime.nix:24`, `config/FastAnime/config.ini:1`), and Pry reads lowercase ENV[pwd] for its vterm cwd (`modules/_home/modules/pry.nix:13`). Score **7**; confidence **high**.

### P

Scope · pros · cons/coverage: Real Linux, Darwin and standalone Darwin home consumers coexist (`modules/aspects/lsframework.nix:3`, `modules/aspects/lsair.nix:7`, `modules/aspects/lsair.nix:8`). Dotfiles argument injection guards synthetic classless host/home contexts (`modules/batteries/dotfiles.nix:20`, `modules/batteries/dotfiles.nix:38`); native Linux additions and conditional editor packaging are explicit (`modules/_home/modules/linux.nix:10`, `modules/aspects/doomemacs.nix:71`). 8 reflects these concrete scope examples and guards without a tested OS/context matrix; cold native modules are not promised portable across all targets (`modules/_home/modules/terminals/rio.nix:13`). Score **8**; confidence **high**.

### L

Scope · pros · cons/coverage: README provides HM/macOS operational commands (`README.md:7`, `README.md:17`), not a Den/provider entry-point walkthrough (`modules/aspects/lsair.nix:11`). It still names obsolete framework/LsMBP/LsGamingDarwin outputs (`README.md:7`, `README.md:17`, `README.md:20`), whereas current declarations include LsFramework and the LsAir standalone home (`modules/aspects/lsframework.nix:3`, `modules/aspects/lsair.nix:8`). Baseline 2; comments on the native host-key API help that unit but do not teach overall composition (`modules/_darwin/modules/openssh-host-keys.nix:101`). Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: Selected LsWootingMBP includes Claude (`modules/aspects/lswootingmbp.nix:14`), whose installed hook packages include buildCommand test invocations (`modules/aspects/claude.nix:39`, `packages/claude-bash-guard/default.nix:7`, `packages/claude-statusline/default.nix:11`). Guard tests exercise ordinary/denied commands, missing data and installed-binary behavior (`packages/claude-bash-guard/test.clj:21`, `packages/claude-bash-guard/test.clj:50`, `packages/claude-bash-guard/test.clj:167`); selected Wezterm config contains positive contrast/hash assertions (`modules/aspects/lsair.nix:29`, `config/wezterm/config.lua:184`). 4 credits real build/runtime helper tests; CI only mirrors Git refs, and no Den host/context regression fixture is visible (`.build.yml:7`, `.build.yml:21`). No tests were executed here. Score **4**; confidence **high**.

### O

Scope · pros · cons/coverage: NH packages derive host/home activation choices from Den (`modules/nh.nix:10`, `modules/nh.nix:16`); per-host aspect secret entries derive owners/destination paths from native primary-user configuration (`modules/aspects/lsair.nix:60`, `modules/aspects/lswootingmbp.nix:96`). 6 interpolates generated activation tooling plus live aspect-selected secret provisioning. Builders and backup destinations remain manually specified rather than one comprehensive Den inventory flow (`modules/aspects/lsair.nix:131`, `modules/_nixos/modules/services/restic.nix:41`, `modules/_nixos/modules/services/valheim.nix:83`). Native SSH key generation is useful operations code but is not an additional Den-data generator (`modules/_darwin/modules/openssh-host-keys.nix:56`). Score **6**; confidence **high**.

### X

Scope · pros · cons/coverage: Evaluated targets are ordinary NixOS/Darwin/HM (`modules/aspects/lsair.nix:7`, `modules/aspects/lsframework.nix:3`). Exposed native module paths and ordinary package forwarding do not create another module/output target contract (`modules/den.nix:38`, `modules/nh.nix:16`). Baseline 2. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Selected/max-depth census contributes 9 points, diversity grade7: concrete host/provider includes and native imports establish the scope (`modules/aspects/lswootingmbp.nix:12`, `modules/aspects/lsframework.nix:10`, `modules/aspects/lsframework.nix:307`). Complete independent app-unit inventory below has 12 units, reference grade7 => B7. Native files count alongside Den aspects; SSH host-key generation owns its activation job, not merely passive settings (`modules/_darwin/modules/openssh-host-keys.nix:116`). Exclude settings-only Qutebrowser (no app enable/install; `modules/_home/modules/qutebrowser.nix:3`), package-only/tiny flag leaves, broad inseparable default bundles, native custom self.packages/dotfiles dependencies without an exported closure, missing assets, identity-bound services and Neovim whose forced Wezterm bridge requires an unprovided terminal (`config/neovim/smart-splits.lua:68`). Codium compatibility is confirmed by the [exact pinned HM renamed-option bridge](https://github.com/nix-community/home-manager/blob/32904dfe1cf86039f3c8c9f41f94e1cfd76dbb34/modules/programs/vscode/default.nix#L53) (`flake.lock:363`); fonts are ordinary fallback preferences, not absent mandatory assets. Score **7**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":9.0,"diversity_grade":7,"reference_grade":7,"reference_units":[{"name":"vscodium","evidence":"modules/_home/modules/editors/codium.nix:3"},{"name":"helix","evidence":"modules/_home/modules/editors/helix.nix:3"},{"name":"zellij","evidence":"modules/_home/modules/multiplexers/zellij.nix:3"},{"name":"canario-shell-compat","evidence":"modules/aspects/canario.nix:7"},{"name":"gram","evidence":"modules/aspects/gram.nix:22"},{"name":"mpv-uosc","evidence":"modules/aspects/mpv.nix:12"},{"name":"openssh-host-keys","evidence":"modules/_darwin/modules/openssh-host-keys.nix:85"},{"name":"rift","evidence":"modules/_darwin/modules/rift/default.nix:7"},{"name":"keyd","evidence":"modules/_nixos/modules/keyd.nix:16"},{"name":"nix-builder-account-daemon","evidence":"modules/_nixos/modules/services/remote-builder.nix:4"},{"name":"scrutiny-influxdb","evidence":"modules/_nixos/modules/services/scrutiny.nix:6"},{"name":"comma-database","evidence":"modules/aspects/comma.nix:8"}]}}
```

**Total:** 48.0/100. **Shortlists:** showcase no; library openssh-host-keys, mpv-uosc, comma; starter no. Library shortlist for the typed native SSH key generator, complete MPV integration and small comma/database unit. Showcase withheld because composition/source indexing is not structured-fact flow; starter withheld for shared environment constants, cold broken units and stale entry-point docs.

Overall pros:
- Typed native SSH key generator owns options, config fragment and activation (`modules/_darwin/modules/openssh-host-keys.nix:85`, `modules/_darwin/modules/openssh-host-keys.nix:116`).
- Real Linux/Darwin/standalone-home boundaries include classless-context guards (`modules/aspects/lsair.nix:8`, `modules/batteries/dotfiles.nix:22`).
- Selected hook packages execute focused negative/end-to-end tests during their build (`packages/claude-bash-guard/default.nix:7`, `packages/claude-bash-guard/test.clj:167`).

Overall cons / scope limits:
- Shared native source retains checkout, identity and service-network assumptions (`modules/_home/modules/zsh.nix:166`, `modules/_nixos/modules/services/blocky.nix:39`).
- Some cold legacy modules have unresolved asset paths (`modules/_home/modules/fastanime.nix:24`).
- README targets are stale and provider composition is unexplained (`README.md:17`, `README.md:20`, `modules/aspects/lsair.nix:11`).
- CI mirrors refs rather than checking representative configurations (`.build.yml:21`).

# DylanRJohnston__nixos

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/DylanRJohnston__nixos.md)

- Upstream: [DylanRJohnston/nixos](https://github.com/DylanRJohnston/nixos)
- Reviewed revision: [`505097f4d0fd`](https://github.com/DylanRJohnston/nixos/commit/505097f4d0fd9fe271bd1f5a75a6791564333b8f)
- Author: DylanRJohnston
- Score: **56.5 / 100**, rank 27 of 103 ranked configs. D 5 · I 8 · S 5 · R 5 · P 8 · L 5 · V 9 · O 5 · B 5 · X 2. Shortlists: library units (1).
- Summary: Tested namespace composition is notable, with a useful B leaf; direct entity flow and advanced import prerequisites prevent showcase/starter selection.

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
A raw nixpkgs evalModules entry imports both modules and hosts, then returns config.flake (`flake.nix:25`, `flake.nix:28`). An exported/importable arc namespace carries custom host/user schemas and strict class declarations (`modules/namespace.nix:13`, `modules/namespace.nix:45`).

## 2. Common patterns
- namespace: arc can either export local definitions or import an upstream namespace (`modules/namespace.nix:10`, `modules/namespace.nix:27`).
- define-user+primary-user share the identity aspect (`modules/users.nix:17`).
- host-aspects forwards host composition to both user and homeManager classes (`modules/host-aspects.nix:5`).

## 3. Novel patterns
The import adapter strips navigation aliases recorded by __providesForwarded before strict-mode re-import, keeping reusable namespace definitions independent of exported navigation helpers (`modules/namespace.nix:11`, `modules/namespace.nix:20`).

## 4. Library candidates
- fstrim · `modules/fstrim.nix:5` · enables NixOS periodic filesystem trimming · inputs: NixOS/nixpkgs, arc namespace · parameterization: none · **B**, extract the leaf from its automatic arc.base inclusion (`modules/fstrim.nix:3`).

## 5. den friction
The namespace comment explicitly identifies strict-mode rejection of upstream navigation aliases and removes them as a compatibility adapter (`modules/namespace.nix:11`, `modules/namespace.nix:20`).

## 6. Docs and complexity
Docs **4**: README explains discovery, aspect ownership and ADR locations (`README.md:40`), while the adapter explains its strict-mode workaround (`modules/namespace.nix:11`). Complexity **4**: custom schemas, strict class declarations and reusable module exports (`modules/namespace.nix:37`, `modules/namespace.nix:45`).

## 6a. Defects and scoring notes

- **S · moderate:** Raw 27 literals form **21 grouped leaks** under the maintainer ruling: full name/email (`modules/git.nix:28`); dylanj and personal cache key (`modules/nix.nix:45`, `modules/nix.nix:72`); loki/odin/eu.nixbuild.net (`modules/remote-builders.nix:14`, `modules/remote-builders.nix:28`, `modules/remote-builders.nix:42`); mimir, absolute project path (`modules/zed.nix:203`, `modules/zed.nix:217`); Sway checkout (`modules/sway.nix:160`); HA checkout, timezone, serial identity, two receiver IPs (`modules/home-automation/home-assistant.nix:17`, `modules/home-automation/home-assistant.nix:21`, `modules/home-automation/home-assistant.nix:30`, `modules/home-automation/home-assistant.nix:43`, `modules/home-automation/home-assistant.nix:44`); router endpoint (`modules/home-automation/router.nix:8`); two Bluetooth MACs and GOPATH (`modules/zsh.nix:63`, `modules/zsh.nix:78`, `modules/zsh.nix:80`); Thread CIDR/interface (`modules/home-automation/matter.nix:18`, `modules/home-automation/matter.nix:36`); latitude/longitude (`modules/sunset.nix:8`, `modules/sunset.nix:9`); media root/source checkout (`modules/media-server/media-server.nix:36`, `modules/media-server/media-server.nix:57`); monitor serial (`modules/niri.nix:47`); personal SSH host thoth (`modules/ssh.nix:31`). Grouping: author name/email/login =1; nixbuild endpoint/key =1; project/Sway .nixpkgs root =1; HA/media /etc/nixos root =1; latitude/longitude =1; the other 16 hostnames, distinct device/host addresses, interface, location/storage roots and timezone remain separate. Ports/upstreams/preset settings and overrideable defaults excluded. Coverage cap 5; primaryUser additionally warns/nulls instead of validating (`modules/users.nix:12`, `modules/meta.nix:7`).
- **O · moderate:** builder inventory duplicates host topology despite its derivation TODO (`modules/remote-builders.nix:11`). Endpoints enter S coverage above, but list-maintenance cost is charged only O.
- **R · minor:** exported namespace re-import depends on internal navigation metadata (`modules/namespace.nix:20`); this is a maintenance prerequisite, not an I defect.
- **L · minor:** README links a personal Den fork while input is denful (`README.md:49`, `flake.nix:3`).

## 7. Template notes
Good advanced namespace export material; alias stripping and strict-schema customization add more machinery than a first host needs (`modules/namespace.nix:20`, `modules/namespace.nix:47`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: SSH facts `modules/mesh/keys.nix:43`, `modules/mesh/keys.nix:49` → den.hosts fold `modules/mesh/keys.nix:16` → authorizedKeys `modules/mesh/keys.nix:35`; null filtering `modules/mesh/keys.nix:33`, duplicate accumulation test `modules/mesh/keys.nix:88`. Direct entity iteration is capped at 5; no pipe route credited. Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: Namespace/feature ownership (`modules/namespace.nix:27`, `modules/gaming/sunshine.nix:11`) and optional debug child (`modules/bluetooth.nix:22`) localize concerns. Baseline fragments such as Tmux still share arc.base (`modules/tmux.nix:2`): above 5, short of uniformly independent 9 boundaries; no extra charged defect. Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract grade 7: typed storage and provider-valued boot with invalid-input cases (`modules/storage.nix:3`, `modules/bootloader.nix:9`, `modules/bootloader.nix:47`); primaryUser remains anything/null (`modules/users.nix:7`). Coverage grade 5: 21 grouped leaks from 27 raw literals (§6a); lower grade controls. Ordinary module options/default presets and fixtures excluded. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":5,"distinct_leaks":21}}
```

### R

Scope · pros · cons/coverage: Existing B candidate fstrim needs namespace/auto-inclusion extraction (`modules/fstrim.nix:3`, `modules/fstrim.nix:5`). Useful light extraction meets 5; tiny enable-only leaf is not a substantial A consumer example and is excluded from B_ref. Alias import also depends on internal metadata (`modules/namespace.nix:20`). Score **5**; confidence **medium**.

### P

Scope · pros · cons/coverage: Strict standard class set (`modules/namespace.nix:49`) and positive/negative Linux/Darwin helpers (`modules/lib.nix:50`, `modules/lib.nix:56`) plus real projection contexts (`modules/host-aspects-test.nix:178`). Above honest-scope 5; boundary tests cover representative bridges rather than every hardware/service arm, so 8, not 9. Score **8**; confidence **medium**.

### L

Scope · pros · cons/coverage: README maps discovery/hosts/modules/ADRs (`README.md:42`, `README.md:46`); adapter explains alias rejection (`modules/namespace.nix:11`). Stale Den link (`README.md:49`) and Darwin-only bootstrap (`README.md:7`) leave 5-level navigation rather than a complete 9 tutorial. Score **5**; confidence **high**.

### V

Scope · pros · cons/coverage: Enabled/omitted classes and empty users (`modules/host-aspects-test.nix:194`, `modules/host-aspects-test.nix:211`) plus same-user/two-host test (`modules/host-aspects-test.nix:230`) exercise actual context semantics. CI invokes checks and nix-unit (`.github/workflows/CI.sh:4`, `.github/workflows/CI.yml:27`). Meets 9 intent; passing status unknown. Score **9**; confidence **high**.

### O

Scope · pros · cons/coverage: SSH recipients derive from host/user facts (`modules/mesh/keys.nix:28`, `modules/mesh/keys.nix:35`); secret path derives host name (`modules/public-ingress.nix:13`). One useful provisioning concern meets 5. Builder topology remains a hand-kept list (`modules/remote-builders.nix:11`), not unified deploy/install/rekey. Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: Explicit class surface is OS/user/HM (`modules/namespace.nix:49`). CrossInk is an ordinary package (`modules/platform-io.nix:41`), not a Den device class. Literal 2 baseline; no additional target-family claim. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census maximum-depth dedup gives Tmux/Zsh/Starship/Zed/Niri/Vim = 6 points → B_div 5. The standard Den os bridge was verified at exact locked 37eb88ce (https://raw.githubusercontent.com/denful/den/37eb88ce28a9e42d5b367b967a9097030ff4f665/modules/aspects/batteries/os-class.nix, default attachment line24 and route line40); OpenSSH therefore needs no private class adapter. Full application-body scan counts the nine units in the block → B_ref 5. Each is a complete substantive app/service preset; exclude fstrim/Direnv bare enables, disabled Nushell (`modules/nushell.nix:14`), Wezterm config without installation (`modules/wezterm.nix:26`), and household/identity-dependent units (`modules/home-automation/matter.nix:36`). Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":6,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"bluez","evidence":"modules/bluetooth.nix:7"},{"name":"gamemode","evidence":"modules/gaming/gamemode.nix:14"},{"name":"steam","evidence":"modules/gaming/steam.nix:13"},{"name":"sunshine","evidence":"modules/gaming/sunshine.nix:30"},{"name":"tmux","evidence":"modules/tmux.nix:3"},{"name":"vim","evidence":"modules/vim.nix:5"},{"name":"homebrew","evidence":"modules/homebrew.nix:7"},{"name":"openssh-server","evidence":"modules/mesh/ssh.nix:8"},{"name":"plymouth","evidence":"modules/plymouth.nix:10"}]}}
```

**Total:** 56.5/100. **Shortlists:** showcase no; library fstrim; starter no. Tested namespace composition is notable, with a useful B leaf; direct entity flow and advanced import prerequisites prevent showcase/starter selection.

Overall pros:
- Topology-derived SSH authorization (`modules/mesh/keys.nix:35`).
- Typed alternative boot and storage contracts (`modules/bootloader.nix:9`, `modules/storage.nix:3`).
- Negative/context tests have a real CI invocation (`modules/host-aspects-test.nix:194`, `.github/workflows/CI.sh:4`).

Overall cons / scope limits:
- S: author facts remain in shared features (`modules/git.nix:28`, `modules/niri.nix:47`).
- O: builder inventory is manually synchronized (`modules/remote-builders.nix:11`).
- R/L: internal alias adapter and stale docs complicate adoption (`modules/namespace.nix:20`, `README.md:49`).

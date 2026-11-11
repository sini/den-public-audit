# theutz

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/theutz.md)

- Upstream: [~theutz/flake](https://git.sr.ht/~theutz/flake)
- Reviewed revision: [`3ede31e7a4e9`](https://git.sr.ht/~theutz/flake/commit/3ede31e7a4e906e7bded05e46b209caaa12af3c5)
- Author: theutz
- Score: **53.0 / 100**, rank 37 of 103 ranked configs. D 7 · I 7 · S 4 · R 5 · P 6 · L 1 · V 2 · O 7 · B 7 · X 2. Shortlists: library units (2).
- Summary: D 7 four live routed channels (deploy, casks/brews/taps, treefmt, devshell) but single-consumer and ~20 aspects bypass the casks quirk; I 7 thin hosts + per-feature files; S 4 no settings contract, 3 distinct leaks; L 1 no docs; O 7 deploy class + host.pubkey rekey; B 7 (B_div 9.5 -> 7, B_ref 14 -> 7)

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

flake-file generated flake with flake-parts + import-tree over `modules/` (`modules/flake/flake-file.nix:14-17`). One file per
feature under `modules/aspects/`, hosts under `modules/host/<name>/`, one user, quirks under `modules/quirks/`. Two hosts:
`kocaeli` (aarch64-darwin) and `istanbul` (NixOS). Uses hjem and home-manager side by side as user classes
(`modules/host/kocaeli/kocaeli.nix:27-30`). Eval measured PASS on both hosts.

## 2. Common patterns

- `den.default includes` with batteries: `modules/flake/den.nix:17-24` (define-user, hostname, host-aspects, flake-scope, inputs', self').
- `define-user+primary-user`, user-shell: `modules/users/theutz/theutz.nix:11-12`.
- `angle-bracket refs`, including sub-aspect paths `<cli/zmx>` and `<gui/sketchybar>`: `modules/users/theutz/theutz.nix:27-30`, `modules/host/kocaeli/kocaeli.nix:41`.
- `parametric aspect (fn args)`: user class keyed on `host.class`, `modules/users/theutz/theutz.nix:33-42`.
- `quirks`: `den.quirks.casks/brews/taps`, `modules/quirks/casks.nix:2`, consumed as module args `modules/aspects/homebrew.nix:6-8`, produced per aspect `modules/aspects/omniwm.nix:8`.
- `policies` + `custom schema/classes`: `modules/deploy.nix:14-35`, `modules/flake/treefmt.nix:11-23`, `modules/flake/devshell.nix:17-20`.
- `provides tree`: `modules/aspects/editors/nvf.nix:62`.
- host `excludes`: `modules/host/kocaeli/kocaeli.nix:41`.

## 3. Novel patterns

- `modules/deploy.nix:14-35`: a `deploy` class routed by `policy.route` into `flake.deployNodes.<host>`, then `flake.deploy.nodes`.
  Host-level `deploy` attrs (`modules/host/kocaeli/kocaeli.nix:17-24`) are merged over defaults with `recursiveUpdate`. It is a full deploy-rs
  integration in about 50 lines, with no per-host boilerplate.
- `modules/flake/treefmt.nix:13-23` and `modules/flake/devshell.nix:19-20`: aspects contribute `treefmt`/`devshell` classes
  that a policy routes into flake-parts perSystem, so a feature aspect carries its own formatter and devshell commands
  (`modules/deploy.nix:38-42`).
- `modules/aspects/nix-output-monitor.nix:13-14`: one aspect included both at `den.schema.flake-parts` and `den.schema.host`.
- `modules/flake/aspect-path-helpers.nix:1-37`: path helpers for out-of-store config links (`/etc/nixos/modules/aspects/...`).
- `modules/flake/pipe.nix`, `modules/flake/dag.nix:9`: the den-ecosystem `pipe` and `dag` libs exposed as module args.

## 4. Library candidates

- deploy · `modules/deploy.nix` · deploy-rs nodes from den hosts via a class + route policy · deploy-rs · host attr `deploy` (options-like) · A
- homebrew quirks · `modules/aspects/homebrew.nix` + `modules/quirks/*.nix` · aspects declare casks/brews/taps; one darwin aspect collects them · nix-darwin · quirk values · A
- treefmt/devshell routing · `modules/flake/treefmt.nix`, `modules/flake/devshell.nix` · per-aspect formatter and devshell contributions · treefmt-nix, devshell · none · B

## 5. den friction

- `modules/aspects/slack.nix:11` writes `homebrew.casks` directly while `modules/aspects/omniwm.nix:8` and `modules/aspects/marked.nix:7` use the `casks` quirk.
  Two idioms for one job suggest the quirk route is not obvious.
- `modules/flake/den.nix:13` and `modules/flake/flake-parts.nix:8` re-export `__findFile` and `policy` via `_module.args`.
  This is a common boilerplate line; den could ship it.
- `modules/flake/den.nix:21-23` and `modules/flake/flake-parts.nix:19-21` both include `inputs'`/`self'` (one via `den._`,
  one via `den.batteries`), which is duplicated inclusion.

## 6. Docs and complexity

No README and no markdown (`readme_bytes: 0`), comment ratio 0.03: doc_quality 1. Complexity 4: only two hosts, but
three custom classes, four route policies, quirks and dual user classes (hjem + HM) across darwin and NixOS.

## 6a. Defects and scoring notes

- `modules/aspects/slack.nix:11` · D · minor · writes `homebrew.casks` directly instead of emitting the `casks` quirk that `modules/aspects/omniwm.nix:8` and `modules/aspects/marked.nix:7` use; one producer bypasses the channel
- `modules/flake/aspect-path-helpers.nix:12-20` · S · minor · the out-of-store config root `/etc/nixos/modules/aspects` is hard-coded, so the checkout location is assumed
- `modules/flake/agenix-rekey.nix:26` · S · minor · the owner's master SSH pubkey sits inline in a flake-level module rather than in a user/host setting
- `modules/flake/den.nix:21-23` + `modules/flake/flake-parts.nix:19-21` · I · minor · `inputs'`/`self'` batteries are included twice from two files
- repo root (`readme_bytes: 0`, `md_files: 0`) · L · moderate · no README or docs; the entry-to-feature route must be read from the code
- repo-wide · V · minor · no flake `checks` found by a repo-wide grep; observation only

## 7. Template notes

It is a strong reference for den's newer surfaces (policies, classes, quirks) used for real work: deploy-rs, treefmt and
homebrew. It is a poor first example, because nothing is explained and there is no README. Its deploy and homebrew
modules could be lifted almost verbatim.

## 8. Scorecard
### D (7, high)
Scope: `modules/deploy.nix`, `modules/quirks/{casks,brews,taps}.nix`, `modules/aspects/homebrew.nix`, `modules/flake/{treefmt,devshell}.nix`.
Pros: casks chain: producers `modules/aspects/omniwm.nix:8`, `modules/aspects/marked.nix:7`, `modules/aspects/rootshell.nix:5`; declaration `modules/quirks/casks.nix:2`; route is den's default quirk collection; consumer `modules/aspects/homebrew.nix:6` takes `casks` as a module arg and assigns `homebrew.casks` (taps get a string-to-record map). Deploy chain: host attr `deploy` (`modules/host/kocaeli/kocaeli.nix:17-24`) merged by `recursiveUpdate` with `den.aspects.deploy.hosts` (`modules/deploy.nix:44-58`), `policy.route` fromClass `deploy` into `flake.deployNodes.<host.name>` (`modules/deploy.nix:18-30`), consumer `flake.deploy.nodes` (`modules/deploy.nix:16`). Four live routed channels, no ceremony.
Cons: all single-consumer with no validation or duplicate/empty semantics (left to nix-darwin); `modules/aspects/slack.nix:11` and about 20 more aspects write `homebrew.casks` directly (22 files) while 5 emit the quirk, so the quirk is bypassed. Between anchors 5 and 9; policy routing is present, so 6.
Re-score under the quirk ruling (was 6): casks, brews and taps are three live quirk channels with traced emitters (`modules/aspects/marked.nix:6-8`, `modules/aspects/rift.nix:4-5`) and one consumer (`modules/aspects/homebrew.nix:6`), plus routed deploy, treefmt and devshell classes. Not above 7: no cross-scope pipes, no missing/duplicate semantics, and the casks quirk is bypassed by about 20 aspects.
Confidence: high.

### I (7, medium)
Scope: tree layout, `kocaeli.nix`, `theutz.nix`, sampled aspects.
Pros: one small file per feature (`aspects/git.nix` is 27 lines), hosts are include lists (`modules/host/kocaeli/kocaeli.nix:34-42`), `excludes` used (`modules/host/kocaeli/kocaeli.nix:41`).
Cons: features self-attach to the kocaeli host (`modules/aspects/herdr.nix:32`, `modules/aspects/karabiner.nix:5`, `modules/aspects/aerospace.nix:444`); `inputs'`/`self'` batteries included from two files (`modules/flake/den.nix:21-23`, `modules/flake/flake-parts.nix:19-21`).
Confidence: medium.

### S (4, medium)
Scope: grep of settings/options in aspects, host and user files; leak grep over `modules/aspects` and `modules/flake`.
Pros: user-entity attributes are read by consumers (`jj` reads `user.email`); host-specific values live in host files, which is acceptable (`modules/host/kocaeli/kocaeli.nix:15,31`). Leak grade 10: only 3 distinct leaks, no cap.
Cons: no settings contract at all, variation is by editing the aspect (contract grade 4). Distinct leaks (3): master pubkey `modules/flake/agenix-rekey.nix:26`, a committed credential (reported privately; not located here), `/etc/nixos` checkout root `modules/flake/aspect-path-helpers.nix:12`. S = min(4, 10) = 4.
```score-evidence
{"S": {"contract_design": 4, "leak_coverage": 10, "distinct_leaks": 3}}
```
Confidence: medium.

### R (5, medium)
Scope: `deploy.nix`, homebrew quirks, `zmx.nix`.
Pros: `modules/deploy.nix:44-58` is adoptable by changing <=3 values (`sshUser`, `remoteBuild` defaults at `:50-51`, the deploy-rs input); `modules/aspects/zmx.nix:1` is a self-contained HM module with its own options.
Cons: implicit contract, no consumer example or docs; one aspect embeds a committed credential (reported privately; not located here). Grade B units, no documented grade A.
Confidence: medium.

### P (6, medium)
Scope: darwin vs nixos arms, `host.class` guards, rekey imports.
Pros: arms selected by class keys and `host.class` guards (`modules/aspects/ghostty.nix:30`, `modules/aspects/browsers/browsers.nix:24`, `modules/aspects/media/media.nix:20`); `modules/host/kocaeli/kocaeli.nix:41` excludes a darwin-only aspect; `modules/flake/agenix-rekey.nix:8-14` splits darwin/nixos imports.
Cons: no failing-clearly mechanism and no boundary checks.
Confidence: medium.

### L (1, high)
Scope: repo root and flake header.
Pros: flake-file header comment explains regeneration (`flake.nix:1`).
Cons: no README and no markdown at all (`readme_bytes: 0`), comment ratio 0.03; the route from entry point to features must be read from filenames. Calibration: absence = 1.
Confidence: high.

### V (2, high)
Scope: repo-wide grep for checks and CI.
Pros: treefmt module gives formatting only (`modules/flake/treefmt.nix:7-33`).
Cons: no flake checks and no CI found; observation, not a failing claim.
Confidence: high.

### O (7, high)
Scope: `modules/deploy.nix`, `modules/flake/agenix-rekey.nix`, `host/kocaeli/kocaeli.nix`.
Pros: `deploy` class routed per host from den hosts with per-host overrides (`modules/deploy.nix:14-58`); agenix-rekey takes `hostPubkey = host.pubkey` and a per-host storage dir from host data (`modules/flake/agenix-rekey.nix:19-23`); no hand-kept host list.
Cons: no install/bootstrap or builder list from den data (`modules/aspects/linux-builder.nix:1` is a plain aspect); two hosts only; master identity fixed (an S matter).
Confidence: high.

### B (7, medium)
Scope: census record plus aspect reads; B_div 9.5 -> 7, B_ref 13 -> 7, B = mean(7,7) = 7.
Pros: B_div = 9.5: selection-verified substantive 1 each: nushell, zsh, starship, tmux, zellij, neovim (nvf), niri, aerospace = 8; enable-only 0.5 each: bash, fish, gnome = 1.5; no named peers (omniwm/rift are `defined` only). Band <=11 -> 7. B_ref units are the 13 listed in the evidence block below: aerospace, starship, karabiner, tmux, zellij, jj, ghostty, sketchybar, zmx, jjui, nushell, zk, herdr.
Cons: bash, fish and gnome are enable-only (`modules/aspects/bash.nix:3`, `modules/aspects/fish.nix:3`), omniwm and rift are installed via casks only (`modules/aspects/omniwm.nix:8`), and the nvf aspect is a devshell wrapper (`modules/aspects/editors/nvf.nix:14`) not a configured editor; one aspect is excluded because it carries a committed credential (reported privately; not located here). No browser, mail or server-service domain.
```score-evidence
{"B": {"diversity_points": 9.5, "diversity_grade": 7, "reference_grade": 7, "reference_units": [{"name": "aerospace", "evidence": "modules/aspects/aerospace.nix:187"}, {"name": "starship", "evidence": "modules/aspects/starship.nix:7"}, {"name": "karabiner", "evidence": "modules/aspects/karabiner.nix:18"}, {"name": "tmux", "evidence": "modules/aspects/tmux.nix:27"}, {"name": "zellij", "evidence": "modules/aspects/zellij.nix:26"}, {"name": "jj", "evidence": "modules/aspects/jj.nix:17"}, {"name": "ghostty", "evidence": "modules/aspects/ghostty.nix:27"}, {"name": "sketchybar", "evidence": "modules/aspects/gui/sketchybar.nix:30"}, {"name": "zmx", "evidence": "modules/aspects/zmx.nix:15"}, {"name": "jjui", "evidence": "modules/aspects/jjui.nix:15"}, {"name": "nushell", "evidence": "modules/aspects/nushell.nix:20"}, {"name": "zk", "evidence": "modules/aspects/zk.nix:7"}, {"name": "herdr", "evidence": "modules/aspects/herdr.nix:12"}]}}
```
Representative cited units: pro `modules/aspects/aerospace.nix:187` and `modules/aspects/ghostty.nix:27` are cited at the line where their configuration begins; the other units in the block are cited the same way.
Confidence: medium.

### X (2, high)
Scope: class declarations in `deploy.nix`, `treefmt.nix`, `devshell.nix`.
Pros: class routing is explicit (`modules/deploy.nix:14`).
Cons: only darwin and NixOS hosts; deploy is O only; treefmt/devshell are trivial wrappers (`modules/flake/treefmt.nix:11-25`, `modules/flake/devshell.nix:17-20`).
Confidence: high.


### Total
2*7+7+4+5+6+1+7+7+2/2+2/2 = **53.0/100**

### Shortlist judgment
Not a showcase on this rubric (D 6, L 1, X 2); deploy class and casks quirks are library units; not a starter (no docs). Differs from the pilot (44) by the added B term and weights; D, I, S, O differ by <=1 from the reconciled pilots.

Overall pros:
- Deploy as a 50-line class + route policy, no per-host boilerplate (`deploy.nix:14-58`).
- Aspects emit casks/brews/taps facts consumed by one darwin aspect (`omniwm.nix:8`, `homebrew.nix:6`).
- Broad application coverage with small per-app files (B 7).

Overall cons:
- No README or docs (`readme_bytes: 0`).
- No settings contract; master pubkey inline (`agenix-rekey.nix:26`), and a committed credential (reported privately; not located here).
- Casks quirk bypassed by ~20 aspects (`slack.nix:11`).

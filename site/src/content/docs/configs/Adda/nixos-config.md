---
title: "Adda/nixos-config"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/adda/nixos-config/)

- Upstream: [Adda/nixos-config](https://codeberg.org/Adda/nixos-config)
- Reviewed revision: [`31f3e4b1489f`](https://codeberg.org/Adda/nixos-config/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a)
- Author: Adda
- Score: **59.5 / 100**, rank 15 of 101 ranked configs. D 7 · I 7 · S 6 · R 6 · P 5 · L 8 · V 3 · O 3 · B 8 · X 2. Shortlists: library units (4).
- Summary: D 7 live editor/service quirks with default collection, fixed-name `host.users.adda` lookups, aspect-settings has no consumer; I 7 namespace tree; S 6 documented per-user `opt` contracts but fixed user key + personal defaults; L 8 generated README + AGENTS.md; V 3, O 3, X 2; B 8 (B_div 12 -> 9, B_ref 19 -> 7)

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

flake-file generated flake with flake-parts + import-tree over `modules/` ([`flake.nix:6`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/flake.nix#L6)). den plumbing (namespace,
classes, quirks, aspect settings) is isolated in `modules/plumbing/den/`. Features live in a local `addax` namespace
built by `omniflake.unified.den.namespace` ([`modules/plumbing/den/namespaces.nix:21`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/namespaces.nix#L21)) under `modules/aspects/<area>/`.
Five NixOS hosts, mostly VMs and work VMs, and one user. Private modules come in as a second import-tree from a private
flake, with an in-tree stub ([`modules/flake/addax-private.nix:11-12`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/addax-private.nix#L11-L12)). It is the largest local repo (20.5k LOC).

## 2. Common patterns

- `namespace` + `angle-bracket refs`: [`modules/plumbing/den/namespaces.nix:21,31`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/namespaces.nix#L21).
- `define-user+primary-user`, `host-aspects`: [`modules/users/adda/user.nix:29-30,88`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/users/adda/user.nix#L29-L30), [`modules/users/adda/server.nix:11-13`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/users/adda/server.nix#L11-L13).
- vm-autologin battery per host: [`modules/hosts/_system.nix:52`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/_system.nix#L52), [`modules/hosts/mensa-nixos/system.nix:108`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/mensa-nixos/system.nix#L108).
- `policies`: `den.policies.system-to-flake-parts` at flake-parts scope ([`modules/defaults.nix:2-4`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/defaults.nix#L2-L4)).
- `custom schema/classes`: host options `isWorkstation`, `longDescription` ([`modules/hosts/host.nix:2-17`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/host.nix#L2-L17)); `aliases` and
  `abbreviations` classes ([`modules/plumbing/den/classes/aliases.nix:52-55`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/aliases.nix#L52-L55)).
- `forward`: aliases into `home.shellAliases`, abbreviations into fish, nushell and zsh-abbr ([`modules/plumbing/den/classes/aliases.nix:3-48`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/aliases.nix#L3-L48)).
- `quirks`: ten collector channels, e.g. `helixExtraPackages`, `zedEditorExtensions`, `serviceDomains`
  ([`modules/plumbing/den/quirks/helix-extra_packages.nix:2`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/quirks/helix-extra_packages.nix#L2), [`modules/plumbing/den/quirks/service-domains.nix:2`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/quirks/service-domains.nix#L2)).
- `den.default` class config: [`modules/defaults.nix:10,390`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/defaults.nix#L10).

## 3. Novel patterns

- [`modules/plumbing/den/aspect-settings.nix:12-15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/aspect-settings.nix#L12-L15) + [`modules/plumbing/den/_aspect-settings-type.nix:1-40`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/_aspect-settings-type.nix#L1-L40): typed per-aspect `settings`. The
  key is reserved via `den.reservedKeys`, the aspect tree is walked, and one submodule per node with settings becomes an
  option on host and user schemas. It skips den structural, class and quirk keys via
  `den.lib.aspects.fx.keyClassification.isStructuralKey` (`:4,7`).
- [`modules/plumbing/den/classes/aliases.nix:16-48`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/aliases.nix#L16-L48): one `abbreviations` class fanned out to three shells by a list of forwards.
- [`modules/flake/addax-private.nix:3-12`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/addax-private.nix#L3-L12) + `addax-private-stub/flake.nix`: a private overlay repo imported as more
  flake-parts modules, with a committed empty stub so the public repo still evaluates.
- [`modules/hosts/host.nix:11-17`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/host.nix#L11-L17) + `modules/flake/readme.nix`: host `description`/`longDescription` render the README's host
  list ([`README.md:22`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/README.md#L22)), so the docs are generated from den host data.
- [`modules/tests.nix:11-26`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tests.nix#L11-L26): flake checks asserting host builds and HM settings per user@host.

## 4. Library candidates

- aspect-settings · `modules/plumbing/den/aspect-settings.nix` + `_aspect-settings-type.nix` · typed per-aspect settings on host/user · none · options · B (depends on den internals `fx.keyClassification`)
- shell aliases/abbreviations classes · `modules/plumbing/den/classes/aliases.nix` · write aliases once for bash, fish, nushell and zsh · home-manager · none · A
- editor quirk collectors · `modules/plumbing/den/quirks/*.nix` · aspects contribute helix/zed/vscodium packages, settings and extensions · none · quirk values · A
- private-overlay stub · `modules/flake/addax-private.nix` + `addax-private-stub/` · optional private module repo with a public stub · import-tree · none · A

## 5. den friction

- [`modules/hosts/fabrica-nixos/system.nix:13-15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/fabrica-nixos/system.nix#L13-L15) (same at [`modules/hosts/harena-nixos/system.nix:14`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/harena-nixos/system.nix#L14)): FIXME, the user registry key must
  stay `adda` while `userName` differs, because host-level settings are read off `host.users.adda`. User identity versus
  key is confusing in den.
- [`modules/plumbing/den/_aspect-settings-type.nix:4`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/_aspect-settings-type.nix#L4): a reach into `den.lib.aspects.fx.keyClassification`, an internal,
  to tell aspect children from structural keys. den lacks a public "child aspects of a node" API.
- [`modules/hosts/host.nix:11-12`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/host.nix#L11-L12): the comment notes den's `description` is a one-line `str`, so a second option is needed.
- [`modules/users/adda/user.nix:92`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/users/adda/user.nix#L92): `user-shell` cannot be used for `dash`.
- [`modules/aspects/lib.nix:56-122`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/lib.nix#L56-L122): "FIXME: How to do this?" above a commented-out block experimenting with
  `den.lib.parametric.exactly` / `den.lib.take.unused`, so it is unfinished.

## 6. Docs and complexity

A generated README with a per-host prose list, a 13 KB AGENTS.md explaining den building blocks, runbooks and templates,
and a comment ratio of 0.28 with long why-comments ([`modules/users/adda/ssh.nix:5-13`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/users/adda/ssh.nix#L5-L13)): doc_quality 5. Complexity 5:
custom classes, ten quirks, aspect-settings schema machinery, a private overlay, terraform (`modules/tofunix.nix`), work
VMs and checks.

## 6a. Defects and scoring notes

- [`modules/hosts/fabrica-nixos/system.nix:13-15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/fabrica-nixos/system.nix#L13-L15), [`modules/hosts/harena-nixos/system.nix:14`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/harena-nixos/system.nix#L14) · S · moderate · the user registry key must stay `adda` while `userName` differs, because shared aspects read `host.users.adda` by fixed name
- [`modules/aspects/work-vm/default.nix:69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/work-vm/default.nix#L69) · S · minor · a personal SSH key is inline in a shared aspect
- [`modules/aspects/services/pinepods.nix:69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/pinepods.nix#L69) · S · minor · placeholder email with a TODO, not a setting
- [`modules/aspects/lib.nix:56-122`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/lib.nix#L56-L122) · I · minor · a commented-out experimental block ("FIXME: How to do this?")
- [`outputs.nix:1-31`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/outputs.nix#L1-L31) · I · minor · unused flake-parts template scaffolding ([`flake.nix:6`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/flake.nix#L6) bypasses it)
- [`modules/tests.nix:12-29`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tests.nix#L12-L29) · V · minor · most checks are commented-out template checks for hosts that don't exist (igloo, apple); one live check
- [`modules/tofunix.nix:35`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tofunix.nix#L35) · O · minor · the terraform env secret is outside the tree

## 7. Template notes

It is a rich source of den extension techniques: typed aspect settings, multi-target forwarding, quirk collectors and
the private stub. It is too large and too deep in den internals for a first example. A new user should read
`modules/plumbing/den/` and AGENTS.md, not the 20k-line tree.

## 8. Scorecard
### D (7, low)
Scope: `modules/plumbing/den/quirks/*.nix`, `aspect-settings.nix`, caddy/helix/zed consumers, `defaults.nix`.
Pros: live emit->consume channels: `serviceDomains` emitted by about 14 service aspects ([`modules/aspects/services/grafana.nix:39`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/grafana.nix#L39), [`modules/aspects/services/freshrss.nix:62`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/freshrss.nix#L62)) and consumed by [`modules/aspects/services/caddy.nix:9`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/caddy.nix#L9); `helixSettings` consumed with `lib.mkMerge` ([`modules/aspects/development/editors/helix.nix:192`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/development/editors/helix.nix#L192)); zed, vscodium and overlay quirks likewise.
Cons: route is den's default quirk collection; policy routes exist only for flake plumbing ([`modules/plumbing/den/classes/devshell.nix:15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/devshell.nix#L15), [`modules/plumbing/den/classes/nix-unit.nix:25`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/nix-unit.nix#L25)); no missing/duplicate semantics beyond `mkMerge`; shared aspects read `host.users.adda.opt.network.*` by fixed name (about 25 sites, [`modules/aspects/services/caddy.nix:63`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/caddy.nix#L63), [`modules/aspects/services/dns/blocky.nix:17`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/dns/blocky.nix#L17)); [`modules/plumbing/den/aspect-settings.nix:12`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/aspect-settings.nix#L12) builds typed settings but no aspect reads `host.settings`. Capped at 5 by the D rulings.
Hidden evidence: the private addax-private overlay modules ([flake.nix:35](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/flake.nix#L35)) may add more quirk emitters or consumers; direction: D could rise.
Re-score under the quirk ruling (was 5): independent live quirk channels with traced producers and consumers (serviceDomains to [`modules/aspects/services/caddy.nix:9`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/caddy.nix#L9), helixSettings to [`modules/aspects/development/editors/helix.nix:19`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/development/editors/helix.nix#L19), plus zed, vscodium and overlays). Not above 7: no cross-scope policy or pipe routing, no missing/duplicate semantics, fixed-name `host.users.adda` lookups remain.
Confidence: low.

### I (7, medium)
Scope: `modules/aspects/**`, host files, `modules/plumbing/den/`.
Pros: namespace tree by area, hosts are include lists ([`modules/hosts/mensa-nixos/system.nix:60`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/mensa-nixos/system.nix#L60)), plumbing isolated under `plumbing/den/`, cross-feature exclusion assertion ([`modules/aspects/hardware/cpu.nix:7-26`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/hardware/cpu.nix#L7-L26)).
Cons: commented-out experiment ([`modules/aspects/lib.nix:56-122`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/lib.nix#L56-L122)); unused scaffolding [`outputs.nix:1-31`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/outputs.nix#L1-L31); [`modules/aspects/work-vm/default.nix:69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/work-vm/default.nix#L69) mixes an SSH key into a VM profile.
Confidence: medium.

### S (6, medium)
Scope: user/host option files, shared aspects grep.
Pros: contract grade 7: typed per-user `opt.*` submodules with descriptions and defaults ([`modules/aspects/console/vcs/options.nix:1-62`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/console/vcs/options.nix#L1-L62), [`modules/aspects/network/options.nix:9`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/network/options.nix#L9)), host fact `isWorkstation` ([`modules/hosts/host.nix:5`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/host.nix#L5)).
Cons: distinct leaks (6, cap 6): author email default [`modules/aspects/console/vcs/options.nix:35`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/console/vcs/options.nix#L35) (also [`modules/aspects/console/vcs/jujutsu.nix:95`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/console/vcs/jujutsu.nix#L95)), tailnet default [`modules/aspects/network/options.nix:9`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/network/options.nix#L9), SSH key [`modules/aspects/work-vm/default.nix:69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/work-vm/default.nix#L69), `USERNAME = "adda"` and a placeholder email [`modules/aspects/services/pinepods.nix:67-69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/pinepods.nix#L67-L69), user name in [`modules/aspects/development/languages/nix.nix:484`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/development/languages/nix.nix#L484). Shared aspects read `host.users.adda` by fixed key (FIXME [`modules/hosts/fabrica-nixos/system.nix:13-15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/fabrica-nixos/system.nix#L13-L15)). S = min(7, 6) = 6.
```score-evidence
{"S": {"contract_design": 7, "leak_coverage": 6, "distinct_leaks": 6}}
```
Confidence: medium.

### R (6, medium)
Scope: `plumbing/den/classes/aliases.nix`, quirk collectors, `flake/addax-private.nix`.
Pros: grade A: aliases/abbreviations forwarders ([`modules/plumbing/den/classes/aliases.nix:1-40`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/aliases.nix#L1-L40), needs only home-manager), editor quirk collectors, private-overlay stub ([`modules/flake/addax-private.nix:3-12`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/addax-private.nix#L3-L12)); AGENTS.md documents them.
Cons: aspect-settings is grade B and uses a den internal ([`modules/plumbing/den/_aspect-settings-type.nix:4`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/_aspect-settings-type.nix#L4)); no minimal consumer example.
Confidence: medium.

### P (5, medium)
Scope: host list, `isWorkstation` guards, cpu exclusion.
Pros: NixOS (+HM) only, honest scope; guards on `host.isWorkstation` ([`modules/aspects/security/gpg.nix:18`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/security/gpg.nix#L18), [`modules/aspects/virtualisation/default.nix:38`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/virtualisation/default.nix#L38)); mutual-exclusion assertion ([`modules/aspects/hardware/cpu.nix:7-26`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/hardware/cpu.nix#L7-L26)).
Cons: all hosts x86_64 Linux; no boundary checks or other platforms.
Confidence: medium.

### L (8, medium)
Scope: `README.md`, `AGENTS.md`, comments.
Pros: generated README with per-host prose ([`modules/flake/readme.nix:1`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/readme.nix#L1)), a 13 KB AGENTS.md covering building blocks and runbooks, long why-comments ([`modules/users/adda/ssh.nix:5-13`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/users/adda/ssh.nix#L5-L13), [`modules/hosts/mensa-nixos/system.nix:33-48`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/hosts/mensa-nixos/system.nix#L33-L48)).
Cons: no step-by-step tutorial and heavy on den internals.
Confidence: medium.

### V (3, high)
Scope: `modules/tests.nix`, `plumbing/den/classes/nix-unit.nix`, CI workflow.
Pros: one live host-build check and one HM-enabled check ([`modules/tests.nix:12-29`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tests.nix#L12-L29)); a `tests` class routed into nix-unit ([`modules/plumbing/den/classes/nix-unit.nix:10-26`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/nix-unit.nix#L10-L26)).
Cons: most checks are commented template leftovers; the nix-unit class has one user ([`modules/aspects/ai/rules.nix:206`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/ai/rules.nix#L206)); the CI workflow is fully commented ([`modules/flake/ci/workflows/github/gh-actions-check.nix:1-20`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/ci/workflows/github/gh-actions-check.nix#L1-L20)). In-tree checks no CI invokes cap V.
Confidence: high.

### O (3, high)
Scope: `modules/tofunix.nix`, `terraform/tailscale/config.nix`, sops usage, justfile.
Pros: sops secret paths are per-user options ([`modules/aspects/console/vcs/options.nix:47`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/console/vcs/options.nix#L47)); tailnet terraform generated from Nix ([`modules/tofunix.nix:1-35`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tofunix.nix#L1-L35)).
Cons: terraform names `mensa-nixos` literally ([`terraform/tailscale/config.nix:43`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/terraform/tailscale/config.nix#L43)) and never reads den hosts; secret env outside the tree ([`modules/tofunix.nix:35`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/tofunix.nix#L35)); no deploy or builder list from den data.
Confidence: high.

### B (8, medium)
Scope: census record plus aspect reads; B_div 12 -> 9, B_ref 18 -> 7, B = round-half-up((9 + 7) / 2) = 8.
Pros: B_div = 12: selection-verified substantive 1 each: bash, zsh, fish, nushell, starship, zellij, helix, kde, vscode, zed = 10; tmux enable-only 0.5; peers: screen substantive 1, clion/pycharm none 0.5 -> 12, band >11 -> 9 (neovim/nvchad is `defined` only). B_ref lists 18 units (evidence block) after the substantive-useful ruling, each a coherent preset or wired integration and free of `host.users.adda` or identity. Dropped: waydroid (token `enable` plus a personal ~/documents/guitar share), nvchad (mostly commented out: one plugin and a small LSP package list).
Cons: tmux is enable-only and clion/pycharm are installed only; [`modules/aspects/media/music/beets.nix:11`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/media/music/beets.nix#L11) is a one-plugin tweak and was dropped; nvchad is only defined, not selected; [`modules/aspects/work-vm/default.nix:69`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/work-vm/default.nix#L69) and the tailnet-coupled service aspects ([`modules/aspects/services/caddy.nix:63`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/services/caddy.nix#L63)) are excluded for identity and fleet dependency.
```score-evidence
{"B": {"diversity_points": 12.0, "diversity_grade": 9, "reference_grade": 7, "reference_units": [{"name": "lazygit", "evidence": "modules/aspects/console/vcs/lazygit.nix:8"}, {"name": "plasma", "evidence": "modules/aspects/desktop/environments/plasma.nix:80"}, {"name": "fish", "evidence": "modules/aspects/console/shells/fish.nix:20"}, {"name": "atuin", "evidence": "modules/aspects/console/atuin.nix:18"}, {"name": "zellij", "evidence": "modules/aspects/console/terminal-multiplexers/zellij.nix:4"}, {"name": "omp", "evidence": "modules/aspects/ai/omp.nix:422"}, {"name": "vscodium", "evidence": "modules/aspects/development/editors/vscodium.nix:18"}, {"name": "git", "evidence": "modules/aspects/console/vcs/git.nix:19"}, {"name": "xremap", "evidence": "modules/aspects/xremap.nix:10"}, {"name": "browsers", "evidence": "modules/aspects/desktop/browsers.nix:143"}, {"name": "zed", "evidence": "modules/aspects/development/editors/zed-editor.nix:27"}, {"name": "isd", "evidence": "modules/aspects/console/isd.nix:5"}, {"name": "helix", "evidence": "modules/aspects/development/editors/helix.nix:33"}, {"name": "zsh", "evidence": "modules/aspects/console/shells/zsh.nix:16"}, {"name": "starship", "evidence": "modules/aspects/console/shells/starship.nix:4"}, {"name": "intellishell", "evidence": "modules/aspects/console/intellishell.nix:8"}, {"name": "yazi", "evidence": "modules/aspects/console/yazi.nix:5"}, {"name": "languagetool", "evidence": "modules/aspects/services/languagetool.nix:8"}]}}
```
Representative cited units: pro [`modules/aspects/console/vcs/lazygit.nix:8`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/console/vcs/lazygit.nix#L8) and [`modules/aspects/desktop/browsers.nix:143`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/desktop/browsers.nix#L143) are cited at the line where their configuration begins; the other units in the block are cited the same way.
Confidence: medium.

### X (2, high)
Scope: class declarations and terraform.
Pros: classes `devshell`, `files`, `packages`, `tests` exist ([`modules/plumbing/den/classes/devshell.nix:15`](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/devshell.nix#L15)).
Cons: NixOS targets only; tofunix terraform is not fed by den data; the classes are plumbing wrappers.
Confidence: high.


### Total
2*7+7+6+6+5+8+3+8+3/2+2/2 = **59.5/100**

### Shortlist judgment
Not a showcase (D 5, no pipes/policies for facts); library_units are the aliases/abbreviations classes, editor quirk collectors, private-overlay stub and aspect-settings (B); not a starter (20k LOC, den internals).

Overall pros:
- Documented per-user option contracts with defaults and descriptions (`vcs/options.nix`).
- Generated README + AGENTS.md teaches building blocks and runbooks.
- Very wide reference-quality app coverage (B 9) and reusable forwarder classes (`aliases.nix`).

Overall cons:
- Typed aspect-settings machinery has no consumer; shared aspects read `host.users.adda` by fixed key (~25 sites).
- Almost no verification: one live check, CI commented out.
- No ops derived from den data (tofunix names host literally).

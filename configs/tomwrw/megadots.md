# tomwrw/megadots

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/tomwrw/megadots.md)

- Upstream: [tomwrw/megadots](https://github.com/tomwrw/megadots)
- Reviewed revision: [`09aae5c6af50`](https://github.com/tomwrw/megadots/commit/09aae5c6af50ecb9a2e8d0abccfac614ff712f93)
- Author: tomwrw
- Score: **67.5 / 100**, rank 4 of 103 ranked configs. D 8 · I 9 · S 6 · R 7 · P 6 · L 9 · V 5 · O 6 · B 5 · X 2. Shortlists: showcase, library units (4).
- Summary: cross-scope persist/firewall/syncthing quirk channels with documented semantics lift D; typed host schema and a 376-line README lift S contract and L; leaked tasks/locale/network constants cap S at 6; CI instantiates every host but there are no invariants (V 5); NixOS only (X 2).

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
- [Total](#total)
- [Shortlist judgment](#shortlist-judgment)

## 1. Shape

flake-parts + import-tree with flake-file managing inputs per aspect ([`modules/aspects/system/impermanence.nix:10-14`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L10-L14)).
`modules/den/` holds the den-level wiring: defaults, the host roster, schema options, and every quirk and policy in one
file ([`modules/den/quirks.nix:8-11`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L8-L11)). Aspects sit under `modules/aspects/{apps,desktop,hardware,roles,system}`, with
roles composing them. One user, two NixOS hosts, impermanence, lanzaboote and stylix. Both hosts PASS under eval.

## 2. Common patterns

- `den.default includes` with batteries: [`modules/den/defaults.nix:6-9`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/defaults.nix#L6-L9).
- `define-user+primary-user`, `user-shell`: [`modules/users/tomwrw/tomwrw.nix:25-26`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/users/tomwrw/tomwrw.nix#L25-L26).
- `custom schema/classes`: typed host options (`syncthing`, `disk`, `stateVersion`, `network.lanInterface`,
  `linux-kernel.variant`) at [`modules/den/schema.nix:3-71`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L3-L71); user classes `homeManager` + `user` at `:85-88`.
- `quirks`: persist, firewall, theme, terminal, syncthing-peer ([`modules/den/quirks.nix:31,52,66,84,93`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31)).
- `policies`: `pipe.from ... pipe.expose` for user-to-host quirk flow ([`modules/den/quirks.nix:39-44,56-61`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L39-L44)), and
  `pipe.collectAll` across hosts (`:123-146`).
- `mutual-provider`/`provides.to-users` from roles: [`modules/aspects/roles/gaming.nix:16-20`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/roles/gaming.nix#L16-L20), [`modules/aspects/system/libvirt.nix:65`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/libvirt.nix#L65).
- `provides tree` for alternatives: [`modules/aspects/system/boot.nix:33-35`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/boot.nix#L33-L35) (systemd-boot vs lanzaboote),
  [`modules/aspects/apps/zsh.nix:18`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/zsh.nix#L18) (`shell.provides.zsh`).
- unfree battery per aspect: [`modules/aspects/apps/obsidian.nix:5`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/obsidian.nix#L5).

## 3. Novel patterns

- [`modules/den/quirks.nix:100-151`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L100-L151): a fleet-wide Syncthing mesh. Every host emits a `syncthing-peer` record via
  `den.schema.host.includes`; the syncthing aspect collects all of them with `pipe.collectAll` and appends
  external peers from a flake-level option ([`modules/den/hosts.nix:11`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/hosts.nix#L11)). There is no per-host peer list.
- [`modules/den/quirks.nix:17-30`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L17-L30): the `persist` quirk is split into `system` and `home` halves, so one aspect at
  either scope names its paths and impermanence is the sole consumer ([`modules/aspects/system/impermanence.nix:16-17`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L16-L17)).
- [`modules/den/quirks.nix:52-61`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L52-L61): a `firewall` quirk aggregated onto `host.network.lanInterface`, so no aspect opens ports globally.
- [`modules/den/quirks.nix:84-86`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L84-L86): a `terminal` quirk carries a function of `pkgs` so consumers can launch a command in
  whatever terminal is installed.
- [`modules/flake/checks.nix:12-18,26-37`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L12-L18): a check builds every host and greps the tree for private-key needles.

## 4. Library candidates

- persist quirk + impermanence · [`modules/den/quirks.nix:31-44`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31-L44), `modules/aspects/system/impermanence.nix` · split system/home persistence channel · impermanence · quirk values · A
- LAN firewall quirk · [`modules/den/quirks.nix:52-61`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L52-L61) + `modules/aspects/system/networking.nix` · per-aspect ports bound to the LAN iface · none · host option `network.lanInterface` · A
- syncthing mesh · [`modules/den/quirks.nix:93-151`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L93-L151) + `modules/aspects/apps/syncthing.nix` · fleet-wide peer discovery · none · host option `syncthing.id` · A
- terminal quirk · [`modules/den/quirks.nix:84-86`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L84-L86) · terminal-agnostic launchers · none · quirk value (fn of pkgs) · B

## 5. den friction

- Silent drops: quirks emitted at user scope are "collected in the user scope and silently discarded" unless a policy
  exposes them ([`modules/den/quirks.nix:35-36,153-158`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L35-L36)). This is the strongest den signal here.
- [`modules/den/quirks.nix:118-122`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L118-L122): the `pipe.collectAll ({ host, ... }: true)` predicate's formal argument names
  matter. Simplifying to `_: true` "matches nothing, and the mesh silently empties", so a deadnix exemption is
  needed. Dispatch on argument names fights linters.
- [`modules/aspects/roles/gaming.nix:11-15`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/roles/gaming.nix#L11-L15): `provides.<name>` silently matches host names, so a renamed host switched
  features off with no error.
- [`modules/den/schema.nix:73-82`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L73-L82): narrowing `classes` disables home-manager "silently - no eval error".
- `README.md` "Known trade-offs": stylix's HM auto-import must be disabled because den's HM import and
  `home-manager.sharedModules` double-evaluate it.

## 6. Docs and complexity

There is a 22 KB README with layout, a quirks walkthrough, checks, trade-offs and bootstrap steps ([`README.md:90`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L90), `:138`,
`:198`, `:307`). The comment ratio is 0.33, and comments explain the why, often with the failure mode: doc_quality 5.
Complexity 4: only two hosts, but five quirks, three policies, custom host schema and cross-host collection.

## 6a. Defects and scoring notes

- [`modules/flake/tasks.nix:6`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L6) · S · minor · `user = "tomwrw"` is hard-coded in a flake task module
- `modules/aspects/desktop/cosmic.nix` (README "Known trade-offs") · V · minor · the COSMIC aspect is carried but no host evaluates it, so it is untested by the build-every-host check ([`modules/flake/checks.nix:29-34`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L29-L34))
- [`modules/den/quirks.nix:118-122`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L118-L122) · D · minor · the mesh depends on a load-bearing formal-argument name with a deadnix exemption; a lint-driven edit empties it silently (the guard is a comment, not a check)
- README "Known trade-offs" (laptop firewall) · P · minor · LAN-scoped firewall rules bind to the Wi-Fi interface on `flatmate`, so the LAN boundary does not hold on a laptop

- [`modules/flake/tasks.nix:7`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L7) · S · minor · USB path `/run/media/tomwrw/SURVIVOR/keys` fixed (env override exists)
- [`modules/aspects/system/locale.nix:7,13`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/locale.nix#L7) · S · minor · `Europe/London` and `en_GB.UTF-8` in a shared aspect (mkDefault, so overridable)
- [`modules/aspects/system/networking.nix:18-19`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L18-L19) · S · minor · `home.arpa` domain fixed in the shared networking aspect
- [`modules/den/defaults.nix:25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/defaults.nix#L25) · S · minor · HM `stateVersion = "26.05"` literal in `den.default`, while the NixOS one comes from the host schema

## 7. Template notes

It is the best teaching repo in the local set for quirks and policies. Each channel is documented with the failure it
prevents, and it shows how to keep aspects ignorant of consumers. A new user should start with `modules/den/quirks.nix`
and the README. The friction notes in its comments double as a den bug list.

## 8. Scorecard

### D (8, high)
Scope: `modules/den/quirks.nix`, `modules/aspects/system/{impermanence,networking}.nix`, `modules/aspects/apps/syncthing.nix`, `modules/den/schema.nix`.
Chains: (1) persist: emit [`modules/aspects/apps/syncthing.nix:25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L25) / [`modules/aspects/apps/zsh.nix:28`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/zsh.nix#L28) / [`modules/users/tomwrw/tomwrw.nix:117`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/users/tomwrw/tomwrw.nix#L117) -> `pipe.from "persist" [ pipe.expose ]` ([`modules/den/quirks.nix:39-44`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L39-L44), attached at user scope `:155-158`) -> sole consumer [`modules/aspects/system/impermanence.nix:46,57,73-74`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L46), with separate system/home halves so scopes cannot be misread ([`modules/den/quirks.nix:17-26`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L17-L26)). (2) firewall: emit [`modules/aspects/apps/syncthing.nix:14-20`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L14-L20) -> expose ([`modules/den/quirks.nix:56-61`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L56-L61)) -> [`modules/aspects/system/networking.nix:28-31`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L28-L31) onto `host.network.lanInterface`, `lib.unique` for the double emission (`:26-27`) plus an interface assertion (`:34-38`). (3) syncthing mesh: every host emits via `den.schema.host.includes` ([`modules/den/quirks.nix:100-109,151`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L100-L109)), `pipe.collectAll` plus `pipe.append` of external peers (`:123-146`), consumer [`modules/aspects/apps/syncthing.nix:33,42-44,64`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L33); opt-out filtered at the producer (`:97-99,102`). (4) theme and terminal quirks read at two scopes ([`modules/den/quirks.nix:66,84`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L66)).
Missing/duplicate: documented (empty pool warning [`modules/aspects/apps/syncthing.nix:6-8`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L6-L8), silent-drop [`modules/den/quirks.nix:35-36`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L35-L36), unique on firewall); persist lists are not deduplicated and the mesh depends on a formal-argument name guarded only by a comment ([`modules/den/quirks.nix:118-122`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L118-L122)).
Pros: four live routed channels, several consumers, scope-aware, semantics written down. Cons: one dedup gap, one comment-guarded predicate. Between 5 and 9, scored 8 (not 9: no check backs the load-bearing predicate).

Confidence: high.

### I (9, medium)
Scope: tree layout, `endgame/default.nix`, `tomwrw.nix`, `roles/gaming.nix`.
Pros: `apps/ system/ desktop/ hardware/ roles/` with one concern per file; host files are 24-line include lists plus a hardware import ([`modules/hosts/endgame/default.nix:4-23`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/hosts/endgame/default.nix#L4-L23)); user file never names a host ([`modules/users/tomwrw/tomwrw.nix:20-22`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/users/tomwrw/tomwrw.nix#L20-L22)); role-to-user features via `provides.to-users` instead of `provides.<hostname>` ([`modules/aspects/roles/gaming.nix:11-20`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/roles/gaming.nix#L11-L20)); `boot` alternatives as provides ([`modules/aspects/system/boot.nix:33-35`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/boot.nix#L33-L35)). Cons: none on the ledger beyond minor cosmic/tasks coupling.

Confidence: medium.

### S (6, high)
Scope: settings contract and shared-aspect constants across `modules/den/schema.nix`, `modules/aspects/system/*.nix`, `modules/flake/tasks.nix`.
Pros: required no-default host options ([`modules/den/schema.nix:15-45`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L15-L45)), enum kernel variant ([`modules/den/schema.nix:47-70`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L47-L70)), interface assertion ([`modules/aspects/system/networking.nix:34-38`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L34-L38)).
Cons: five distinct constants in shared files ([`modules/flake/tasks.nix:6`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L6), [`modules/flake/tasks.nix:7`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L7), [`modules/aspects/system/locale.nix:7`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/locale.nix#L7), [`modules/aspects/system/networking.nix:18`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L18), [`modules/den/defaults.nix:25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/defaults.nix#L25)).
Contract grade 9: typed host schema with required no-default fields ([`modules/den/schema.nix:15-45`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L15-L45)), `stateVersion` deliberately without a default (`:28-38`), enum kernel variant (`:47-70`), interface assertion ([`modules/aspects/system/networking.nix:34-38`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L34-L38)), `fleet.externalPeers` option ([`modules/den/hosts.nix:11-32`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/hosts.nix#L11-L32)).
Leak grade: about 5 distinct constants in shared files, so cap 6: [`modules/flake/tasks.nix:6`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L6) user, [`modules/flake/tasks.nix:7`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L7) USB path, [`modules/aspects/system/locale.nix:7,13`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/locale.nix#L7) timezone and locale (mkDefault), [`modules/aspects/system/networking.nix:18-19`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L18-L19) `home.arpa`, [`modules/den/defaults.nix:25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/defaults.nix#L25) HM stateVersion literal. Identity sits in the user entity ([`modules/users/tomwrw/tomwrw.nix:7-15,138-139`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/users/tomwrw/tomwrw.nix#L7-L15)), as intended. S = min(9, 6) = 6.

Confidence: high.

```score-evidence
{"S": {"contract_design": 9, "leak_coverage": 6, "distinct_leaks": 5}}
```

### R (7, medium)
Scope: the quirk-based units (persist, firewall, syncthing mesh) and their consumers.
Pros: persist quirk + [`modules/aspects/system/impermanence.nix:16`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L16) is near drop-in; the emitter contract is in the quirk description ([`modules/den/quirks.nix:32`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L32)).
Cons: quirk declarations share one monolith file ([`modules/den/quirks.nix:31-151`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31-L151)); `/persist` is fixed ([`modules/aspects/system/impermanence.nix:24`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L24)); no consumer example outside the README.
persist quirk + `impermanence.nix` is near drop-in: needs the impermanence input (`:10-14`), the quirk and expose policy ([`modules/den/quirks.nix:31-44`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31-L44)), and `/persist` is fixed ([`modules/aspects/system/impermanence.nix:24`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L24)); explicit emitter contract in the description. LAN firewall and syncthing mesh need one host option each ([`modules/den/schema.nix:4-13,40-45`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L4-L13)). Quirk declarations live in a monolith file, so adoption means extracting them. No consumer example beyond the README. Grade A for persist, B for the others; 7.

Confidence: medium.

### P (6, medium)
Scope: platform assumptions across NixOS-only aspects and host schema.
Pros: interface assertion fails clearly ([`modules/aspects/system/networking.nix:34-38`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L34-L38)); platform choices are provides ([`modules/aspects/system/boot.nix:33-35`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/boot.nix#L33-L35)).
Cons: LAN firewall binds to Wi-Fi on the laptop host, so the LAN boundary is weak ([`modules/den/hosts.nix:69`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/hosts.nix#L69)); COSMIC aspect is carried but no host evaluates it ([`modules/aspects/desktop/cosmic.nix:2`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/desktop/cosmic.nix#L2)).
NixOS only and honest about it. Boundary checks: interface assertion ([`modules/aspects/system/networking.nix:34-38`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L34-L38)), COSMIC carried but not host-selected. Con: LAN-scoped firewall binds to Wi-Fi on `flatmate` (README "Known trade-offs"), so the LAN boundary is weak on a laptop.

Confidence: medium.

### L (9, high)
Pros: 22 KB README with layout, quirk walkthrough, checks, trade-offs and bootstrap ([`README.md:90`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L90), [`README.md:138`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L138), [`README.md:198`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L198), [`README.md:307`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L307)); comments give each choice's failure mode ([`modules/den/quirks.nix:118-122`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L118-L122)).
Cons: no short 'add a host' recipe found in the README sections read.
Scope: `README.md` (376 lines), `quirks.nix` comments (comment ratio 0.33). The README teaches layout, the quirk walkthrough, checks, trade-offs and bootstrap ([`README.md:90,138,198,307`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/README.md#L90)); comments give the failure mode of each choice ([`modules/den/quirks.nix:17-30,118-122`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L17-L30), [`modules/den/schema.nix:73-82`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/schema.nix#L73-L82)). Separates the default path from internals. Not 10: no consumer-facing "add a host" quick path checked beyond the README sections.

Confidence: high.

### V (5, high)
Scope: `.github/workflows/check.yml`, `modules/flake/checks.nix`.
Pros: CI builds checks, packages and instantiates every host from a derived list ([`.github/workflows/check.yml:50-80`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/.github/workflows/check.yml#L50-L80)); secrets guard ([`modules/flake/checks.nix:36-68`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L36-L68)).
Cons: no invariants ([`modules/flake/checks.nix:23-25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L23-L25)); no variation, collision or missing-data tests.
CI ([`.github/workflows/check.yml:31-35,44-48,70-80`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/.github/workflows/check.yml#L31-L35)) runs treefmt, flake-file and secrets checks, builds every package and instantiates every host (derived list, `:50-57`); [`modules/flake/checks.nix:29-34`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L29-L34) builds each host and `:36-68` scans for key material and unencrypted secrets files, so the invocation is traceable. Cons: "There are no invariants here" ([`modules/flake/checks.nix:23-25`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/checks.nix#L23-L25)); no enabled/disabled, collision or missing-data tests; COSMIC is never evaluated. 5.

Confidence: high.

### O (6, medium)
Scope: `modules/flake/tasks.nix`, `.sops.yaml`, `modules/aspects/system/sops.nix`, `modules/aspects/system/disko.nix`.
Pros: `deploy` task = nixos-anywhere install derived from `config.flake.nixosConfigurations` ([`modules/flake/tasks.nix:11-47,96-110`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L11-L47)), host disk and swap from the host schema ([`modules/aspects/system/disko.nix:28,126`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/disko.nix#L28)), USB layout mirrors the destination so adding a key needs no repo change ([`modules/flake/tasks.nix:78-95`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L78-L95)); per-host sops files read by `config.networking.hostName` ([`modules/aspects/system/sops.nix:35`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/sops.nix#L35)); packages/apps/devshell from one definition ([`modules/flake/tasks.nix:268-279`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/flake/tasks.nix#L268-L279)). Cons: `.sops.yaml` recipients and creation rules are hand-kept per host ([`.sops.yaml:1-30`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/.sops.yaml#L1-L30)); no fleet deploy or builders data; user constant in tasks.

Confidence: medium.

### B (5)
Scope: census record `census/records/megadots.json` and the aspect files listed in the evidence block.
Pros: 14 self-contained reference aspects (list in the evidence block); substantive configs with the failure modes explained.
Cons: only five selection-verified families; narrow application mix (no WM beyond GNOME).
B_div: 5 selection-verified substantive families (zsh, starship, neovim, gnome, vscode); cosmic is `defined`, not selection-verified, so no peer credit. 5.0 -> band <=5 -> 3.
B_ref (14 units, band <=19 -> 7): neovim [`modules/aspects/apps/neovim.nix:59`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/neovim.nix#L59); gnome [`modules/aspects/desktop/gnome.nix:4`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/desktop/gnome.nix#L4); firefox [`modules/aspects/apps/firefox.nix:28`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/firefox.nix#L28); stylix [`modules/aspects/desktop/stylix.nix:86`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/desktop/stylix.nix#L86); vscodium [`modules/aspects/apps/vscodium.nix:5`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/vscodium.nix#L5); zsh+starship [`modules/aspects/apps/zsh.nix:18`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/zsh.nix#L18); git [`modules/aspects/apps/git.nix:3`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/git.nix#L3); steam [`modules/aspects/apps/steam.nix:13`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/steam.nix#L13); sunshine [`modules/aspects/apps/sunshine.nix:3`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/sunshine.nix#L3); impermanence [`modules/aspects/system/impermanence.nix:16`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L16); disko [`modules/aspects/system/disko.nix:10`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/disko.nix#L10); libvirt [`modules/aspects/system/libvirt.nix:3`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/libvirt.nix#L3); ssh [`modules/aspects/apps/ssh.nix:12`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/ssh.nix#L12); syncthing [`modules/aspects/apps/syncthing.nix:5`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L5).
B = round-half-up((3 + 7) / 2) = 5.

Confidence: medium.

```score-evidence
{"B": {"diversity_points": 5.0, "diversity_grade": 3, "reference_grade": 7, "reference_units": [{"name": "neovim", "evidence": "modules/aspects/apps/neovim.nix:59"}, {"name": "gnome", "evidence": "modules/aspects/desktop/gnome.nix:4"}, {"name": "firefox", "evidence": "modules/aspects/apps/firefox.nix:28"}, {"name": "stylix", "evidence": "modules/aspects/desktop/stylix.nix:86"}, {"name": "vscodium", "evidence": "modules/aspects/apps/vscodium.nix:5"}, {"name": "zsh+starship", "evidence": "modules/aspects/apps/zsh.nix:18"}, {"name": "git", "evidence": "modules/aspects/apps/git.nix:3"}, {"name": "steam", "evidence": "modules/aspects/apps/steam.nix:13"}, {"name": "sunshine", "evidence": "modules/aspects/apps/sunshine.nix:3"}, {"name": "impermanence", "evidence": "modules/aspects/system/impermanence.nix:16"}, {"name": "disko", "evidence": "modules/aspects/system/disko.nix:10"}, {"name": "libvirt", "evidence": "modules/aspects/system/libvirt.nix:3"}, {"name": "ssh", "evidence": "modules/aspects/apps/ssh.nix:12"}, {"name": "syncthing", "evidence": "modules/aspects/apps/syncthing.nix:5"}]}}
```

### X (2, high)
Scope: non-host targets: none found in `modules/flake/tasks.nix` or `modules/den/hosts.nix`.
Pros: n/a (baseline).
Cons: only NixOS hosts with HM ([`modules/den/hosts.nix:47-72`](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/hosts.nix#L47-L72)).
Only NixOS hosts with HM; no non-host target class. Baseline per the X ruling.

Confidence: high.

## Total
2*8 + 9 + 6 + 7 + 6 + 9 + 6 + 5 + 5/2 + 2/2 = 16 + 9 + 6 + 7 + 6 + 9 + 6 + 5 + 2.5 + 1 = **67.5/100**

## Shortlist judgment
- showcase: yes. D leads (8) and the quirk/scope design is the best teaching material in this batch; L 9, I 9.
- library_units: persist quirk + impermanence consumer (A), LAN firewall quirk (B), syncthing mesh (B), terminal quirk (B).
- starter: no. The entry path is short, but it assumes impermanence, lanzaboote, sops and per-host disk ids.

Overall pros: documented quirk channels that cross scopes and hosts; typed host schema with no-default install facts; CI that instantiates every host plus a secrets guard; README and comments that give the failure mode of each choice. Cons: leaked constants in tasks/locale/network files; no invariant tests; monolithic quirks file; comment-guarded predicate name; LAN firewall weak on the laptop.

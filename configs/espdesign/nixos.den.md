# espdesign/nixos.den

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/espdesign/nixos.den.md)

- Upstream: [espdesign/nixos.den](https://github.com/espdesign/nixos.den)
- Reviewed revision: [`f52aed42f511`](https://github.com/espdesign/nixos.den/commit/f52aed42f511eef8b036676309c42c32bd657175)
- Author: espdesign
- Score: **38.5 / 100**, rank 93 of 103 ranked configs. D 3 · I 6 · S 3 · R 5 · P 5 · L 4 · V 5 · O 3 · B 3 · X 2. Shortlists: starter, library units (3).
- Summary: no quirks or policies and host variation by literal names (D 3); more than ten leaked LAN/host/device constants and no settings contract (S 3); CI flake check plus per-host builds on lock update (V 5); short readable tree with README and AGENTS rules (L 4, starter).

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

A plain flake with no flake-parts: `outputs` calls `lib.evalModules` over `import-tree ./modules` and returns
`config.flake` ([`flake.nix:26-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L26-L40)). den comes in through `inputs.den.flakeModule` ([`modules/den.nix:8`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L8)). The repo is flat:
one file per feature under `modules/`, host aspects in `modules/hosts/`, users in `modules/users/`, and all four
`den.hosts` declared in one place ([`modules/den.nix:18-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L18-L30)). Every host PASSes under eval.

## 2. Common patterns

- `define-user+primary-user`, `user-shell` via `den.provides.*`: [`modules/users/espdesign.nix:16-18`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L16-L18), [`modules/users/jake.nix:8-9`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/jake.nix#L8-L9).
- `mutual-provider` set on the user schema, with `provides.to-users.includes` on hosts: [`modules/den.nix:16`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L16), [`modules/hosts/hinekora.nix:15-27`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hosts/hinekora.nix#L15-L27).
- `den.default includes` + shared class config: [`modules/default.nix:6-20`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L6-L20).
- `parametric aspect (fn args)`: [`modules/auto-upgrade.nix:3-4`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L3-L4) (`{ host, ... }` builds the flake URI at `:14`), [`modules/users/espdesign.nix:6-12`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L6-L12).
- `provides tree`: `den.aspects.gnome.provides.<user>` for per-user dconf (stated in `AGENTS.md`, rule "Aspect Granularity").
- unfree battery per aspect: [`modules/nvidia.nix:5`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/nvidia.nix#L5), [`modules/rustdesk.nix:5`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/rustdesk.nix#L5).
- `den.schema.user.classes = mkDefault [ "homeManager" ]`: [`modules/den.nix:11`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L11).

## 3. Novel patterns

- [`flake.nix:35-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L35-L40): strips den-internal attrs (`denful`, `resolved`, `id_hash`, `collisionPolicy`) from
  `config.flake` before returning outputs. Without flake-parts, den's internal flake attrs leak into the flake outputs.
- `.agents/skills/den-debugging/SKILL.md` and `AGENTS.md`: agent-facing rules for den, e.g. "never `{ ... }:` because
  `functionArgs` returns `{}`" (AGENTS.md "Aspect Functions" rule). It is a user-written explanation of den's dispatch
  semantics.
- `modules/auto-upgrade.nix`: a self-updating host that pulls `github:espdesign/nixos.den#<host>` with a fast-forward-only
  guard (`:77-79`).

## 4. Library candidates

- auto-upgrade · `modules/auto-upgrade.nix` · systemd auto-upgrade from a flake URI, with desktop notification and an ff-only guard · none · fn args (`host`) · B (repo URL hardcoded at `:14`)
- hardened-server · `modules/hardened-server.nix` · fail2ban sshd jail and server hardening (`:7-19`) · none · none · B

## 5. den friction

- [`flake.nix:35-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L35-L40): den leaks internal attrs (`denful`, `resolved`, `id_hash`, `collisionPolicy`) into `config.flake`
  when used without flake-parts, and users must `removeAttrs` them by hand.
- Re-implemented batteries: `den.aspects.autologin-vm` ([`modules/vm.nix:43-54`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/vm.nix#L43-L54)) duplicates den's `vm-autologin`
  battery, and `den.provides.tty-autologin` ([`modules/vm.nix:57`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/vm.nix#L57)) redefines den's own `tty-autologin` battery name
  (present in den main at `modules/aspects/batteries/tty-autologin.nix`).
- [`modules/users/espdesign.nix:8-12`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L8-L12): `host ? null` plus a `hostName != "valako"` test inside a user aspect. Host-name
  branching in a user aspect means the host-to-user context had no cleaner selector, such as a host role or a
  per-host include.

## 6. Docs and complexity

README explains den concepts and maps them to the directory layout (`README.md` "Structure"). AGENTS.md documents
composition rules, and comment ratio is 0.11, the highest in the local set. doc_quality 4. Complexity 2: four NixOS
hosts, two users, plain aspects and batteries, no custom classes or policies.

## 6a. Defects and scoring notes

- [`modules/pipewire.nix:23`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/pipewire.nix#L23), [`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10), [`modules/dev.nix:64`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/dev.nix#L64) · S · moderate · shared aspects branch on literal host names (`hinekora`, `valako`) instead of a host fact
- [`modules/users/espdesign.nix:12`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L12) · S · minor · the user aspect branches on `hostName != "valako"`
- [`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14) · S · moderate · the flake URI `github:espdesign/nixos.den` is fixed inside the auto-upgrade aspect
- [`modules/default.nix:27-38`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L27-L38) · S · minor · a LAN hosts table with fixed IPs sits in `den.default`
- [`modules/hardened-server.nix:11-13`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hardened-server.nix#L11-L13) · S · minor · trusted LAN CIDRs are inline rather than a setting
- [`modules/vm.nix:43-57`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/vm.nix#L43-L57) · I · minor · re-implements den's `vm-autologin` and redefines the `tty-autologin` battery name
- [`flake.nix:35-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L35-L40) · I · minor · hand-stripping of den-internal flake attrs (a workaround for den, recorded once here)
- repo-wide · V · minor · no flake `checks` found by a repo-wide grep; observation only

- [`modules/gnome.nix:32-73`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/gnome.nix#L32-L73) · I · minor · per-user dconf blocks for `espdesign` and `jake` live inside the shared gnome aspect
- [`modules/syncthing.nix:16-35`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/syncthing.nix#L16-L35) · S · moderate · device IDs and host names of all peers inline in a shared aspect
- [`modules/default.nix:42-56`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L42-L56) · S · minor · timezone and locale inline; a user file also carries a committed credential (reported privately; not located here)
- [`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14) (kept) and [`modules/default.nix:27-39`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L27-L39) (kept) count toward the 11-30 leak band, S cap 5

## 7. Template notes

It is a good first example: one-file-per-feature, explicit `den.hosts` table, batteries by name, `provides.to-users`
for host-driven user features, and comments that explain why. Avoid copying [`flake.nix:35-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L35-L40) without understanding
it, the host-name branch in `espdesign.nix`, and the hand-rolled autologin, which den already ships.

## 8. Scorecard

### D (3, high)
Pros: parametric context args used for `host.hostName` ([`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14)) and `user.userName` ([`modules/virt-manager.nix:15`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/virt-manager.nix#L15)).
Cons: literal host-name branches ([`modules/pipewire.nix:23`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/pipewire.nix#L23), [`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10)); no quirks, pipes or policies.
Scope: `modules/den.nix`, `modules/default.nix`, parametric aspects (`auto-upgrade.nix`, `docker.nix`, `pipewire.nix`, `dev.nix`, `users/espdesign.nix`).
No quirks, pipes, policies or custom schema. Channels: `{ host }` / `{ user }` context args used for `host.hostName` in the auto-upgrade URI ([`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14)) and `user.userName` in groups ([`modules/virt-manager.nix:15`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/virt-manager.nix#L15), [`modules/homelab-compose.nix:28`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/homelab-compose.nix#L28)). Variation across hosts is by literal-name tests ([`modules/pipewire.nix:23`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/pipewire.nix#L23), [`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10), [`modules/dev.nix:64`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/dev.nix#L64), [`modules/users/espdesign.nix:12`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L12)), which the D ruling caps at 4. The syncthing roster and LAN host table are literal data ([`modules/syncthing.nix:16-35`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/syncthing.nix#L16-L35), [`modules/default.nix:26-39`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L26-L39)), not derived from `den.hosts`. Scored 3.

Confidence: high.

### I (6, medium)
Scope: `modules/den.nix`, `modules/hosts/*.nix`, shared feature files.
Pros: one file per feature, `hosts/` and `users/` split, hosts are include lists via `provides.to-users` ([`modules/hosts/hinekora.nix:15-27`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hosts/hinekora.nix#L15-L27)), granularity rules written down (AGENTS.md "Aspect Granularity"), `_nixos/` for generated hardware. Cons: [`modules/default.nix:14-57`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L14-L57) puts bootloader, timezone, locale and a host table in `den.default`; [`modules/gnome.nix:32-73`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/gnome.nix#L32-L73) embeds per-user blocks for `espdesign` and `jake` inside the shared aspect; [`modules/vm.nix:43-57`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/vm.nix#L43-L57) re-implements den batteries; `docker.nix`/`dev.nix` mix host-conditional behaviour into features.

Confidence: medium.

### S (3, high)
Scope: shared aspects and `den.default`.
Pros: user identity kept in user files ([`modules/users/espdesign.nix:85-87`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L85-L87)).
Cons: no settings contract; more than ten constants inline ([`modules/default.nix:27-38`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L27-L38), [`modules/syncthing.nix:17-34`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/syncthing.nix#L17-L34), [`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14)).
Contract grade 3: no settings or options; variation by editing aspects or testing the host name. Leak grade: well over 10 distinct constants in shared files, cap 5: host names `hinekora`/`kitava`/`valako` ([`modules/pipewire.nix:23`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/pipewire.nix#L23), [`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10), [`modules/dev.nix:64`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/dev.nix#L64), [`modules/users/espdesign.nix:12`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/users/espdesign.nix#L12)), IPs and domains ([`modules/default.nix:27-38`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L27-L38)), timezone and locale ([`modules/default.nix:42-56`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L42-L56)), device IDs ([`modules/syncthing.nix:17-34`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/syncthing.nix#L17-L34)), flake URI ([`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14)), LAN CIDRs ([`modules/hardened-server.nix:11-14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hardened-server.nix#L11-L14)), mount paths ([`modules/homelab-compose.nix:28-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/homelab-compose.nix#L28-L30)), per-user dconf blocks ([`modules/gnome.nix:34,73`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/gnome.nix#L34)), state versions ([`modules/default.nix:12,19`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/default.nix#L12)). S = min(3, 5) = 3. Identity in a user file is acceptable.

Confidence: high.

```score-evidence
{"S": {"contract_design": 3, "leak_coverage": 5, "distinct_leaks": 14}}
```

### R (5, medium)
Scope: `modules/auto-upgrade.nix`, `modules/hardened-server.nix`, `modules/nvidia.nix`.
Pros: nvidia is drop-in ([`modules/nvidia.nix:3-31`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/nvidia.nix#L3-L31)); the other two need at most three values.
Cons: no documentation or consumer example per unit ([`modules/hardened-server.nix:10-15`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hardened-server.nix#L10-L15)).
`auto-upgrade.nix` (needs the flake URI, `:14`) and `hardened-server.nix` (needs the CIDRs, `:10-15`) are adoptable by changing at most three values; `nvidia.nix` is nearly drop-in ([`modules/nvidia.nix:3-31`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/nvidia.nix#L3-L31)). No docs per unit or consumer example. 5.

Confidence: medium.

### P (5, medium)
Pros: NixOS-only scope is stated and hardware is isolated ([`modules/den.nix:18-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L18-L30)).
Cons: no boundary checks; host-name branches inside features ([`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10)).
Honest narrow scope: x86_64 NixOS hosts only ([`modules/den.nix:18-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/den.nix#L18-L30)). Hardware modules isolated in `_nixos/`. Host-name branches in features ([`modules/docker.nix:10`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/docker.nix#L10)) are a boundary smell filed under S, not deducted twice.

Confidence: medium.

### L (4, medium)
Scope: `README.md` (40 lines), `AGENTS.md`, `.agents/skills/den-debugging/SKILL.md`.
Pros: `README.md` maps den concepts onto the directory layout and gives a quick start (`nix flake check`, `nix run .#vm`); [`AGENTS.md:1-24`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/AGENTS.md#L1-L24) states composition rules and a debugging skill (`.agents/skills/den-debugging/SKILL.md`). Cons: 40-line README defers to den docs, no "add a host/user" walk-through; comment ratio 0.11.

Confidence: medium.

### V (5, medium)
Scope: `.github/workflows/ci.yml`, `.github/workflows/update-flake.yml`, `.github/scripts/*.sh`.
Pros: flake check with warnings as errors ([`.github/scripts/flake-check.sh:5-15`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/.github/scripts/flake-check.sh#L5-L15)); per-host builds on lock update ([`.github/workflows/update-flake.yml:51-70`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/.github/workflows/update-flake.yml#L51-L70)).
Cons: no in-tree checks; no variation tests.
CI ([`.github/workflows/ci.yml:16-24`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/.github/workflows/ci.yml#L16-L24)) runs `nix flake check` with evaluation warnings promoted to errors (`.github/scripts/flake-check.sh`) and a lint job (nixfmt, deadnix, statix: `lint.sh`); [`.github/workflows/update-flake.yml:15-70`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/.github/workflows/update-flake.yml#L15-L70) builds every host (list from `modules/hosts/*.nix`, `discover-hosts.sh`) on each lock update. No in-tree checks and no variation tests. 5.

Confidence: medium.

### O (3, medium)
Scope: `modules/auto-upgrade.nix`, `.github/workflows/update-flake.yml`, `modules/users/espdesign.nix`.
Pros: auto-upgrade derives the flake attribute from the host ([`modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14)); daily lock update with build matrix ([`.github/workflows/update-flake.yml:15-30`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/.github/workflows/update-flake.yml#L15-L30)).
Cons: no deploy, secrets or bootstrap from den data; a committed credential (reported privately; not located here).
`auto-upgrade.nix` pulls the host's own flake attribute from `host.hostName` with an ff-only guard (`:14,77-79`); daily lock update PR with per-host build matrix (`update-flake.yml`). No deploy, secrets or bootstrap derived from den data; the repo carries a committed credential (reported privately; not located here). 3.

Confidence: medium.

### B (3)
Scope: census record `census/records/nixos.den.json` and the aspect files in the evidence block.
Pros: five substantive families; nvidia and steam aspects are self-contained.
Cons: only two reference units; most aspects carry host or user names.
B_div: 5 selection-verified substantive families (zsh, starship, neovim, gnome, vscode). 5.0 -> band <=5 -> 3.
B_ref (2 units, band <=2 -> 2): nvidia [`modules/nvidia.nix:3`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/nvidia.nix#L3); steam/gamemode [`modules/gaming/default.nix:3`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/gaming/default.nix#L3). Others carry host names, user names or package lists only (`gnome.nix`, `docker.nix`, `cli.nix`, `fonts.nix`).
B = round-half-up((3 + 2) / 2) = 3.

Confidence: medium.

```score-evidence
{"B": {"diversity_points": 5.0, "diversity_grade": 3, "reference_grade": 2, "reference_units": [{"name": "nvidia", "evidence": "modules/nvidia.nix:3"}, {"name": "steam-gamemode", "evidence": "modules/gaming/default.nix:3"}]}}
```

### X (2, high)
NixOS and HM only; the `vm` runner ([`modules/vm.nix:11-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/vm.nix#L11-L40)) is a convenience package, not a class.

Confidence: high.

## Total
2*3 + 6 + 3 + 5 + 5 + 4 + 3 + 3 + 5/2 + 2/2 = 6 + 6 + 3 + 5 + 5 + 4 + 3 + 3 + 2.5 + 1 = **38.5/100**

## Shortlist judgment
- showcase: no. D is 3.
- library_units: auto-upgrade (B), hardened-server (B), nvidia (A, small).
- starter: yes, with caveats. Short path (`flake.nix` -> `den.nix` -> hosts table), few prerequisites, README plus AGENTS rules, honest NixOS-only scope. Do not copy the host-name branches or the [`flake.nix:35-40`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/flake.nix#L35-L40) attribute stripping.

Overall pros: very small readable tree; explicit hosts table; agent-facing composition rules; CI that fails on evaluation warnings and builds every host on lock updates. Cons: no data flow beyond context args; literal host names and LAN data in shared aspects; re-implemented den batteries; no in-tree tests.

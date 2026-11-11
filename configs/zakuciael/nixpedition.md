# zakuciael/nixpedition

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/zakuciael/nixpedition.md)

- Upstream: [zakuciael/nixpedition](https://github.com/zakuciael/nixpedition)
- Reviewed revision: [`b45ae683a1b2`](https://github.com/zakuciael/nixpedition/commit/b45ae683a1b29f465bb683d6b73974e167c2080f)
- Author: zakuciael
- Score: **57.5 / 100**, rank 20 of 103 ranked configs. D 7 · I 8 · S 6 · R 5 · P 5 · L 2 · V 6 · O 8 · B 3 · X 7. Shortlists: showcase, library units (4).
- Summary: host constants feed nixos, a traefik quirk and a routed terranix class (D 7, X 7); deploy effect, clan vars and terraform derive from host config (O 8); identity constants in service aspects cap S at 6; stale README (L 2); few applications (B 3).

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

flake-file generated flake ([`nix/dendritic.nix:7-18`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/dendritic.nix#L7-L18)), flake-parts + import-tree over `nix/` and `modules/`. den is
pinned to `vic/den/v0.17.0` with `flake-aspects/v0.7.0` ([`nix/den.nix:14-17`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L14-L17)). Hosts live in `machines/<name>/` and
are instantiated as clan machines rather than `nixosConfigurations` ([`nix/den.nix:20-29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20-L29)). Features are grouped in
three namespaces: `hardware`, `services`, `virtualisation`. Both hosts (esquie, francois) PASS under eval.

## 2. Common patterns

- `namespace`: [`modules/hardware/default.nix:4`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/hardware/default.nix#L4), [`modules/services/default.nix:4`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/default.nix#L4), [`modules/virtualisation/default.nix:4`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/virtualisation/default.nix#L4);
  aspects are then written as `services.traefik.nixos` ([`modules/services/traefik/default.nix:6`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L6)).
- `angle-bracket refs` into namespaces: [`machines/esquie/default.nix:14-17`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/machines/esquie/default.nix#L14-L17) (`<hardware/amdgpu/sea-islands>`).
- `mutual-provider` and `define-user` in schema includes: [`modules/defaults/config.nix:21-22`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/config.nix#L21-L22), plus `den.batteries.inputs'/self'` `:24-25`.
- `define-user+primary-user`: [`modules/users/zakuciael.nix:9`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/users/zakuciael.nix#L9).
- `den.default includes` as plain class config: [`modules/defaults/nix-index.nix:8`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/nix-index.nix#L8), [`modules/defaults/vm-variants.nix:3`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/vm-variants.nix#L3).
- `quirks`: `den.quirks.traefik` ([`modules/services/traefik/default.nix:2`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L2)), consumed as a module arg `:8` and folded at `:23`;
  produced by service aspects, e.g. [`modules/services/niks3/traefik.nix:2`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/traefik.nix#L2).
- `forward`: [`modules/services/terranix/routing.nix:73`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L73).
- `policies` + `custom schema/classes`: `terranix` class + `policy.instantiate` ([`modules/services/terranix/routing.nix:101-120`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L101-L120)).

## 3. Novel patterns

- [`nix/den.nix:20-29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20-L29): `den.schema.host` overrides `instantiate` to a bare `{ imports = modules; }` and `intoAttr` to
  `clan.machines.<host>`, so den produces clan machine modules and clan does the NixOS instantiation.
- [`modules/services/terranix/routing.nix:70-120`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L70-L120): per-host terranix, split into `.global` (collected flake-wide via
  `policy.instantiate` into `terranixModules.<host>`) and `.local` (forwarded into the host's `services.terranix`
  with `osConfig` passed through). Infrastructure-as-code is co-located with the service aspect that needs it.
- [`modules/defaults/user-vars.nix:59-67`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/user-vars.nix#L59-L67): `den.lib.aspects.resolve "nixos"` turns a parametric aspect into a module for
  `root`, so per-user clan-vars secrets are reused for a non-den user.
- [`modules/defaults/config.nix:29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/config.nix#L29): `user.classes = mkDefault [ "homeManager" ]` set at the schema level.

## 4. Library candidates

- traefik quirk · `modules/services/traefik/default.nix` · aspects contribute traefik dynamic files; one aspect writes them · none · quirk values · A
- terranix routing · `modules/services/terranix/routing.nix` · per-host terraform modules (global and local) from aspects · terranix · class content · B
- nixos-containers · `modules/virtualisation/nixos-containers/` · container NAT plus an options/mapper layer · none · options · B

## 5. den friction

- [`modules/services/terranix/routing.nix:12-28`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L12-L28): quirks inject collision-validator modules that set `warnings`/`assertions`,
  so any private `evalModules` that consumes quirks must declare those options. This is a leak of den internals into
  non-NixOS classes and is worth fixing in den.
- `__findFile ? __findFile` with `# deadnix: skip` repeats across files ([`modules/defaults/config.nix:4-5`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/config.nix#L4-L5),
  [`machines/esquie/default.nix:3-4`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/machines/esquie/default.nix#L3-L4), [`modules/virtualisation/nixos-containers/default.nix:2-3`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/virtualisation/nixos-containers/default.nix#L2-L3)). The angle-bracket
  arg trips linters.
- Pinned to den v0.17.0 / flake-aspects v0.7.0 ([`nix/den.nix:15-16`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L15-L16)). Against current den main, schema/`intoAttr`
  semantics may drift; the eval PASS was measured on the repo's own lock.

## 6. Docs and complexity

README has a structure tree and machine table ([`README.md:36-63`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L36-L63)), but the tree is stale. It lists `modules/hosts/`,
`modules/lib.nix` and `defaults.nix`, while the repo uses `machines/` and `modules/defaults/`. `TODO.md` holds design
notes on terranix. doc_quality 2. Complexity 4: only two hosts, but clan integration, a custom class with
instantiate + forward policies, quirks and namespaces.

## 6a. Defects and scoring notes

- [`modules/services/traefik/default.nix:103`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L103) · S · moderate · the ACME contact email is hard-coded in the shared traefik service aspect
- [`README.md:36-49`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L36-L49) · L · minor · the structure tree is stale (lists `modules/hosts/`, `modules/lib.nix`, `defaults.nix`; the repo uses `machines/`, `modules/defaults/`)
- [`modules/services/terranix/routing.nix:15-28`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L15-L28) · I · minor · a compat options shim (`warnings`/`assertions`) is needed so private `evalModules` survive quirk validators; the workaround lives in the feature, not in a shared helper
- [`nix/den.nix:15-16`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L15-L16) · V · minor · den and flake-aspects pinned to old tags (v0.17.0/v0.7.0); upgrade boundary unstated

- [`modules/services/niks3/default.nix:78-81`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L78-L81), [`modules/services/nixbot/default.nix:69-70`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/nixbot/default.nix#L69-L70), [`modules/services/nixbot/vars.nix:40,56`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/nixbot/vars.nix#L40) · S · moderate · GitHub owners/repos fixed in service aspects
- [`modules/services/terranix/global/providers/ovh.nix:8,22-25`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/global/providers/ovh.nix#L8) · S · minor · the `francois` VPS name is a literal in the provider module
- [`modules/services/traefik/default.nix:23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L23) · D · minor · dynamic files merge by `recursiveUpdate`, so duplicate names merge silently with no stated semantics
- [`README.md:41-62`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L41-L62) · L · moderate · lists hosts `maelle` and `sciel` that are not in the tree (README "stale tree" fact kept)

## 7. Template notes

It is the best corpus example of den feeding another framework (clan) through `den.schema.host` instantiate/intoAttr, and
of a non-OS class (terranix) with a global/local split. It is too specialised for a first example. The traefik quirk is a
clean, small teaching case for quirks.

## 8. Scorecard

### D (7, medium)
Pros: three routed channels with several consumers ([`modules/services/traefik/default.nix:23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L23), [`modules/defaults/constants.nix:61-77`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/constants.nix#L61-L77), [`modules/services/terranix/routing.nix:103-120`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L103-L120)).
Cons: duplicate dynamic files merge silently ([`modules/services/traefik/default.nix:23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L23)); no stated missing-data semantics.
Scope: `modules/services/traefik`, `niks3/*`, `nixbot/*`, `modules/defaults/constants.nix`, `modules/services/terranix/routing.nix`.
Chain 1 (quirk): declare [`modules/services/traefik/default.nix:2`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L2); producers [`modules/services/niks3/traefik.nix:2-37`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/traefik.nix#L2-L37) (and nixbot's `traefik.nix`); consumer [`modules/services/traefik/default.nix:6-8,23,123-135`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L6-L8) folds all emissions into per-name dynamic files via tmpfiles. Chain 2 (host constants): producer [`modules/defaults/constants.nix:61-77`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/constants.nix#L61-L77) reads per-machine clan vars files into typed `host.constants`; consumers in three classes: nixos ([`modules/services/niks3/default.nix:22-27`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L22-L27)), traefik quirk ([`modules/services/niks3/traefik.nix:5`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/traefik.nix#L5)) and terranix ([`modules/services/niks3/terranix.nix:13`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/terranix.nix#L13)). Chain 3 (terranix class): `policies.host-to-terranix` with `policy.instantiate` into `terranixModules.<host>` ([`modules/services/terranix/routing.nix:103-115`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L103-L115)) plus `batteries.forward` of the `local` part into `services.terranix` (`:70-97`, included at `:117-120`). Chain 4: den.default clan CI key generators ([`modules/defaults/ci.nix:17-64`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/ci.nix#L17-L64)).
Missing/duplicate: quirk values merge by `recursiveUpdate` ([`modules/services/traefik/default.nix:23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L23)), so a duplicate dynamic file name merges silently; no explicit semantics. Scored 7 (routed policies, several consumers; duplicate semantics unstated).

Confidence: medium.

### I (8, medium)
Scope: `modules/services/*`, `machines/*`, `nix/*`.
Pros: three namespaces, one directory per service with the nixos/traefik/terranix/vars split by file (`niks3/`), thin machine files ([`machines/esquie/default.nix:8-19`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/machines/esquie/default.nix#L8-L19), angle-bracket refs), hardware/disko separated. Cons: private `evalModules` compat shim lives inside the feature ([`modules/services/terranix/routing.nix:12-28`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L12-L28)); [`nix/den.nix:11`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L11) globs machines.

Confidence: medium.

### S (6, high)
Scope: `modules/defaults/constants.nix`, service aspects and providers.
Pros: typed host constants from clan prompts ([`modules/defaults/constants.nix:12-23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/constants.nix#L12-L23), [`modules/services/niks3/vars.nix:23-40`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/vars.nix#L23-L40)).
Cons: identity constants in service aspects ([`modules/services/traefik/default.nix:103`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L103), [`modules/services/niks3/default.nix:78-81`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L78-L81), [`modules/services/nixbot/default.nix:69-70`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/nixbot/default.nix#L69-L70)).
Contract grade 8: per-host typed constants from clan prompts with a type for values ([`modules/defaults/constants.nix:12-23`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/constants.nix#L12-L23), [`modules/services/niks3/vars.nix:13-40`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/vars.nix#L13-L40)), `mkDefault` hooks ([`modules/services/niks3/default.nix:42`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L42), [`modules/services/traefik/default.nix:93`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L93)). Leak grade, about 6 distinct constants in shared aspects, cap 6: ACME email [`modules/services/traefik/default.nix:103`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L103); GitHub owners [`modules/services/niks3/default.nix:78-81`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L78-L81), [`modules/services/nixbot/default.nix:69-70`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/nixbot/default.nix#L69-L70), [`modules/services/nixbot/vars.nix:40,56`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/nixbot/vars.nix#L40); `francois` VPS in the OVH provider [`modules/services/terranix/global/providers/ovh.nix:8,22-25`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/global/providers/ovh.nix#L8); bucket location [`modules/services/niks3/terranix.nix:47`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/terranix.nix#L47); zone [`nix/terranix/emails.nix:24`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/terranix/emails.nix#L24). S = min(8, 6) = 6.

Confidence: high.

```score-evidence
{"S": {"contract_design": 8, "leak_coverage": 6, "distinct_leaks": 7}}
```

### R (5, medium)
Scope: traefik quirk, terranix routing, nixos-containers.
Pros: traefik quirk needs about three values ([`modules/services/traefik/default.nix:43`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L43), [`modules/services/traefik/default.nix:103`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L103)).
Cons: terranix routing needs `modules/services/terranix/_types.nix`; no docs or consumer example.
traefik quirk adoption needs the ACME email, resolver/provider and the sops template path ([`modules/services/traefik/default.nix:43,98-105`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L43)): about three values, grade A/B. terranix routing needs `_types.nix` and a utils set (grade B). nixos-containers has an options/mapper layer (`nixos-containers/options.nix`, B). No consumer example or docs. 5.

Confidence: medium.

### P (5, medium)
Pros: VM variants handled ([`modules/services/traefik/default.nix:139-152`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L139-L152)); soft guard ([`modules/services/terranix/routing.nix:83`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L83)).
Cons: x86_64 NixOS via clan only; README names hosts not in the tree ([`README.md:58-61`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L58-L61)).
x86_64 NixOS only, through clan; VM variants handled ([`modules/services/traefik/default.nix:139-152`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L139-L152), [`modules/services/niks3/default.nix:35-38`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L35-L38)); `guard` on `options.services ? terranix` ([`modules/services/terranix/routing.nix:83`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L83)) fails soft. Honest narrow scope. README lists hosts that are not in the tree.

Confidence: medium.

### L (2, high)
Scope: `README.md`, `TODO.md`, code comments.
Pros: code comments explain why ([`modules/services/terranix/routing.nix:12-14`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L12-L14), [`modules/services/niks3/default.nix:66-68`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L66-L68)).
Cons: README is a banner with a stale tree and non-existent hosts ([`README.md:41-62`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L41-L62)).
`README.md` is a personal banner with a disclaimer and a stale tree (lists `modules/hosts/`, `lib.nix`, `defaults.nix`, hosts `maelle`/`sciel` that do not exist: [`README.md:41-62`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/README.md#L41-L62)); `TODO.md` is design notes. Comments in code explain why in places ([`modules/services/terranix/routing.nix:12-14,30-31`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L12-L14), [`modules/services/niks3/default.nix:66-68`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/default.nix#L66-L68)). Operation-only/placeholder docs: 2.

Confidence: high.

### V (6, medium)
Scope: `nix/checks.nix`, `modules/services/terranix/global/checks.nix`, `nix/effects/deploy.nix`.
Pros: a check per den host plus packages and devshells ([`nix/checks.nix:11-38`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/checks.nix#L11-L38)); terraform validate ([`modules/services/terranix/global/checks.nix:10-19`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/global/checks.nix#L10-L19)).
Cons: no variation or collision tests; old den pin ([`nix/den.nix:15-16`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L15-L16)).
[`nix/checks.nix:11-38`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/checks.nix#L11-L38) derives a check per `den.hosts` entry (host toplevels), plus packages, devshells and package tests; [`modules/services/terranix/global/checks.nix:10-19`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/global/checks.nix#L10-L19) runs `terraform validate` on the generated config. CI is the nixbot service and the `deploy` effect on push to main ([`nix/effects/deploy.nix:155-157`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/effects/deploy.nix#L155-L157)), so invocation is traceable inside the repo's own service config. No variation, collision or negative tests. Den and flake-aspects pinned to old tags ([`nix/den.nix:15-16`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L15-L16)). 6.

Confidence: medium.

### O (8, medium)
Scope: `nix/effects/deploy.nix`, `modules/defaults/ci.nix`, service `vars.nix` files.
Pros: deploy effect derives defer-restart targets from `self.nixosConfigurations` clan deployment config ([`nix/effects/deploy.nix:40-55`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/effects/deploy.nix#L40-L55)), runs terraform from the same flake (`:27-38`), deploys on push; secrets are clan vars generators declared per service aspect ([`modules/services/niks3/vars.nix:13`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/vars.nix#L13), `nixbot/vars.nix`) with sops groups per machine, shared CI key generators in `den.default` ([`modules/defaults/ci.nix:17-64`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/defaults/ci.nix#L17-L64)); host IPs reach terraform via `machine-<host>-ipv4` locals ([`modules/services/niks3/terranix.nix:41`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/terranix.nix#L41)); cache and build service as aspects (`niks3`, `nixbot`). Cons: OVH VPS name is a literal ([`modules/services/terranix/global/providers/ovh.nix:22`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/global/providers/ovh.nix#L22)).

Confidence: medium.

### B (3)
Scope: census record `census/records/nixpedition.json` and the aspect files in the evidence block.
Pros: three infrastructure units that stand alone (evidence block).
Cons: only fish, bash and a package-only neovim in the census; service aspects carry identity.
B_div: fish, bash selection-verified enable-only (0.5 each) and neovim installed-only (0.5) = 1.5 -> band <=3 -> 2.
B_ref (3 units, band <=5 -> 4): nixos-containers [`modules/virtualisation/nixos-containers/default.nix:1`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/virtualisation/nixos-containers/default.nix#L1); clan defer-restart `modules/clan/defer-restart.nix` with `packages/clan-defer-restart`; terranix routing module system [`modules/services/terranix/routing.nix:99`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L99). These are infrastructure rather than applications; traefik, niks3 and nixbot leak identity and do not count.
B = round-half-up((2 + 4) / 2) = 3.

Confidence: medium.

```score-evidence
{"B": {"diversity_points": 1.5, "diversity_grade": 2, "reference_grade": 4, "reference_units": [{"name": "nixos-containers", "evidence": "modules/virtualisation/nixos-containers/default.nix:1"}, {"name": "clan-defer-restart", "evidence": "modules/clan/defer-restart.nix:1"}, {"name": "terranix-routing", "evidence": "modules/services/terranix/routing.nix:99"}]}}
```

### X (7, medium)
Scope: terranix class, clan instantiation: `modules/services/terranix/routing.nix`, `nix/den.nix`.
terranix is a per-host den class with a `global` (collected flake-wide through `policy.instantiate`) and a `local` (forwarded into the host's `services.terranix`, [`modules/services/terranix/routing.nix:70-120`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L70-L120)), fed by the same aspects and `host.constants` as the NixOS side ([`modules/services/niks3/terranix.nix:13`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/niks3/terranix.nix#L13)), with Cloudflare, OVH and email providers (`terranix/global/providers/`). den also feeds clan machines through `intoAttr` ([`nix/den.nix:20-29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20-L29)). One mature non-host family; not several; 7.

Confidence: medium.

## Total
2*7 + 8 + 6 + 5 + 5 + 2 + 8 + 3 + 6/2 + 7/2 = 14 + 8 + 6 + 5 + 5 + 2 + 8 + 3 + 3 + 3.5 = **57.5/100**

## Shortlist judgment
- showcase: yes. D 7 with O 8 and X 7: den drives clan instantiation, a routed terranix class and a quirk-fed gateway from one set of host constants.
- library_units: traefik dynamic-file quirk (A/B), terranix global/local routing (B), nixos-containers (B), clan instantiate override shape ([`nix/den.nix:20-29`](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20-L29), B).
- starter: no. Needs clan, sops groups, cloud accounts; README is stale.

Overall pros: cross-class host constants; routed terranix with validation check; deploy and secrets derived from host config; thin machines. Cons: stale README; identity constants in service aspects; silent recursive merge on duplicate dynamic files; pinned to old den; breadth of applications is small.

# lucasshiva/nixconfig

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/lucasshiva/nixconfig.md)

- Upstream: [lucasshiva/nixconfig](https://github.com/lucasshiva/nixconfig)
- Reviewed revision: [`9e8aa1ba03ce`](https://github.com/lucasshiva/nixconfig/commit/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6)
- Author: lucasshiva
- Score: **48.0 / 100**, rank 57 of 101 ranked configs. D 4 · I 7 · S 6 · R 6 · P 6 · L 5 · V 2 · O 3 · B 5 · X 2. Shortlists: starter, library units (3).
- Summary: a documented `my.*` option contract on ~10 features and one policy.resolve guard lift S/R/P; one single-consumer channel plus a host-name-keyed provides tree hold D to 4; inline /home/lucas, /mnt/data and syncthing constants cap S at 6; no checks, bootstrap script outside den.

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

flake-parts + import-tree, with den configuration in `modules/den/` and reusable features in an exported `shiv` namespace
([`modules/den/namespace.nix:3`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/namespace.nix#L3)) under `modules/features/<area>/`. One physical PC is used two ways: `void` as NixOS with HM
as a module ([`modules/hosts/void/void.nix:7-9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L7-L9)), and `astra` as standalone HM on CachyOS ([`modules/hosts/astra.nix:7`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L7)).
One user, `lucas`. Archived and never evaluated.

## 2. Common patterns

- `namespace`: [`modules/den/namespace.nix:3`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/namespace.nix#L3); `with shiv; [ hardware.gpu.nvidia ... ]` ([`modules/hosts/void/void.nix:15-20`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L15-L20)).
- `homes (standalone HM)`: [`modules/hosts/astra.nix:7`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L7) (`"lucas@astra"`).
- `define-user+primary-user`, `host-aspects`, `user-shell`: [`modules/users/lucas.nix:7,11,16`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/users/lucas.nix#L7).
- `den.default includes` with per-line explanations: [`modules/den/defaults.nix:50-68`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L50-L68).
- `policies`: `host-guards` uses `policy.resolve` to inject `isNixos`/`isDarwin` args ([`modules/den/policies/host-guards.nix:3-12`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/policies/host-guards.nix#L3-L12)),
  consumed at [`modules/features/core/fonts.nix:74,82`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L74).
- `provides tree` keyed by home host name: `den.aspects.lucas.provides.astra` ([`modules/hosts/astra.nix:9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L9)).

## 3. Novel patterns

- [`modules/den/policies/host-guards.nix:6-11`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/policies/host-guards.nix#L6-L11): `policy.resolve` adds derived boolean args to every class module, so the
  same feature (fonts) installs packages only off-NixOS ([`modules/features/core/fonts.nix:82`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L82)). This handles one feature
  set across NixOS and foreign-distro HM.
- [`modules/hosts/astra.nix:16-26`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L16-L26): per-app notes on which apps work under standalone HM on a non-NixOS distro.

## 4. Library candidates

- host-guards · `modules/den/policies/host-guards.nix` · `isNixos`/`isDarwin` args for class modules · none · none · A
- nvidia/cpu/ssd hardware set · `modules/features/hardware/` · GPU/CPU/SSD basics · none · none · B

## 5. den friction

- [`modules/hosts/void/void.nix:11-12`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L11-L12): "Would be nice if we could decide between running home-manager as a nixos module
  or standalone on the fly." It is a request for one user config to target both modes without duplicate declarations.
- [`modules/hosts/astra.nix:51-53`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L51-L53): `nixpkgs.config.allowUnfree` under `den.default.homeManager` warns on NixOS (with
  useGlobalPkgs), so it has to be opt-in per standalone home. The unfree battery does not cover standalone HM cleanly.
- [`modules/features/services/syncthing.nix:11-12`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L11-L12): a shared path is repeated across aspects; the author suggests
  `den.schema` but has not used it.

## 6. Docs and complexity

The README has a structure tree, machine and host tables, and usage (`README.md` "Structure", "Hosts"). Comments explain
each battery choice ([`modules/den/defaults.nix:51-63`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L51-L63)). doc_quality 4. Complexity 3: one machine with two deployment
modes, a namespace with about 58 features and a resolve policy.

## 6a. Defects and scoring notes

- [`modules/features/apps/steam.nix:13,19`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L13) · S · moderate · `/home/lucas` and user `lucas` are hard-coded in a shared feature
- [`modules/features/services/syncthing.nix:8-19`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L8-L19) · S · minor · data-drive and device paths fixed inline (the author's own comment suggests `den.schema`)
- [`modules/hosts/astra.nix:9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L9) · S · minor · standalone-home config keyed by host name (`provides.${hostname}`)
- [`modules/hosts/astra.nix:51-53`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L51-L53) · P · minor · `allowUnfree` has to be set per standalone home because the shared default warns on NixOS
- repo-wide · V · minor · no flake `checks` found by a repo-wide grep; observation only

## 7. Template notes

It is a good template for "NixOS host plus the same user's standalone HM on another distro", with clearly commented
defaults. Avoid copying `provides.<hostname>` for the standalone home; a host fact or a policy guard is more robust.

## 8. Scorecard

Verified at rev 9e8aa1ba03ce. §6a changes: all five defects hold ([modules/features/apps/steam.nix:13](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L13),19; [modules/features/services/syncthing.nix:8](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L8); [modules/hosts/astra.nix:9](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L9); [modules/hosts/astra.nix:51](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L51); no checks). Added: [`modules/features/apps/distrobox.nix:31`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/distrobox.nix#L31) (`users.users.lucas` in a shared nixos arm, S); [`modules/features/desktop/noctalia.nix:32`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/noctalia.nix#L32) (`/mnt/data/Media/Pictures/Wallpapers`, S); [`modules/features/apps/steam.nix:18`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L18) (`/mnt/test/SteamLibrary`, S); [`modules/den/defaults.nix:27`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L27) (nine `pt_BR.UTF-8` locale lines in the global default, S minor); `modules/features/desktop/gnome.nix` (`altgr-intl` layout inline, S minor). The identity at [`modules/users/lucas.nix:54`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/users/lucas.nix#L54) is a user file feeding the `my.git` option, which is the intended pattern, so it is not a defect.

### D (4, high)
Scope: `modules/den/policies/host-guards.nix`, [`modules/den/defaults.nix:50`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L50), [`modules/hosts/astra.nix:9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L9), consumers by grep of `isNixos|host\.|user\.`.
Chain: producer [`modules/den/policies/host-guards.nix:9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/policies/host-guards.nix#L9) (`policy.resolve` from `host.class`); route is den's resolve into every class module's args ([`modules/den/defaults.nix:61`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L61)); consumer [`modules/features/core/fonts.nix:74,82`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L74) (`home.packages = mkIf (!isNixos)`). That is the only consumer (grep finds `isNixos`/`isDarwin` nowhere else). Missing semantics: `host.class or ""` handles a standalone home. Duplicates: n/a.
Cons: one single-consumer boolean; the standalone home is selected by a literal host-name key, `den.aspects.lucas.provides.astra` ([`modules/hosts/astra.nix:9`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L9)); the shared `dataDrive` is repeated in four files because no schema fact carries it (author comment at [`modules/features/services/syncthing.nix:11`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L11)).
Pros: the channel is live and the comment explains why. Anchor 5 requires "limited routing/validation"; with one consumer and a fixed-name provides key it sits at 4.
Confidence: high.

### I (7, medium)
Scope: tree layout, `void.nix`, `astra.nix`, `lucas.nix`, ten feature files.
Pros: aspect-per-feature under `modules/features/<area>/` in the `shiv` namespace, small files (`yazi.nix` 12 lines), hosts are include lists with per-line comments ([`modules/hosts/void/void.nix:15`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L15)), optional concerns (`opentabletdriver`, `apps.osu`) stay opt-in ([`modules/hosts/void/void.nix:47`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L47)).
Cons: [`modules/features/apps/steam.nix:12`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L12) mixes a bind mount and tmpfiles for one machine into the feature; [`modules/features/desktop/kde.nix:4`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/kde.nix#L4) includes `apps.kitty`; the host aspect carries inline packages and X11 settings ([`modules/hosts/void/void.nix:56`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L56), host-specific so acceptable). No cap triggered.
Confidence: medium.

### S (6, medium) — contract grade 7, leak-coverage grade 6
Scope: shared feature aspects under `modules/features/` and `modules/den/defaults.nix`.
Pros (contract): per-feature `options.my.<feature>` with type, description, default, example ([`modules/features/apps/kitty.nix:14`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/kitty.nix#L14), [`modules/features/apps/osu.nix:15`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/osu.nix#L15), [`modules/features/apps/musicbee.nix:10`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/musicbee.nix#L10), [`modules/features/apps/calibre.nix:11`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/calibre.nix#L11), [`modules/features/cli/git.nix:10`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/cli/git.nix#L10) with required `str` options, [`modules/features/desktop/niri/niri.nix:79`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L79)), set per host in [`modules/hosts/void/void.nix:62`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L62) and [`modules/hosts/astra.nix:55`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L55); font tokens are `readOnly` ([`modules/features/core/fonts.nix:5`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L5)). No validation beyond types and the `readOnly` flags.
Cons (leaks): distinct author constants inlined in shared features: username `lucas` ([`modules/features/apps/steam.nix:13,19`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L13), [`modules/features/apps/distrobox.nix:31`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/distrobox.nix#L31)), `/mnt/test/SteamLibrary` ([`modules/features/apps/steam.nix:18`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/steam.nix#L18)), `/mnt/data` ([`modules/features/services/syncthing.nix:13`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L13), [`modules/features/desktop/noctalia.nix:32`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/noctalia.nix#L32)), the phone name and Syncthing device id ([`modules/features/services/syncthing.nix:16,34`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L16)), `pt_BR` locale ([`modules/den/defaults.nix:28`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L28)), `altgr-intl` (`gnome.nix`). Grouped (user name and home paths, the `/mnt/*` path root, the phone and device id, the locale, the keyboard layout) that is 5 distinct groups (raw 8), so the 4-10 band caps at 6.
Score 6 (min of 7 and 6).
Confidence: medium.

```score-evidence
{"S": {"contract_design": 7, "leak_coverage": 6, "distinct_leaks": 5, "raw_leaks": 8}}
```

### R (6, medium)
Scope: the feature aspects and `modules/den/policies/host-guards.nix`.
Pros: adoptable with at most three values: `host-guards` (zero), `kitty` (one optional option, [`modules/features/apps/kitty.nix:14`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/kitty.nix#L14)), `osu` (two options), `fonts` (declared tokens), `cosmic` (`autoLogin` bool, [`modules/features/desktop/cosmic.nix:18`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/cosmic.nix#L18)). Cons: all need the `shiv` namespace and `inputs.*` for niri/dms. No consumer example outside the author's own hosts, and no unit is documented as a drop-in, so it stays under 9. `steam`, `syncthing` and `distrobox` are not adoptable without rewriting.
Confidence: medium.

### P (6, medium)
Pros: one feature serves NixOS and a foreign-distro standalone home through `isNixos` ([`modules/features/core/fonts.nix:74`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L74)); class arms (`nixos`/`homeManager`) are selected per feature; [`modules/hosts/astra.nix:16`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L16) records which apps work on a non-NixOS distro; `targets.genericLinux` is set ([`modules/hosts/astra.nix:69`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L69)).
Cons: `allowUnfree` must be set per standalone home because the shared default warns ([`modules/hosts/astra.nix:51`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L51)); no failing-clearly mechanism; no darwin. Honest narrow two-mode scope; no boundary checks.
Confidence: medium.

### L (5, medium)
Scope: `README.md`, comments in `modules/den/defaults.nix` and `modules/hosts/astra.nix`.
Pros: README with structure tree, machine and host tables, build/update commands for both modes, and a worked sops/age bootstrap (`README.md`); comments explain battery choices ([`modules/den/defaults.nix:51`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/defaults.nix#L51)) and per-app standalone notes ([`modules/hosts/astra.nix:16`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L16)); `option` descriptions.
Cons: no walk-through for adding a host or a feature; the README warns that the config is over-engineered.
Confidence: medium.

### V (2, high)
Scope: repo-wide search for checks, tests and CI; [`flake.nix:1`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/flake.nix#L1).
Pros: none to credit.
Cons: no `checks`, no tests, no CI file (the root holds only `.sops.yaml` among dotfiles). Observation, not a failing claim.
Confidence: high.

### O (3, medium)
Scope: `bootstrap.sh`, `modules/features/secrets/sops.nix`, [`modules/features/services/syncthing.nix:3,22-28`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L3).
Pros: sops secrets are declared by the aspect that needs them ([`modules/features/services/syncthing.nix:22`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/services/syncthing.nix#L22)); `sops.nix` provides the age wiring once.
Cons: bootstrap is a standalone script with its own hard-coded defaults ([`bootstrap.sh:5`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/bootstrap.sh#L5)), not derived from den data; no deploy, no builders; one machine. Anchor 2-5; one concern driven by aspects, scored 3.
Confidence: medium.

### X (2, high)
Scope: [`modules/hosts/void/void.nix:7`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/void/void.nix#L7), [`modules/hosts/astra.nix:7`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/hosts/astra.nix#L7).
Pros: none beyond the baseline.
Cons: NixOS plus standalone home-manager only; both are P by the X baseline ruling.
Confidence: high.

### B (5, medium)
B_div 5, B_ref 5
Scope: `census/records/lucasshiva.json` and the feature aspects under `modules/features/`.
B_div from `census/records/lucasshiva.json`, selection-verified families at maximum depth, deduped: zsh 1 (substantive), bash 1, starship 1, niri 1, zed 1, kde 1, fish 0.5 (enable-only), nushell 0.5, neovim 0.5 (`none`: a bare package). vscode, gnome and cosmic are `defined` only and not counted. Total 7.5, in the 6-8 band, so B_div = 5.
B_ref units read (substantive, no leaked identity, usable from the aspect alone): niri [`modules/features/desktop/niri/niri.nix:79`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/niri/niri.nix#L79) (+`binds.nix`); zed [`modules/features/apps/zed.nix:2`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/zed.nix#L2); zsh [`modules/features/shell/zsh.nix:3`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/shell/zsh.nix#L3); kitty [`modules/features/apps/kitty.nix:2`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/kitty.nix#L2); nvidia [`modules/features/hardware/gpu/nvidia.nix:2`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/hardware/gpu/nvidia.nix#L2); cosmic [`modules/features/desktop/cosmic.nix:2`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/cosmic.nix#L2); git [`modules/features/cli/git.nix:3`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/cli/git.nix#L3) (identity is an option); dms [`modules/features/desktop/dms.nix:41`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/desktop/dms.nix#L41); fonts [`modules/features/core/fonts.nix:44`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L44); musicbee [`modules/features/apps/musicbee.nix:10`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/musicbee.nix#L10). That is 10, and in the 6-10 band B_ref = 5. Excluded: noctalia (wallpaper path), steam, syncthing, distrobox (leaks), gnome (inline layout), and enable-only files (yazi, btop, fzf).
B = (5 + 5) / 2 = 5.
Confidence: medium.

```score-evidence
{"B": {"diversity_points": 7.5, "diversity_grade": 5, "reference_grade": 5, "reference_units": [{"name": "niri", "evidence": "modules/features/desktop/niri/niri.nix:79"}, {"name": "zed", "evidence": "modules/features/apps/zed.nix:2"}, {"name": "zsh", "evidence": "modules/features/shell/zsh.nix:3"}, {"name": "kitty", "evidence": "modules/features/apps/kitty.nix:2"}, {"name": "nvidia", "evidence": "modules/features/hardware/gpu/nvidia.nix:2"}, {"name": "cosmic", "evidence": "modules/features/desktop/cosmic.nix:2"}, {"name": "git", "evidence": "modules/features/cli/git.nix:3"}, {"name": "dms", "evidence": "modules/features/desktop/dms.nix:41"}, {"name": "fonts", "evidence": "modules/features/core/fonts.nix:44"}, {"name": "musicbee", "evidence": "modules/features/apps/musicbee.nix:10"}]}}
```

## Total
2*4 + 7 + 6 + 6 + 6 + 5 + 3 + 5 + 1 + 1 = **48.0/100**

## Shortlist judgment
Showcase: no, D is 4 and there is one channel. library_units: `host-guards.nix` (A: no inputs, two derived booleans); `kitty` (B: one optional option); `fonts` (B: declared tokens, light parametrizing). Starter: yes, with caveats. Two entry points (host and standalone home) show one user across NixOS and a foreign distro, the README gives build commands, and platform scope is stated honestly; avoid copying `provides.<hostname>`.

Pros: clear option contract on many features; one user across two deployment modes with honest per-app notes; comments teach; clean namespace layout.
Cons: author constants in a handful of features; one thin data channel and a host-name provides key; no verification; bootstrap outside den.

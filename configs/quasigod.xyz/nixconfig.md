# quasigod.xyz/nixconfig

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/quasigod.xyz/nixconfig.md)

- Upstream: [quasigod.xyz/nixconfig](https://tangled.org/quasigod.xyz/nixconfig)
- Reviewed revision: `570018d633c7`
- Author: quasigod.xyz
- Score: **43.0 / 100**, rank 77 of 101 ranked configs. D 5 · I 7 · S 4 · R 6 · P 5 · L 2 · V 2 · O 2 · B 5 · X 2. Shortlists: library units (3).
- Summary: typed displays schema with explicit primary semantics (D 5 capped); more than eleven personal constants in shared aspects and no settings contract (S 4); README is a screenshot (L 2); no checks or ops (V 2, O 2); broad editor/shell/WM coverage (B 5).

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

flake-parts + import-tree over `modules/`, with den's flakeModule and an exported `styx` namespace (`modules/den.nix:6-9`).
Each feature is `styx.<name>`, with variants as sub-provides (`gaming._.min`, `gaming._.max`, `helix.with-tools`). Two
NixOS hosts, `hades` (desktop) and `zagreus` (Framework laptop), and one user, `quasi` (`modules/quasi.nix:3`). Both hosts
fail under eval (see regression).

## 2. Common patterns

- `namespace` + `angle-bracket refs`: `modules/den.nix:8`, `modules/quasi.nix:5-30`; `with styx; [ ... ]` lists in host aspects
  (`modules/hosts/hades/default.nix:37-43`).
- `mutual-provider` via the `den._` alias: `modules/den.nix:4`.
- `define-user+primary-user`: `modules/default.nix:6`, `modules/quasi.nix:5`.
- `custom schema/classes`: a typed `displays` host option with a derived read-only `primaryDisplay`
  (`modules/meta/displays.nix:58-75`).
- `provides tree` for variants: `modules/networking.nix:3-8` (`static`, `wol`, `wireless`), `modules/apps/helix.nix:81`.
- Host-to-user provides by user name: `den.aspects.hades.provides.quasi` (`modules/hosts/hades/default.nix:27-36`).
- `den.lib.perHost` inside a namespace aspect: `modules/niri/default.nix:14`.

## 3. Novel patterns

- `modules/hosts/hades/default.nix:5-6`: overrides a host's `instantiate` with `nixpkgs-patcher.lib.nixosSystem`, so one
  host builds on a patched nixpkgs without a second nixpkgs input.
- `modules/meta/displays.nix:58-75`, consumed at `modules/niri/default.nix:15-25`: display facts drive both niri outputs and
  per-output wallpapers. Wallpaper paths are resolved against `inputs.self` (`modules/meta/displays.nix:50-51`).
- `modules/groups.nix:3-14`: a user-defined "battery" in the namespace (`styx.batteries._.privileged-user`) that declares a
  `users.privilegedGroups` option and maps it onto the user's `extraGroups`. Aspects append groups without naming the user.
- `modules/services/syncthing.nix:2-12`: the device roster is kept in aspect `meta` and fed into HM syncthing config.

## 4. Library candidates

- displays schema · `modules/meta/displays.nix` · typed monitors, primary detection, wallpapers · none · host options · A
- privileged-user · `modules/groups.nix` · aspect-contributed groups for the primary user · none · NixOS option · A
- microvm host · `modules/microvm.nix` · microvm host import, tap0 addressing and NAT · microvm.nix · none · B (fixed subnet at `:8,17`)

## 5. den friction

- zagreus fails against current den main with `users.users.quasi.__scopeName does not exist` (measured). This is a den
  regression or contract change hitting a user-scope `users.users.<name>` write; the battery at `modules/groups.nix:9` is the
  likely trigger. It is worth a minimal repro in den's test suite.
- `modules/hosts/hades/default.nix:27`: `provides.<username>` on a host aspect keys config by a name string, the same
  silent-mismatch hazard tomwrw/megadots documents for `provides.<hostname>`.
- `modules/meta/_compat.nix:3-5`: a `mkCompat` version shim for stable/unstable option names. It is not den-specific.

## 6. Docs and complexity

The README is a screenshot and an inspirations list, with no structure notes; the comment ratio is 0.03: doc_quality 2.
Complexity 3: two hosts and one user, but a namespace with variant sub-provides, a custom display schema, a patched
nixpkgs instantiate and microvm hosting.

## 6a. Defects and scoring notes

- `modules/services/sshd.nix:12-13` · S · moderate · personal authorized keys are inline in the shared sshd aspect
- `modules/wayland.nix:35-38`, `modules/niri/dms.nix:8` · S · moderate · `/home/quasi` paths are hard-coded in shared desktop aspects
- `modules/microvm.nix:8,17` · S · minor · the microvm host subnet `10.4.4.0/30` is fixed
- `modules/hosts/hades/default.nix:27` · S · minor · host-to-user config keyed by user name (`provides.quasi`)
- `flake.nix:13-16` · V · moderate · a patch-diff URL input whose hash rots (measured narHash mismatch on hades)
- zagreus (measured) · V · moderate · incompatible with current den main (`users.users.quasi.__scopeName` does not exist)

- `modules/apps/git.nix:23-24`, `modules/apps/jujutsu.nix:12-13`, `modules/apps/halloy.nix:11` · S · minor · name, email and IRC nick inline in shared app aspects
- `modules/services/syncthing.nix:9-21` · S · minor · four device IDs inline in the shared syncthing aspect
- `modules/gaming.nix:107`, `modules/niri/default.nix:71`, `modules/security.nix:25,31` · S · minor · user name `quasi` fixed in shared aspects
- `modules/default.nix:32,31,42` · S · minor · timezone and state versions fixed in `den.default`

## 7. Template notes

The namespace-with-variants style (`styx.gaming._.min` vs `._.max`) and the displays schema are good to learn from. The
repo is currently unbuildable on both hosts, and one input rots by construction (patch-diff URL), so it is not a starting
point.

## 8. Scorecard

### D (5, medium)
Pros: explicit primary-display semantics (`modules/meta/displays.nix:76-81`); consumer derives outputs from `host.displays` (`modules/niri/default.nix:22-33`).
Cons: no quirks or policies; syncthing roster literal (`modules/services/syncthing.nix:7-24`).
Scope: `modules/meta/displays.nix`, `modules/niri/default.nix`, `modules/groups.nix`, `modules/services/syncthing.nix`.
Chain 1 (schema fact via context args): producer `den.schema.host` option `displays` plus read-only `primaryDisplay` (`modules/meta/displays.nix:58-83`); consumer `modules/niri/default.nix:15-34` (`den.lib.perHost`, `host.displays`) derives niri outputs and per-output wallpaper commands. Missing/duplicate semantics are explicit: one display defaults to primary, none gives null, several primaries throw with names (`modules/meta/displays.nix:76-81`). Chain 2: `styx.batteries._.privileged-user` declares `users.privilegedGroups` and maps it to the primary user's groups (`modules/groups.nix:9-13`), a module-system channel. Chain 3: the syncthing device roster in aspect `meta` feeds HM config (`modules/services/syncthing.nix:5-30`), literal, not derived from `den.hosts`.
No quirks or policies. Capped at 5 by the schema-fact ruling; 5.

Confidence: medium.

### I (7, medium)
Scope: `modules/den.nix`, `modules/hosts/*`, namespace aspects.
Pros: `styx` namespace, variants as sub-provides (`gaming._.min/_.max`, `networking.provides.{static,wol,wireless}`, `shell/full`), hosts as `with styx;` include lists (`modules/hosts/hades/default.nix:37-43`), user as a list of angle-bracket refs (`modules/quasi.nix:4-37`). Cons: `modules/hosts/hades/default.nix:27-36` keys host-to-user config by user name; `modules/niri/default.nix:71` sets the greetd user; `core.nix`/`extras.nix`/`gui.nix` are broad bundles; `hades` carries a lot of inline desktop and game config (`:45-107`).

Confidence: medium.

### S (4, medium)
Scope: displays schema and shared-aspect constants.
Pros: typed displays options (`modules/meta/displays.nix:5-55`).
Cons: keys, names, IDs, paths and cache URLs in shared aspects (`modules/services/sshd.nix:12-13`, `modules/wayland.nix:35-38`, `modules/services/syncthing.nix:9-21`, `modules/services/ncro.nix:14-35`).
Contract grade 4: only the displays option set is a real contract (`modules/meta/displays.nix:5-55`); everything else is edit-in-place. Leak grade: more than 11 distinct constants in shared aspects, cap 5: SSH keys `modules/services/sshd.nix:12-13`, user name `modules/gaming.nix:107`, `modules/niri/default.nix:71`, `modules/security.nix:25,31`, `/home/quasi` in `modules/wayland.nix:35-38`, `modules/niri/dms.nix:8`, git/jj/irc identity `modules/apps/git.nix:23-24`, `modules/apps/jujutsu.nix:12-13`, `modules/apps/halloy.nix:11`, timezone `modules/default.nix:32`, state versions `modules/default.nix:31,42`, microvm subnet `modules/microvm.nix:8,17`, syncthing device IDs `modules/services/syncthing.nix:9-21`, binary caches `modules/services/ncro.nix:14-35`. S = min(4, 5) = 4.

Confidence: medium.

```score-evidence
{"S": {"contract_design": 4, "leak_coverage": 5, "distinct_leaks": 14}}
```

### R (6, medium)
Scope: `modules/groups.nix`, `modules/meta/displays.nix`, `modules/catppuccin.nix`.
Pros: privileged-user is drop-in (`modules/groups.nix:3-14`); catppuccin takes flavor/accent (`modules/catppuccin.nix:7`).
Cons: displays needs `inputs.self` (`modules/meta/displays.nix:51`); no docs or example.
Two small adoptable-as-written units: `privileged-user` battery (`modules/groups.nix:3-14`, needs only `user.userName`) and the displays schema (`modules/meta/displays.nix:58-83`, needs `inputs.self` for wallpapers at `:50-51`); `catppuccin` takes flavor and accent as arguments (`modules/catppuccin.nix:7-14`). No consumer example or docs, units are small. 6.

Confidence: medium.

### P (5, medium)
Scope: `modules/meta/_compat.nix`, `modules/microvm.nix`, host instantiate override.
Pros: compat shim isolated (`modules/meta/_compat.nix:3-5`); instantiate override contained (`modules/hosts/hades/default.nix:5-6`).
Cons: no boundary checks; microvm host only (`modules/microvm.nix:8`).
NixOS only; `modules/meta/_compat.nix:3-5` shim for stable/unstable option names; microvm host only (no guests). The `hades` instantiate override for a patched nixpkgs (`modules/hosts/hades/default.nix:5-6`) is contained. Measured eval failures (zagreus with current den, hades patch-diff hash) are regression facts, not scored again.

Confidence: medium.

### L (2, high)
Scope: `README.md` and in-tree comments.
Pros: screenshot and inspirations (`README.md:6-19`).
Cons: no structure, wiring or feature-selection guidance; comment ratio 0.03.
`README.md` is a screenshot and an inspirations list (`README.md:1-19`); comment ratio 0.03; no structure notes. Operation-only/placeholder: 2.

Confidence: high.

### V (2, high)
Scope: whole tree and `flake.nix`.
Pros: none to credit.
Cons: no checks or CI; rotting patch-diff input (`flake.nix:13-16`).
No checks, no CI; a patch-diff URL input whose hash rots (`flake.nix:13-16`). Observation under the anchor; the rot is a maintenance fact recorded in 6a, not deducted again.

Confidence: high.

### O (2, medium)
Scope: `modules/secrets/default.nix`, `.sops.yaml`.
Pros: sops-nix wired in one aspect (`modules/secrets/default.nix:10-23`).
Cons: fixed key file (`modules/secrets/default.nix:6`); no deploy, bootstrap or builder data.
sops-nix wired through one aspect with a fixed key file (`modules/secrets/default.nix:3-23`, `.sops.yaml`); no deploy, bootstrap or builder data driven by hosts; two hosts managed by hand. Baseline 2.

Confidence: medium.

### B (5)
Scope: census record `census/records/quasigod-xyz-nixconfig.json` and the aspect files in the evidence block.
Pros: seven substantive families plus a package-only multiplexer; six standalone reference aspects.
Cons: niri, gaming, git, jujutsu and halloy carry identity (`modules/niri/default.nix:71`, `modules/apps/git.nix:23-24`).
B_div: helix, nushell, fish, bash, starship, emacs and niri are selection-verified and substantive (7) plus zellij package-only (0.5) = 7.5 -> band <=8 -> 5. Cosmic is `defined` only, no peer credit.
B_ref (6 units, band <=10 -> 5): helix `modules/apps/helix.nix:3`; nushell `modules/apps/nushell.nix:2`; starship prompt `modules/apps/prompt.nix:2`; catppuccin theming `modules/catppuccin.nix:7`; wezterm `modules/apps/wezterm/default.nix`; easyeffects `modules/services/easyeffects/default.nix`. Not counted: niri (user name and paths), gaming, jujutsu/git/halloy (identity), emacs (package list only).
B = round-half-up((5 + 5) / 2) = 5.

Confidence: medium.

```score-evidence
{"B": {"diversity_points": 7.5, "diversity_grade": 5, "reference_grade": 5, "reference_units": [{"name": "helix", "evidence": "modules/apps/helix.nix:3"}, {"name": "nushell", "evidence": "modules/apps/nushell.nix:2"}, {"name": "starship-prompt", "evidence": "modules/apps/prompt.nix:2"}, {"name": "catppuccin", "evidence": "modules/catppuccin.nix:7"}, {"name": "wezterm", "evidence": "modules/apps/wezterm/default.nix:1"}, {"name": "easyeffects", "evidence": "modules/services/easyeffects/default.nix:1"}]}}
```

### X (2, high)
Scope: non-host targets: none; `modules/microvm.nix` is host support only.
Pros: n/a (baseline).
Cons: NixOS and HM only (`modules/microvm.nix:3`).
NixOS and HM only. `microvm.nix` is host support with no guests as classes.

Confidence: high.

## Total
2*5 + 7 + 4 + 6 + 5 + 2 + 2 + 5 + 2/2 + 2/2 = 10 + 7 + 4 + 6 + 5 + 2 + 2 + 5 + 1 + 1 = **43.0/100**

## Shortlist judgment
- showcase: no. D is capped at 5; L and V are weak; S is poor.
- library_units: displays schema (A), privileged-user battery (A), parametric catppuccin (B), `microvm` host (C).
- starter: no. Unbuildable on both hosts at the measured revs and no documentation.

Overall pros: typed display schema with explicit primary semantics; namespace with variant sub-provides; broad shell/editor/WM coverage. Cons: personal constants throughout shared aspects; no docs or checks; both hosts fail under eval; host-to-user config keyed by name.

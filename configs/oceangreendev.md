# oceangreendev

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/oceangreendev.md)

- Upstream: [OceangreenDev/nix-config](https://github.com/OceangreenDev/nix-config)
- Reviewed revision: [`5103cc02832d`](https://github.com/OceangreenDev/nix-config/commit/5103cc02832d2d857cd87e8748e926b4221cc90d)
- Author: OceangreenDev
- Score: **42.0 / 100**, rank 82 of 103 ranked configs. D 4 · I 5 · S 5 · R 6 · P 5 · L 3 · V 4 · O 3 · B 4 · X 2. Shortlists: library units (5).
- Summary: parametric batteries with usage docs and guarded class forwards give R 6; policies keyed by literal user/host names cap D at 4 and the systemType chain is inactive; NAS paths, a committed credential (reported privately; not located here) and secret paths in shared programs cap S at 4; a nix-unit tests class exists but with three cases and no CI.

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
- [Total](#total)
- [Shortlist judgment](#shortlist-judgment)

## 1. Shape

flake-parts + import-tree (with a flake-compat `default.nix`). Every directory carries a platform suffix: `__N` NixOS,
`__D` darwin, `__G` global (flake-level), and lowercase `n`/`d` for HM on NixOS/darwin, e.g. `users/oceangreendev__Nn`,
`tools/secrets__NDnd`. The tree is split into `hosts/`, `nix/tools/`, `programs/`, `provides/`, `services/`, `system/`
and `users/`. There are two namespaces, a public `ocean` and a private `oceani`
(`modules/nix/tools/den__G/features/namespace.nix:11-13`). Hosts: `po3-600` (desktop), `crosswork` (WSL) and `macbook`
(darwin). Derived from Doc-Steve's dendritic design (SPDX headers, e.g.
`modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:1`). Archived and never evaluated.

## 2. Common patterns

- `namespace` (public and private): `modules/nix/tools/den__G/features/namespace.nix:11-13`.
- `define-user+primary-user` via wrapped batteries: `(<den/define-user-adv> false)`, `<den/primary-user-adv>`
  (`modules/users/oceangreendev__Nn/oceangreendev.nix:12-13`).
- `angle-bracket refs` into services: `modules/hosts/crosswork__N/den.nix:18-21`.
- `policies` local to a host aspect: `den.lib.policy.include` setting HM stateVersion for that host's users
  (`modules/hosts/crosswork__N/den.nix:22-33`).
- `parametric aspect (fn args)`: `{ host, user }` context in `extraUserContext` (`modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:29-46`).
- `custom schema/classes`: host `systemType` (`modules/hosts/crosswork__N/den.nix:13`, `modules/hosts/po3-600/den.nix:12`).
- unfree battery: extract counts 3 uses; `broken`/`unsupported` siblings below.

## 3. Novel patterns

- User-defined batteries in `den.batteries.*` with in-code usage docs: `define-user-adv` (adds a per-user group, wheel and
  darwin `primaryUser`; `modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:11-55`), `user-shell-adv`, `facter`, `treefmt`, `udiskie`, and parametric
  account batteries `accounts.exchange/google/apple` (`modules/provides/accounts__nd/gmail.nix:139`). This extends den's
  battery namespace as a personal library.
- `modules/nix/tools/den__G/provides/broken/broken.nix:10-40` and `modules/nix/tools/den__G/provides/unsupported/unsupported.nix:11-23`: clones of den's unfree
  battery for `allowBroken`/`allowUnsupportedSystem` by package name.
- The directory platform-suffix convention, like gwenodai-nixos's `[H]/[U]`, encodes where an aspect applies.
- `modules/hosts/crosswork__N/den.nix:25-33`: a policy stored under the aspect's own `policies.` key and included by
  reference, giving host-scoped HM defaults without touching `den.default`.

## 4. Library candidates

- broken/unsupported batteries · `modules/nix/tools/den__G/provides/{broken,unsupported}/` · per-package allowBroken/allowUnsupported, like unfree · none · fn args (names) · A (and a candidate for den itself)
- define-user-adv · `modules/provides/user/define-user-adv__NDnd/define-user-adv.nix` · user group, wheel, darwin primaryUser · none · fn arg (isAdmin) · A
- mail accounts · `modules/provides/accounts__nd/{gmail,exchange,icloud}.nix` · HM accounts for three providers · home-manager · fn args · B
- btrfs+luks+impermanence disko layout · `modules/provides/disko/btrfs-imper-luks.nix:5-8` · disko layout with swap and boot sizing · disko, impermanence · fn args · B

## 5. den friction

- `modules/nix/tools/den__G/provides/broken/broken.nix:1` cites den's `unfree.nix` at a fixed commit, and the clone re-implements den battery internals
  (`__functor`, `__fn`, `meta.provider`, `:22-33`). den has no public constructor for "a battery like unfree but for another
  nixpkgs predicate".
- `# deadnix: skip` on `__findFile`/`user` formals repeats in nearly every file (`modules/hosts/crosswork__N/den.nix:5,27`),
  the same argument-name-dispatch-versus-linter tension seen in megadots and nixpedition.
- Two near-duplicate disko layouts, `modules/provides/disko/btrfs-imper-luks.nix` and
  `modules/provides/disko/partition-layouts__N/btrfs-inpermanence-luks.nix:51`, and an `impermanence__N/old/` tree suggest an in-flight migration.

## 6. Docs and complexity

There is no README, only an mkdocs stub (`docs/mkdocs.yml`). The comment ratio is 0.16, and batteries carry usage
`description` blocks (`modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:11-27`). doc_quality 3. Complexity 4: three hosts across NixOS, WSL and
darwin, two namespaces, about 15 custom batteries, sops and impermanence.

## 6a. Defects and scoring notes

- `modules/programs/editor/obsidian__n/obsidian.nix:21` · S · moderate · a personal NAS path (`/mnt/synology-nas/ocean/...`) in a shared aspect
- `modules/provides/disko/btrfs-imper-luks.nix:5` vs `modules/provides/disko/partition-layouts__N/btrfs-inpermanence-luks.nix:51` · I · moderate · two near-duplicate disko layouts
- `modules/nix/tools/impermanence__N/old/` · I · minor · a superseded tree kept in the import path
- `modules/nix/tools/den__G/provides/broken/broken.nix:22-33` · R · moderate · the broken/unsupported batteries copy den internals (`__functor`, `__fn`, `meta.provider`) at a fixed den rev
- repo root · L · moderate · no README (mkdocs stub only)

## 7. Template notes

It is good for learning how to write your own batteries with usage docs, and the broken/unsupported batteries belong in
den. The platform-suffix naming is dense and the tree is deep (272 files), so it is a hard first read.

## 8. Scorecard

Verified at rev 5103cc02832d. The `_system-types.nix` chain is inactive (its filename starts with `_` and the pinned import-tree skips it; settled in the census record), so it earns nothing; its own first line says "Currently broken" (`modules/system/types/_system-types.nix:4`). §6a changes: all five defects hold. Added: a committed credential (reported privately; not located here) in a shared program aspect (S major); `modules/programs/security/keepassxc/keepassxc.nix:21` and `modules/programs/cli__nd/_rclone/rclone.nix:36` (Synology NAS paths and secret names, S moderate); `modules/programs/web/mozilla_nd/common/profiles/default.nix:12` (`ocean.home.arpa` homepage, S minor); `modules/hosts/po3-600/den.nix:25` and `:45-48` (the same four `<system/types/*>` listed in the host and again in the user policy, I minor); `modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:19,22` (usage text says `den.define-user.adv`, the battery is `den.batteries.define-user-adv`; L minor).

### D (4, medium)
Scope: `hosts/po3-600/den.nix`, `hosts/crosswork__N/den.nix`, `users/.../homemanager.nix`, `nas.nix`, `mozilla-fwd.nix`, `impermanence-fwd.nix`, `nix-unit.nix`, `_system-types.nix`; grep finds no `quirk` or `pipe`.
Pros: guarded class routes are live (browser classes, impermanence forwards, tests).
Cons: chains: policies are attached by literal identity, `lib.optional (user.name == "OceanGreenDev")` (`modules/hosts/po3-600/users/oceangreendev/homemanager.nix:20`, `modules/hosts/po3-600/users/oceangreendev/nixos.nix:38`, `modules/hosts/po3-600/users/oceangreendev/ssh/known-host.nix:20`, `modules/hosts/po3-600/users/oceangreendev/ssh/secret-config.nix:21`, `modules/hosts/macbook__D/users/oceangreendev.nix:27`) and `host.name == "po3-600"` (`modules/hosts/po3-600/users/oceangreendev/services/smb/nas.nix:40`): fixed-name lookups. Class routes exist: `mozilla`/`librewolf`/`firefox` into `programs.<browser>` with an options-presence guard (`modules/programs/web/mozilla_nd/mozilla-fwd.nix:10`), `perhost`/`perhome` forwards into impermanence with guards (`modules/nix/tools/impermanence__N/impermanence-fwd.nix:11`), and `tests` into nix-unit with `adaptArgs` (`modules/nix/tools/nix-unit__G/nix-unit.nix:52`, copied from den's template). These move content between classes; none derives config from declared facts. The `systemType` host option read by a parametric aspect (`modules/system/types/_system-types.nix:75`) would be a schema-fact channel but is inactive.
Score 4 (fixed-name cap; live class routes with guards).
Confidence: medium.

### I (5, medium)
Pros: per-feature files under `programs/`, `services/`, `system/`, `provides/`; the suffix convention documents scope (`kde__Nn`); batteries live in `provides/`.
Cons: the platform suffix is documentation only, since import-tree loads every directory regardless (census); two near-duplicate disko layouts (`provides/disko/btrfs-imper-luks.nix`, `partition-layouts__N/btrfs-inpermanence-luks.nix`); `impermanence__N/old/` stays in the import path; the system-type includes are repeated by hand in each host (`modules/hosts/po3-600/den.nix:25,45-48`); a broken, inactive abstraction is left in the tree.
Confidence: medium.

### S (5, high) — contract grade 5, leak-coverage grade 6
Scope: shared aspects under `modules/programs/`, `modules/provides/`, `modules/services/`.
Pros (contract): parametric batteries take arguments with defaults (`define-user-adv` `isAdmin`, `mount-cifs.nix` six args with `readOnly ? false`, `accounts` `mkEmail` with defaults), and `wslCustom.ssh-dir-mount.sshDir` is a typed option (`modules/services/wsl/wsl-ssh-dir-mount__N/wsl-ssh-dir-mount.nix:22`); the `systemType` enum is inactive. Most programs are configured directly.
Cons (leaks) in shared programs and provides: Synology NAS path and secret names (`modules/programs/editor/obsidian__n/obsidian.nix:21`, `modules/programs/security/keepassxc/keepassxc.nix:21`, `modules/programs/cli__nd/_rclone/rclone.nix:36`), the user name in secret paths (`modules/programs/cli__nd/_rclone/rclone-sops.nix:12,16`, `modules/programs/security/keepassxc/sops-keys.nix:16`), the `ocean.home.arpa` homepage (`modules/programs/web/mozilla_nd/common/profiles/default.nix:12`), German locale choices (`modules/programs/editor/vscode__nd/plugins.nix:58`, `modules/programs/editor/eclipse__n/eclipse.nix:52`), `modules/programs/desktop/idescriptor__N/idescriptor.nix:8` (`users = [ "OceanGreenDev" ]`), `modules/programs/security/kopia.nix:4` (user and Windows profile), a committed credential (reported privately; not located here), and the literal user and host names in policies. Grouped (NAS host and path root, user name in secret paths, home domain, German locale choices, Windows profile path, the committed credential, literal names in policies) that is 7 distinct groups (raw about 14), so 4-10 caps at 6; the committed credential is a major finding.
Score 5 (min of 5 and 6).
Confidence: high.

```score-evidence
{"S": {"contract_design": 5, "leak_coverage": 6, "distinct_leaks": 7, "raw_leaks": 14}}
```

### R (6, medium)
Scope: `modules/provides/` batteries, `modules/nix/tools/den__G/provides/`, `modules/nix/tools/impermanence__N/impermanence-fwd.nix`.
Pros: adoptable with ≤3 values: `define-user-adv` (one boolean, usage docs in `description`, `modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:11`), `mount-cifs` (four required args), the `accounts.*` factories (account name, address, secret paths), `perhost`/`perhome` forwards (guarded on module presence), `broken`/`unsupported` (a package list, with usage docs). Cons: the `broken`/`unsupported` batteries copy den's `__functor`/`__fn`/`meta.provider` internals at a fixed rev (`modules/nix/tools/den__G/provides/broken/broken.nix:1,22-33`); the usage text in `define-user-adv` names the wrong path; nothing is published with a consumer example outside the author's hosts. 6.
Confidence: medium.

### P (5, medium)
Pros: nixos / darwin / homeManager arms are distinct (`modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:34`); darwin extras are separate (`macos-apps-fix.nix`, `homebrew__D`); forwards guard on option presence (`modules/nix/tools/impermanence__N/impermanence-fwd.nix:27,46`); WSL host option `wsl.enable` plus `systemType = "wsl"` (`modules/hosts/crosswork__N/den.nix:12`).
Cons: the suffix naming claims platform scope that nothing enforces; the WSL system-type chain is inactive so crosswork receives no cli software (census); darwin host `systemType` is commented out (`modules/hosts/macbook__D/den.nix:11`). 5.
Confidence: medium.

### L (3, medium)
Scope: repo root, `docs/mkdocs.yml:1`, in-code battery docs.
Pros: batteries carry usage text.
Cons: no README; `docs/mkdocs.yml` is a stub (`site_name` only). Compensation: batteries carry usage descriptions (`modules/provides/user/define-user-adv__NDnd/define-user-adv.nix:11`, `broken.nix`), SPDX headers, comment ratio 0.16, and `modules/system/types/_system-types.nix:7` documents the intended hierarchy (though broken). Placeholder docs are 2; the in-code battery docs lift it to 3.
Confidence: medium.

### V (4, medium)
Scope: `nix-unit.nix`, `hosts/po3-600/tests.nix`, `users/oceangreendev__Nn/tests.nix`.
Pros: a real `tests` class routed into `nix-unit` (`modules/nix/tools/nix-unit__G/nix-unit.nix:52`) with host/user config handed to tests; cases check that NetworkManager has the `home-lan` and `home-wifi` profiles and that the user's shell is zsh.
Cons: three live cases (the NAS mount tests are commented out, `modules/hosts/po3-600/tests.nix:24`); no enabled/disabled, platform or collision coverage; no CI file, so the cap of 6 applies and nothing traces the invocation; tests are tied to `po3-600` and `OceanGreenDev` by name. 4.
Confidence: medium.

### O (3, medium)
Scope: `modules/programs/cli__nd/_rclone/rclone-sops.nix:1`, `modules/programs/security/keepassxc/sops-keys.nix:1`, `modules/provides/disko/btrfs-imper-luks.nix:1`.
Pros: sops-nix secrets declared next to the aspects that use them (`rclone-sops.nix`, `nas-sops.nix`, `sops-keys.nix`, `sops-user-password.nix`); disko layouts as fn-arg library files.
Cons: no deploy, builders or install data; secrets are bound to the user and host by literal paths (`inputs.secrets/po3-600/users/OceanGreenDev/...`); no hand-kept host list because there is no fleet. 3.
Confidence: medium.

### X (2, high)
Scope: `modules/hosts/crosswork__N/den.nix:12`, `modules/hosts/macbook__D/den.nix:11`.
Pros: none beyond the baseline.
Cons: nixos, darwin, WSL (a nixos variant, P) and home-manager only.
Confidence: high.

### B (4, medium)
Scope: `census/records/oceangreendev.json` and the aspects under `modules/programs/` and `modules/system/`. B_div 3, B_ref 4.
B_div from `census/records/oceangreendev.json`: zsh 1, vscode 1, kde 1, starship 0.5 (enable-only), neovim 0.5 (enable-only). Total 4, band ≤5 → 3. Defined-only rows (wsl type chain, bash) are not counted.
B_ref units read: KDE Plasma + connect `modules/programs/session/kde__Nn/default.nix:1`, `kde-apps.nix`, `kde-connect.nix` (one app); nvidia `modules/system/settings/nvidia__N/nvidia.nix:1`; yubikey `modules/system/settings/yubikey__N/yubikey.nix:1` (+ u2f sops); podman `modules/programs/virtualization/podman/podman.nix:1`. Four units, band ≤5 → 4. Excluded: vscode (German packs, personal extension list), librewolf/firefox (homepage and policy constants), keepassxc (leaked key, NAS path), zsh (30 lines, "TODO: add options"), the batteries (libraries, not apps), and one-liners.
B = (3 + 4) / 2 = 3.5, rounded half up to 4.
Confidence: medium.

```score-evidence
{"B": {"diversity_points": 4.0, "diversity_grade": 3, "reference_grade": 4, "reference_units": [{"name": "kde plasma + connect", "evidence": "modules/programs/session/kde__Nn/default.nix:1"}, {"name": "nvidia", "evidence": "modules/system/settings/nvidia__N/nvidia.nix:1"}, {"name": "yubikey", "evidence": "modules/system/settings/yubikey__N/yubikey.nix:1"}, {"name": "podman", "evidence": "modules/programs/virtualization/podman/podman.nix:1"}]}}
```

## Total
2*4 + 5 + 5 + 6 + 5 + 3 + 3 + 4 + 2 + 1 = **42.0/100**

## Shortlist judgment
Showcase: no. D is 4. library_units: `define-user-adv` (A: one boolean, documented); `mount-cifs` (B); `accounts.google/exchange/apple` (B: homeManager account factories); `perhost`/`perhome` impermanence forwards (B: assumes `/persistent`); `broken`/`unsupported` batteries (B, and a candidate for den itself; they copy den internals). Not a starter: deep platform-suffix tree, inactive abstraction, no README.

Pros: parametric batteries with in-code usage docs; guarded class forwards for browsers and impermanence; a nix-unit tests class wired to host and user config; three platforms in one flake.
Cons: literal user and host names in policies; NAS paths, secret paths and a committed credential (reported privately; not located here) in shared programs; an inactive, self-described broken system-type chain; no README, tests thin and without CI.

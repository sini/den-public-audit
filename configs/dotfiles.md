# dotfiles

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/dotfiles.md)

- Upstream: [cmetz/dotfiles](https://github.com/cmetz/dotfiles)
- Reviewed revision: [`0c38be9224d7`](https://github.com/cmetz/dotfiles/commit/0c38be9224d7276100c5c835a2eea1c712dec2c9)
- Author: cmetz
- Score: **42.0 / 100**, rank 82 of 103 ranked configs. D 5 · I 6 · S 4 · R 5 · P 5 · L 2 · V 2 · O 4 · B 4 · X 2. Shortlists: library units (3).
- Summary: D 5 one live polybar quirk + conditional policy, hostname-keyed provides; I 6 gloom namespace but per-host package lists in the user file; S 4 host-name-keyed user config and root-key template; L 2 351-byte build notes; O 4 deploy targets derived from hosts for a script, builders hand-kept; B 4 (B_div 5 -> 3, B_ref 9 -> 5)

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

npins + with-inputs: `default.nix:20-23` builds flake-style `inputs` from `npins/` with `follows.nix`, then runs
flake-parts + import-tree over `modules/`. `flake.nix:1` is a one-line shim (`outputs = _: import ./.`). Feature aspects
live in an exported `gloom` namespace (`modules/den.nix:9`). All nine hosts are listed in `modules/hosts.nix:3-12`:
four workstations/Pi boards and five Proxmox LXC service containers. One user, `loom`. Eight of nine hosts PASS; pdfler
fails on the private input.

## 2. Common patterns

- `namespace` + `angle-bracket refs`: `modules/den.nix:9,12`, `modules/users/loom.nix:5-10`.
- `mutual-provider` on the user schema: `modules/default.nix:3`; hosts push user features with `provides.to-users.includes`
  (`modules/hosts/evo-x2.nix:7-9`).
- `den.default includes`: `modules/default.nix:37-42` (hostname battery commented out at `:39`).
- `define-user+primary-user`: `modules/default.nix:38`, `modules/gloom/everywhere.nix:11`.
- `forward`: a custom `git` class forwarded into `programs.git.settings` (`modules/gloom/classes.nix:14-27`).
- `quirks`: `den.quirks.gloom-polybar`, consumed as an arg (`modules/gloom/apps/polybar/default.nix:2,9`).
- `policies`: `den.lib.policy.when` + `policy.provide` gate HM globals on `host.home-manager.enable` (`modules/default.nix:5-23`).
- `provides tree` keyed by host name in the user aspect: `modules/users/loom.nix:14,31`.

## 3. Novel patterns

- `modules/default.nix:21-23`: a conditional policy, `policy.when (host.home-manager.enable)`, so the
  HM `useGlobalPkgs` defaults apply only to hosts that actually have users. LXC hosts with no users stay HM-free.
- `modules/gloom/classes.nix:14-27`: a `git` pseudo-class lets an aspect write git settings as a class, forwarded into HM with
  a guard on `programs.git.enable`.
- `modules/hosts/_templates/proxmox-lxc.nix`, imported by service hosts (`modules/hosts/pdfler.nix:8`): one den host per
  LXC container, built as a `system.build.proxmox-lxc` tarball (`modules/hosts/_templates/proxmox-lxc.nix:42`).
- `modules/flake/shells/default.nix:15-18`: `den.lib.nh.denApps` puts per-host nh apps into the devshell.

## 4. Library candidates

- gitClass forward · `modules/gloom/classes.nix:14-27` · `git` class to `programs.git.settings` · home-manager · none · A
- proxmox-lxc template · `modules/hosts/_templates/proxmox-lxc.nix` · LXC base plus image build · none · none · B (a committed credential (reported privately; not located here))
- polybar quirk · `modules/gloom/apps/polybar/default.nix` · extra polybar modules contributed by other aspects · home-manager · quirk values · B

## 5. den friction

- `modules/users/loom.nix:14-31` (and `:63`, `:161`): per-host user config through `provides.<hostname>`. This is the
  form megadots calls out as silently failing on host rename (megadots `modules/aspects/roles/gaming.nix:11-15`).
- `modules/default.nix:7-8`: `# deadnix: skip` on an unused `host` formal that den dispatch needs.
- `modules/hosts/pdfler.nix:8`: LXC hosts import a template as a NixOS module rather than an aspect, so the template
  cannot use den context (users, host facts).

## 6. Docs and complexity

The README is 351 bytes of German build notes (`README.md:1-4`) with no structure doc, and there are few comments:
doc_quality 1. Complexity 3: nine hosts across two arches with service containers and a namespace, but simple policy use
and one user.

## 6a. Defects and scoring notes

- `modules/users/loom.nix:14-31` (also `:63`, `:161`) · S · moderate · per-host user config keyed by host name (`provides.powerpi`, `provides.loombox`, ...) rather than host facts
- S · moderate · the shared LXC template carries a committed credential (reported privately; not located here)
- `modules/hosts/pdfler.nix:8` (also `modules/hosts/paperless.nix:6`, `modules/hosts/cachix.nix:6`) · I · minor · LXC hosts import a template NixOS module instead of including an aspect
- `modules/hosts/pdfler.nix:27` · R · moderate · a host depends on a private SSH input (`npins/sources.json:179`) with no stub
- `README.md:1-4` · L · moderate · the README is build notes only; there is no structure doc
- repo-wide · V · minor · no flake `checks` found by a repo-wide grep; observation only

## 7. Template notes

It is the corpus reference for the npins + with-inputs entry (`default.nix:20-23`) with a flake shim, and for
den hosting a fleet of single-purpose LXC containers. It is not a good first example: there are no docs, user
config is keyed by hostname, and one host depends on a private SSH input.

## 8. Scorecard
### D (5, medium)
Scope: `modules/gloom/apps/polybar/**`, `modules/default.nix`, `users/loom.nix`, `flake/systems.nix`.
Pros: quirk `gloom-polybar` declared `modules/gloom/apps/polybar/default.nix:2`, emitted by `modules/gloom/apps/polybar/modules/plantronics.nix:8` and `modules/gloom/apps/polybar/modules/razermon.nix:9`, consumed with a priority sort at `modules/gloom/apps/polybar/default.nix:135`; `policy.when host.home-manager.enable` gates HM globals (`modules/default.nix:5-23`).
Cons: a single emit->consume channel via default quirk collection with no empty/duplicate contract; per-host config reached by hostname key (`modules/users/loom.nix:14,31`), a fixed-name lookup.
Confidence: medium.

### I (6, medium)
Scope: `modules/gloom/**`, hosts, `users/loom.nix`.
Pros: `gloom` namespace with one file per app (`modules/gloom/apps/helix.nix:1`), small host files.
Cons: package lists copy-pasted between `provides.evo-x2` and `provides.loom-center` (`modules/users/loom.nix:66-140`); LXC hosts import a template as a NixOS module (`modules/hosts/pdfler.nix:8`); stale `modules/den.nix-old`.
Confidence: medium.

### S (4, medium)
Scope: `gloom/options.nix`, `users/loom.nix`, LXC template, leak grep.
Pros: contract grade 4: typed `gloom.bspwm.monitors` option (`modules/gloom/options.nix:1-30`) and the git class.
Cons: host differences are `provides.<hostname>` blocks (`modules/users/loom.nix:14-31`); distinct leaks (6): account emails in `modules/gloom/apps/my-totp/src/my-totp.py:11-18`, a committed credential (reported privately; not located here), `/home/${user.name}/dotfiles` in `modules/gloom/apps/helix.nix:152`, builder `evo-x2.lan` in `modules/hosts/powerpi.nix:46`. S = min(4, 6) = 4.
```score-evidence
{"S": {"contract_design": 4, "leak_coverage": 6, "distinct_leaks": 6}}
```
Confidence: medium.

### R (5, low)
Scope: `gloom/classes.nix`, polybar quirk, LXC template.
Pros: grade A: `git` class forward (`modules/gloom/classes.nix:14-27`, needs only home-manager); grade B polybar quirk and LXC template.
Cons: `modules/hosts/pdfler.nix:27` depends on a private input without a stub; no consumer example.
Hidden evidence: the private pdfler input (npins/sources.json:179) is not visible; direction: R unchanged or slightly lower.
Confidence: low.

### P (5, medium)
Scope: host list, Pi board.
Pros: x86_64 and aarch64 NixOS, Pi via nixos-hardware (`modules/hosts/powerpi.nix:21`); honest narrow scope.
Cons: no darwin and no boundary checks.
Confidence: medium.

### L (2, high)
Scope: `README.md`.
Pros: build notes exist (`README.md:1-4`).
Cons: 351 bytes of German build notes, no structure doc, few comments; operation-only = 2.
Confidence: high.

### V (2, high)
Scope: Justfile, tree.
Pros: none found.
Cons: no flake checks and no CI; `just ci` calls `(import ./.).ci` which the tree does not define (`Justfile:ci`, grep finds no `ci` output; recipe at `Justfile:30`). No relevant checks.
Confidence: high.

### O (4, medium)
Scope: `flake/systems.nix`, hosts, Justfile, scripts.
Pros: `self.lib.deploymentTargets` derives FQDN and proxmox type from `nixosConfigurations` for `scripts/deploy.sh` (`modules/flake/systems.nix:25-55`); LXC image build per host (`modules/hosts/_templates/proxmox-lxc.nix:42`).
Cons: builders hand-written per host (`modules/hosts/powerpi.nix:46`, `modules/hosts/evo-x2.nix:88`, `modules/hosts/loom-center.nix:93`); secrets outside den; deployment is a shell script.
Confidence: medium.

### B (4, medium)
Scope: census record plus aspect reads; B_div 5 -> 3, B_ref 8 -> 5, B = mean(3,5) = 4.
Pros: B_div = 5: selection-verified substantive: helix, tmux, bash, vscode = 4; peer bspwm substantive 1 (neovim is `defined` only). B_ref lists 8 gloom aspects (evidence block): helix, bspwm, polybar, yazi, vscode, autorandr, mailcow, lazygit.
Cons: neovim is only defined (`modules/gloom/apps/neovim.nix:1`); `modules/gloom/apps/st/default.nix:5` is a package build in perSystem, not an aspect, and was dropped; `modules/gloom/apps/my-totp/src/my-totp.py:11` is excluded for personal accounts. No shell, prompt or multiplexer beyond tmux/bash.
```score-evidence
{"B": {"diversity_points": 5, "diversity_grade": 3, "reference_grade": 5, "reference_units": [{"name": "helix", "evidence": "modules/gloom/apps/helix.nix:21"}, {"name": "bspwm", "evidence": "modules/gloom/apps/bspwm.nix:19"}, {"name": "polybar", "evidence": "modules/gloom/apps/polybar/default.nix:16"}, {"name": "yazi", "evidence": "modules/gloom/apps/yazi.nix:20"}, {"name": "vscode", "evidence": "modules/gloom/apps/vscode.nix:14"}, {"name": "autorandr", "evidence": "modules/gloom/apps/autorandr.nix:6"}, {"name": "mailcow", "evidence": "modules/gloom/services/mailcow.nix:20"}, {"name": "lazygit", "evidence": "modules/gloom/apps/lazygit.nix:7"}]}}
```
Representative cited units: pro `modules/gloom/apps/helix.nix:21` and `modules/gloom/apps/vscode.nix:14` are cited at the line where their configuration begins; the other units in the block are cited the same way.
Confidence: medium.

### X (2, high)
Scope: hosts, LXC template.
Pros: Proxmox LXC image attribute (`modules/hosts/_templates/proxmox-lxc.nix:42`).
Cons: NixOS only; the image is a host build output, not a separate class.
Confidence: high.


### Total
2*5+6+4+5+5+2+4+4+2/2+2/2 = **42.0/100**

### Shortlist judgment
Not a showcase; library units git class forward (A), polybar quirk (B), proxmox-lxc template (B); not a starter.

Overall pros:
- npins + with-inputs entry with flake shim (`default.nix:20-23`).
- `git` pseudo-class forwarded into HM (`classes.nix:14-27`).
- A fleet of LXC service hosts as den hosts.

Overall cons:
- Hostname-keyed user config with large duplicated package lists (`users/loom.nix`).
- 351-byte README; no checks; a stale `ci` recipe.
- Private input without stub (`pdfler.nix:27`); a committed credential (reported privately; not located here).

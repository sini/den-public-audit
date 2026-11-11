# drupol/infra

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/drupol/infra.md)

- Upstream: [drupol/infra](https://github.com/drupol/infra)
- Reviewed revision: [`b8cf59f140f5`](https://github.com/drupol/infra/commit/b8cf59f140f54f4f920d9f8070a3194eac38a8ae)
- Author: drupol
- Score: **39.0 / 100**, rank 92 of 103 ranked configs. D 3 · I 6 · S 3 · R 4 · P 5 · L 3 · V 2 · O 4 · B 6 · X 2. Shortlists: library units (2).
- Summary: D 3 untyped `meta` store with fixed-name lookups, no live channel; S 3 untyped meta and major/moderate leaks; R 4 unguarded private input; L 3 layout+commands README; O 4 deploy-rs nodes from nixosConfigurations; B 6 (B_div 7.5 -> 5, B_ref 13 -> 7)

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

## 1. Shape

flake-file generated flake using the den and flake-file `dendritic` flake modules plus `auto-follow`
([`modules/dendritic.nix:7-21`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dendritic.nix#L7-L21)). There are about 50 feature directories under `modules/` (base, desktop, dev, ai, services,
...), each a `den.aspects.<name>`. Hosts live in `modules/hosts/<name>/default.nix`, where each file declares both the
host aspect and `den.hosts` ([`modules/hosts/x280/default.nix:172,263`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x280/default.nix#L172)). There are ten hosts (x86_64 and rpi4) and users
`pol`, `user` and `root`. `_to_migrate/` holds legacy config that is not loaded.

## 2. Common patterns

- `define-user+primary-user` via `den.provides.*`: [`modules/users/pol/default.nix:19-20`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L19-L20), [`modules/users/user/default.nix:10-11`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/user/default.nix#L10-L11).
- `host-aspects`: [`modules/users/pol/default.nix:22`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L22).
- `provides.to-users` on hosts, including user aspects themselves: [`modules/hosts/x280/default.nix:245-258`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x280/default.nix#L245-L258) (`root`, `user` at `:256-257`).
- `provides tree` used as a shared helper bucket: `den.aspects.tools.provides.nix-trusted-user` ([`modules/users/nix-trusted-user.nix:2`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/nix-trusted-user.nix#L2)),
  consumed at [`modules/users/root/default.nix:10`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/root/default.nix#L10).
- `parametric aspect (fn args)` taking a non-context arg: `den.aspects.facter = facterReportPath: ...` ([`modules/facter/facter.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/facter/facter.nix#L7)),
  used as `(facter ./facter.json)` ([`modules/hosts/x280/default.nix:250`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x280/default.nix#L250)).
- unfree/insecure batteries: [`modules/hosts/imac/default.nix:9,14`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/imac/default.nix#L9).
- hostname battery inside a feature aspect: [`modules/base/network/default.nix:8`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/base/network/default.nix#L8).

## 3. Novel patterns

- Aspect `meta` as a per-user data store: `meta.authorizedKeys` ([`modules/users/root/default.nix:15,18-19`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/root/default.nix#L15)) and
  `meta.fullname`, read back from HM via `den.aspects.${config.home.username}.meta.fullname`
  ([`modules/dev/git/git.nix:293`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/git.nix#L293), [`modules/dev/git/jujutsu.nix:148`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/jujutsu.nix#L148)). It stands in for typed user facts.
- [`modules/facter/facter.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/facter/facter.nix#L7): an aspect as a plain function of a path, giving per-host facter reports without host schema.
- [`modules/hosts/x280/default.nix:9-28`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x280/default.nix#L9-L28): desktop entries generated from `den.aspects.user.meta.desktopEntries`.
- [`modules/flake-parts/deploy.nix:22-42`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/flake-parts/deploy.nix#L22-L42): deploy-rs nodes mapped over `config.nixosConfigurations`, not over den hosts.

## 4. Library candidates

- facter · `modules/facter/facter.nix` · nixos-facter import and report path · nixos-facter-modules · fn arg (report path) · A
- deploy-rs nodes · `modules/flake-parts/deploy.nix` · deploy nodes for every nixosConfiguration · deploy-rs, make-shell · none · B (compare theutz `modules/deploy.nix`, which routes from den hosts)
- nix-trusted-user · `modules/users/nix-trusted-user.nix` · adds the user to nix trusted-users · none · none · A

## 5. den friction

- `meta.fullname` lookups by `config.home.username` ([`modules/dev/git/git.nix:293`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/git.nix#L293)) re-implement user facts that
  `den.schema.user` options would type. This suggests that schema is not discoverable.
- `den.aspects.tools.provides.*` ([`modules/users/nix-trusted-user.nix:2`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/nix-trusted-user.nix#L2)) uses `provides` as a namespace, without den's
  `namespace` battery.
- The same aspect name `user` is used for a person (`modules/users/user/default.nix`) and the `user` class key
  ([`modules/users/root/default.nix:13`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/root/default.nix#L13)). It is legal but confusing.
- A private input with partial guards ([`modules/users/pol/default.nix:26-28`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L26-L28) guarded, [`modules/wifi/default.nix:17`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/wifi/default.nix#L17) not)
  makes the repo unbuildable for anyone else, despite the README's invitation.

## 6. Docs and complexity

README covers layout and commands (`README.md` "Repository layout", "Common commands"). Comments are sparse
(ratio 0.05) and no aspect is documented: doc_quality 3. Complexity 4: ten hosts, three users, about 36 feature
areas, deploy-rs and two arches, though den use is conventional (no policies, quirks or classes).

## 6a. Defects and scoring notes

- [`modules/ai/litellm/default.nix:17`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/litellm/default.nix#L17) · S · major · a secrets env file at `/home/pol/Code/...` is assumed inside a shared aspect
- [`modules/ai/open-webui.nix:50-59`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/open-webui.nix#L50-L59), [`modules/noise-station-client/default.nix:108,115`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/noise-station-client/default.nix#L108), [`modules/ai-local/mcp.nix:30`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai-local/mcp.nix#L30) · S · moderate · the LAN endpoint `192.168.2.116` is hard-coded across several shared aspects
- [`modules/dev/git/jujutsu.nix:14`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/jujutsu.nix#L14), [`modules/desktop/environment/kdeplasma.nix:370`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/desktop/environment/kdeplasma.nix#L370) · S · moderate · shared aspects point into `files/home/pol/...`
- [`modules/dev/git/git.nix:293`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/git.nix#L293), [`modules/dev/git/jujutsu.nix:148`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/jujutsu.nix#L148) · D · minor · a fixed-name lookup `den.aspects.${config.home.username}.meta.fullname` instead of a typed user fact
- [`modules/wifi/default.nix:17`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/wifi/default.nix#L17), [`modules/ai/open-webui.nix:15`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/open-webui.nix#L15) · R · major · the private `infra-private` input is used unguarded (only [`modules/users/pol/default.nix:28`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L28) guards it), so every host fails without access
- `_to_migrate/` · I · minor · legacy tree kept beside the live one

## 7. Template notes

It is useful as a large, conventional aspect-per-feature repo and for the facter-as-function and
users-included-by-host idioms. It is a poor template: it can't be evaluated without the private repo, per-user data
lives in untyped `meta`, and `_to_migrate/` noise.

## 8. Scorecard
### D (3, medium)
Scope: `users/pol/default.nix`, `users/root/default.nix`, `dev/git/git.nix`, `facter/facter.nix`, `flake-parts/deploy.nix`.
Pros: aspect `meta` acts as a data store: `meta.authorizedKeys` ([`modules/users/pol/default.nix:67`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L67)) and `meta.fullname` read back in HM ([`modules/dev/git/git.nix:293`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/git.nix#L293)).
Cons: that read is a fixed-name lookup `den.aspects.${config.home.username}.meta.fullname` with no declaration, route or missing/duplicate behaviour ([`modules/dev/git/jujutsu.nix:148`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/jujutsu.nix#L148)); root copies the key string instead of sharing it ([`modules/users/root/default.nix:15-19`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/root/default.nix#L15-L19)); no quirks, policies or pipes. Fixed-name cap 4, lowered to 3.
Confidence: medium.

### I (6, medium)
Scope: `modules/**`, host files.
Pros: about 50 feature directories each a `den.aspects.<name>` ([`modules/dev/editors/vscode.nix:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/editors/vscode.nix#L1), [`modules/desktop/environment/default.nix:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/desktop/environment/default.nix#L1)); hosts list features.
Cons: hosts inline disk UUIDs and boot config ([`modules/hosts/x13/default.nix:30-70`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x13/default.nix#L30-L70)); legacy `_to_migrate/` tree ([`_to_migrate/imports/checks.nix:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/_to_migrate/imports/checks.nix#L1)).
Confidence: medium.

### S (3, medium)
Scope: `meta` attrs, shared aspects grep.
Pros: leak grade 6: about 7 distinct leaks but no more than 10.
Cons: contract grade 3: untyped `meta`, no options or schema. Distinct leaks (7, cap 6): `/home/pol/Code/drupol/litellm-secrets.env` ([`modules/ai/litellm/default.nix:17`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/litellm/default.nix#L17)), `192.168.2.116` ([`modules/ai/open-webui.nix:50-59`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/open-webui.nix#L50-L59), [`modules/noise-station-client/default.nix:108`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/noise-station-client/default.nix#L108), [`modules/ai-local/mcp.nix:30`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai-local/mcp.nix#L30)), `192.168.1.123` ([`modules/ai-local/_mcp-gateway-config.nix:147`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai-local/_mcp-gateway-config.nix#L147)), `files/home/pol` ([`modules/dev/git/jujutsu.nix:14`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/jujutsu.nix#L14), [`modules/desktop/environment/kdeplasma.nix:370`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/desktop/environment/kdeplasma.nix#L370)), `github:drupol/infra` ([`modules/base/system/auto-upgrade/default.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/base/system/auto-upgrade/default.nix#L7)), `/home/user/bin` ([`modules/dev/git/git.nix:62`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/git/git.nix#L62)), inline SSH key ([`modules/users/pol/default.nix:67`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L67)). S = min(3, 6) = 3.
```score-evidence
{"S": {"contract_design": 3, "leak_coverage": 6, "distinct_leaks": 7}}
```
Confidence: medium.

### R (4, low)
Scope: facter aspect, trusted-user helper, private-input use.
Pros: small grade A units: facter-as-function ([`modules/facter/facter.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/facter/facter.nix#L7), used [`modules/hosts/x280/default.nix:250`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/x280/default.nix#L250)), nix-trusted-user ([`modules/users/nix-trusted-user.nix:2`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/nix-trusted-user.nix#L2)).
Cons: feature imports drag identity paths; `infra-private` is used unguarded ([`modules/wifi/default.nix:17`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/wifi/default.nix#L17), [`modules/ai/open-webui.nix:15`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/open-webui.nix#L15)), so nothing evaluates without it (guard only at [`modules/users/pol/default.nix:28`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/pol/default.nix#L28)).
Hidden evidence: the private infra-private input ([flake.nix:49-50](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/flake.nix#L49-L50)) hides pol home modules and wifi config; direction: R could rise if guarded paths are complete.
Confidence: low.

### P (5, medium)
Scope: host list.
Pros: NixOS x86_64 and rpi4, honest narrow scope ([`modules/hosts/rpi4/default.nix:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/hosts/rpi4/default.nix#L1)).
Cons: no guards or boundary checks.
Confidence: medium.

### L (3, medium)
Scope: `README.md`.
Pros: README documents layout, commands and the generated flake ([`README.md:12-30`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/README.md#L12-L30)).
Cons: no explanation of composition or adding a host/feature; comment ratio 0.05.
Confidence: medium.

### V (2, high)
Scope: workflows, check files.
Pros: weekly lock-update workflow builds two hosts ([`.github/workflows/auto-upgrade-flakes.yaml:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/.github/workflows/auto-upgrade-flakes.yaml#L1)).
Cons: [`_to_migrate/imports/checks.nix:1`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/_to_migrate/imports/checks.nix#L1) is not loaded (underscore tree); no relevant checks. Observation.
Confidence: high.

### O (4, medium)
Scope: `flake-parts/deploy.nix`, auto-upgrade, facter.
Pros: deploy-rs nodes for every `nixosConfiguration` ([`modules/flake-parts/deploy.nix:22-42`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/flake-parts/deploy.nix#L22-L42)), so derived from the host set; auto-upgrade aspect ([`modules/base/system/auto-upgrade/default.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/base/system/auto-upgrade/default.nix#L7)).
Cons: fixed `sshUser = "root"` with no per-host overrides; secrets live in a private repo; one concern driven by host data.
Confidence: medium.

### B (6, medium)
Scope: census record plus aspect reads; B_div 7.5 -> 5, B_ref 12 -> 7, B = mean(5,7) = 6.
Pros: B_div = 7.5: selection-verified substantive: zellij, fish, starship, vscode, zed, kde = 6; peers: micro substantive 1; gram/antigravity (installed, no config) 0.5. B_ref lists 12 units (evidence block): gram, vscode, zeditor, firefox, git, reticulum-server, email, gh-dash, searx, guacamole, konsole, noise-station-server.
Cons: gram and antigravity are installed with no configuration (counted 0.5), [`modules/games/enemy-territory.nix:14`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/games/enemy-territory.nix#L14) is a package plus desktop entries and was dropped; [`modules/ai/open-webui.nix:50`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/ai/open-webui.nix#L50) and [`modules/desktop/environment/kdeplasma.nix:370`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/desktop/environment/kdeplasma.nix#L370) are excluded for leaked IPs and paths. No fish/starship-level shell units beyond what the census credits.
```score-evidence
{"B": {"diversity_points": 7.5, "diversity_grade": 5, "reference_grade": 7, "reference_units": [{"name": "gram", "evidence": "modules/dev/editors/gram/gram.nix:63"}, {"name": "vscode", "evidence": "modules/dev/editors/vscode.nix:26"}, {"name": "zeditor", "evidence": "modules/dev/editors/zeditor.nix:45"}, {"name": "firefox", "evidence": "modules/desktop/web-browsers/firefox.nix:18"}, {"name": "git", "evidence": "modules/dev/git/git.nix:20"}, {"name": "reticulum-server", "evidence": "modules/reticulum/reticulum-server.nix:109"}, {"name": "email", "evidence": "modules/email/default.nix:6"}, {"name": "gh-dash", "evidence": "modules/dev/git/gh-dash.nix:16"}, {"name": "searx", "evidence": "modules/searx/searx.nix:13"}, {"name": "guacamole", "evidence": "modules/guacamole/guacamole.nix:17"}, {"name": "konsole", "evidence": "modules/desktop/environment/konsole.nix:16"}, {"name": "noise-station-server", "evidence": "modules/noise-station-server/default.nix:43"}]}}
```
Representative cited units: pro [`modules/dev/editors/gram/gram.nix:63`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/dev/editors/gram/gram.nix#L63) and [`modules/email/default.nix:6`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/email/default.nix#L6) are cited at the line where their configuration begins; the other units in the block are cited the same way.
Confidence: medium.

### X (2, high)
Scope: hosts, deploy.
Pros: deploy nodes generated per host ([`modules/flake-parts/deploy.nix:22`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/flake-parts/deploy.nix#L22)), credited under O only.
Cons: NixOS only; no non-host targets.
Confidence: high.


### Total
2*3+6+3+4+5+3+4+6+2/2+2/2 = **39.0/100**

### Shortlist judgment
Not a showcase or starter; library units facter aspect (A) and nix-trusted-user (A).

Overall pros:
- Large aspect-per-feature tree with solid app configs (B 6).
- facter report passed as an aspect function arg ([`facter.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/facter/facter.nix#L7)).
- deploy-rs nodes generated for every host ([`deploy.nix:22-42`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/flake-parts/deploy.nix#L22-L42)).

Overall cons:
- Untyped `meta` store with fixed-name lookups; no quirks/policies.
- Several leaked paths/IPs in shared aspects; unguarded private input blocks evaluation.
- No checks; README lacks add-a-host guidance.

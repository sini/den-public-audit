# hmajid2301__nixicle

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/hmajid2301__nixicle.md)

- Upstream: [hmajid2301/nixicle](https://github.com/hmajid2301/nixicle)
- Reviewed revision: [`ca0d927add73`](https://github.com/hmajid2301/nixicle/commit/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0)
- Author: hmajid2301
- Score: **57.0 / 100**, rank 24 of 103 ranked configs. D 6 · I 6 · S 4 · R 9 · P 6 · L 2 · V 6 · O 7 · B 7 · X 2. Shortlists: library units (2).
- Summary: Live persistence forward and host facts, derived deploy/secrets/backups, independent TUIOS HM module and broad native references; identity gaps, global side effects, operation-only docs and uninvoked focused tests constrain the vector.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

## Contents

- [1. Shape](#1-shape)
- [2. Common patterns](#2-common-patterns)
- [3. Novel patterns](#3-novel-patterns)
- [4. Library candidates](#4-library-candidates)
- [5. den friction](#5-den-friction)
- [6. Docs and complexity](#6-docs-and-complexity)
- [6a. Defects and scoring notes.](#6a-defects-and-scoring-notes)
- [7. Template notes](#7-template-notes)
- [8. Scorecard.](#8-scorecard)

## 1. Shape
A feature-aspect tree combines fleet defaults with user-specific service profiles (`modules/defaults.nix:115`, `modules/hosts.nix:73`). Host/user wiring is separated from small class-targeted modules (`modules/aspects/programs/obs.nix:2`).

## 2. Common patterns
- den.default includes account definition (`modules/defaults.nix:117`).
- provides tree: the VPS profile selects shell, git, SSH and agent tools (`modules/hosts.nix:73`).
- primary-user is selected at the user composition point (`modules/hosts.nix:69`).

## 3. Novel patterns
The VPS provider groups terminal and agent tools as a distinct user deployment profile instead of enabling every workstation feature (`modules/hosts.nix:73`).

## 4. Library candidates
- vpn · `modules/aspects/services/vpn.nix:2` · WireGuard support plus Tailscale daemon · inputs: NixOS/nixpkgs · parameterization: none (`modules/aspects/services/vpn.nix:4`) · **A**, a small opt-in connectivity bundle; no peer or authentication material is embedded.

- tuios-home-module · `modules/aspects/cli/multiplexers/tuios/_home-manager.nix:20` · native HM app module with package/settings and guarded Fish/Pi/Claude integration · inputs: nixpkgs, HM (TUIOS package) · typed options, disabled by default · **A**, exported independently (`modules/aspects/cli/multiplexers/tuios/default.nix:4`), with minimal x86 Linux consumer and disabled/configured controls (`modules/aspects/cli/multiplexers/tuios/_tests.nix:3`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:7`).

## 5. den friction
No verified den-specific friction in the reviewed default, provider and VPN fragments (`modules/defaults.nix:115`, `modules/hosts.nix:73`, `modules/aspects/services/vpn.nix:2`).

## 6. Docs and complexity
Docs **3**: install/build/deploy usage is explained (`README.md:12`, `README.md:35`). Complexity **4**: shared defaults, primary-user wiring and differentiated VPS provider composition (`modules/defaults.nix:115`, `modules/hosts.nix:69`, `modules/hosts.nix:73`).

## 6a. Defects and scoring notes.

- **I · moderate**: Neovim also modifies system-wide Nix cache policy (`modules/aspects/cli/editors/neovim/default.nix:101`); unrelated side effects cap I6.
- **S · moderate**: declared user email/signing options (`modules/defaults.nix:51`, `modules/defaults.nix:56`) do not control the Git owner’s fixed identity (`modules/aspects/cli/tools/git.nix:8`); the 19 grouped adaptations below limit contract design/coverage.
- **L · moderate**: operation-first README lacks a composition/adoption route (`README.md:12`, `README.md:61`), matching L2 rather than asserting a missing runtime feature.
- **V · minor**: isolated TUIOS test definitions (`modules/aspects/cli/multiplexers/tuios/_tests.nix:37`) are not included in exported checks (`modules/flake-outputs.nix:279`); focused verification remains uninvoked.
- Withdraw the earlier VPN concern: an explicit opt-in WireGuard/Tailscale bundle is coherent functionality, not a verified selection defect (`modules/aspects/services/vpn.nix:4`). Narrow Linux scope and ordinary fixed service ports are not defects.

## 7. Template notes
Small aspects are easy to transplant; use the VPS profile to learn provider composition before adopting personal tool selections (`modules/hosts.nix:73`).

## 8. Scorecard.

### D
Scope / pros: Docker emits persistence data (`modules/aspects/services/docker.nix:3`); the host schema forwards the selected aspect class into environment.persistence./persist, guarded on available options (`modules/aspects/system/impermanence.nix:20`, `modules/aspects/system/impermanence.nix:25`, `modules/aspects/system/impermanence.nix:33`); impermanence imports its consumer module (`modules/aspects/system/impermanence.nix:47`). Host laptop facts also cross into HM arguments and condition actual lid bindings (`modules/hosts.nix:200`, `modules/defaults.nix:26`, `modules/aspects/desktops/niri/_settings/lid.nix:15`). Cons: one routed resource channel, not cross-host policy/pipe routing or explicit conflict diagnostics (`modules/aspects/system/impermanence.nix:32`). Interpolation 6 above the single-channel 5 anchor for an actual forward route plus context variation; no extra credit for package lookup or selection bags. Score **6**; confidence **medium**.

### I
Scope / pros: many app owners stay small, while profiles select them explicitly (`modules/aspects/cli/editors/helix/default.nix:3`, `modules/aspects/profiles/development/default.nix:29`); TUIOS separates reusable native module from preset/tests (`modules/aspects/cli/multiplexers/tuios/default.nix:14`). Cons: Neovim also changes global Nix substituters (`modules/aspects/cli/editors/neovim/default.nix:101`), and common desktop configuration owns unrelated apps together (`modules/aspects/profiles/common/desktop-apps.nix:25`, `modules/aspects/profiles/common/desktop-apps.nix:43`). Interpolation 6, capped by unrelated global side effects. Score **6**; confidence **medium**.

### S
Scope / pros: typed host/user/domain and app settings exist (`modules/defaults.nix:46`, `modules/aspects/system/identity-options.nix:5`, `modules/aspects/ai/pi-coding-agent/default.nix:74`). Cons: Git ignores declared user email/signing variation, using a fixed name and fleet library identity instead (`modules/aspects/cli/tools/git.nix:8`, `modules/aspects/cli/tools/git.nix:9`, `modules/defaults.nix:51`). Contract 4, below 5 because those contracts incompletely cover real variation. Conservative **19 groups** across shared defined bodies: main domain/subdomains and primary identity (`lib/default.nix:96`, `lib/default.nix:101`, `modules/aspects/cli/tools/git.nix:8`); banterbus.games domain (`modules/aspects/services/traefik.nix:69`); subtitle account (`modules/aspects/services/nixflix.nix:191`); Tangled DID (`modules/aspects/services/tangled.nix:50`); private cache URL/key (`modules/aspects/cli/tools/attic/cache.nix:17`, `modules/aspects/cli/tools/attic/cache.nix:23`); B2 bucket (`modules/aspects/services/btrbk.nix:105`); checkout root (`modules/aspects/profiles/desktop/default.nix:69`); two media mount roots (`modules/aspects/services/immich.nix:3`, `modules/aspects/services/jellyfin.nix:44`); work organization (`modules/aspects/cli/shells/fish.nix:124`); three fixed hostnames, vps/nas/desktop (`modules/aspects/cli/tools/attic/server.nix:66`, `modules/aspects/services/monitoring/prometheus.nix:108`, `modules/aspects/services/gitlab-runner.nix:21`); two runtime UID roots (`modules/aspects/profiles/common/default.nix:191`, `modules/hosts.nix:104`); VAPID key (`modules/aspects/services/goroutinely.nix:76`); OAuth client identifier (`modules/aspects/services/gothreads.nix:58`); a committed credential (reported privately; not located here). Raw occurrences exceed 19: repeated identities, subdomains, paths and the cache pair are grouped. Coverage caps at 5; min(4,5)=4. Constants in defined alternatives are included without asserting activation. Score **4**; confidence **medium**.
```score-evidence
{"S":{"contract_design":4,"leak_coverage":5,"distinct_leaks":19}}
```

### R
Scope / pros: exported TUIOS HM module owns typed package/settings and opt-in integrations (`modules/aspects/cli/multiplexers/tuios/default.nix:4`, `modules/aspects/cli/multiplexers/tuios/_home-manager.nix:20`), with guarded effects and selected-package consumers (`modules/aspects/cli/multiplexers/tuios/_home-manager.nix:33`, `modules/aspects/cli/multiplexers/tuios/_home-manager.nix:78`). The minimal independent x86 Linux HM consumer demonstrates disabled, default and configured cases (`modules/aspects/cli/multiplexers/tuios/_tests.nix:3`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:7`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:21`). Cons: this clean contract does not make identity-bound Git or media owners portable (`modules/aspects/cli/tools/git.nix:8`, `modules/aspects/services/jellyfin.nix:47`). Literal 9 for at least one substantial grade-A unit plus explicit consumer; test presence is not a passing-test claim. Score **9**; confidence **medium**.

### P
Scope / pros: x86 Linux and ARM host constructors are distinct (`modules/hosts.nix:17`, `modules/hosts.nix:27`, `modules/hosts.nix:238`); standalone Linux homes use a separate constructor and native graphics/PAM wrappers (`modules/hosts.nix:38`, `modules/aspects/profiles/non-nixos/default.nix:17`). Cons: generic-Linux wrappers explicitly rely on external system binaries and hardware assumptions (`modules/aspects/profiles/non-nixos/_wrappers.nix:35`, `modules/aspects/profiles/non-nixos/_session.nix:8`), with Dell-specific repairs rather than general boundary tests (`hosts/dell/default.nix:18`). Interpolation 6 for real architecture/home separation above honest narrow 5, below validated cross-platform 9. Score **6**; confidence **medium**.

### L
Scope / pros: install/build/home/deploy commands are concrete (`README.md:17`, `README.md:35`, `README.md:54`), and local module options document integration switches (`modules/aspects/cli/multiplexers/tuios/_home-manager.nix:26`). Cons: README provides operations and screenshots rather than an entry→inventory→feature/provider composition tutorial (`README.md:61`, `README.md:76`); task selection is operational too (`Taskfile.yml:15`). Literal 2 for primarily operation-only adoption documentation. Score **2**; confidence **medium**.

### V
Scope / pros: CI builds desktop/VPS/NAS and evaluates all six listed hosts (`.gitlab-ci.yml:132`, `.gitlab-ci.yml:144`, `.gitlab-ci.yml:169`); deploy output checks are exported (`modules/flake-outputs.nix:279`). Isolated TUIOS tests cover disabled effects, chosen package and integration guards (`modules/aspects/cli/multiplexers/tuios/_tests.nix:38`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:68`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:90`). Cons: those isolated test files have no traced CI/recipe import, while exported checks contain deploy/precommit checks (`modules/flake-outputs.nix:279`); CI keeps a manual host list (`.gitlab-ci.yml:169`). Interpolation 6, capped for uninvoked focused tests; no builds/tests executed in this audit. Score **6**; confidence **medium**.

### O
Scope / pros: deploy nodes derive from generated configurations and platform/user facts (`lib/default.nix:63`, `lib/default.nix:69`, `lib/default.nix:79`, `modules/flake-outputs.nix:269`). App-owned secrets feed service consumers (`modules/aspects/services/crowdsec.nix:139`, `modules/aspects/services/crowdsec.nix:240`). Backup objects emit paths/hooks; typed defaults feed restic jobs and expected metrics (`modules/aspects/services/garage.nix:12`, `modules/aspects/system/backup.nix:6`, `modules/aspects/system/backup.nix:75`, `modules/aspects/system/backup.nix:116`). Cons: key enrollment, CI host lists and installer selection remain hand-maintained (`lib/default.nix:19`, `.gitlab-ci.yml:169`, `Taskfile.yml:22`); deploy chooses the first normal user when not overridden (`lib/default.nix:70`). Interpolation 7 for three derived concerns, below 9 provisioning/install coverage. Score **7**; confidence **medium**.

### X
Scope / pros: the reusable TUIOS module and Neovim wrapper are useful native HM integrations (`modules/aspects/cli/multiplexers/tuios/default.nix:4`, `modules/aspects/cli/editors/neovim/default.nix:99`). Cons: neither is registered/evaluated as its own Den target class; Tangled microVM images are built beside Den outputs (`modules/flake-outputs.nix:126`). The persistence class is an operational resource projection, already accounted in D/O (`modules/aspects/system/impermanence.nix:25`). Literal baseline 2. Score **2**; confidence **medium**.

### B
Scope / pros: the enumerated owners below are complete app presets or real integrations. Standard persistence/secrets/backup collectors are allowed: backup paths/hooks have typed defaults and a traced consumer (`modules/aspects/system/backup.nix:6`, `modules/aspects/system/backup.nix:116`). Native TUIOS module counts independently because it is explicitly exported, not an extracted inner fragment (`modules/aspects/cli/multiplexers/tuios/default.nix:4`). Redis and Valkey variants count once (`modules/aspects/services/redis.nix:7`); ordinary optional Fish integration is allowed for otherwise usable installed Worktrunk/Carapace (`modules/aspects/cli/tools/worktrunk/default.nix:13`, `modules/aspects/profiles/common/cli.nix:16`). Cons / exclusions: lib.nixicle proxy/domain-dependent services (`modules/aspects/services/adguard.nix:51`), identity/mount-bound media/Git (`modules/aspects/services/jellyfin.nix:44`, `modules/aspects/cli/tools/git.nix:8`), Neovim checkout default (`modules/aspects/cli/editors/neovim/_nix/default.nix:44`), Fish aliases with unowned commands and Zellij personal roots (`modules/aspects/cli/shells/fish.nix:152`, `modules/aspects/cli/multiplexers/zellij/config.kdl:190`), unowned-Fish-launching terminals (`modules/aspects/cli/terminals/kitty.nix:10`), fleet skill assets (`modules/aspects/ai/skills/hister/SKILL.md:13`), and token/package/include-only bags. Twenty enumerated references give 9, diversity gives 5; B7. Score **7**; confidence **medium**.
B_div: 6.5 points → 5; B_ref: 20 units → 9; half-up mean → 7.
```score-evidence
{"B":{"diversity_points":6.5,"diversity_grade":5,"reference_grade":9,"reference_units":[{"name":"CrowdSec","evidence":"modules/aspects/services/crowdsec.nix:117"},{"name":"Docker","evidence":"modules/aspects/services/docker.nix:15"},{"name":"Garage","evidence":"modules/aspects/services/garage.nix:25"},{"name":"Nixery","evidence":"modules/aspects/services/nixery.nix:22"},{"name":"Ollama","evidence":"modules/aspects/services/ollama.nix:25"},{"name":"Podman","evidence":"modules/aspects/services/podman.nix:7"},{"name":"PostgreSQL","evidence":"modules/aspects/services/postgresql.nix:18"},{"name":"Valkey/Redis","evidence":"modules/aspects/services/redis.nix:6"},{"name":"Tailscale","evidence":"modules/aspects/services/tailscale.nix:5"},{"name":"Unbound","evidence":"modules/aspects/services/unbound.nix:5"},{"name":"Loki","evidence":"modules/aspects/services/monitoring/loki.nix:11"},{"name":"Tempo","evidence":"modules/aspects/services/monitoring/tempo.nix:11"},{"name":"Helix","evidence":"modules/aspects/cli/editors/helix/default.nix:7"},{"name":"GPG/keyring","evidence":"modules/aspects/cli/tools/gpg.nix:10"},{"name":"KVM/libvirt","evidence":"modules/aspects/hardware/kvm.nix:6"},{"name":"PipeWire audio","evidence":"modules/aspects/hardware/audio.nix:9"},{"name":"Worktrunk","evidence":"modules/aspects/cli/tools/worktrunk/default.nix:6"},{"name":"Carapace","evidence":"modules/aspects/profiles/common/cli.nix:11"},{"name":"TUIOS","evidence":"modules/aspects/cli/multiplexers/tuios/_home-manager.nix:20"},{"name":"Steam gaming stack","evidence":"modules/aspects/profiles/gaming/default.nix:30"}]}}
```

Total: **57.0/100**. Shortlists: showcase false; library_units ['vpn', 'tuios-home-module']; starter false.

Overall pros:
- Real persistence route connects feature data to the OS consumer (`modules/aspects/services/docker.nix:3`, `modules/aspects/system/impermanence.nix:23`).
- TUIOS provides an independently exported native module and minimal consumer (`modules/aspects/cli/multiplexers/tuios/default.nix:4`, `modules/aspects/cli/multiplexers/tuios/_tests.nix:7`).
- Deploy and backup jobs derive from declared outputs/resources (`lib/default.nix:63`, `modules/aspects/system/backup.nix:116`).

Overall cons / limits:
- Typed identity options do not cover the actual fixed Git identity (`modules/defaults.nix:51`, `modules/aspects/cli/tools/git.nix:8`).
- Native app files sometimes modify unrelated global policy (`modules/aspects/cli/editors/neovim/default.nix:101`).
- The README teaches operations without a composition path, and focused tests are outside exported checks (`README.md:35`, `modules/flake-outputs.nix:279`).

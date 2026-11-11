# sk4rd/mikos-den

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/sk4rd/mikos-den.md)

- Upstream: [sk4rd/mikos-den](https://github.com/sk4rd/mikos-den)
- Reviewed revision: [`de31f342886a`](https://github.com/sk4rd/mikos-den/commit/de31f342886ae653aa46264d60587661476ea9b9)
- Author: sk4rd
- Score: **57.0 / 100**, rank 24 of 103 ranked configs. D 7 · I 9 · S 6 · R 5 · P 5 · L 7 · V 4 · O 5 · B 3 · X 2. Shortlists: showcase, library units (1).
- Summary: D several built-in quirk channels capped7; I feature ownership; S typed contracts/leakcoverage6; R opt-in SSH extraction; P Linux/Hjem; L architecture/install guides; V assertions/manual VM recipe; O service provisioning; X baseline; B three census families and four references.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

## Contents

- [1. Shape.](#1-shape)
- [2. Common patterns.](#2-common-patterns)
- [3. Novel patterns.](#3-novel-patterns)
- [4. Library candidates.](#4-library-candidates)
- [5. den friction.](#5-den-friction)
- [6. Docs and complexity.](#6-docs-and-complexity)
- [6a. Defects and scoring notes.](#6a-defects-and-scoring-notes)
- [7. Template notes.](#7-template-notes)
- [8. Scorecard.](#8-scorecard)

## 1. Shape.

A feature-oriented NixOS fleet uses hjem for user files and host lists for composition ([`README.md:5`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L5), [`README.md:19`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L19)). Den is extended with typed settings and service/storage contribution channels ([`modules/den.nix:13`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L13)).


## 2. Common patterns.

- custom schema/classes: host.settings uses a custom settings type ([`modules/den.nix:21`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L21)).
- quirks: route, endpoint, heartbeat and dataset contributions have explicit channels ([`modules/den.nix:16`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L16)).
- provides tree: NAS supplies a user media group while laptop supplies user applications ([`modules/hosts/nas.nix:30`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/hosts/nas.nix#L30), [`modules/hosts/thinkpad-z13.nix:24`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/hosts/thinkpad-z13.nix#L24)).


## 3. Novel patterns.

Service-owned routes are emitted by Jellyfin ([`modules/features/jellyfin.nix:9`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L9)), aggregated into reverse-proxy hosts ([`modules/features/service-names.nix:32`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L32)) and filtered for public DDNS records ([`modules/features/ddns.nix:31`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ddns.nix#L31)). Status endpoints flow from Jellyfin to the status consumer ([`modules/features/jellyfin.nix:16`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L16), [`modules/features/status.nix:56`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L56)); this is working source-level dataflow beyond quirk declarations.


## 4. Library candidates.

- openssh · [`modules/features/openssh.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/openssh.nix#L4) · passwordless-key SSH service with root login disabled · nixpkgs/NixOS · none · B: separate the global schema include at line 14 from opt-in service configuration.


## 5. den friction.

The reservedKeys declaration explicitly prevents settings declarations being interpreted as aspects ([`modules/den.nix:13`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L13)); a concrete extension seam to document upstream.


## 6. Docs and complexity.

Docs 4: README explains feature, host, dotfile and secret boundaries and links architecture documentation ([`README.md:12`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L12), [`README.md:19`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L19)). Complexity 5: typed schema and four quirk channels support a workstation/laptop/NAS fleet ([`modules/den.nix:16`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L16), [`modules/hosts/nas.nix:31`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/hosts/nas.nix#L31)).


## 6a. Defects and scoring notes.

- S · moderate: seven grouped deployment values bypass typed settings; groups/citations in S card ([`modules/features/service-names.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L4), [`modules/features/nas-vpn-client.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-vpn-client.nix#L4), [`modules/features/proton-backup.nix:7`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/proton-backup.nix#L7)). Former domain-emitter architect deduction belongs here, not D.
- R · moderate: shared WireGuard feature fixes the repository secret asset path rather than accepting it as an extraction input ([`modules/features/wireguard-server.nix:43`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/wireguard-server.nix#L43)).
- D · minor: status-heartbeat records are folded with overwrite semantics and no duplicate diagnostic ([`modules/features/status.nix:98`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L98)).

## 7. Template notes.

Strong advanced reference for service composition and hjem; keep private topology and VPN secrets out of a starter ([`modules/hosts/nas.nix:7`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/hosts/nas.nix#L7), [`README.md:8`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L8)).

## 8. Scorecard.

### D
Scope: service routes, health, heartbeats and datasets. Pros: Jellyfin emits routes/health ([`modules/features/jellyfin.nix:9`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L9), [`modules/features/jellyfin.nix:16`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L16)); built-in quirk aggregation feeds Caddy, public-only DDNS and status ([`modules/features/service-names.nix:32`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L32), [`modules/features/ddns.nix:31`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ddns.nix#L31), [`modules/features/status.nix:56`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L56)). Dataset emitter→collector also rejects duplicate/base overrides ([`modules/features/home-assistant.nix:50`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/home-assistant.nix#L50), [`modules/features/nas-storage.nix:125`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L125), [`modules/features/nas-storage.nix:135`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L135)); empty contributions fold safely. Cons: heartbeat merging silently overwrites duplicate keys ([`modules/features/status.nix:98`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L98)); no cross-scope policy/pipe routing. Calibration7 for several live built-in channels, below8-9 cross-scope semantics. Score **7**; confidence **medium**.

### I
Scope: aspect owners and host assembly. Pros: one owner carries service/data/health concerns, optional host lists choose it ([`modules/features/jellyfin.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L4), [`docs/architecture.md:18`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/architecture.md#L18)). Cons: no additional concrete isolation defect verified; broad service units coordinate related responsibilities ([`modules/features/home-assistant.nix:33`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/home-assistant.nix#L33)). Literal9: ownership fits the real three-host scope, with no scale bonus. Score **9**; confidence **medium**.

### S
Scope: typed host settings and shared service/network/storage bodies. Pros: typed WireGuard peers/interface/port and DDNS settings support real consumer variation ([`modules/features/wireguard-server.nix:6`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/wireguard-server.nix#L6), [`modules/features/wireguard-server.nix:23`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/wireguard-server.nix#L23), [`modules/features/ddns.nix:7`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ddns.nix#L7)). Cons: coverage6 for seven adaptation groups: sk4rd.com domain family, LAN network, VPN network, tank storage root/pool, NAS public identity, owner/YubiKey identities, Proton remote backup location ([`modules/features/service-names.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L4), [`modules/features/service-names.nix:10`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L10), [`modules/features/service-names.nix:11`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L11), [`modules/features/nas-storage.nix:60`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L60), [`modules/features/nas-vpn-client.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-vpn-client.nix#L4), [`modules/features/yubikey.nix:46`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/yubikey.nix#L46), [`modules/features/proton-backup.nix:7`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/proton-backup.nix#L7)). Contract7 exceeds5 through typed/defaulted variation, short of9 because these bypass it; min(7,6)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":7}}
```

### R
Scope: existing §4 openssh. Pros: independent SSH security preset requires no author identity ([`modules/features/openssh.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/openssh.nix#L4)). Cons: module also globally attaches itself to host schema, so an opt-in consumer must separate that statement ([`modules/features/openssh.nix:14`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/openssh.nix#L14)). Literal5 gradeB; secret asset dependency in WireGuard limits other extraction candidates without a second S deduction ([`modules/features/wireguard-server.nix:43`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/wireguard-server.nix#L43)). Score **5**; confidence **medium**.

### P
Scope: NixOS hosts and Hjem user class. Pros: OS/user ownership is explicit and hardware class boundaries localized ([`modules/features/ghostty.nix:20`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ghostty.nix#L20), [`modules/features/ghostty.nix:24`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ghostty.nix#L24)). Cons: native Linux services and Plasma shortcuts define a narrow target, not cross-platform examples ([`modules/features/ghostty.nix:37`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/ghostty.nix#L37)). Literal5 honest narrow scope; Hjem is standard home management, not X breadth. Score **5**; confidence **medium**.

### L
Scope: README and architecture/install/secrets guides. Pros: teaches feature ownership, typed host settings and actual quirk consumers ([`docs/architecture.md:25`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/architecture.md#L25), [`docs/architecture.md:28`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/architecture.md#L28)); install explains key ordering ([`docs/install.md:27`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/install.md#L27)). Cons: walkthrough assumes an existing personal host/key inventory rather than a minimal independent consumer ([`docs/install.md:3`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/install.md#L3), [`docs/secrets.md:10`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/secrets.md#L10)). Interpolated7: substantial teaching beyond5, below a self-contained first-user9 path. Score **7**; confidence **medium**.

### V
Scope: runtime health, assertions and documented VM recipe. Pros: duplicate routes and datasets have assertions ([`modules/features/service-names.nix:62`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L62), [`modules/features/nas-storage.nix:135`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L135)); README gives representative VM checking ([`README.md:31`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/README.md#L31)). Cons: runtime health checks are not a composition regression suite ([`modules/features/media-vpn-health.nix:21`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/media-vpn-health.nix#L21)); no CI invocation of negative context tests established. Interpolated4: meaningful safeguards/manual recipe, short of5 representative automated output checks; passing unknown. Score **4**; confidence **medium**.

### O
Scope: secret delivery and storage/backup provisioning. Pros: service dataset emissions drive ZFS creation and snapshot templates ([`modules/features/home-assistant.nix:50`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/home-assistant.nix#L50), [`modules/features/nas-storage.nix:164`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L164)); backup results feed generated status checks ([`modules/features/proton-backup.nix:11`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/proton-backup.nix#L11), [`modules/features/status.nix:175`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L175)). Cons: host keys/recipients and installation remain manual ([`docs/install.md:14`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/install.md#L14), [`docs/secrets.md:10`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/secrets.md#L10)). Literal5: real service-driven provisioning, no unified deploy/bootstrap/builder lifecycle. Score **5**; confidence **medium**.

### X
Scope: Hjem, testing VM and keyboard package. Pros: standard VMVariant and device package outputs are explicit ([`modules/features/nixos-testing-vm.nix:7`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nixos-testing-vm.nix#L7), [`modules/features/keyboard.nix:12`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/keyboard.nix#L12)). Cons: neither is a non-host Den class; the keyboard output aliases an external package rather than deriving from entity facts ([`modules/features/keyboard.nix:13`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/keyboard.nix#L13)). Baseline2; ordinary home class belongs under P. Score **2**; confidence **medium**.

### B
Scope: census max-depth apps and complete reference units. Pros: list includes all counted identity-free meaningful presets ([`modules/features/git.nix:5`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/git.nix#L5)). Cons: theme-dependent desktop apps require external config.theme; service/VPN leaves require fleet storage/settings/identity envelope, and package-only leaves are not substantive references ([`modules/features/neovim.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/neovim.nix#L4), [`modules/features/nas-vpn-client.nix:25`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-vpn-client.nix#L25), [`modules/features/gh.nix:5`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/gh.nix#L5)). Bare PipeWire enablement is not counted ([`modules/features/audio.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/audio.nix#L4)). Score **3**; confidence **medium**.
B_div: 3 points → 2; B_ref: 4 units → 4; half-up mean → 3.
```score-evidence
{"B":{"diversity_points":3,"diversity_grade":2,"reference_grade":4,"reference_units":[{"name":"openssh","evidence":"modules/features/openssh.nix:4"},{"name":"git","evidence":"modules/features/git.nix:2"},{"name":"flatpak","evidence":"modules/features/flatpak.nix:4"},{"name":"flaresolverr","evidence":"modules/features/flaresolverr.nix:4"}]}}
```

Total: **57.0/100**. Shortlists: showcase true; library_units ['openssh']; starter false.

Overall pros:
- Several real service-owned channels ([`modules/features/jellyfin.nix:9`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/jellyfin.nix#L9)).
- Collision checks protect dataset ownership ([`modules/features/nas-storage.nix:135`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/nas-storage.nix#L135)).
- Docs teach boundaries and key provisioning ([`docs/architecture.md:28`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/architecture.md#L28), [`docs/install.md:27`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/docs/install.md#L27)).

Overall cons / limits:
- Fleet domain/network values remain inline (§6a S; [`modules/features/service-names.nix:4`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/service-names.nix#L4)).
- WireGuard extraction needs a secret source contract (§6a R; [`modules/features/wireguard-server.nix:43`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/wireguard-server.nix#L43)).
- Heartbeat duplicate keys overwrite silently (§6a D; [`modules/features/status.nix:98`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/status.nix#L98)).

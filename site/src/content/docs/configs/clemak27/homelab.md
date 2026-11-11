---
title: "clemak27/homelab"
---

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](/glossary/). For a guide to the scorecard, see [how to read a scorecard](/#how-to-read-a-scorecard).

[Index](/) · [Ranking](/ranking/) · [Census notes](/census/configs/clemak27/homelab/)

- Upstream: [clemak27/homelab](https://github.com/clemak27/homelab)
- Reviewed revision: [`a8bb1c3f0fec`](https://github.com/clemak27/homelab/commit/a8bb1c3f0fec737ab49636845df4d03374004057)
- Author: clemak27
- Score: **34.5 / 100**, rank 94 of 101 ranked configs. D 2 · I 5 · S 2 · R 6 · P 5 · L 2 · V 5 · O 5 · B 2 · X 2. Shortlists: library units (1).
- Summary: Clear hardware/cluster namespaces and aspect-owned secrets; direct hardcoded service configuration, manual platform assumptions, complete Starship leaf and invoked evaluation checks.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](/method/rubric/).

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

Dendritic imports load Den with separate exported hardware and k3s namespaces ([`modules/defaults.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L3)). Inventory spans an x86 server and two ARM agents ([`modules/hosts/hosts.nix:2`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L2)).

## 2. Common patterns

- namespace separates hardware and k3s concerns ([`modules/defaults.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L6)).
- den.default sets shared OS state version ([`modules/defaults.nix:10`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L10)).

## 3. Novel patterns

Two domain namespaces reflect the split between physical nodes and cluster roles ([`modules/defaults.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L6), [`README.md:5`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L5)).

## 4. Library candidates

- **starship-preset · A:** complete identity-free NixOS Starship preset for directory, Nix-shell and SSH-host display; no custom helpers or assets ([`modules/aspects/shell/starship.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L6), [`modules/aspects/shell/starship.nix:13`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L13)). Rewrite with standard module overrides; NixOS shell scope explicit.

## 5. den friction

No verified Den-specific friction in the reviewed imports ([`modules/defaults.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L3)).

## 6. Docs and complexity

Docs 3: README explains cluster size, layout and software ([`README.md:5`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L5), [`README.md:11`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L11), [`README.md:34`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L34)). Complexity 3: heterogeneous hosts and two namespaces ([`modules/hosts/hosts.nix:2`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L2), [`modules/defaults.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L6)).

## 6a. Defects and scoring notes
- moderate · **S**: shared Blocky/k3s/WireGuard/SOPS owners fix domain, control-plane address, peer identities/network, NIC and operator key-file path ([`modules/aspects/blocky.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/blocky.nix#L25), [`modules/aspects/k3s/agent.nix:18`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L18), [`modules/aspects/wireguard.nix:20`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L20), [`modules/aspects/sops.nix:16`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/sops.nix#L16)). Consumers must patch shared source rather than entity settings.
- minor · **I**: server/agent roles duplicate shutdown, storage-tool, iSCSI and sysctl policies ([`modules/aspects/k3s/server.nix:11`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L11), [`modules/aspects/k3s/server.nix:18`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L18), [`modules/aspects/k3s/agent.nix:21`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L21), [`modules/aspects/k3s/agent.nix:28`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L28)).
- minor · **L**: README lists hosts/ while current inventory is modules/hosts ([`README.md:15`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L15), [`modules/hosts/hosts.nix:2`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L2)) and gives no entry-to-feature selection route.
No successful evaluation or deployment is asserted; disabled cluster-node firewall is an explicit policy, not by itself a verified defect ([`modules/aspects/k3s/server.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L6)).

## 7. Template notes

Useful small heterogeneous homelab example; README frames it as personal inspiration ([`README.md:8`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L8)).

## 8. Scorecard

### D (2, high)
Scope: Pros: three host selections and explicit role/hardware namespaces ([`modules/hosts/hosts.nix:2`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L2), [`modules/defaults.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L6)). Cons: cluster/service facts are literal assignments; secret path linking uses ordinary NixOS configuration, not an authored Den emit/route contract ([`modules/aspects/k3s/agent.nix:17`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L17), [`modules/aspects/wireguard.nix:32`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L32)). Baseline2; no ceremonial data-flow credit. Confidence: high.

### I (5, high)
Scope: Pros: namespaces separate hardware/cluster and app owners ([`modules/defaults.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L6), [`modules/hosts/hl-server.nix:8`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-server.nix#L8)). Cons: storage and shutdown policy are copied between role files (§6a; [`modules/aspects/k3s/server.nix:11`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L11), [`modules/aspects/k3s/agent.nix:21`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L21)). Literal5 named features localize most changes, with some repeated bundles. Confidence: high.

### S (2, medium)
Scope: Pros: host-owned disks remain in host files ([`modules/hosts/hl-server.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-server.nix#L25)). Cons: shared service/network/secret bodies embed operator facts (§6a). Contract2, coverage5 from11 grouped adaptations: wallstreet30.cc domain/subdomains/certificate label; control-plane address; SOPS key-file root; WAN NIC; WireGuard network; five individual peer identities/keys; shared iSCSI initiator identity ([`modules/aspects/blocky.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/blocky.nix#L25), [`modules/aspects/k3s/agent.nix:18`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L18), [`modules/aspects/sops.nix:16`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/sops.nix#L16), [`modules/aspects/wireguard.nix:20`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L20), [`modules/aspects/wireguard.nix:30`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L30), [`modules/aspects/wireguard.nix:42`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L42), [`modules/aspects/k3s/server.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L25)). Domain variants and repeated addresses are grouped, not counted by occurrence; generic public DNS and host-owned hardware UUIDs are not additional leaks. min(2,5)=2. Confidence: medium.
```score-evidence
{"S": {"contract_design": 2, "leak_coverage": 5, "distinct_leaks": 11}}
```

### R (6, medium)
Scope: Pros: Starship is a complete identity-free application preset ([`modules/aspects/shell/starship.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L6)); hardware and role modules show a useful separation ([`modules/hosts/hl-agent-00.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-agent-00.nix#L3)). Cons: service owners require source patching or custom SOPS inclusion, and no exported independent consumer demonstrates the preset ([`modules/aspects/k3s/agent.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L3), [`modules/aspects/blocky.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/blocky.nix#L25)). Interpolation6 for a complete grade-A leaf above light-adaptation5, below explicit exported/consumer9. Confidence: medium.

### P (5, high)
Scope: Pros: x86 server and ARM Pi targets select distinct hardware owners ([`modules/hosts/hosts.nix:2`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L2), [`modules/hosts/hl-agent-00.nix:4`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-agent-00.nix#L4), [`modules/hosts/hl-server.nix:9`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-server.nix#L9)). Cons/limit: Pi filesystem label and networking assumptions remain manual scope ([`modules/hardware/rpi4.nix:21`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hardware/rpi4.nix#L21)), without dedicated platform-boundary fixtures. Literal5 honest narrow Linux support with manual exceptions, not a penalty for lacking Darwin. Confidence: high.

### L (2, high)
Scope: Pros: README explains physical layout and NixOS versus Flux responsibilities ([`README.md:5`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L5), [`README.md:38`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L38), [`README.md:46`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L46)). Cons: it is an operational overview with stale structure and no Den entry-to-feature route (§6a; [`README.md:15`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L15)). Literal operation-only2, not absent1. Confidence: high.

### V (5, medium)
Scope: Pros: CI evaluates the flake and validates Flux configuration; separate lint covers workflows/YAML ([`.github/workflows/test.yaml:26`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/test.yaml#L26), [`.github/workflows/test.yaml:43`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/test.yaml#L43), [`.github/workflows/lint.yaml:24`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/lint.yaml#L24), [`.github/workflows/lint.yaml:37`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/lint.yaml#L37)). Cons: no authored enabled/disabled or duplicate/missing Den contract fixtures in the entry ([`flake.nix:4`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/flake.nix#L4)). Literal5 representative output-validation intent with invocation; --no-build means no closure realization claim. Confidence: medium.

### O (5, medium)
Scope: Pros: selected WireGuard and k3s agent aspects own SOPS entries and consume deployed paths ([`modules/aspects/wireguard.nix:10`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L10), [`modules/aspects/wireguard.nix:32`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/wireguard.nix#L32), [`modules/aspects/k3s/agent.nix:10`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L10)); the SOPS owner imports the provisioning module ([`modules/aspects/sops.nix:11`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/sops.nix#L11)). Cons: key enrollment is a fixed manual file contract and bootstrap/deploy/builder inventory is not derived from Den ([`modules/aspects/sops.nix:16`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/sops.nix#L16)). Literal5 for one aspect-driven secrets concern; no credit for unrelated Flux operation. Confidence: medium.

### X (2, high)
Scope: Pros: Kubernetes responsibilities are explicit ([`README.md:46`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L46)). Cons: Flux manifests live beside Den and k3s is a NixOS service; the authored activation emits a literal HelmChartConfig, not a first-class Den manifest class ([`modules/aspects/k3s/server.nix:47`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L47), [`modules/defaults.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/defaults.nix#L3)). Baseline2, without treating Kubernetes presence as Den integration coverage. Confidence: high.

### B (2, medium)
Scope: Census: Zsh1 + Starship1 + installed-only Neovim.5 =2.5→diversity2. One complete reference→2; mean2. Pros: Starship owns a coherent display preset ([`modules/aspects/shell/starship.nix:8`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L8)). Cons: Blocky/WireGuard/k3s/SOPS carry fleet identity/dependencies, Zsh includes an external application aspect, and raw Neovim has only installation/default-editor aliases rather than a real preset ([`modules/aspects/blocky.nix:25`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/blocky.nix#L25), [`modules/aspects/shell/zsh.nix:4`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/zsh.nix#L4), [`modules/aspects/shell/nvim.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/nvim.nix#L6)). Package bundles and host profiles count zero. Confidence: medium.
```score-evidence
{"B": {"diversity_points": 2.5, "diversity_grade": 2, "reference_grade": 2, "reference_units": [{"name": "starship-preset", "evidence": "modules/aspects/shell/starship.nix:6"}]}}
```

Total: **34.5/100**. Shortlists: showcase no; library_units starship-preset; starter no. Notable for the independent small prompt preset, not cluster breadth.

Overall pros:
- Heterogeneous hardware and cluster roles are explicitly selected ([`modules/hosts/hl-agent-00.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hl-agent-00.nix#L3)).
- A complete Starship preset is independently owned ([`modules/aspects/shell/starship.nix:8`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L8)).
- Evaluation and Flux-validation commands are traceable to CI ([`.github/workflows/test.yaml:26`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/test.yaml#L26), [`.github/workflows/test.yaml:43`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/.github/workflows/test.yaml#L43)).

Overall cons / limits:
- Shared cluster roles embed the server address ([`modules/aspects/k3s/agent.nix:18`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/agent.nix#L18)).
- SOPS key location is operator-specific ([`modules/aspects/sops.nix:16`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/sops.nix#L16)).
- Duplicated storage/shutdown policy and stale docs increase change cost ([`modules/aspects/k3s/server.nix:18`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L18), [`README.md:15`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/README.md#L15)).

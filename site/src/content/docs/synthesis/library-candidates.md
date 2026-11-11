---
title: "Library candidate groups and resource inventories"
---

This doc is the raw input for a future harvest of aspects into a community library. It is for library contributors
and den maintainers. It groups the library candidates that the reviews nominate, names a preferred source for each
recurring problem, and lists the resources that each candidate owns. It introduces no new scores or reuse grades. It
complements the [adoption census](/census/summary/): the census counts what configs select, and this doc lists
reusable units and their contracts.

## Contents

- [About this document](#about-this-document)
  - [Sources](#sources)
  - [Grades and preferred sources](#grades-and-preferred-sources)
  - [Resource vocabulary](#resource-vocabulary)
  - [What recurrence means](#what-recurrence-means)
- [Preferred sources for recurring or cross-cutting groups](#preferred-sources-for-recurring-or-cross-cutting-groups)
- [Detailed catalog: resource mechanisms and fleet/app contracts](#detailed-catalog-resource-mechanisms-and-fleetapp-contracts)
  - [Resource requests and collectors](#resource-requests-and-collectors)
  - [Settings, classes and export adapters](#settings-classes-and-export-adapters)
  - [Checkout, linking and package discovery](#checkout-linking-and-package-discovery)
  - [Operations and builders](#operations-and-builders)
  - [Security, SSH and credentials](#security-ssh-and-credentials)
  - [Networking, synchronization and containers](#networking-synchronization-and-containers)
  - [Application and service envelopes](#application-and-service-envelopes)
  - [Desktop, audio, devices and platform adapters](#desktop-audio-devices-and-platform-adapters)
  - [Terminal, editor and preferences](#terminal-editor-and-preferences)
  - [Recurrence map and preferred source boundaries](#recurrence-map-and-preferred-source-boundaries)
  - [Coverage and unresolved contracts](#coverage-and-unresolved-contracts)
- [Detailed catalog: native applications, account/storage/device contracts](#detailed-catalog-native-applications-accountstoragedevice-contracts)
  - [Repeated application functions: environment loading](#repeated-application-functions-environment-loading)
  - [Repeated application functions: audio](#repeated-application-functions-audio)
  - [Repeated applications: Ghostty, terminals, prompts and editors](#repeated-applications-ghostty-terminals-prompts-and-editors)
  - [Accounts, privileged membership and authentication](#accounts-privileged-membership-and-authentication)
  - [SSH, intrusion prevention and key lifecycle](#ssh-intrusion-prevention-and-key-lifecycle)
  - [Storage layouts, persistence protocols and maintenance](#storage-layouts-persistence-protocols-and-maintenance)
  - [Power, devices and graphics](#power-devices-and-graphics)
  - [Theming, fonts and display contracts](#theming-fonts-and-display-contracts)
  - [Containers, native services and developer workstations](#containers-native-services-and-developer-workstations)
  - [VCS, search tools and document/media workflows](#vcs-search-tools-and-documentmedia-workflows)
  - [Generic class/schema/export adapters](#generic-classschemaexport-adapters)
  - [Preserved shortlist-only / conflicting-evidence appendix](#preserved-shortlist-only--conflicting-evidence-appendix)
- [Separate namespace-library prior art](#separate-namespace-library-prior-art)
  - [Best exemplar per application/resource family](#best-exemplar-per-applicationresource-family)
  - [Recurrence and broad owners retained](#recurrence-and-broad-owners-retained)
  - [Obvious config-shortlist comparisons](#obvious-config-shortlist-comparisons)
  - [How to group later work](#how-to-group-later-work)
- [Coverage and next harvest boundary](#coverage-and-next-harvest-boundary)

## About this document

### Sources

- **Nominations.** This doc consolidates the **93 repository nominations** in
  [the config shortlist](/ranking/#library-units) and their source-led reviews.
- **Namespace libraries.** It also uses the three [namespace library pilots](/method/library-pilot/). The three
  namespace libraries are separate prior art. They do not re-enter the config corpus counts.
- **Corpus.** The config corpus has 108 included repositories.
- **Revisions.** Each config page lists its review revision. Each source citation below is relative to its named
  repository.

### Grades and preferred sources

A **preferred source** is the best existing cited contract for the particular problem. It is not the
highest-scoring repository. Each candidate keeps its recorded grade:

| Grade | Meaning |
|---|---|
| **A** | drop-in at its stated interface |
| **B** | needs light parametrizing |
| **C** | idea only |

- Pilot completeness labels are kept as they are.
- An ungraded candidate is not silently promoted to A/B.
- All implementations will be rewritten, and ideas attributed.
- A published grade does not establish permission to copy code, successful evaluation, or compatibility with a
  future resource protocol.

### Resource vocabulary

The resource fields are **persist/state**, **secrets**, **ports/firewall**, **users/groups** and **services**.
Mutable files and activation/lifecycle are added where they are central.

- "Not inventoried" means that the existing review did not establish the payload. It does not mean that the unit
  needs no resources.
- Native modules can own resources indirectly.
- Platform and module prerequisites are part of a unit's contract.

### What recurrence means

- Recurrence lists include only reviewed nominations or explicit pilot units that solve the named problem.
- They are not popularity counts.
- They are not evidence that every listed implementation uses the same routing mechanism.
- Installation/selection counts belong in [the adoption census](/census/summary/).
- Include-only profiles, scaffolds, adapters and tools stay distinct from complete application presets.

## Preferred sources for recurring or cross-cutting groups

This index chooses one source at the stated boundary. It does not compare unlike apps by a new score. A baseline and
an extended integration can both be useful. The detailed catalogs list singleton applications and other distinct
primitives, each with its own source and grade. Related resource use is not reported as recurrence of the same app.
| Group / boundary | Preferred existing source | Recorded grade | Resource inventory / limit | Repos where it recurs or related boundaries |
|---|---|---|---|---|
| Persistence requests/collector | [tomwrw/megadots · modules/den/quirks.nix:31](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31) | A | system/home path requests; Impermanence mounts; retain expose policy and fixed-root adaptation | tomwrw/megadots; a config whose source is no longer public and a config whose source is no longer public provide different native class-forwarding adapters; see catalog |
| Secret collection | [sini/nix-config · modules/den/aspects/core/secrets/collector.nix:17](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/core/secrets/collector.nix#L17) | B in §4; summary A/B | agenix-rekey entries and collection; exact per-app payload remains to inventory | sini; soriPhoono Sops wiring and a config whose source is no longer public rekey defaults solve adjacent provisioning problems; Crocuda mail partial/ungraded |
| HTTP service facts | [byte-sized-emi/nix-config · modules/fleet.nix:3](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/fleet.nix#L3) | A | normalized host/service/URL/scheme/port facts, not service activation | byte-sized-emi, Keyruu proxy/monitor collection; zakuciael/nixpedition Traefik dynamic-config channel; payloads differ |
| Typed aspect settings | [Aor-Li/Infra · modules/meta/aspect-settings/default.nix:15](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/meta/aspect-settings/default.nix#L15) | A | typed host/user/home settings and lint/context injection, not inherent runtime resources | Aor-Li, sini, adda; retain adda no-native-reader caveat |
| Live checkout links | [Aor-Li/Infra · modules/aspects/default/home.nix:18](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L18) | B | HM workspace-relative files/symlinks; expose checkout fallback and identity | Aor-Li, auscyber file-local, amatos repo-dir |
| Standalone Syncthing service | [nazarewk-iac/nix-configs · modules/den/aspects/service-syncthing.nix:47](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/aspects/service-syncthing.nix#L47) | A | Linux HM user service, config/data and persistence lists | Nazarewk; tomwrw/megadots mesh additionally collects peers, secrets, firewall and persistence (B summary/R, A §4) |
| Fleet deploy projection | [theutz · modules/deploy.nix:18](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/deploy.nix#L18) | A §4; collective R wording B | deploy-rs nodes and root activation; host.deploy overrides | theutz; Sonntag Nixible is a playbook bridge, not the same activation protocol |
| Darwin Linux builder | [motheki/nix · modules/aspects/features/linux-builder.nix:3](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/aspects/features/linux-builder.nix#L3) | A | native Linux builder VM/service; exact user/port/state payload not inventoried | motheki; sini nix-builders is the B fleet-fact chain, not the same VM owner |
| SSH server hardening + key state | [henriquekirchheck/nixos-flake · modules/aspects/services/sshd.nix:2](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/aspects/services/sshd.nix#L2) | B | OpenSSH hardening, persisted host keys, allowed-user collector | henriquekirchheck, sk4rd; Crocuda ssh is ungraded candidate; native key lifecycle below is separate |
| SSH client + agent | [jkopano/nixiak · modules/services/ssh.nix:3](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L3) | A | client multiplexing/keepalive and agent; caller owns keys | jkopano; server presets and host-key generation are distinct contracts |
| Darwin SSH host keys | [scoiatael/dotfiles · modules/_darwin/modules/openssh-host-keys.nix:85](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/_darwin/modules/openssh-host-keys.nix#L85) | A | typed key paths/bits/comments and missing-key generation activation | scoiatael; Sini/Crocuda server presets do not establish identical key generation |
| Fail2ban | [vitalyavolyn/dotfiles · modules/services/fail2ban.nix:4](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/modules/services/fail2ban.nix#L4) | A | native banning service follows firewall enable; exact state not inventoried | vitalyavolyn; espdesign/nixos.den hardened-server adds trusted CIDR/SSH policy (B) |
| PipeWire baseline | [Steven-S1020/Nixos-Configuration · modules/system/audio.nix:2](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2) | A | RTKit, ALSA/32-bit, Pulse, JACK and WirePlumber service policy | Steven-S1020, Erastos, loystonpais, Shawn8901, Heromercer; Heromercer adds EasyEffects, Shawn adds realtime limits |
| Audio device naming/rules | [anders130/dotfiles · modules/hardware/audio.nix:2](https://github.com/anders130/dotfiles/blob/470c551356c8ccc92421f2d863cc0c15058df035/modules/hardware/audio.nix#L2) | B | typed per-device names/profiles/disable rules | anders130; complements five baseline audio nominations, not a sixth identical baseline |
| Bluetooth + A2DP audio stack | [auscyber/dotfiles · aspects/nixos/bluetooth.nix:7](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/nixos/bluetooth.nix#L7) | A | BlueZ roles, experimental mode, Blueman and PipeWire/RTKit integration | auscyber, Kykero, andreshungbz, Spebby nominate Bluetooth; smaller/device-specific scopes differ; Normal has pilot access preset |
| HM Direnv/Nix-direnv | [Draculestein/nixos-config · modules/aspects/cli/direnv.nix:5](https://github.com/Draculestein/nixos-config/blob/3514a1d2e512358af6d8357d389cfa9e11d49c2b/modules/aspects/cli/direnv.nix#L5) | A | conditional enabled-shell integration; state/secrets/ports not inventoried | Draculestein, Sharparam, voidlily, aullisia, Likivik; aullisia is NixOS-level; Sharparam/voidlily use direnv-instant |
| Ghostty preset | [aullisia/nixos-config · modules/programs/ghostty.nix:10](https://github.com/aullisia/nixos-config/blob/233eb5e4cfaf27a454f3b27b5a496c7f7eb2f1e8/modules/programs/ghostty.nix#L10) | A | app/config and owned fallback palette | aullisia, talarys; Syahrul is a nixGL wrapping adapter (B), not the same native contract |
| Starship prompt | [sini/nix-config · modules/den/aspects/applications/dev/shell/starship.nix:2](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/applications/dev/shell/starship.nix#L2) | A | prompt preset; exact state payload not inventoried | sini, clemak27, Heromercer; Crocuda Fish bundles prompt assets but remains partial/ungraded |
| NVF class evaluation | [JoonasKajava/nvf-config · modules/nvf-integration.nix:12](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12) | B | custom editor-module evaluation/package; ctx adaptation not implemented | Joonas; sini nvf is an HM module-contribution integration (B), retaining collector requirement |
| Current-user group primitive | [SuNNjek/nixos-config · modules/batteries/add-user-to-group.nix:7](https://github.com/SuNNjek/nixos-config/blob/f40297e9d045387227869245163e7e2b6c7799f9/modules/batteries/add-user-to-group.nix#L7) | A | current-user extraGroups from group argument | SuNNjek; quasigod A and oxce5 B provide configurable privileged group lists; account creation/Nix trust stay separate |
| Encrypted Btrfs layout | [jasperro/dotfiles · modules/system/encrypted-btrfs-filesystem.nix:19](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/system/encrypted-btrfs-filesystem.nix#L19) | B | typed devices, LUKS, subvolumes, initrd/mount lifecycle | jasperro; muhammadtalha ext4-simple is B Disko/GPT/ESP/swap, not the same filesystem contract |
| Podman engine/socket | [KGB33/homelab · nixos/services/podman.nix:2](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/services/podman.nix#L2) | A | native engine/Docker compatibility/socket policy; caller accepts access implications | KGB33, aveeryy B; Crocuda Docker/Podman membership is partial/ungraded; Colima/Incus are different engines |
| Font installation | [pdarulewski/dotfiles · modules/features/fonts.nix:2](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2) | A | cross-OS font packages; no secret/firewall/service inventory claimed | pdarulewski, lucasshiva B font-token/native install contract; Normal font schema/constructors do not install fonts |
| Mutable palette lifetime | [adanoelle/garden-shell · modules/aspects/palette.nix:6](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/palette.nix#L6) | A as adapter | seed-once writable palette; toolkit generated themes/manifest and reload; no app activation implied | Garden; Rafael Stylix B/quasigod Catppuccin B are distinct declarative theme contracts; Calibre/OmniWM share mutable-config concerns, not palette protocol |
| Substantial multi-resource service API | [FastTrackStudios/task · nix/nixos/task-server.nix:64](https://github.com/FastTrackStudios/task/blob/a40932117efadcace0179d510514d6470df318cd/nix/nixos/task-server.nix#L64) | A, native NixOS module | dataDir, optional EnvironmentFile, optional TCP9090, service user/group, hardened restart lifecycle | Task; XO, I2P, media appliance and Incus are different apps with analogous multi-resource inventories, not Task recurrence |
## Detailed catalog: resource mechanisms and fleet/app contracts

This catalog covers the nominations that route resources, settings, classes, checkouts and operations, and the
application envelopes that own several resources. Each row gives the existing grade, the exact clone evidence, the
resources in scope, and the adoption caveat. The [recurrence map](#recurrence-map-and-preferred-source-boundaries)
at the end compares the rows.
### Resource requests and collectors
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **age-secrets quirk+collector** — [sini/nix-config](/configs/sini/nix-config/) | B (§4); summary A/B | [modules/den/aspects/core/secrets/collector.nix:17](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/core/secrets/collector.nix#L17) @ `7e267a559e4a` | secrets: agenix-rekey entries/collection; persist/ports/users unknown | Retain emitters and collector; shallow last-wins dedup is documented. Summary A/B is not resolved here. |
| **persist quirk + impermanence consumer** — [tomwrw/megadots](/configs/tomwrw/megadots/) | A | [modules/den/quirks.nix:31](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L31) @ `09aae5c6af50` | persist: system/home paths; services: impermanence mounts | Consumer [modules/aspects/system/impermanence.nix:16](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/impermanence.nix#L16) and :68; retain expose policy and upstream input; /persist fixed. |
| **LAN firewall quirk** — [tomwrw/megadots](/configs/tomwrw/megadots/) | B (summary/R); §4 A | [modules/den/quirks.nix:52](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L52) @ `09aae5c6af50` | ports: TCP/UDP scoped to host.network.lanInterface | Consumer [modules/aspects/system/networking.nix:28](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/system/networking.nix#L28); explicit dedup and interface assertion. Laptop Wi-Fi boundary caveat; grade conflict retained. |
| **collect-service-facts** — [Keyruu/shinyflakes](/configs/keyruu/shinyflakes/) | B | [modules/policies/services-collect.nix:6](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/policies/services-collect.nix#L6) @ `021ee48343db` | resource records: dashboard/monitor/proxy/OIDC; no direct provisioning | Retain five quirk types, host collection and consumer policies; collector alone deploys nothing. Prometheus first-value semantics at [modules/aspects/server/monitoring/prometheus.nix:44](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/aspects/server/monitoring/prometheus.nix#L44) remain a caveat. |
| **fleet-http-services** — [byte-sized-emi/nix-config](/configs/byte-sized-emi/nix-config/) | A | [modules/fleet.nix:3](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/fleet.nix#L3) @ `8df6aa42d1bb` | HTTP service facts: host/service_name plus normalized scheme/port/URL; service activation unknown | Generic collector/normalizer; schema attachment :43. Downstream unchecked head consumers are not part of a safe cardinality contract. |
| **traefik dynamic-file quirk** — [zakuciael/nixpedition](/configs/zakuciael/nixpedition/) | A | [modules/services/traefik/default.nix:2](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/traefik/default.nix#L2) @ `b45ae683a1b2` | files: generated dynamic config; full owner also ports80/443, Sops env and service | Best treated as collector mechanism, not automatically closed app. Full owner reads config.sops.templates at :43 and OCI backend :42; preserve declared prerequisites. |
| **nix-ld aggregation** — [AnonymousRand/nix_config](/configs/anonymousrand/nix_config/) | B | [modules/batteries/nix-ld.nix:2](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/batteries/nix-ld.nix#L2) @ `583567f25d10` | user library requests→host nix-ld libraries; native service/resource impact otherwise unknown | Producer [modules/profiles/meow/batteries/nix-ld.nix:3](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/meow/batteries/nix-ld.nix#L3); route :7, native consumer :17. Document quirk value type; retain whole route. |
### Settings, classes and export adapters
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **host-aspect settings mirror recipe** — [sini/nix-config](/configs/sini/nix-config/) | B | [modules/den/schema/_settings-type.nix:41](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/schema/_settings-type.nix#L41) @ `7e267a559e4a` | typed settings/schema only; no inherent persist/secrets/ports/users/service | Read with docs/host-aspect-settings.md; extraction contract depends on aspect identity paths and surrounding injection machinery. |
| **aspect-settings** — [Aor-Li/Infra](/configs/aor-li/infra/) | A | [modules/meta/aspect-settings/default.nix:15](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/meta/aspect-settings/default.nix#L15) @ `87405e2c8b13` | typed host/user/home settings, validation and native context injection | Best documented settings source: includes _lib/tree.nix and _lib/lint.nix; minimal declaration/entity/consumer example :6; reserve settings and install policy. |
| **aspect-settings** — [Adda/nixos-config](/configs/adda/nixos-config/) | B | [modules/plumbing/den/aspect-settings.nix:12](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/aspect-settings.nix#L12) @ `31f3e4b1489f` | typed host/user settings declarations; no direct resources | Uses fx.keyClassification internals; review D card says no aspect reads host.settings. Retain nomination as incomplete mechanism evidence, not demonstrated settings adoption. |
| **home-platform classes** — [sini/nix-config](/configs/sini/nix-config/) | B | [modules/den/classes/home-platform.nix:3](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/classes/home-platform.nix#L3) @ `7e267a559e4a` | class/platform routing only; individual resources supplied by consumers | Normalize §4 classes/home-platform shorthand to full clone path; preserve platform context and forwarding contract. |
| **shell aliases/abbreviations classes** — [Adda/nixos-config](/configs/adda/nixos-config/) | A | [modules/plumbing/den/classes/aliases.nix:3](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/classes/aliases.nix#L3) @ `31f3e4b1489f` | shell alias/abbreviation config; no service/resource provisioning | Forwarders target HM aliases and Fish/Nushell/Zsh abbreviation options; globally installs forwards at :55. Retain all target prerequisites, not just declaration. |
| **editor quirk collectors** — [Adda/nixos-config](/configs/adda/nixos-config/) | A | [modules/plumbing/den/quirks/helix-settings.nix:2](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/plumbing/den/quirks/helix-settings.nix#L2) @ `31f3e4b1489f` | editor packages/settings/extensions contributions; app activation belongs to collectors | Helix consumer [modules/aspects/development/editors/helix.nix:192](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/aspects/development/editors/helix.nix#L192); Zed/VSCodium sibling collectors. A declaration file alone is not the complete nomination. |
| **activeAspects schema** — [Gwenodai/nixos](/configs/gwenodai/nixos/) | B | [modules/schema/activeAspects.nix:3](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/schema/activeAspects.nix#L3) @ `ab05d3c6e156` | entity aspect names/category groups; no direct runtime resources | Inputs entity/typeName/Den/lib; document traversal limits. Category consumers require this schema, so this is a helper contract, not a closed app. |
| **Disko class bridge** — [greysilly7/nixos-config](/configs/greysilly7/nixos-config/) | A | [modules/core/disko.nix:19](https://github.com/greysilly7/nixos-config/blob/955ea233631099163a21c8bd7b8290d2bf1f86f7/modules/core/disko.nix#L19) @ `955ea2336310` | disk configuration forwarded to NixOS; storage operations delegated to Disko | Retain declared input/schema/forward at :8/:14/:27/:35; caller supplies Disko config. No independent minimal consumer example. |
| **den-library-surface** — [nazarewk-iac/nix-configs](/configs/nazarewk-iac/nix-configs/) | A | [modules/den/lib.nix:478](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/lib.nix#L478) @ `a1a10f5c8272` | module selection/export/owned dependency closure; resources belong to chosen app | Explicit class/aspects/select/modules/extraInputs with unknown/empty-selection guards. Minimal adopter [modules/den/README.md:163](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/README.md#L163); no generic promise that every exported app is complete. |
| **terranix global/local routing** — [zakuciael/nixpedition](/configs/zakuciael/nixpedition/) | B | [modules/services/terranix/routing.nix:73](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/services/terranix/routing.nix#L73) @ `b45ae683a1b2` | Terraform module/output routing; cloud resources supplied by selected modules | Global instantiate :101; local native service forward with osConfig. Retain complete namespace/class/context envelope. |
| **clan instantiate/intoAttr override** — [zakuciael/nixpedition](/configs/zakuciael/nixpedition/) | B (summary only; absent §4) | [nix/den.nix:20](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/nix/den.nix#L20) @ `b45ae683a1b2` | Den host modules→clan.machines; no app resources of its own | Explicitly retains plain module instantiate :23 and intoAttr :24. Keep summary nomination but flag missing curated §4 contract. |
### Checkout, linking and package discovery
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **file-local** — [auscyber/dotfiles](/configs/auscyber/dotfiles/) | B | [aspects/base/file-local.nix:8](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/file-local.nix#L8) @ `96be028eaba6` | HM out-of-store files/symlinks; no service/persist provisioning demonstrated | Requires rootPath/user entity/optional flakeFolder. Standalone home identity and root membership validation incomplete (:12/:21). |
| **workspace-links** — [Aor-Li/Infra](/configs/aor-li/infra/) | B | [modules/aspects/default/home.nix:18](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L18) @ `87405e2c8b13` | workspace-relative files/symlinks, lib.owner; no direct daemon | Inputs self/lib/HM plus identity/repoRoot options; parameterize fallback checkout; documented repository-path precondition :13. |
| **repo-dir** — [amatos/magnanix](/configs/amatos/magnanix/) | B | [modules/den/repo-dir.nix:6](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/repo-dir.nix#L6) @ `7675475f0509` | HM live-checkout option for external links; resources beyond links unknown | Rename magnanix prefix and parameterize fallback directory :11; helper does not alone make dependent app modules closed. |
| **homelab overlay discovery** — [icebluerabbit/nixos](/configs/icebluerabbit/nixos/) | B | [modules/overlays.nix:11](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/overlays.nix#L11) @ `21a704b338c3` | package discovery under pkgs.homelab; no runtime resource ownership | Local package tree required; expose root/namespace. Do not present as a service or application preset. |
| **private-overlay stub** — [Adda/nixos-config](/configs/adda/nixos-config/) | A | [modules/flake/addax-private.nix:3](https://codeberg.org/Adda/nixos-config/src/commit/31f3e4b1489fcd0a6d66c4d612a2294225c8299a/modules/flake/addax-private.nix#L3) @ `31f3e4b1489f` | optional private module import with empty public replacement; runtime resources unknown | Explicit stub override :6 and template :7; actual private source unavailable, so this is dependency-boundary prior art, not evidence of private app closure. |
| **runtime-manifest** — [r17x/universe](/configs/r17x/universe/) | B | [nix/den/aspects/runtime.nix:3](https://github.com/r17x/universe/blob/f8bc64a503b4f09b8eb325d07a5e1b37e6a49cc7/nix/den/aspects/runtime.nix#L3) @ `f8bc64a503b4` | HM runtime theme manifest file; no ports/users/services demonstrated | Requires runtime quirk and colors namespace; parameterize output path/colors. Review notes implicit collision/missing-name semantics (:20). |
### Operations and builders
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **nix-builders pipe chain** — [sini/nix-config](/configs/sini/nix-config/) | B | [modules/den/aspects/roles/nix-builder.nix:40](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/roles/nix-builder.nix#L40) @ `7e267a559e4a` | builder peer facts, SSH keys/remote build settings | Consumer [modules/den/aspects/core/nix/remote-build-client.nix:9](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/core/nix/remote-build-client.nix#L9); fixed SSH user/port need extraction contract; port absent from record per §6a. |
| **deploy** — [~theutz/flake](/configs/theutz/flake/) | A (§4); R card calls units B | [modules/deploy.nix:18](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/deploy.nix#L18) @ `3ede31e7a4e9` | deploy-rs nodes/root activation; host.deploy overrides | Concrete route and native output; defaults :50/:51 require adaptation. Preserve grade disagreement; no minimal external consumer docs. |
| **homebrew quirks** — [~theutz/flake](/configs/theutz/flake/) | A | [modules/aspects/homebrew.nix:6](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/aspects/homebrew.nix#L6) @ `3ede31e7a4e9` | casks/brews/taps collection; package installation via nix-darwin | Declarations [modules/quirks/casks.nix:2](https://git.sr.ht/~theutz/flake/tree/3ede31e7a4e906e7bded05e46b209caaa12af3c5/item/modules/quirks/casks.nix#L2) and siblings. Same app functionality as package lists, distinct contribution mechanism; several owners bypass collection. |
| **nixible playbook bridge** — [sonntag/nix](/configs/sonntag/nix/) | B | [modules/nixible/playbooks.nix:42](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/nixible/playbooks.nix#L42) @ `816947c6a270` | enabled playbook/dependency/collection/target CLI projection; resource effects caller playbook-defined | Retain user class and entity-context projection. [scripts/nixctl:431](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/scripts/nixctl#L431) silently skips evaluation errors; not a proven fail-closed runner. |
| **linux-builder** — [motheki/nix](/configs/motheki/nix/) | A | [modules/aspects/features/linux-builder.nix:3](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/aspects/features/linux-builder.nix#L3) @ `e75e72ed08cc` | persistent ARM Linux builder VM/service on Darwin; native module owns detailed paths/ports/users | Focused opt-in owner; no author identity. Exact resource filenames/ports unknown from reviewed summary; verify native module contract before harvest. |
| **fstrim** — [DylanRJohnston/nixos](/configs/dylanrjohnston/nixos/) | B | [modules/fstrim.nix:5](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/fstrim.nix#L5) @ `505097f4d0fd` | periodic filesystem trim service/timer; native module owns schedule | Separate arc.base auto-inclusion :3 and register/rebind namespace. Tiny enable-only leaf; nomination retained, explicitly not substantive B_ref app. |
### Security, SSH and credentials
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **desktop.bitwarden** — [repparw/nix](/configs/repparw/nix/) | B | [modules/aspects/bitwarden.nix:16](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/aspects/bitwarden.nix#L16) @ `b2a680435a4e` | OS polkit/keyring + user background broker/service | Document manual unlock and separate browser-specific assumptions; complete preset evidence :24/:42, not a secrets-provisioning pipeline. |
| **secrets-guard** — [adanoelle/fern](/configs/adanoelle/fern/) | A | [modules/secrets-guard.nix:3](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/secrets-guard.nix#L3) @ `060cd42a3d02` | git-secrets/trufflehog packages and Git initialization-template files | Policy applies to newly initialized repositories (:13); this guards repositories, not host secret decryption/rekey. |
| **services.sshd** — [henriquekirchheck/nixos-flake](/configs/henriquekirchheck/nixos-flake/) | B | [modules/aspects/services/sshd.nix:2](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/aspects/services/sshd.nix#L2) @ `f9b5451633a4` | OpenSSH hardening, persisted host keys, user allowlist | Retain persist/allow-user collectors; key emitter :15, preservation consumer [modules/inputs/preservation.nix:81](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/inputs/preservation.nix#L81). No independent worked extraction example. |
| **openssh** — [sk4rd/mikos-den](/configs/sk4rd/mikos-den/) | B | [modules/features/openssh.nix:4](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/features/openssh.nix#L4) @ `de31f342886a` | key-only SSH service, no root login; native resource details unknown | Separate global host-schema self-inclusion :14 before opt-in use. |
| **sops wiring** — [soriPhoono/homelab](/configs/soriphoono/homelab/) | B | [modules/sops.nix:14](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/sops.nix#L14) @ `c6599b697b93` | OS/HM Sops imports and entity-derived secret files | Expose secret root/key policy; filename convention and host/home/user args are prerequisites, recipients/operator provisioning remain caller-owned. |
| **management CIDR guard** — [closure-labs/maestro](/configs/closure-labs/maestro/) | B | [modules/features/operator/access.nix:12](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/features/operator/access.nix#L12) @ `6d707f35e29b` | management CIDR validation + iptables/nftables access rules/assertions | Expose namespace and guarded ports; literals repeated at :25/:40/:48 do not follow a changed SSH listener automatically. |
### Networking, synchronization and containers
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **syncthing mesh pipe** — [tomwrw/megadots](/configs/tomwrw/megadots/) | B (summary/R); §4 A | [modules/den/quirks.nix:93](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L93) @ `09aae5c6af50` | peer records plus persisted sync/state, ports22000/21027, Sops key/cert/GUI credentials | Consumer [modules/aspects/apps/syncthing.nix:5](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/aspects/apps/syncthing.nix#L5). Retain pipe, schema syncthing.id and Sops/impermanence/firewall collectors. Formal-name/deadnix fragility documented. Grade conflict retained. |
| **service-syncthing** — [nazarewk-iac/nix-configs](/configs/nazarewk-iac/nix-configs/) | A | [modules/den/aspects/service-syncthing.nix:47](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/aspects/service-syncthing.nix#L47) @ `a1a10f5c8272` | Linux HM user service, XDG config/data and read-only persistence lists; no secrets/ports declared in this owner | Use supplied denLib.imports closure (:478), nullable GUI address :60; caller wires persistence outputs. This is standalone service behavior, not mesh discovery. |
| **vpn** — [hmajid2301/nixicle](/configs/hmajid2301/nixicle/) | A | [modules/aspects/services/vpn.nix:2](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/aspects/services/vpn.nix#L2) @ `ca0d927add73` | WireGuard support + Tailscale daemon; no embedded peers/auth | Small opt-in connectivity bundle; resource provisioning beyond native modules unknown. Not an authenticated VPN deployment recipe. |
| **podman** — [aveeryy/kadachi](/configs/aveeryy/kadachi/) | B | [aspects/adachi/services/podman.nix:3](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/adachi/services/podman.nix#L3) @ `ba03c6ede780` | Podman pruning, Docker socket compatibility, DNS, nftables-aware interface trust | Standard namespace rebind; native NixOS settings, no fleet schema required. Keep whole owner :11/:16. |
| **nixos-containers options layer** — [zakuciael/nixpedition](/configs/zakuciael/nixpedition/) | B | [modules/virtualisation/nixos-containers/default.nix:7](https://github.com/zakuciael/nixpedition/blob/b45ae683a1b29f465bb683d6b73974e167c2080f/modules/virtualisation/nixos-containers/default.nix#L7) @ `b45ae683a1b2` | container NAT/IPv6 and unmanaged veths; options/mapper requires sibling owners | Default file alone is only networking half. Retain entire modules/virtualisation/nixos-containers/ closure; detailed mapper lifecycle unknown from nomination. |
### Application and service envelopes
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **calibre** — [Occhima/nix-conf](/configs/occhima/nix-conf/) | A | [modules/home-manager/desktop/apps/calibre.nix:75](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/home-manager/desktop/apps/calibre.nix#L75) @ `201ebbb67074` | Calibre native app + mutable GUI config merger, owned Python helper/icon theme | Best source for atomic mutable-GUI overlay: typed modules.desktop.apps.calibre.gui and independent export; helper/asset closure :10/:47. Not the broken Poetry nomination. |
| **espanso-user-service** — [closure-labs/foundation](/configs/closure-labs/foundation/) | A | [modules/apps/espanso/_settings.nix:1](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/apps/espanso/_settings.nix#L1) @ `0715d5823b45` | store-owned executable, graphical-session user service, restart policy | Standard HM/pkgs, Wayland package explicit :9; do not infer whole Foundation app-descriptor graph is equally standalone. |
| **mish USB coordinator mode** — [closure-labs/mish](/configs/closure-labs/mish/) | A | [nix/den/outputs.nix:16](https://github.com/closure-labs/mish/blob/6587ee6dbb2fa81a0075d08c8a118f3032176645/nix/den/outputs.nix#L16) @ `6587ee6dbb2f` | Mish coordinator service, package overlay, optional USB radio access | Retain [nix/den/aspects.nix:21](https://github.com/closure-labs/mish/blob/6587ee6dbb2fa81a0075d08c8a118f3032176645/nix/den/aspects.nix#L21) and native service; caller stable device path/commissioning. Minimal independent consumer [docs/den-architecture.md:69](https://github.com/closure-labs/mish/blob/6587ee6dbb2fa81a0075d08c8a118f3032176645/docs/den-architecture.md#L69). |
| **Media appliance** — [soriPhoono/homelab](/configs/soriphoono/homelab/) | A | [modules/systems/nixos/aspects/hosting/media.nix:157](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/systems/nixos/aspects/hosting/media.nix#L157) @ `c6599b697b93` | typed media-root/GPU pair, dirs, containers and Sops secrets | Retain generic Docker/Microserver/Docktail label helpers (:3; [hosting/microserver.nix:10](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/systems/nixos/aspects/hosting/microserver.nix#L10)); no isolated minimal consumer guide. Whole appliance, not one app per container. |
| **xo-service-suite** — [closure-labs/maestro](/configs/closure-labs/maestro/) | A | [modules/features/xo/options.nix:15](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/features/xo/options.nix#L15) @ `6d707f35e29b` | Xen Orchestra package/user/group/state/TLS/storage/file-restore services | Complete service/options/storage/TLS/helper closure; service.nix:68, [storage.nix:29](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/features/xo/storage.nix#L29). Independent VM consumer [modules/ci/security/_tests/runtime-security.nix:18](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/ci/security/_tests/runtime-security.nix#L18). |
| **llama-cpp-darwin** — [auscyber/dotfiles](/configs/auscyber/dotfiles/) | B | [aspects/services/llama-cpp.nix:59](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/services/llama-cpp.nix#L59) @ `96be028eaba6` | typed model/alias/port/package, launchd activation/cache/logs | Darwin-only extraction :111. Linux :146 ignores package setting and lacks Install target; do not silently advertise same Linux lifecycle. |
| **Managed Flatpak/Flathub** — [lorenzorapetti/nix](/configs/lorenzorapetti/nix/) | A | [modules/desktop/flatpak.nix:2](https://github.com/lorenzorapetti/nix/blob/e6b3e716d30a98a32ee8e76bfafbee6828d40357/modules/desktop/flatpak.nix#L2) @ `e6b3e716d30a` | owns nix-flatpak import, Flathub registration, weekly updates | Input inputs.nix-flatpak required; native options allow variation (:4/:10/:16). No independent minimal app tutorial. |
### Desktop, audio, devices and platform adapters
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **bluetooth-a2dp-pipewire** — [auscyber/dotfiles](/configs/auscyber/dotfiles/) | A | [aspects/nixos/bluetooth.nix:7](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/nixos/bluetooth.nix#L7) @ `96be028eaba6` | BlueZ roles/experimental, Blueman, RTKit, PipeWire ALSA/Pulse/WirePlumber | Best source for complete Bluetooth/audio stack in this subset; no custom capability router. Real appliance caller [aspects/hosts/birdsarentreal.nix:77](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/hosts/birdsarentreal.nix#L77). |
| **desktop-bluetooth** — [Kykero/Nazunix](/configs/kykero/nazunix/) | A | [modules/desktop/bluetooth.nix:4](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4) @ `469bacd7b841` | BlueZ enable + power-on-boot; native service resources | Independent of Noctalia; small leaf, not evidence of richer audio ownership. |
| **bluetooth** — [andreshungbz/nixconfig](/configs/andreshungbz/nixconfig/) | B | [modules/aspects/desktop/components/nixos/bluetooth.nix:2](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/desktop/components/nixos/bluetooth.nix#L2) @ `bdee3f6ec030` | BlueZ enable + power-on-boot; native service resources | Register/rebind pkt namespace; small leaf retained as nominated, not a new substantive application count. |
| **audio** — [anders130/dotfiles](/configs/anders130/dotfiles/) | B | [modules/hardware/audio.nix:2](https://github.com/anders130/dotfiles/blob/470c551356c8ccc92421f2d863cc0c15058df035/modules/hardware/audio.nix#L2) @ `470c551356c8` | typed device naming/profile/disable rules + audio enablement | Best parameterized audio-device source; my.audio.devices grammar documented at :86, rule generation :71/:102. Paths/secrets/ports not established here. |
| **Kanata Darwin integration** — [sonntag/nix](/configs/sonntag/nix/) | B | [modules/services/kanata/default.nix:25](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/services/kanata/default.nix#L25) @ `816947c6a270` | driver/signed app/keyboard config, privileged+user launchd, diagnostics | Retain [pkgs/kanata-app.nix:17](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/pkgs/kanata-app.nix#L17) and [setup.m:168](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/pkgs/kanata-app/setup.m#L168)/assets; move den.default to opt-in aspect and expose config path :274. Not just a Kanata settings snippet. |
| **wsl variant** — [hoanhxlyn/andrewix](/configs/hoanhxlyn/andrewix/) | B | [modules/devices/wsl.nix:7](https://github.com/hoanhxlyn/andrewix/blob/bd9927ece041a42e81cd3aa5d22cf6e513b17206/modules/devices/wsl.nix#L7) @ `bd9927ece041` | NixOS-WSL module/default-user/PATH policy plus wsl-open BROWSER shim | Needs host.windows.root and core git/agents/editor/Sops/Stylix/shell/locale includes (:8). Explicitly fleet-composed variant, not closed native WSL leaf. |
| **mkHost monitors** — [hoanhxlyn/andrewix](/configs/hoanhxlyn/andrewix/) | B | [modules/_lib/mk-host.nix:11](https://github.com/hoanhxlyn/andrewix/blob/bd9927ece041a42e81cd3aa5d22cf6e513b17206/modules/_lib/mk-host.nix#L11) @ `bd9927ece041` | Niri output position configuration from monitor facts; no runtime service | Needs Niri/shared settings/typed host facts; preserve constructor envelope, no consumer example. |
| **amd-cpu** — [aveeryy/kadachi](/configs/aveeryy/kadachi/) | B | [aspects/megurine/has/amd-cpu.nix:3](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/megurine/has/amd-cpu.nix#L3) @ `ba03c6ede780` | firmware-sensitive microcode + optional kvm-amd provider | Rebind standard namespace; native firmware option :7; virtualization remains opt-in provider :10. Hardware preset, not an application. |
| **autofirma-firefox** — [aveeryy/kadachi](/configs/aveeryy/kadachi/) | B | [aspects/kasane/programs/autofirma.nix:12](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/aspects/kasane/programs/autofirma.nix#L12) @ `ba03c6ede780` | AutoFirma app + Firefox PKCS11/OpenSC profile integration | Retain autofirma-nix input and namespace/profile-name provider :18. Minimal actual caller [hosts/totsugeki/user.nix:26](https://github.com/aveeryy/kadachi/blob/ba03c6ede7801b46182399a78bbec1f041920e95/hosts/totsugeki/user.nix#L26). |
### Terminal, editor and preferences
| Existing nomination / source review | Existing grade | Exact clone evidence | Resources and scope | Adoption caveat |
|---|---|---|---|---|
| **terminal quirk** — [tomwrw/megadots](/configs/tomwrw/megadots/) | B | [modules/den/quirks.nix:84](https://github.com/tomwrw/megadots/blob/09aae5c6af50ecb9a2e8d0abccfac614ff712f93/modules/den/quirks.nix#L84) @ `09aae5c6af50` | terminal-command contribution for launchers; activation/resources belong to chosen terminal | Function-of-pkgs contract; declaration alone is not a terminal app. |
| **tmux** — [sini/nix-config](/configs/sini/nix-config/) | A | [modules/den/aspects/applications/dev/mux/tmux.nix:2](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/applications/dev/mux/tmux.nix#L2) @ `7e267a559e4a` | complete mux preset; standard persist quirk may need collector; exact paths unknown here | No fleet inputs according to §4/R; retain resource declarations rather than dropping standard collector dependency. |
| **starship** — [sini/nix-config](/configs/sini/nix-config/) | A | [modules/den/aspects/applications/dev/shell/starship.nix:2](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/applications/dev/shell/starship.nix#L2) @ `7e267a559e4a` | prompt preset; persist/secrets/ports/users/services unknown | Full clone path normalized from §4 shorthand; no fleet inputs claimed by review. |
| **zellij** — [sini/nix-config](/configs/sini/nix-config/) | A | [modules/den/aspects/applications/dev/mux/zellij/zellij.nix:9](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/applications/dev/mux/zellij/zellij.nix#L9) @ `7e267a559e4a` | mux preset; exact native/persist resources unknown here | Full owner path, not basename shorthand; no fleet inputs claimed by review. |
| **aerospace** — [sini/nix-config](/configs/sini/nix-config/) | A | [modules/den/aspects/macos/wm/aerospace.nix:5](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/macos/wm/aerospace.nix#L5) @ `7e267a559e4a` | Darwin window-manager app/service/settings; exact state paths unknown | No fleet inputs according to §4; ordinary Darwin target, not another integration class. |
| **nvf** — [sini/nix-config](/configs/sini/nix-config/) | B | [modules/den/aspects/applications/dev/editor/nvf.nix:3](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/applications/dev/editor/nvf.nix#L3) @ `7e267a559e4a` | NVF app module + homeManagerModules resource contribution | Retain HM-module collector [modules/den/aspects/core/users/home-manager/home-manager.nix:67](https://github.com/sini/nix-config/blob/7e267a559e4a93f6f83d2f9e96f47b75b227a88c/modules/den/aspects/core/users/home-manager/home-manager.nix#L67); selected slab route misses collector per §6a. Helper/collector coupling is material. |
| **tuios-home-module** — [hmajid2301/nixicle](/configs/hmajid2301/nixicle/) | A | [modules/aspects/cli/multiplexers/tuios/_home-manager.nix:20](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/aspects/cli/multiplexers/tuios/_home-manager.nix#L20) @ `ca0d927add73` | typed package/settings, guarded Fish/Pi/Claude integrations; disabled by default | Independent export default.nix:4, minimal disabled/configured consumer [_tests.nix:3](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/aspects/cli/multiplexers/tuios/_tests.nix#L3). Tests are not wired into exported checks; presence is not passing evidence. |
| **Firefox privacy/search preset** — [jadestar1864/nix-config](/configs/jadestar1864/nix-config/) | B | [modules/web-browsers/firefox.nix:15](https://github.com/jadestar1864/nix-config/blob/1e0fcc909f4f8ac2e762111b7c413ec201c8dd70/modules/web-browsers/firefox.nix#L15) @ `1e0fcc909f4f` | HM browser activation, policies/search/NUR add-ons; optional Plasma integration | Rename pc address, retain NUR/Den input projection and optional Plasma companion. No personal network schema, but prerequisites must travel with unit. |
| **app-preferences** — [raphaelladinig/dotfiles](/configs/raphaelladinig/dotfiles/) | B | [modules/app-preferences.nix:3](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/app-preferences.nix#L3) @ `f29658d31d04` | typed macOS preference activation, running-app guard and warning helper | Retain [modules/_lib/app-preferences-warning.nix:1](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/_lib/app-preferences-warning.nix#L1); document primaryUser. Preference constructor is not an app installer. |
### Recurrence map and preferred source boundaries

Each row names a family, the repos that share its functionality, and the preferred source and its boundaries.

| Family | Who shares it | Preferred source and boundaries |
|---|---|---|
| **Persistence/resource requests** | Functional persistence recurs in tomwrw/megadots, henriquekirchheck and the standard collector-dependent Sini leaves. | Prefer tomwrw/megadots' explicit system/home persist producer+collector boundary as prior art. Sini age-secrets is the secrets counterpart, not the same resource. Similar mechanisms: AnonymousRand user→host nix-ld requests, Keyruu service-fact collection, byte HTTP normalization. Do not merge their record shapes without a designed protocol. |
| **Service discovery/proxy facts** | Keyruu, byte-sized-emi and zakuciael/nixpedition recur functionally around service metadata/proxy/monitoring. | The best compact normalization owner is byte modules/fleet.nix:3. The best broader consumer set is Keyruu [services-collect.nix:6](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/policies/services-collect.nix#L6). A host-info aspect in a config whose source is no longer public is SSH identity/address discovery: it shares cross-host collection mechanics, but has a different payload and fork dependencies. All retain the source-noted collision/cardinality limits. |
| **Settings/schema** | Aor, Sini and adda share the settings-mirror mechanism, not identical application functionality. | Prefer Aor's declared three-file closure and minimal example. Keep adda's no-live-reader caveat and Sini's aspect-identity dependency. Gwen activeAspects is introspection, not a settings replacement. |
| **Class adapters** | Sini home-platform, adda shell/editor classes, greysilly Disko, zakuciael/nixpedition Terranix/Clan and a config whose source is no longer public route factories recur mechanically. | They target different native systems and resources. The best closed Disko owner is greysilly's whole declared file. Nazarewk's tested export surface is the stronger generic consumer-boundary reference. It is not a substitute for each adapter's semantics. |
| **Live checkout links** | auscyber file-local, Aor workspace-links and amatos repo-dir share functionality. | Aor documents a repository-path precondition. auscyber still needs path-membership and standalone-home handling. amatos is the smallest option adapter. Ice overlay discovery and adda private stub recur only in dependency/discovery mechanics, not in live file-link behavior. |
| **SSH/network access** | henriquekirchheck services.sshd and sk4rd openssh share SSH-server functionality. | Prefer henriquekirchheck when you harvest hardening plus the key-persistence/allow-user resource inventory. sk4rd is a small security preset that requires removal of auto-inclusion. A WireGuard aspect in a config whose source is no longer public and hmajid vpn share connectivity functionality only loosely: one needs fork settings/peers, and the latter is an opt-in support/daemon bundle without authentication material. |
| **Syncthing** | tomwrw/megadots and Nazarewk share file-sync functionality. | Prefer Nazarewk for a supplied standalone Linux HM export. Prefer tomwrw/megadots for peer discovery, secrets, ports and persistence mechanism evidence. Their different adoption envelopes must remain visible. |
| **Bluetooth/audio** | auscyber, Kykero and andresh share Bluetooth functionality. | Only auscyber's nomination owns the complete A2DP/PipeWire stack. Anders130 is complementary typed device-policy/rule generation, not a duplicate of enablement. Kanata, AMD CPU and monitor constructors are distinct device resources, not audio recurrence. |
| **App/imperative lifecycle** | Calibre's atomic mutable-config merger, Espanso's graphical-session service, Mish USB commissioning and XO storage/TLS lifecycle. | These are distinct applications with reusable lifecycle ideas. They share explicit owned-resource boundaries, not interchangeable apps. The media appliance remains one coherent multi-container envelope. |
| **Desktop app presets** | Sini tmux/Zellij and hmajid TUIOS share terminal-multiplexer functionality, with different native contracts. | Sini Starship is a prompt, AeroSpace a WM, NVF an editor. Firefox/NVF/native app-preferences recur only mechanically, as native configuration/extension/preference owners. Retain NVF's missing-collector platform caveat. |
| **Operations** | Sini nix-builders and motheki linux-builder share builder functionality. Theutz deploy and Sonntag Nixible share operational target projection. | Sini routes fleet peer facts. motheki owns a Darwin Linux-builder service. Theutz deploys NixOS activation, and Sonntag deploys imperative playbooks. Theutz Homebrew is package-contribution collection. Dylan fstrim is maintenance. Neither has a recurrence claim to builders/deploy. |

### Coverage and unresolved contracts

- **Shortlist.** Every one of the 38 assigned shortlist repos is retained. Only shortlisted nominations are included.
  There is no expansion to all B_ref applications.
- **Grade disagreements** stay explicit: Sini age-secrets summary A/B versus §4 B; tomwrw/megadots LAN firewall and
  Syncthing §4 A versus summary/R B; theutz deploy §4 A versus R's collective B wording. No new grade resolves these
  conflicts.
- **Summary-only nominations** are retained and flagged: zakuciael/nixpedition Clan override; a config whose source is no
  longer public WireGuard, Vaultwarden, wake pair and host-info/SSH. These lack the same curated §4 contract as their
  summary names. Vaultwarden's locator exists at the manifest revision, but its independent closure remains
  unresolved.
- **Helper cautions.** adda settings has no verified native reader. Declarations alone do not provide editor/terminal
  activation. file-local lacks standalone-home/path containment handling. Sini NVF requires its actual HM module
  collector. Standard resource collectors are legitimate dependencies. Fleet-specific schema/fork dependencies remain
  separate.
- **Method.** No cloning, Nix evaluation, repository code, builds or runtime services were run. This document only summarises existing reviews.

## Detailed catalog: native applications, account/storage/device contracts

This catalog covers application presets and native account, storage, device and display contracts. Each subsection
opens with the best source and the recurrence boundary. Then a table lists every nomination. The last column is a
resource vector:

| Code | Meaning |
|---|---|
| **P** | state/mutable/persisted paths |
| **S** | credentials/secret handling |
| **F** | listeners/firewall |
| **U** | users/access |
| **V** | services/activation |
| **?** | not inventoried, never absence |

P alone does not prove persistence. S identity settings alone do not prove secret storage or provisioning.

### Repeated application functions: environment loading

- **Best general HM source:** Draculestein's **direnv-shell-integration (A)**. Its complete native body conditionally
  integrates enabled Bash/Zsh, without the editor policy found in Likivik.
- Five nominated repos share Direnv/Nix-direnv functionality.
- Sharparam/voidlily share the additional direnv-instant mechanism.
- aullisia is NixOS-level, not the same HM adapter.
- There is no evidence that all five share implementation provenance.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **direnv-shell-integration** | A | [Draculestein/nixos-config](/configs/draculestein/nixos-config/) | [`Draculestein/nixos-config:modules/aspects/cli/direnv.nix:5`](https://github.com/Draculestein/nixos-config/blob/3514a1d2e512358af6d8357d389cfa9e11d49c2b/modules/aspects/cli/direnv.nix#L5) | HM/Den/nixpkgs; retain native module; conditional enabled-shell hooks. | P=? S=? F=? U=? V=HM shell initialization. |
| **direnv-instant** | B | [Sharparam/nix-config](/configs/sharparam/nix-config/) | [`Sharparam/nix-config:modules/base/direnv.nix:11`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L11) | direnv-instant import, HM, Lix nix-direnv and Mise/dotenv policy; extract from base, expose preferences. | P=? S=dotenv loading (not secret provisioning) F=? U=? V=HM shell integration. |
| **direnv** | B | [voidlily/dotfiles](/configs/voidlily/dotfiles/) | [`voidlily/dotfiles:modules/direnv.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L15) | Bundle default module import at line11 with opt-in aspect; direnv-instant + nix-direnv. | P=? S=? F=? U=? V=HM environment/shell integration. |
| **direnv** | A | [aullisia/nixos-config](/configs/aullisia/nixos-config/) | [`aullisia/nixos-config:modules/shell/direnv.nix:6`](https://github.com/aullisia/nixos-config/blob/233eb5e4cfaf27a454f3b27b5a496c7f7eb2f1e8/modules/shell/direnv.nix#L6) | NixOS/nixpkgs; native packages/options own activation, no external assets. | P=? S=? F=? U=? V=NixOS shell integration. |
| **direnv** | B | [Likivik/spectacle](/configs/likivik/spectacle/) | [`Likivik/spectacle:modules/aspects/dev/direnv.nix:3`](https://github.com/Likivik/spectacle/blob/ce6d767b84e901fd044ac0693c21646cb739120c/modules/aspects/dev/direnv.nix#L3) | Four shell integrations; separate VSCodium/editor policy and provision chosen OS EDITOR; this coupling is explicitly in §6a. | P=? S=? F=? U=? V=HM/shell integration. |
### Repeated application functions: audio

- **Best small all-protocol source:** Heromercer **audio (A)**. It owns PipeWire ALSA/Pulse/JACK, RTKit and
  EasyEffects.
- Five nominations share PipeWire service integration: loystonpais, Shawn8901, Steven-S1020, Erastos, Heromercer.
- Their native service mechanism is broadly the same. Exact options/tools differ.
- Recursivepaws VST discovery solves a separate plugin-discovery problem. It must not inflate that five-repo count.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **audio** | A | [Heromercer/nixfiles](/configs/heromercer/nixfiles/) | [`Heromercer/nixfiles:modules/features/audio.nix:12`](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/features/audio.nix#L12) | NixOS/nixpkgs; native audio stack plus EasyEffects client. | P=? S=? F=? U=? V=PipeWire/RTKit. |
| **audio** | B | [loystonpais/lunar](/configs/loystonpais/lunar/) | [`loystonpais/lunar:modules/lunar/audio.nix:2`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/lunar/audio.nix#L2) | Lift lunar namespace; separate optional controls from ALSA/Pulse/JACK core. | P=? S=? F=? U=? V=PipeWire/audio controls. Unrelated global type errors in review are not charged to this unit. |
| **desktop.audio** | B | [Shawn8901/nixos-configuration](/configs/shawn8901/nixos-configuration/) | [`Shawn8901/nixos-configuration:modules/aspects/cfg/desktop/audio.nix:2`](https://github.com/Shawn8901/nixos-configuration/blob/890a465d7eb34855c4f34a0f82191fdab41041b6/modules/aspects/cfg/desktop/audio.nix#L2) | Lift cfg namespace; expose realtime users-group limits (line15). | P=? S=? F=? U=users realtime limits V=PipeWire/Pulse/ALSA. |
| **system/audio** | A | [Steven-S1020/Nixos-Configuration](/configs/steven-s1020/nixos-configuration/) | [`Steven-S1020/Nixos-Configuration:modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2) | NixOS/nixpkgs; namespace lifting only. | P=? S=? F=? U=? V=PipeWire/ALSA/Pulse/JACK/RTKit. |
| **audio** | B | [Erastos/nixos-dotfiles](/configs/erastos/nixos-dotfiles/) | [`Erastos/nixos-dotfiles:parts/aspects/features/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L2) | Retain or inline owned native [modules/system/audio.nix:2](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L2); NixOS only. | P=? S=? F=? U=? V=PipeWire/Pulse-compatible service policy. |
| **Native VST discovery** | A | [recursivepaws/nix](/configs/recursivepaws/nix/) | [`recursivepaws/nix:modules/aspects/audio/native-vst-plugins.nix:3`](https://github.com/recursivepaws/nix/blob/c4317eb95fad0ffcb7b5ce2056e83b82f046920a/modules/aspects/audio/native-vst-plugins.nix#L3) | Own native plugin packages, discovery env and profile links (lines13/50/62); ordinary Linux HM. | P=? (profile links are derived config) S=? F=? U=? V=profile/plugin discovery, no daemon claimed. |
### Repeated applications: Ghostty, terminals, prompts and editors

- **Best closed Ghostty preset:** aullisia **ghostty (A)**, because it owns a fallback palette.
- Three repos nominate Ghostty-related work: aullisia/talarys native terminal presets and Syahrul nixGL wrapping.
- That is repeated app functionality, not one shared mechanism. The nixGL adapter deliberately needs a graphics
  overlay/external config.
- For Starship, clemak27 and Heromercer are two independent complete prompt nominations. Neither is evidence of
  resource routing.
- The editor units below have different targets/contracts.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **ghostty** | A | [aullisia/nixos-config](/configs/aullisia/nixos-config/) | [`aullisia/nixos-config:modules/programs/ghostty.nix:10`](https://github.com/aullisia/nixos-config/blob/233eb5e4cfaf27a454f3b27b5a496c7f7eb2f1e8/modules/programs/ghostty.nix#L10) | HM/nixpkgs; optional Stylix colors with owned fallback (line31); native settings. | P=? S=? F=? U=? V=HM config/package. |
| **ghostty** | B | [talarys/den](/configs/talarys/den/) | [`talarys/den:modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2) | Lift apps namespace; expose font/theme choices and retain split/navigation bindings. | P=? S=? F=? U=? V=HM config/package. |
| **ghostty-nixgl** | B | [SyahrulBhudiF/dotfiles](/configs/syahrulbhudif/dotfiles/) | [`SyahrulBhudiF/dotfiles:modules/terminal.nix:3`](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/terminal.nix#L3) | Extract from broad aspect, expose config source; supply nixGLMesa overlay ([modules/den.nix:20](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/den.nix#L20)). | P=? S=? F=? U=? V=nixGL-wrapped executable/config link. |
| **kitty shell option (B)** | B | [lucasshiva/nixconfig](/configs/lucasshiva/nixconfig/) | [`lucasshiva:modules/features/apps/kitty.nix:14`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/apps/kitty.nix#L14) | Native optional shell package, theme/font and shell integrations; lift shiv namespace. This nomination is absent from §4 but explicitly graded B in R/shortlist cards. | P=? S=? F=? U=? V=HM package/config/shell integration. |
| **starship-preset** | A | [clemak27/homelab](/configs/clemak27/homelab/) | [`clemak27/homelab:modules/aspects/shell/starship.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L6) | Identity-free NixOS prompt settings; native overrides; no extra helpers/assets. | P=? S=? F=? U=? V=NixOS shell prompt integration. |
| **starship** | A | [Heromercer/nixfiles](/configs/heromercer/nixfiles/) | [`Heromercer/nixfiles:modules/features/starship.nix:4`](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/features/starship.nix#L4) | HM/Fish prompt format, directory/OS presentation; no external asset. | P=? S=? F=? U=? V=Fish prompt integration. |
| **helix** | A | [aullisia/nixos-config](/configs/aullisia/nixos-config/) | [`aullisia/nixos-config:modules/programs/helix.nix:9`](https://github.com/aullisia/nixos-config/blob/233eb5e4cfaf27a454f3b27b5a496c7f7eb2f1e8/modules/programs/helix.nix#L9) | HM/nixpkgs; owned optional theme fallback and Nix LSP/formatter (lines44/57). | P=? S=? F=? U=? V=HM editor/config/tool installation. |
| **nvf-integration** | B | [JoonasKajava/nvf-config](/configs/joonaskajava/nvf-config/) | [`JoonasKajava/nvf-config:modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12) | Den/NVF/lib/pkgs; retain mapModule adapter; args pkgs/vimAspect/ctx. ctx is currently unused except commented proposed hook (line50), so do not promise context adaptation. | P=? S=? F=? U=? V=class→evaluated editor package, not a service. |
| **OmniWM writable preset** | B | [derangga/dotfiles](/configs/derangga/dotfiles/) | [`derangga/dotfiles:modules/omniwm/default.nix:13`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/modules/omniwm/default.nix#L13) | HM with OmniWM support; retain settings.nix and shell.nix (lines20/32); expose workspace/monitor policy. | P=writable main/shell TOML S=? F=? U=? V=activation creates writable native configuration. |
| **Fish shell handoff** | B | [jmartindf/dendritic](/configs/jmartindf/dendritic/) | [`jmartindf/dendritic:modules/desertflood/den/cli/fish.nix:3`](https://github.com/jmartindf/dendritic/blob/db88ba8d4a1081f7bcd3be81037c54d007298bbf/modules/desertflood/den/cli/fish.nix#L3) | Den0.8 context helpers/lib/pkgs/local df namespace; retain OS/HM closure; no fleet schema. | P=? S=? F=? U=login-shell behavior V=Bash→Fish handoff across NixOS/Darwin + HM enable (lines35/92). |
| **fish** | A | [klchen0112/dotfiles](/configs/klchen0112/dotfiles/) | [`klchen0112/dotfiles:modules/shell/fish/default.nix:13`](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/shell/fish/default.nix#L13) | HM lib/pkgs; owner supplies plugins/Tide/macchina (lines9/15), activation configures Tide (line42). | P=? S=? F=? U=? V=Fish/Tide activation. Different mechanism from jmartindf login handoff. |
### Accounts, privileged membership and authentication

The recurring problem is contextual account/access policy. But these mechanisms are not interchangeable: group
enrollment, primary-user selection, account creation and Nix trust have distinct semantics.

- **Best minimal current-user group primitive:** SuNNjek **add-user-to-group (A)**.
- **Best explicitly configured privileged-group list:** quasigod **privileged-user battery (A)**.
- Keep primary-status selection separate from implicit privilege. rhedgeco already calls out that adaptation.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **add-user-to-group** | A | [SuNNjek/nixos-config](/configs/sunnjek/nixos-config/) | [`SuNNjek/nixos-config:modules/batteries/add-user-to-group.nix:7`](https://github.com/SuNNjek/nixos-config/blob/f40297e9d045387227869245163e7e2b6c7799f9/modules/batteries/add-user-to-group.nix#L7) | Den/NixOS; group argument plus current-user scope. | P=? S=? F=? U=extraGroups membership V=? |
| **privileged-user** | B | [oxce5/chimera](/configs/oxce5/chimera/) | [`oxce5/chimera:modules/groups.nix:2`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/groups.nix#L2) | Lift namespace; configurable users.privilegedGroups plus user arg; document group ownership. | P=? S=? F=? U=current-user configured groups V=? |
| **privileged-user battery (A)** | A | [quasigod.xyz/nixconfig](/configs/quasigodxyz/nixconfig/) | `quasigod-xyz-nixconfig:modules/groups.nix:3` | Typed users.privilegedGroups default[] drives user.userName extraGroups; standard namespace rebind. | P=? S=? F=? U=current-user group membership V=? |
| **schema-primary** | B | [rhedgeco/nix-config](/configs/rhedgeco/nix-config/) | [`rhedgeco/nix-config:modules/utils/primary.nix:8`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/utils/primary.nix#L8) | Typed user.primary and trusted-user membership; split trust policy from primary status. | P=? S=? F=? U=primary/trusted-user policy V=? |
| **nix-trusted-user** | A | [drupol/infra](/configs/drupol/infra/) | [`drupol:modules/users/nix-trusted-user.nix:2`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/users/nix-trusted-user.nix#L2) | Current user.userName only; native Nix trusted-users policy. | P=? S=? F=? U=Nix trust V=? |
| **fingerprint** | A | [Shochraos/nixfiles](/configs/shochraos/nixfiles/) | [`Shochraos/nixfiles:modules/features/fingerprint.nix:2`](https://github.com/Shochraos/nixfiles/blob/4d7c551873771cfd65ed440b8f97f3401f504551/modules/features/fingerprint.nix#L2) | fprintd with intentional password-only login/greetd PAM exclusions; standard NixOS. | P=? S=? F=? U=PAM authentication policy V=fprintd. |
| **1password-shell-integration** | B | [acrobertson/infra](/configs/acrobertson/infra/) | [`acrobertson/infra:modules/features/authentication.nix:5`](https://github.com/acrobertson/infra/blob/05a8582100fb93d1de94b5119cc5dddc86f4ba45/modules/features/authentication.nix#L5) | Own Darwin GUI + CLI/gh shell-plugin module; retain input/unfree policy; isolate sudo TouchID and expose plugins (lines12/24). | P=? S=1Password credential mediation F=? U=TouchID/sudo policy coupled V=GUI/CLI shell wrapper integration. Exact pinned upstream closure is cited in review. |
| **gpg** | B | [elianiva/dotfiles](/configs/elianiva/dotfiles/) | [`elianiva/dotfiles:modules/aspects/gpg.nix:34`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/aspects/gpg.nix#L34) | HM/Den/nixpkgs; OS-specific pinentry and pass/agent/cache; document key provisioning, no personal key asset. | P=? S=consumer-provisioned GPG keys/pass F=? U=? V=GPG agent/pinentry. |
### SSH, intrusion prevention and key lifecycle

- **Best agent/client preset:** jkopano **OpenSSH client/agent (A)**.
- **Best Darwin host-key lifecycle:** scoiatael **openssh-host-keys (A)**.
- Shared "SSH" functionality does not establish one common mechanism. Key generation/sshd config and client
  multiplexing are distinct.
- Fail2ban and espdesign/nixos.den hardening share SSH defense functionality (two nominees), with different
  settings/adaptation.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **OpenSSH client/agent** | A | [jkopano/nixiak](/configs/jkopano/nixiak/) | [`jkopano/nixiak:modules/services/ssh.nix:3`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/services/ssh.nix#L3) | Ordinary HM/Den; client keepalive/multiplexing plus agent (lines6/9); no identity. | P=? S=agent manages caller keys F=? U=? V=SSH agent/client. |
| **openssh-host-keys** | A | [scoiatael/dotfiles](/configs/scoiatael/dotfiles/) | [`scoiatael/dotfiles:modules/_darwin/modules/openssh-host-keys.nix:85`](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/_darwin/modules/openssh-host-keys.nix#L85) | Standalone nix-darwin module; typed hostKeys type/path/bits/comment (line11); activation generates missing keys (line113). | P=host-key paths S=private host keys F=? U=? V=activation/sshd configuration. |
| **fail2ban** | A | [vitalyavolyn/dotfiles](/configs/vitalyavolyn/dotfiles/) | [`vitalyavolyn/dotfiles:modules/services/fail2ban.nix:4`](https://github.com/vitalyavolyn/dotfiles/blob/4fbe31ccb7bb6f48ddef19b90b4069cab3fb3567/modules/services/fail2ban.nix#L4) | Native config/lib; mkDefault follows firewall enable state (line5), no identity/secret. | P=? S=? F=firewall-dependent banning U=? V=Fail2ban. |
| **hardened-server (B)** | B | [espdesign/nixos.den](/configs/espdesign/nixosden/) | [`nixos.den:modules/hardened-server.nix:7`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/hardened-server.nix#L7) | Native fail2ban sshd jail/server hardening; adapt trusted LAN CIDRs (lines11–13). | P=? S=? F=trusted CIDRs/ban policy U=? V=Fail2ban/SSH hardening. |
### Storage layouts, persistence protocols and maintenance

- **Best closed layout contract among these nominations:** jasperro **encrypted BTRFS filesystem (B)**. It owns
  typed schema/policy/guards. Its supplied device paths are actual consumer settings.
- muhammadtalha's ext4 layout requires the host.disko schema instead. The two share provisioning functionality, but
  not the filesystem/contract.
- A Preservation forward in a config whose source is no longer public, and a config whose source is no longer public's Impermanence forwards, share the class→native-persistence adaptation pattern.
  But they target different native modules and guarded paths.
- Neither is proof of a frozen standard resource protocol.
- Preserve grade conflicts. Do not silently upgrade them.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **encrypted BTRFS filesystem** | B | [jasperro/dotfiles](/configs/jasperro/dotfiles/) | [`jasperro/dotfiles:modules/system/encrypted-btrfs-filesystem.nix:19`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/system/encrypted-btrfs-filesystem.nix#L19) | Retain own schema/policy; namespace register/rename; caller supplies real partition paths (lines89/99). | P=guarded Btrfs subvolumes/initrd/LUKS S=LUKS provisioning prerequisite F=? U=? V=boot/mount lifecycle. |
| **disko.ext4-simple** | B | [muhammadtalha-quant/denix](/configs/muhammadtalha-quant/denix/) | [`muhammadtalha-quant/denix:modules/disko/ext4-simple.nix:2`](https://github.com/muhammadtalha-quant/denix/blob/70e67b484b5efe04a60d9982e41c3a66eeb0135c/modules/disko/ext4-simple.nix#L2) | Disko/NixOS + host.disko schema; package schema and expose ESP size. | P=GPT ESP/swap/ext4 root S=? F=? U=? V=partition/install. |
| **btrfs-scrub** | A | [klchen0112/dotfiles](/configs/klchen0112/dotfiles/) | [`klchen0112/dotfiles:modules/btrfs.nix:2`](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/btrfs.nix#L2) | Self-contained native weekly scrub policy. | P=filesystem integrity operation, not a persistence declaration S=? F=? U=? V=scheduled Btrfs scrub. |
| **nix-maintenance** | A | [arichtman/nix](/configs/arichtman/nix/) | [`arichtman/nix:modules/den/aspects/nixOptimizations.nix:5`](https://github.com/arichtman/nix/blob/a33136e4580dd700bdf822e7a7314b475fbd0f11/modules/den/aspects/nixOptimizations.nix#L5) | Daemon/GC/optimisation/restart/user-generation pruning (line35); expose retention/schedule. | P=Nix store/generation cleanup S=? F=? U=user-generation policy V=scheduled maintenance/restart. |
### Power, devices and graphics

- **Best AMD unit:** eldios **AMD GPU integration (A)**.
- **Best NVIDIA unit:** espdesign/nixos.den **nvidia (A)**.
- These repeat graphics-driver ownership, but they are not the same app or mechanism.
- Power facts (UPower), suspend-then-hibernate and Plex sleep inhibition also solve different resource questions.
  Group them for harvest, but do not claim three occurrences of a single battery.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **AMD GPU integration** | A | [eldios/dotfiles](/configs/eldios/dotfiles/) | [`eldios/dotfiles:modules/aspects/hardware/gpu-amd.nix:4`](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/hardware/gpu-amd.nix#L4) | Declared nixos-hardware input + native driver/compute tools/home VA/VDPAU settings; compatible AMD Linux host. | P=? S=? F=? U=? V=driver initrd/LACT native service. |
| **nvidia (A)** | A (shortlist/R; absent §4) | [espdesign/nixos.den](/configs/espdesign/nixosden/) | [`nixos.den:modules/nvidia.nix:3`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/nvidia.nix#L3) | Declared unfree battery; native stable driver/open/power-management options. | P=? S=? F=? U=? V=graphics kernel/session driver. Keep pinned Den compatibility; no new verification implied. |
| **upower** | A | [akeuben/dotfiles](/configs/akeuben/dotfiles/) | [`akeuben/dotfiles:modules/config/upower.nix:2`](https://github.com/akeuben/dotfiles/blob/48183786da040379d88ad2f23dbdc796de4093dc/modules/config/upower.nix#L2) | Minimal independently includable native service; no parameters. | P=? S=? F=? U=? V=UPower. |
| **hibernation** | B | [aeshakhzod/blazingly-fast](/configs/aeshakhzod/blazingly-fast/) | [`aeshakhzod/blazingly-fast:modules/batteries/hibernation.nix:2`](https://github.com/aeshakhzod/blazingly-fast/blob/2c2fb84d6b397a4d35c7af318d1a672294ab398a/modules/batteries/hibernation.nix#L2) | Native systemd suspend→suspend-then-hibernate; expose delay; caller must provision working swap/hibernation (line15). | P=swap/resume prerequisite S=? F=? U=? V=sleep transition override. |
| **ideapad-bluetooth** | B | [Spebby/NixOS](/configs/spebby/nixos/) | [`Spebby/NixOS:modules/services/bluetooth.nix:2`](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/services/bluetooth.nix#L2) | BlueZ plus unconditional Ideapad rfkill unblock; expose workaround/pairing policy, avoid unrelated hardware (lines12/20). | P=? S=? F=? U=device/rfkill access V=BlueZ/oneshot workaround. |
| **plex-streaming-inhibitor** | B | [Spebby/NixOS](/configs/spebby/nixos/) | [`Spebby/NixOS:modules/services/plex.nix:9`](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/services/plex.nix#L9) | Typed package/data/account/firewall options; Python/runtime owned; polling timeout/failure behavior needs docs (lines65/78/130). | P=configurable Plex data S=? F=configurable firewall U=configurable account V=Plex/polling sleep inhibitor. |
| **facter** | A | [drupol/infra](/configs/drupol/infra/) | [`drupol:modules/facter/facter.nix:7`](https://github.com/drupol/infra/blob/b8cf59f140f54f4f920d9f8070a3194eac38a8ae/modules/facter/facter.nix#L7) | Declared nixos-facter-modules input and report-path argument; hardware configuration/discovery adapter. | P=consumer report input (not mutable state declaration) S=? F=? U=? V=hardware detection/import. |
### Theming, fonts and display contracts

- Two font-package/interface nominations exist: lucasshiva and pdarulewski. Rafael Stylix/quasigod Catppuccin are
  theme adapters. Do not count them as extra font presets to inflate that recurrence.
- **Best read-only font-token interface:** lucasshiva **fonts (B)**. It retains its host-guards prerequisite.
- **Best minimal cross-OS package aspect:** pdarulewski **fonts (A)**.
- **Best explicit display validation:** quasigod **displays schema (A)**. It detects multiple primaries and uses
  inputs.self for wallpaper paths. Its existing grade remains A despite that prerequisite.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **fonts** | A | [pdarulewski/dotfiles](/configs/pdarulewski/dotfiles/) | [`pdarulewski/dotfiles:modules/features/fonts.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/fonts.nix#L2) | Cross-OS font package set via os class; nixpkgs only. | P=? S=? F=? U=? V=font installation. |
| **fonts feature with readOnly font options (B)** | B (shortlist/R; absent §4) | [lucasshiva/nixconfig](/configs/lucasshiva/nixconfig/) | [`lucasshiva:modules/features/core/fonts.nix:5`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/features/core/fonts.nix#L5) | Read-only font tokens + native NixOS/standalone-HM package/fontconfig; HM needs isNixos from retained host-guards (line74). | P=? S=? F=? U=? V=fontconfig/install; not independently dependency-free. |
| **stylix** | B | [RafaelMuijsert/nixos-config](/configs/rafaelmuijsert/nixos-config/) | [`RafaelMuijsert/nixos-config:modules/meta/stylix.nix:7`](https://github.com/RafaelMuijsert/nixos-config/blob/c2466a023f2071b774238829a853df5a1a943093/modules/meta/stylix.nix#L7) | Own Stylix input/import; carry host.theme scheme/polarity/wallpaper schema and expose font/cursor choices (lines9/12/35). | P=? S=? F=? U=? V=OS/home theme/font/cursor generation. |
| **catppuccin parametric theming (B)** | B (shortlist/R; absent §4) | [quasigod.xyz/nixconfig](/configs/quasigodxyz/nixconfig/) | `quasigod-xyz-nixconfig:modules/catppuccin.nix:7` | Flavor/accent constructor; own Catppuccin+nix-colors imports, retain/replace inputs.self wallpaper and fixed Qt/GTK choices (lines4/21/32). | P=? S=? F=? U=? V=theme/config generation. |
| **displays schema (A)** | A | [quasigod.xyz/nixconfig](/configs/quasigodxyz/nixconfig/) | `quasigod-xyz-nixconfig:modules/meta/displays.nix:58` | Typed monitor records; nullable/unique-primary derivation and duplicate-primary throw (line80); inputs.self-rooted wallpaper path (line51). | P=? S=? F=? U=? V=settings derivation only, no compositor activation claimed. |
### Containers, native services and developer workstations

- **Best full multi-resource native service API:** FastTrackStudios **task-server module (A)**. It is explicitly
  ordinary NixOS, not an implemented den aspect.
- **Best container engine default:** KGB33 **podman (A)**.
- Incus lifecycle reconciliation, the Colima launch agent and the Podman socket share virtualization use. But they are
  three different engines/platform contracts, not one recurring collector implementation.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **task-server module** | A | [FastTrackStudios/task](/configs/fasttrackstudios/task/) | [`FastTrackStudios/task:nix/nixos/task-server.nix:64`](https://github.com/FastTrackStudios/task/blob/a40932117efadcace0179d510514d6470df318cd/nix/nixos/task-server.nix#L64) | Retain exported package-default wrapper [nix/modules/nixos-modules.nix:20](https://github.com/FastTrackStudios/task/blob/a40932117efadcace0179d510514d6470df318cd/nix/modules/nixos-modules.nix#L20); typed mode/data/bind/port/environment/user options; minimal native consumer at line18. | P=dataDir default/var/lib/task-server via StateDirectory/tmpfiles S=optional EnvironmentFile, credentials provisioned externally F=optional TCP port9090 U=owned service account/group V=hardened systemd service/restart/native CLI. |
| **podman** | A | [KGB33/homelab](/configs/kgb33/homelab/) | [`KGB33/homelab:nixos/services/podman.nix:2`](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/services/podman.nix#L2) | Native Podman engine/Docker CLI compatibility; deliberately accept socket policy (line9). | P=? S=? F=? U=socket access implications, exact group policy unknown here V=Podman/socket. |
| **Colima Darwin service** | A | [danielgafni/nixos](/configs/danielgafni/nixos/) | [`danielgafni/nixos:modules/aspects/features/darwin/docker.nix:8`](https://github.com/danielgafni/nixos/blob/26f03bc416ad2535ff4cdf52a1d8cb9ead4b8fd6/modules/aspects/features/darwin/docker.nix#L8) | Darwin config/pkgs primaryUser, Docker/Compose/Colima; native primary-user socket (line15), preset VM sizing (line18). | P=Colima VM state unknown exact root S=? F=? U=primaryUser/socket V=launch agent/Colima VM. |
| **incus-preseed-reconcile** | B | [Draculestein/nixos-config](/configs/draculestein/nixos-config/) | [`Draculestein/nixos-config:modules/aspects/system/incus.nix:3`](https://github.com/Draculestein/nixos-config/blob/3514a1d2e512358af6d8357d389cfa9e11d49c2b/modules/aspects/system/incus.nix#L3) | host.incus.storagePool with dir default; own preseed/reconcile bridge/profile; expose CIDR/listen port (lines41/44). | P=/var/lib/incus/storage-pools/default (default) S=? F=8443 + bridge53/67 TCP/UDP U=? V=Incus + oneshot after preseed. |
| **loki-local** | B | [arichtman/nix](/configs/arichtman/nix/) | [`arichtman/nix:modules/den/aspects/controller/loki.nix:14`](https://github.com/arichtman/nix/blob/a33136e4580dd700bdf822e7a7314b475fbd0f11/modules/den/aspects/controller/loki.nix#L14) | Single-node storage/ring/schema/query preset; analytics disabled, adapt storage/alertmanager (lines42/63). | P=Loki local storage S=? F=listen/alertmanager details unknown here U=? V=Loki. |
| **work** | B | [sm-f/nix](/configs/sm-f/nix/) | [`sm-f/nix:modules/work.nix:3`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/work.nix#L3) | Extract Azure/.NET/Azurite core from VPN/Twingate/office bundle; standard NixOS/nixpkgs. | P=? S=? F=Azurite ports unknown here U=? V=Azurite + coupled workstation tooling. |
### VCS, search tools and document/media workflows

- Git nominates two different units: eugencowie's parameterized Git/Meld aspect and the class-forwarding
  adapter. They share Git functionality, not a common dataflow mechanism.
- fd/ripgrep are separate tools, even when colocated. Preserve the nominated fd. Do not promote its incomplete
  ripgrep wrapper sibling.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **vcs.git** | B | [eugencowie/dotfiles](/configs/eugencowie/dotfiles/) | [`eugencowie/dotfiles:modules/aspects/vcs/git.nix:3`](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/aspects/vcs/git.nix#L3) | name/email args; retain local diff._.meld companion and git-absorb, not just leaf. | P=? S=identity settings, no secret lifecycle claimed F=? U=? V=Git/Meld config/tool integration. |
| **ripgrep** | B | [moxie0420/dotfiles](/configs/moxie0420/dotfiles/) | [`moxie0420/dotfiles:modules/aspects/programs/ripgrep.nix:2`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/aspects/programs/ripgrep.nix#L2) | NixOS package + HM enable; rebind programs namespace. | P=? S=? F=? U=? V=package/native HM config. |
| **cli.fd** | A | [phucisstupid/dotfiles](/configs/phucisstupid/dotfiles/) | [`phucisstupid/dotfiles:modules/aspects/clis/fd-ripgrep.nix:3`](https://github.com/phucisstupid/dotfiles/blob/0e80243bb07bb53e2cb1d118d8dfc7f127ea0b6c/modules/aspects/clis/fd-ripgrep.nix#L3) | Hidden-file search/.git exclusions, ordinary HM/nixpkgs; sibling ripgrep Bat wrapper is explicitly incomplete and not included in this nomination. | P=? S=? F=? U=? V=tool config. |
| **bat** | B | [augustocdias/nixos](/configs/augustocdias/nixos/) | [`augustocdias/nixos:modules/programs/bat/bat.nix:2`](https://github.com/augustocdias/nixos/blob/494e352fa63d971d36e54641c6d8293ebed1dd92/modules/programs/bat/bat.nix#L2) | Ship owned theme directory, expose theme/pager/style; retain cache rebuild activation (lines13/16). | P=generated Bat theme cache S=? F=? U=? V=HM theme deployment/cache refresh. |
| **mpv-uosc** | A | [scoiatael/dotfiles](/configs/scoiatael/dotfiles/) | [`scoiatael/dotfiles:modules/aspects/mpv.nix:10`](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/mpv.nix#L10) | HM/nixpkgs plus owned config/mpv/uosc.conf; uosc/thumbfast/fonts/preview tools (lines27/50). | P=? S=? F=? U=? V=MPV UI/preview config. |
| **comma** | A | [scoiatael/dotfiles](/configs/scoiatael/dotfiles/) | [`scoiatael/dotfiles:modules/aspects/comma.nix:5`](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/comma.nix#L5) | Own declared nix-index-database input/module/enable (lines4/8/10). | P=database cache details unknown S=? F=? U=? V=HM nix-index/comma integration. |
| **yt-audio** | A | [Heromercer/nixfiles](/configs/heromercer/nixfiles/) | [`Heromercer/nixfiles:modules/features/yt-audio.nix:7`](https://github.com/Heromercer/nixfiles/blob/72d86dd2774f83fbaf0708cd0f4e4e78e0cc5ade/modules/features/yt-audio.nix#L7) | Own yt-dlp executable plus caller-argument forwarding; archive/output/metadata/subtitle/concurrency preset. | P=archive.log and output files in caller cwd S=? F=outbound downloader transport, no local firewall declared U=? V=CLI tool, no daemon. |
| **ttypicker-yazi portal** | B | [DJ-Laser/nixos](/configs/dj-laser/nixos/) | [`DJ-Laser/nixos:modules/desktop/tui-file-manager.nix:17`](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/modules/desktop/tui-file-manager.nix#L17) | Retain owned [packages/ttypicker.nix:23](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/ttypicker.nix#L23) and [packages/filechooser-yazi.nix:6](https://github.com/DJ-Laser/nixos/blob/27e216e2f9d3dfdba89177a82535975eb8a89899/packages/filechooser-yazi.nix#L6); expose terminal command/package instead of self'.packages. | P=? S=? F=? U=? V=HM XDG filechooser portal/Yazi plugin. |
### Generic class/schema/export adapters

- **Best small platform-fact adapter:** lucasshiva **host-guards (A)**. It resolves booleans into module arguments.
- The Hjem adapter of a config whose source is no longer public routes whole class bodies under platform predicates
  instead.
- redxtech projects settings. rhedgeco's primary schema is listed above. The Joonas editor bridge above evaluates a
  distinct module system.
- Grouping these as adapters does not establish repeated implementation or protocol compatibility.
| Unit | Grade | Review | Source | Contract and adaptation | Resources (P S F U V) |
|---|---|---|---|---|---|
| **host-guards policy (A)** | A | [lucasshiva/nixconfig](/configs/lucasshiva/nixconfig/) | [`lucasshiva:modules/den/policies/host-guards.nix:3`](https://github.com/lucasshiva/nixconfig/blob/9e8aa1ba03ce981aba3f8cbb430546ca2018b1f6/modules/den/policies/host-guards.nix#L3) | Den policy.resolve adds isNixos/isDarwin from host.class (lines6/9); no new identity/resources. | P=? S=? F=? U=? V=module argument policy, no app activation. |
| **host-settings** | B | [redxtech/nixfiles](/configs/redxtech/nixfiles/) | [`redxtech/nixfiles:modules/host-settings.nix:3`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L3) | Den/HM + surrounding host.settings convention; forwards settings to NixOS and host into HM. | P=? S=? F=? U=? V=settings/context projection. |
| **stable** | A | [KGB33/.dotfiles](/configs/kgb33/dotfiles/) | [`KGB33/.dotfiles:modules/aspects/stable.nix:7`](https://github.com/KGB33/.dotfiles/blob/851fb5b43c9e57a1fc5dfff6169b33b960a40932/modules/aspects/stable.nix#L7) | Own nixpkgs-stable input; derives current system/unfree policy; overlay shared NixOS/HM (lines13/24). | P=? S=? F=? U=? V=package-set overlay, no app activation. |
| **auto-upgrade (B)** | B | [espdesign/nixos.den](/configs/espdesign/nixosden/) | [`nixos.den:modules/auto-upgrade.nix:14`](https://github.com/espdesign/nixos.den/blob/f52aed42f511eef8b036676309c42c32bd657175/modules/auto-upgrade.nix#L14) | host args plus hardcoded repo URI; ff-only guard/desktop notification; expose URI before reuse. | P=system generations/download state unknown S=? F=? U=? V=systemd auto-upgrade/notification. |
### Preserved shortlist-only / conflicting-evidence appendix

Every nomination above is retained. None was quietly removed for mismatch. These need editorial reconciliation
before final publication:

- **lucasshiva/nixconfig Kitty and fonts:** absent from §4, but the R/shortlist cards give explicit source and B grades. The
  exact source lines above are recovered from them. Fonts requires host-guards isNixos, so do not publish it as a
  zero-dependency unit.
- **quasigod Catppuccin:** absent from §4, explicit B in shortlist/R. The actual constructor owns its inputs, but also
  a fixed inputs.self wallpaper and some fixed palette/Qt choices. The existing B is retained. Displays remains A as
  published, with the inputs.self prerequisite stated.
- **espdesign/nixos.den Nvidia:** absent from §4, explicit A in R/shortlist, and the path is verified at the manifest revision.
  Its den unfree battery is version-coupled. It is not automatically portable to current den.
  full-review R/P/shortlist cards. The source paths are verified above.
  both evidence statements.

## Separate namespace-library prior art

The three namespace libraries are separate prior art. Their full inventories preserve all broad/partial/stub units
and dependencies:
- [Crocuda server namespace](/libraries/crocuda/crocudanixos/), revision `226387d876ae`.
- [Normal desktop namespace](/libraries/crocuda/normalnixos/), revision `c8b5cf80b70e`.
- [Garden namespace, packages and eleven generator adapters](/libraries/adanoelle/garden-shell/), revision `e9c3a6b47faf`.
- [Reconciliation](/method/library-pilot/): published consumer-readiness limits remain attached.
### Best exemplar per application/resource family
Each row names a family and its existing exemplar, the kind and existing status or grade, and the resource
material to preserve with its explicit limits.
| Family and existing exemplar | Kind; existing status/grade | Resource material to preserve; explicit limits |
|---|---|---|
| Privacy daemon: Crocuda privacy.i2p | Application; **candidate coherent direct integration, ungraded** | Own user/group, runtime/state/log directories, config and forked-daemon/PID/reload/stop lifecycle ([i2p.nix:12](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/privacy/i2p.nix#L12), [i2p.nix:27](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/privacy/i2p.nix#L27), [i2p.nix:40](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/privacy/i2p.nix#L40)). Port payload and persistence policy beyond these paths: **not inventoried here**. |
| Account→secret provisioning: Crocuda mails.secrets | Integration-adapter; **partial, ungraded** | One Sops secret per account, `/var/lib/maddy/secrets`, root password-init service; caller owns Sops source/provisioning ([mail/default.nix:185](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/mail/default.nix#L185), [default.nix:197](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/mail/default.nix#L197)). Parent mail owner has unresolved companion references; do not call the combined envelope complete. |
| Loopback search/cache service: Normal browser.searxng | Application; **complete B after secret rebinding** | Native Searx+Redis services/state, loopback8888, no public firewall; [default.nix:23](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/browser/searxng/default.nix#L23); a committed credential (reported privately; not located here), overrideable, remains adaptation. Its separate Sops adapter stays **partial C** because of the recorded native-option mismatch; not merged into this grade. |
| Download service/client: Normal torrent | Application+integration; **complete B** | Transmission4 daemon/state/RPC9091 plus configured Rustmission client ([torrent/default.nix:12](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/torrent/default.nix#L12), [config.toml:69](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/torrent/dotfiles/rustmission/config.toml#L69)). RPC/auth behavior unexecuted; exact native user/persistence defaults **not inventoried here**. |
| Printer/discovery access: Normal office.printers | Application+integration; **complete B limited printing preset** | Native printing/Avahi/firewall, drivers and tools; SANE deliberately disabled ([printer.nix:27](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/office_tools/printer.nix#L27), [printer.nix:47](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/office_tools/printer.nix#L47)). Nested user policy is not credited as live group routing. |
| Terminal application: Normal kitty | Application; **complete B desktop preset** | Own app/assets/font-schema dependency plus current-theme symlink via user-tmpfiles ([default.nix:4](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/kitty/default.nix#L4), [default.nix:13](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/kitty/default.nix#L13)). Theme-link ordering untested. Contrast Garden's caller-activated theme adapter below. |
| Editor state/config: Normal nvim variants | **One application**; raw preset **complete B extraction**; NvChad/IDE limits retained | Own config/assets and `/var/lib/nvim/servers` ([default.nix:6](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/text_editors/default.nix#L6), [default.nix:25](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/terminal/text_editors/default.nix#L25)). NvChad online plugin/order untested; IDE has extra runtime prerequisites. Separate deref adapter is **partial C**, with mutable copies and missing ordering—not another editor. |
| Mutable palette lifetime: Garden palette/toolkit | Palette **integration-adapter, complete A**; toolkit **tool, complete A** | Seed-once writable palettes.toml after writeBoundary; generator owns mutable themes/cache/manifest and best-effort reload ([palette.nix:6](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/palette.nix#L6), [palette.nix:17](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/palette.nix#L17), [main.rs:255](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/crates/garden-themes/src/main.rs#L255)). Direct resource ownership, no secret/user/port declaration in these owners. |
| Theme/session integration: Garden terminal/shell | **Integration-adapters**; terminal **partial relocation B**, shell **partial runtime envelope B** | Ordered theme seed; Fish state/cache/links and environment overlays; shell settings/font files, QML links, source marker and best-effort session restart ([terminal.nix:26](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/terminal.nix#L26), [terminal.nix:62](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/terminal.nix#L62), [shell.nix:53](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/modules/aspects/shell.nix#L53)). Caller owns app enable, Quickshell/Niri session and keys; relocation/Yazi-parent gaps remain. |
| Paired settings: Normal font/screen | Font schema **adapter, complete A**; fontSize/screenSize **constructors, complete B** | OS/HM typed settings and writers; explicit selected-schema prerequisite ([font.nix:11](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/batteries/font.nix#L11), [font.nix:35](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/batteries/font.nix#L35), [screen.nix:34](https://github.com/crocuda/normal.nixos/blob/c8b5cf80b70ec9f052640518c09dedaa6e8c3546/modules/aspects/window_managers/niri/screen.nix#L34)). Settings only; no app/font installation or resource provisioning implied. |
| DNS records: Crocuda zone.base/mail | **Constructors; candidates, ungraded**, compatibility unproven | Domain/address→NSD records/validation; mail adds PTR/MX/SPF/DMARC/autoconfig ([zone.nix:171](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/batteries/zone.nix#L171), [zone.nix:183](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/batteries/zone.nix#L183)). Not daemon activation; helper/input-name compatibility and fixed serial caveats stay attached. |
### Recurrence and broad owners retained

- **State/access/lifecycle repeats** across Crocuda I2P, Monero/Wownero, Maddy and Normal Transmission/Searx/editor/Kitty.
  The blockchain owners explicitly use `/persist`. But they remain **partial, ungraded**, because asset log
  destinations conflict with owner directories ([monero.nix:48](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/decentralised_finance/monero.nix#L48), [monerod.conf:7](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/decentralised_finance/dotfiles/monero/monerod.conf#L7)).
  Ordinary state paths elsewhere do not establish a persistence collector policy.
- **Secret/certificate lifecycle repeats** in mails.secrets, the defective Normal Searx Sops adapter and Crocuda SSL.
  SSL stays **partial, ungraded**. Credentials/domains are outside its owned contract, and the timer→instance-service
  linkage is unresolved ([ssl.nix:25](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/web/ssl.nix#L25), [ssl.nix:60](https://github.com/crocuda/crocuda.nixos/blob/226387d876ae3b70b47d510f75e21973d23f7bae/modules/aspects/servers/web/ssl.nix#L60)).
- **Desktop access/session resources** recur in Normal Bluetooth, printing, Flatpak, Yubikey and WM owners. Preserve
  the [full Normal inventory](/libraries/crocuda/normalnixos/). Installation bundles remain bundles. Partial
  browser/LLM/gaming/Niri/GNOME owners retain their runtime/closure defects. No detailed extra resource payload is
  inferred here.
- **Shell/tool and operations breadth** remains in the [full Crocuda inventory](/libraries/crocuda/crocudanixos/):
  partial Fish/Nushell/helper assets; network/multicast, Docker/Podman membership, selected Nix/security policies,
  DHCP/VM constructors, deploy output and destructive VM wrappers. Their candidate/partial labels are ungraded. The
  broad owner links preserve them without inventing completeness.
- **Generated fragments remain adapters.** Garden's [eleven-adapter inventory](/libraries/adanoelle/garden-shell/)
  retains complete A Kitty/Fish/Kakoune/fzf/lazygit/btop/Zathura; bat A for shipped palettes; Yazi partial B; Niri
  reference-only C; Obsidian generated-only B. The Palette→fragment trait does not activate eleven apps
  ([mod.rs:65](https://github.com/adanoelle/garden-shell/blob/e9c3a6b47fafaca0143daeb0da63e82209b2c9e8/crates/garden-themes/src/generators/mod.rs#L65)).
  Garden daemon/ctl/tui/observability remain stubs, not operational resource owners.

### Obvious config-shortlist comparisons

These are existing nominations only. There is no regrading and no exhaustive census.

| Existing nomination | Source | Comparison |
|---|---|---|
| [talarys ghostty B](/configs/talarys/den/) | [`modules/apps/ghostty.nix:2`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/apps/ghostty.nix#L2) | an app-owning terminal preset, compared with Garden theme adapters |
| [RafaelMuijsert stylix B](/configs/rafaelmuijsert/nixos-config/) | [`modules/meta/stylix.nix:7`](https://github.com/RafaelMuijsert/nixos-config/blob/c2466a023f2071b774238829a853df5a1a943093/modules/meta/stylix.nix#L7) | compares host theme/font settings |
| [redxtech host-settings B](/configs/redxtech/nixfiles/) | [`modules/host-settings.nix:3`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L3) | compares OS/HM context forwarding |
| [clemak Starship A](/configs/clemak27/homelab/) | [`modules/aspects/shell/starship.nix:6`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/shell/starship.nix#L6) | a narrow preset, contrasted with Crocuda's broad partial shell owner |

### How to group later work

- Group later work by **application/resource family + existing status + prerequisite**.
- Keep persist, secrets, ports/firewall, users/groups, services, mutable files and lifecycle as separate inventory
  fields.
- Absent detailed payloads above are **not inventoried**. Never infer them as empty.
- These are raw rewrite inputs. They are not runnable deployment recommendations or protocol-conformance claims.

## Coverage and next harvest boundary

- The detailed config catalogs retain **152 nominations from all 93 shortlisted repositories** (71 from 38, 81 from
  55).
- Names that span a constructor family remain one nomination.
- Exact duplicate resource usage is not a count of independently reusable apps.
- The three separate namespace pilots remain excluded from config totals. Their linked inventories preserve
  broad/partial/stub units.
- No additional B_ref apps were promoted into this shortlist.

**Highest-priority missing harvest facts.** These are the payloads marked unknown/not inventoried:

- exact durable paths and ownership;
- secret names/provisioning/recipients;
- listener versus firewall rules;
- user/group privileges;
- service ordering/restart and first/repeated activation behavior.

**Open items:**

- Grade disagreements and shortlist-only contracts above stay unresolved. This draft does not adjudicate them.
- A full rewrite can preserve ideas and resource inventories. It can replace private/fleet dependencies and direct
  effects with the owner's standard resource suite.
- Its protocol pointer is still pending, so there is no conformance claim here.

---
title: "Public configuration themes"
---

This doc collects the themes that recur across the 98 public reviews. It is for den maintainers, for authors who
want to start a config, and for contributors to a community aspect library. It gives recurring composition patterns,
recurring library units, recurring den friction, and an inventory of declared targets. It is independent of
repository scores: no score is used or given here. The [complete census summary](/census/summary/) holds the
full software and machine-role counts.

## Contents

- [Scope and corpus counts](#scope-and-corpus-counts)
- [Recurring composition patterns](#recurring-composition-patterns)
- [Recurring library units across the 98 public reviews](#recurring-library-units-across-the-98-public-reviews)
- [Recurring den friction in 98 public reviews](#recurring-den-friction-in-98-public-reviews)
- [Reviewed public target inventory](#reviewed-public-target-inventory)
- [Platform and extension coverage (historical)](#platform-and-extension-coverage-historical)
- [Starter-template candidates](#starter-template-candidates)

## Scope and corpus counts

The 98 public reviews cover 91 configuration repositories and seven libraries, templates or other projects.
Citations below use `<id>` to identify a repository. Paths and lines refer to its reviewed revision.

| Count | Value |
|---|---|
| Manifest entries in the retained census evidence | 120 |
| Removed by [exclusions](/method/excluded/) | seven archived entries and five public libraries/tools |
| Included in corpus totals | 108 |
| Public reviews (all remain evidence) | 98 |
| Public entries that contribute to included counts now | 93 |

How to read the counts:

- [The census contract](/method/census/) records source-led adoption and host-role counts. A mechanical mention
  is not adoption.
- The [reviewed inventory](#reviewed-public-target-inventory) and the [complete census summary](/census/summary/)
  supersede the earlier platform lower bounds.
- The earlier lower bounds remain as explicitly scoped historical checks. See
  [Platform and extension coverage](#platform-and-extension-coverage-historical).

## Recurring composition patterns

Five composition patterns recur. The table gives each pattern, the repositories that show it, and what it means for
a starter or a library.

| Pattern | Examples (source) | Lesson |
|---|---|---|
| **Shared defaults plus opt-in aspect stacks** | amatos uses a default base ([`modules/den/base.nix:57`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L57)). andreshungbz defaults to account/provider policies ([`modules/defaults.nix:5`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/defaults.nix#L5)). motheki keeps a workstation profile as capability composition ([`modules/aspects/profiles/workstation.nix:4`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/aspects/profiles/workstation.nix#L4)). | A starter should expose the small base. It should teach which defaults produce side effects. |
| **One aspect contributing to several classes** | amatos separates OS, Darwin and NixOS contributions within a baseline ([`modules/den/base.nix:39`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L39), [`modules/den/base.nix:44`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L44), [`modules/den/base.nix:48`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L48)). | Standalone homes need their own inventory and routing. andreshungbz ([`modules/homes/andreshung.nix:4`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/homes/andreshung.nix#L4)) and soriPhoono ([`modules/sops.nix:37`](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/sops.nix#L37)) make that distinction explicit. |
| **Typed entity settings bridging shared aspect bodies** | jasperro ([`modules/schema/settings.nix:50`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/schema/settings.nix#L50)), redxtech ([`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34)), henriquekirchheck ([`modules/aspects/settings/default.nix:5`](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/aspects/settings/default.nix#L5)) and sk4rd ([`modules/den.nix:14`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L14)) repeat this need. | The repeated unit is a settings contract and a traversal recipe. It is not a set of interchangeable author defaults. |
| **Service facts collected across hosts** | Keyruu ([`modules/policies/services-collect.nix:6`](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/policies/services-collect.nix#L6)), byte-sized-emi ([`modules/fleet.nix:3`](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/fleet.nix#L3)), Gwenodai ([`modules/policies/network-backends.nix:18`](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/policies/network-backends.nix#L18)) and repparw ([`modules/service-graph.nix:13`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/service-graph.nix#L13)) show producer/collector/consumer designs. | Provenance and cardinality handling distinguish robust implementations. Only the first two currently nominate the same fleet-service problem in review §4. |
| **Tool-facing inventory as a projection** | motheki projects serializable identity/class data ([`modules/inventory/access.nix:8`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/inventory/access.nix#L8), [`modules/inventory/access.nix:24`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/inventory/access.nix#L24)). auscyber derives builders and deployment from entities ([`aspects/base/builders.nix:121`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/builders.nix#L121), [`aspects/tooling/deploy.nix:23`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/tooling/deploy.nix#L23)). | These are useful advanced examples. They are not mandatory starter machinery. |

## Recurring library units across the 98 public reviews

### How the families were selected

- **Scope.** We read §4 of all 98 public reviews. Then we read the actual source for every member counted below.
- **Revisions.** Every listed clone HEAD matched its extract revision.
- **Evidence.** The evidence is static only. No evaluation, builds, repository scripts, score material or
  independent-scorer artifacts were used.
- **Grades.** The grades below judge the adoption cost of the named unit. They are not repository quality scores.
- **Threshold.** A family must have **at least three distinct repositories whose existing §4 explicitly nominates a
  candidate solving the same problem**. Four families meet this strict threshold.
- **Membership.** Family membership does not imply interchangeable settings.
- **Best representative.** We selected it from actual source. We preserve the differences between members. We do
  not merge them into a lowest-common-denominator package list.

### Summary of the four families

| common unit/problem | strict candidate repos | preferred implementation | grade after extraction |
|---|---:|---|---|
| NixOS PipeWire audio baseline | 4 | Steven-S1020/Nixos-Configuration, [`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2) | A, explicit policy choices |
| HM direnv + nix-direnv integration | 4 | Sharparam/nix-config, [`modules/base/direnv.nix:11`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L11) | B, separate optional aspect and preferences |
| NixOS BlueZ enable + adapter power-on | 3 | Kykero/Nazunix, [`modules/desktop/bluetooth.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4) | A, very small policy leaf |
| Live-checkout root and out-of-store configuration links | 3 | Aor-Li/Infra, [`modules/aspects/default/home.nix:18`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L18) | B, extract repo helper from owner identity |

### 1. NixOS PipeWire audio baseline — four candidates

**Shared function:** configure the machine audio server, including PulseAudio compatibility. These are configuration
units, not only occurrences of the `pipewire` package. Every member is already nominated under its review's §4.

| candidate repo / extract revision | existing §4 name | source proving common function | differences relevant to reuse |
|---|---|---|---|
| Erastos/nixos-dotfiles `f2336347f41d` | audio | [`parts/aspects/features/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/aspects/features/audio.nix#L2) imports [`modules/system/audio.nix:2`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L2); enables PipeWire and Pulse at [`modules/system/audio.nix:3`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/modules/system/audio.nix#L3) | Smallest core. The adapter and the six-line target must travel together. |
| loystonpais/lunar `5f836c9e4a1c` | audio | [`modules/lunar/audio.nix:5`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/lunar/audio.nix#L5) enables PipeWire/ALSA/Pulse/JACK | Adds Crosspipe/pwvucontrol in the base at [`modules/lunar/audio.nix:14`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/lunar/audio.nix#L14), then repeats them in optional tools at [`modules/lunar/audio.nix:17`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/lunar/audio.nix#L17). |
| Shawn8901/nixos-configuration `890a465d7eb3` | desktop.audio | [`modules/aspects/cfg/desktop/audio.nix:2`](https://github.com/Shawn8901/nixos-configuration/blob/890a465d7eb34855c4f34a0f82191fdab41041b6/modules/aspects/cfg/desktop/audio.nix#L2) enables PipeWire/ALSA/Pulse/WirePlumber | Also changes `@users` realtime/memory/nice limits at [`modules/aspects/cfg/desktop/audio.nix:15`](https://github.com/Shawn8901/nixos-configuration/blob/890a465d7eb34855c4f34a0f82191fdab41041b6/modules/aspects/cfg/desktop/audio.nix#L15). This is a stronger policy than audio-server enablement. |
| Steven-S1020/Nixos-Configuration `89fd086f61a5` | system/audio | [`modules/system/audio.nix:2`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L2) owns the complete audio aspect | Disables PulseAudio. Enables rtkit, ALSA/32-bit/Pulse/JACK/WirePlumber at [`modules/system/audio.nix:3`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L3)–[`modules/system/audio.nix:11`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/system/audio.nix#L11). |

**Best actual source:** Steven's complete 14-line leaf (`modules/system/audio.nix:2`). **Grade A**, when a consumer
adopts it as exactly the documented NixOS policy.

- It has no author identity, no private assets and no additional flake inputs.
- Dependencies: den's flake-module context and the standard NixOS/nixpkgs audio options.
- The aspect name is `den.aspects.system._.audio`.
- A consumer includes that leaf and deliberately accepts 32-bit ALSA, JACK and rtkit.
- No platform-test claim is made.

**A more neutral unit:** keep Erastos's minimal server core. Expose the rtkit/JACK/32-bit choices as options. That
generalized version is **B** work. Keep audio-control applications and realtime-limit policy optional.

**Not counted:** Anders130's `audio` candidate is not part of this count. Its unit generates device/profile/disable
rules, which is a different problem (`modules/hardware/audio.nix:23`, `modules/hardware/audio.nix:71`).

### 2. HM direnv + nix-direnv integration — four candidates

**Shared function:** install and configure project environment activation through HM, with nix-direnv enabled.
Instant shell hooks, Poetry, mise and editor selection are variations. The common unit does not require all of them.

| candidate repo / extract revision | existing §4 name | source proving common function | differences relevant to reuse |
|---|---|---|---|
| Likivik/spectacle `ce6d767b84e9` | direnv | [`modules/aspects/dev/direnv.nix:21`](https://github.com/Likivik/spectacle/blob/ce6d767b84e901fd044ac0693c21646cb739120c/modules/aspects/dev/direnv.nix#L21) enables direnv and shell integrations; nix-direnv at [`modules/aspects/dev/direnv.nix:27`](https://github.com/Likivik/spectacle/blob/ce6d767b84e901fd044ac0693c21646cb739120c/modules/aspects/dev/direnv.nix#L27) | Bundles OS EDITOR and HM VSCodium/VISUAL policy at [`modules/aspects/dev/direnv.nix:9`](https://github.com/Likivik/spectacle/blob/ce6d767b84e901fd044ac0693c21646cb739120c/modules/aspects/dev/direnv.nix#L9), [`modules/aspects/dev/direnv.nix:15`](https://github.com/Likivik/spectacle/blob/ce6d767b84e901fd044ac0693c21646cb739120c/modules/aspects/dev/direnv.nix#L15). |
| Occhima/nix-conf `201ebbb67074` | direnv-poetry | [`modules/home-manager/shells/cli/direnv.nix:5`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/home-manager/shells/cli/direnv.nix#L5) enables direnv/nix-direnv | An ordinary exported HM module, not already a den aspect ([`modules/home-manager/shells/cli/direnv.nix:2`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/home-manager/shells/cli/direnv.nix#L2)). The Poetry layout needs a caller-supplied executable ([`modules/home-manager/shells/cli/direnv.nix:17`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/home-manager/shells/cli/direnv.nix#L17)). |
| Sharparam/nix-config `eb5fe2550c15` | direnv-instant | [`modules/base/direnv.nix:15`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L15) imports direnv-instant; direnv/nix-direnv configuration at [`modules/base/direnv.nix:18`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L18) | mise, Lix nix-direnv and strict dotenv policy are explicit additional choices ([`modules/base/direnv.nix:20`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L20), [`modules/base/direnv.nix:23`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L23), [`modules/base/direnv.nix:27`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L27)). |
| voidlily/dotfiles `ef20abb997bd` | direnv | [`modules/direnv.nix:15`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L15) configures direnv/nix-direnv and instant hooks | The input module import is global at [`modules/direnv.nix:11`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L11), separate from the opt-in aspect. Comments distinguish instant hooks from nix-direnv at [`modules/direnv.nix:19`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/direnv.nix#L19). |

**Best actual source:** Sharparam's integration ([`modules/base/direnv.nix:6`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L6), [`modules/base/direnv.nix:15`](https://github.com/Sharparam/nix-config/blob/eb5fe2550c153cfcff9dc78a9c9ddda1cbf428e4/modules/base/direnv.nix#L15)).
**Grade B**, for these reasons:

- It declares its input locally.
- It names the imported HM module.
- It puts its configuration under `programs.direnv.config.global`.
- It makes the alternative nix-direnv package a default, not a forced replacement (`modules/base/direnv.nix:23`,
  `modules/base/direnv.nix:26`).

Dependencies: HM with direnv/mise options, `direnv-instant.homeModules.direnv-instant`, nixpkgs exposing
`lixPackageSets.latest.nix-direnv`, `lib.mkDefault`, and flake-file if you preserve the input declaration.

**Adaptation:**

1. Lift `den.aspects.base.homeManager` to a named opt-in `direnv` aspect.
2. Expose the nix-direnv package, instant hooks, mise integration, `load_dotenv` and `strict_env` choices.
3. Keep ordinary shell environment activation as the core.
4. Bundle the external module import with activation, so that a consumer cannot select only half of the integration.
5. Do not import Likivik's editor choices or Occhima's Poetry stdlib unless the consumer explicitly requests them.

The ordinary HM export in Occhima counts as an existing candidate for the same problem. It is not presented as an
already packaged den battery.

### 3. NixOS BlueZ enable + adapter power-on — three candidates

**Shared function:** enable the Bluetooth service and power the adapters on at boot. There are three existing §4
nominations. One contains extra hardware-specific behavior, which the proposed core excludes.

| candidate repo / extract revision | existing §4 name | source proving common function | differences relevant to reuse |
|---|---|---|---|
| andreshungbz/nixconfig `bdee3f6ec030` | bluetooth | [`modules/aspects/desktop/components/nixos/bluetooth.nix:5`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/desktop/components/nixos/bluetooth.nix#L5) enables Bluetooth and powerOnBoot | The export uses the local `pkt.bluetooth` namespace ([`modules/aspects/desktop/components/nixos/bluetooth.nix:2`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/aspects/desktop/components/nixos/bluetooth.nix#L2)). |
| Kykero/Nazunix `469bacd7b841` | desktop-bluetooth | [`modules/desktop/bluetooth.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4) enables BlueZ/power-on | A comment names Noctalia as a consumer, but the source has no Noctalia dependency ([`modules/desktop/bluetooth.nix:1`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L1), [`modules/desktop/bluetooth.nix:5`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L5)). |
| Spebby/NixOS `e6ea71a1af5e` | ideapad-bluetooth | [`modules/services/bluetooth.nix:16`](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/services/bluetooth.nix#L16) enables Bluetooth/power-on | Also installs an rfkill workaround at [`modules/services/bluetooth.nix:5`](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/services/bluetooth.nix#L5) and a fixed pairing policy at [`modules/services/bluetooth.nix:20`](https://github.com/Spebby/NixOS/blob/e6ea71a1af5e97b4e8fd343ac33c6c97a1e2ead3/modules/services/bluetooth.nix#L20). |

**Best actual source:** Kykero's `den.aspects.desktop-bluetooth.nixos` ([`modules/desktop/bluetooth.nix:4`](https://github.com/Kykero/Nazunix/blob/469bacd7b841df5aaea43ad6027049cb152f394b/modules/desktop/bluetooth.nix#L4)),
**Grade A**.

- Dependencies: den module context and the standard NixOS/nixpkgs BlueZ options only.
- It has no HM, no external input, no desktop shell and no user identity.
- It needs no parameters if you want its two explicit defaults.
- It is a tiny preference leaf. Its value is clear naming and opt-in behavior, not a major abstraction or a large
  code saving.

**Hardware add-on:** keep the IdeaPad rfkill unit as a separate **B** add-on. It requires `pkgs.util-linux`. Its
`rfkill unblock bluetooth` command targets the Bluetooth class, not an individual device
(`modules/services/bluetooth.nix:12`). Pairing policy must be a deliberate option. It must not come silently with the
hardware workaround.

**Not counted:** Crocuda normal also has Bluetooth configuration, but its existing §4 nominates no library candidate.
It is a repeated aspect, **not a fourth candidate vote** (`modules/aspects/bluetooth.nix:29`,
`modules/aspects/bluetooth.nix:59`).

### 4. Live-checkout root and out-of-store configuration links — three candidates

**Shared problem:** one configurable writable checkout location should feed mutable configuration links. This
replaces repeated author-specific absolute paths.

This family has **three §4 candidates, but only two generic link-helper implementations**. amatos supplies a shared
location option, and aspect-specific code consumes it to construct links. Do not report it as three copies of the
same helper.

| candidate repo / extract revision | existing §4 name | source proving common problem | implementation boundary |
|---|---|---|---|
| amatos/magnanix `7675475f0509` | repo-dir | [`modules/den/repo-dir.nix:9`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/repo-dir.nix#L9) declares a shared checkout option; Zed reads it at [`modules/packages/zed/zed.nix:29`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L29) and creates an out-of-store link at [`modules/packages/zed/zed.nix:243`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L243) | Checkout-setting provider. Path construction is still aspect-specific. The default is `~/Developer/magnanix` ([`modules/den/repo-dir.nix:11`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/repo-dir.nix#L11)). |
| Aor-Li/Infra `87405e2c8b13` | workspace-links | [`modules/aspects/default/home.nix:22`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L22) selects the checkout root; prefix removal/link helpers at [`modules/aspects/default/home.nix:23`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L23), [`modules/aspects/default/home.nix:30`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L30) | Generic root/path/link API for both integrated users and standalone homes ([`modules/aspects/default/home.nix:38`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L38)). |
| auscyber/dotfiles `96be028eaba6` | file-local | [`aspects/base/file-local.nix:19`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/file-local.nix#L19) selects the user checkout location; [`aspects/base/file-local.nix:21`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/file-local.nix#L21) maps source paths; link helper at [`aspects/base/file-local.nix:23`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/file-local.nix#L23) | The generic helper uses user context and a caller-supplied rootPath. It does not handle standalone-home identity ([`aspects/base/file-local.nix:12`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/file-local.nix#L12)). |

**Best actual source:** Aor-Li's repo helper ([`modules/aspects/default/home.nix:18`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/aspects/default/home.nix#L18)), **Grade B**.

- Dependencies: den user/home schemas; HM's `config.lib.file.mkOutOfStoreSymlink`; nixpkgs `lib.removePrefix`;
  `inputs.self`; the owner/entity `repoRoot` contract.
- The paired schema defines a nullable repoRoot for both entity kinds (`modules/meta/schema/identity.nix:25`,
  `modules/meta/schema/identity.nix:33`).
- A real consumer uses `.link` on a neighboring config directory
  (`modules/aspects/trait/dev/editor/neovim/lazyvim/lazyvim.nix:6`).

**Adaptation:**

1. Extract only `lib.repo.{root,link,path}` from the unrelated owner fullname/email adapter
   (`modules/aspects/default/home.nix:26`).
2. Retain both the user and the home entry paths.
3. Publish a neutral configurable checkout-root default, not `~/Infra`.
4. Before joining paths, validate that the source being relativized is below `inputs.self`
   (`modules/aspects/default/home.nix:22`, `modules/aspects/default/home.nix:23`).
5. Do not import the whole existing identity schema unchanged. It contains author fullname/email defaults
   (`modules/meta/schema/identity.nix:12`, `modules/meta/schema/identity.nix:18`).

amatos's consumer guard offers a useful optional existence/git-checkout check ([`modules/packages/zed/zed.nix:257`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/packages/zed/zed.nix#L257)).
The generic helper itself does not contain it.

### Threshold discipline and near-misses

- **Fleet service-fact collection** is a promising larger unit. But only **two** current §4 nominations match that
  exact problem: byte-sized-emi's `fleet-http-services` ([`modules/fleet.nix:3`](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/fleet.nix#L3)) and Keyruu's
  `collect-service-facts` (`modules/policies/services-collect.nix:6`).
  - Do not claim three by counting Gwenodai's distinct network-backend collection or its nominated active-aspect
    introspection unit.
  - More recurrent-aspect investigation could nominate a third. That would be new judgment, not a third existing
    candidate.
- **Disk layout and Disko class forwarding are different units.** greysilly7's class bridge
  (`modules/core/disko.nix:19`) and muhammadtalha-quant's ext4 layout ([`modules/disko/ext4-simple.nix:2`](https://github.com/muhammadtalha-quant/denix/blob/70e67b484b5efe04a60d9982e41c3a66eeb0135c/modules/disko/ext4-simple.nix#L2)) do not
  establish three implementations of either unit.
- **No count above is based on package mentions,** language toolchains or standalone package derivations. Existing
  §4 candidate names, concrete config paths and revision pins are included, so that every counted membership is
  auditable.

## Recurring den friction in 98 public reviews

### Method

- **Source.** This is a static synthesis of all 98 `source=public` review texts in the audit's working corpus file.
  It is independent of ratings.
- **Verification.** The reviews identify candidate evidence. We checked important excerpts with
  `git show <extract.rev>:<file>` in the public clones.
- **Not used.** No Nix evaluation/build, repository program or pilot material was used.
- **Author reports.** A source comment that reports a failure is evidence of author experience. It is not an
  independently reproduced den bug.
- **Recurrence counts** name repositories that carry a related signal. They do not count identical bugs or all
  affected users.

Each theme below gives the recurrence, the strongest source-verified examples, and the den action implication. The
"Classification" column says what kind of signal each example is.

### 1. Context and argument ownership across host, user and standalone-home boundaries

**Recurrence:** 9 repositories: adanoelle/fern, derangga/dotfiles, eldios/dotfiles, SyahrulBhudiF/dotfiles,
closure-labs/foundation, soriPhoono/homelab, oxce5/chimera, sonntag/nix, auscyber/dotfiles.

Strongest source-verified examples:

| Repository | Revision | What the source shows | Classification |
|---|---|---|---|
| adanoelle/fern | `060cd42a3d02` | [`modules/hosts.nix:14`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L14) explains that standalone defaults use an unmodified package set. [`modules/hosts.nix:18`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L18) replaces pkgs, and [`modules/hosts.nix:19`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L19)–[`modules/hosts.nix:25`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L25) replaces instantiate to pass inputs. | **API/default ergonomics.** Not proof that den promises inheritance here. |
| derangga/dotfiles | `c43c24f8b7f7` | [`den.nix:8`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L8) says instantiate receives modules without the old specialArgs. [`den.nix:29`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L29) says it cannot read its owning host, so [`den.nix:40`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L40) threads the same identity into construction. [`den.nix:56`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L56) explains the HM package-sharing default difference. [`den.nix:59`](https://github.com/derangga/dotfiles/blob/c43c24f8b7f7af0f0b754efa05bdfa3d7331072f/den.nix#L59) explicitly limits extraSpecialArgs wiring to one user. | **Migration/API workaround.** The one-user restriction belongs to the author's adapter. |
| eldios/dotfiles | `ce9d9573891e` | A shared argument set feeds both host instantiate ([`modules/den.nix:21`](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/den.nix#L21)) and HM extraSpecialArgs ([`modules/den.nix:33`](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/den.nix#L33)). | **Normal compatibility extension.** It shows recurring plumbing, not a bug. |
| soriPhoono/homelab | `c6599b697b93` | [`modules/sops.nix:37`](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/sops.nix#L37) explicitly states that standalone homes do not receive user-schema includes. It then supplies home-schema includes at [`modules/sops.nix:38`](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/sops.nix#L38). | **Expected scope distinction.** Configs repeatedly find it important enough to document. |
| oxce5/chimera | `cc96a65abd5d` | [`modules/assignments.nix:102`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L102) and [`modules/assignments.nix:108`](https://github.com/oxce5/chimera/blob/cc96a65abd5df81cdf2c8829ddff64111d616027/modules/assignments.nix#L108) repeat selected HM halves on a user role, because host-role HM content is inert. | **Routing pedagogy/normal extension.** Not a failed evaluation. |
| sonntag/nix | `816947c6a270` | [`modules/nixible/playbooks.nix:17`](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/nixible/playbooks.nix#L17) explains that a resolved output user lacks a parent-host walk. [`modules/nixible/playbooks.nix:23`](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/nixible/playbooks.nix#L23) appends the concrete host aspect. | **Custom-output context workaround.** |
| auscyber/dotfiles | `96be028eaba6` | [`aspects/base/home-standalone.nix:6`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/home-standalone.nix#L6) reports two user@host homes sharing a scope ID. [`aspects/base/home-standalone.nix:25`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/home-standalone.nix#L25) overrides the name, and [`aspects/base/home-standalone.nix:26`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/home-standalone.nix#L26) pins aspect lookup. | **Reported den identity bug.** Distinct from the normal home/user distinction above. |

**Additional source-verified instances:**

- SyahrulBhudiF/dotfiles (`ba537827987e`): [`modules/den.nix:28`](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/den.nix#L28) passes inputs/flakePkgs.
- closure-labs/foundation (`0715d5823b45`): [`modules/home/construction/_module.nix:33`](https://github.com/closure-labs/foundation/blob/0715d5823b453f4b8d5a2fa4aaa368ef669a2796/modules/home/construction/_module.nix#L33) and
  `modules/home/construction/_module.nix:40` supply a custom constructor/argument set.

These two share the constructor override shape. Neither establishes a failure.

**Den action implication:**

- Publish a context matrix for embedded users, standalone homes and custom outputs. It should show the available
  entity args, package source, input args, inheritance and parent traversal.
- Provide a small supported constructor adapter that accepts entity-derived arguments.
- Add a regression fixture with the same username on two standalone hosts.
- Keep automatic inheritance opt-in. The observed adapters preserve existing module APIs. They do not establish that
  all args should propagate by default.

### 2. Merge semantics and repeated inclusion can silently change contributions

**Recurrence:** 4 repositories: adanoelle/fern, closure-labs/maestro, JoonasKajava/nvf-config, ivokun/kebun. A
fifth, AnonymousRand/nix_config, has a related precedence problem, but its attribution is less conclusive.

| Repository | Revision | What the source shows | Classification |
|---|---|---|---|
| adanoelle/fern | `060cd42a3d02` | [`modules/tailscale.nix:13`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/tailscale.nix#L13) reports that diamond includes duplicate list entries and that Tailscale rejected the flags. [`modules/tailscale.nix:31`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/tailscale.nix#L31) and [`modules/tailscale.nix:41`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/tailscale.nix#L41) give modules explicit keys. | **Reported inclusion/deduplication problem,** with a concrete module-identity workaround. |
| closure-labs/maestro | `6d707f35e29b` | [`modules/features/operator/account.nix:3`](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/features/operator/account.nix#L3) says den v0.16 can reach the account through both host/user providers. [`modules/features/operator/account.nix:4`](https://github.com/closure-labs/maestro/blob/6d707f35e29bb135030b4273e741f966b941d75c/modules/features/operator/account.nix#L4) assigns a key. | **Defensive deduplication workaround.** The excerpt does not independently demonstrate a failing duplicate. |
| JoonasKajava/nvf-config | `9674a20a5632` | [`modules/nvf-integration.nix:20`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L20) reports that nested forwarding through a freeform adapter shallow-merges lazy.plugins and loses definitions. [`modules/nvf-integration.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L24) preserves imports/functions while it nests target modules. [`modules/nvf-integration.nix:41`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L41) installs it through mapModule. | **Reported merge-loss bug/API trap.** The fix lets the NVF option types own the merge. |
| ivokun/kebun | `1038ddc22989` | [`modules/den.nix:10`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/den.nix#L10)–[`modules/den.nix:14`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/den.nix#L14) documents that diagrams' flake.packages contributions silently overwrite each other unless `den.flakeOutputs.packages` is imported. | **Missing typed output declaration/default trap.** Not evidence that the explicitly typed output path itself is broken. |
| AnonymousRand/nix_config | `583567f25d10` | [`modules/profiles/internal/ctx_from_entities.nix:4`](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/internal/ctx_from_entities.nix#L4) describes omitted profile defaults. [`modules/profiles/internal/ctx_from_entities.nix:15`](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/internal/ctx_from_entities.nix#L15) reports mkMerge problems, and [`modules/profiles/internal/ctx_from_entities.nix:17`](https://github.com/AnonymousRand/nix_config/blob/583567f25d101dba657fd1f72e4d10b179599dfc/modules/profiles/internal/ctx_from_entities.nix#L17) uses recursiveUpdate. | **Author's custom profile precedence workaround.** The author speculates about the cause, so do not promote it to an established den merge bug. |

**Den action implication:**

- Document module identity for diamond inclusion together with typed-vs-freeform merge boundaries.
- Add small tests for repeated inclusion, two plugin contributions, two package contributors and target option
  priorities.
- Consider actionable warnings or safer typed-output defaults where contribution loss is otherwise silent.
- Preserve an escape hatch for consumers that want native target-module merge semantics.

### 3. Typed settings and reusable namespace exports repeatedly touch traversal internals

**Recurrence:** 6 repositories: jasperro/dotfiles, redxtech/nixfiles, henriquekirchheck/nixos-flake,
sk4rd/mikos-den, DylanRJohnston/nixos, Le0-dot/config.nix. The first four are the same family of typed-settings
extension. The last two expose adjacent namespace/entity API boundaries.

| Repository | Revision | What the source shows | Classification |
|---|---|---|---|
| jasperro/dotfiles | `37a402659597` | [`modules/schema/settings.nix:15`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/schema/settings.nix#L15) imports `den.lib.aspects.fx.keyClassification`. [`modules/schema/settings.nix:18`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/schema/settings.nix#L18) excludes structural/class/quirk keys, and [`modules/schema/settings.nix:50`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/schema/settings.nix#L50) recursively builds settings submodules. | **Normal extension** coupled to implementation-shaped traversal APIs. |
| redxtech/nixfiles | `f0611199ba42` | [`modules/schema.nix:14`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L14) repeats that key-classification dependency. [`modules/schema.nix:34`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/schema.nix#L34) derives a nested settings schema. [`modules/host-settings.nix:7`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L7) and [`modules/host-settings.nix:8`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/modules/host-settings.nix#L8) manually pass settings/host into OS/HM. | **Normal extension plus argument bridging.** Not a demonstrated upstream defect. |
| henriquekirchheck/nixos-flake | `f9b5451633a4` | [`modules/aspects/settings/default.nix:2`](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/aspects/settings/default.nix#L2) reserves settings, and [`modules/aspects/settings/default.nix:5`](https://github.com/henriquekirchheck/nixos-flake/blob/f9b5451633a403b5381b7dbf7951a978f2ea7032/modules/aspects/settings/default.nix#L5) declares typed host settings. | **Supported extension seam.** The reservation itself is not misuse. |
| sk4rd/mikos-den | `de31f342886a` | [`modules/den.nix:13`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L13) explains that reserving settings prevents den from interpreting option declarations as aspects. [`modules/den.nix:14`](https://github.com/sk4rd/mikos-den/blob/de31f342886ae653aa46264d60587661476ea9b9/modules/den.nix#L14) reserves it. | **Same extension need,** with an explicit rationale. |
| DylanRJohnston/nixos | `505097f4d0fd` | [`modules/namespace.nix:11`](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/namespace.nix#L11) reports that strict re-import rejects exported navigation aliases. [`modules/namespace.nix:20`](https://github.com/DylanRJohnston/nixos/blob/505097f4d0fd9fe271bd1f5a75a6791564333b8f/modules/namespace.nix#L20) strips `__providesForwarded` entries. | **Reported namespace round-trip compatibility problem.** Not only custom settings machinery. |
| Le0-dot/config.nix | `4171c4b9f1f2` | [`modules/containers/schema.nix:8`](https://github.com/Le0-dot/config.nix/blob/4171c4b9f1f2ad0dbcab61f829cea31135064057/modules/containers/schema.nix#L8) imports entity lookup from `${inputs.den}/nix/lib/entities/_types.nix`. | **Internal API dependency** in a custom container entity extension. Not proof that the lookup result is incorrect. |

**Den action implication:**

- Offer or document a stable public "children vs metadata" traversal contract.
- Offer a typed-settings recipe or a small reusable helper.
- Offer a public entity-aspect lookup API.
- Test namespace export→import under strict mode, without consumers stripping implementation metadata.

Similar code in several repositories can share ancestry. The recurrence is demand/maintenance evidence. It is not six
independent discoveries of one bug.

### 4. Cross-host dataflow needs provenance, cardinality and dependency diagnostics

**Recurrence:** 3 repositories with distinct friction signals: Keyruu/shinyflakes, auscyber/dotfiles,
byte-sized-emi/nix-config. Two source-verified positive controls show working provenance usage: Gwenodai/nixos and
repparw/nix.

| Repository | Revision | What the source shows | Classification |
|---|---|---|---|
| Keyruu/shinyflakes | `021ee48343db` | [`modules/policies/services-collect.nix:22`](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/policies/services-collect.nix#L22) explicitly says that withProvenance could not be made to work. [`modules/policies/services-collect.nix:24`](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/modules/policies/services-collect.nix#L24) collects without it. | **Reported API difficulty.** No cause or failing expression is preserved here. |
| Gwenodai/nixos | `ab05d3c6e156` | **Positive control.** [`modules/policies/network-backends.nix:18`](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/policies/network-backends.nix#L18) applies withProvenance. [`modules/aspects/services/ssh.nix:25`](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/aspects/services/ssh.nix#L25)/[`modules/aspects/services/ssh.nix:28`](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/aspects/services/ssh.nix#L28) consume source/value respectively. | The named-host exclusion at [`modules/aspects/services/ssh.nix:34`](https://github.com/Gwenodai/nixos/blob/ab05d3c6e156b7651a1ec6ee874c553f71979734/modules/aspects/services/ssh.nix#L34) is an explicit local staging TODO, **not a den provenance failure**. |
| repparw/nix | `b2a680435a4e` | **Positive control.** [`modules/service-graph.nix:13`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/service-graph.nix#L13) applies withProvenance. [`modules/aspects/services/default.nix:16`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/aspects/services/default.nix#L16) reads the value, [`modules/aspects/services/default.nix:27`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/aspects/services/default.nix#L27) reads the source host, and [`modules/aspects/services/default.nix:33`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/aspects/services/default.nix#L33) checks duplicate names. | This establishes that provenance has working consumer patterns in the sampled revisions. |
| auscyber/dotfiles | `96be028eaba6` | [`aspects/framework/cross-host-dag.nix:21`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/framework/cross-host-dag.nix#L21) reports opaque infinite recursion without cycle identification. [`aspects/framework/cross-host-dag.nix:26`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/framework/cross-host-dag.nix#L26) builds a declaration-level guard. [`aspects/framework/cross-host-dag.nix:34`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/framework/cross-host-dag.nix#L34) reports that the author's sibling check incorrectly treats wrapped functors as nonfunctions. | **Two distinct things:** reported missing den diagnostics, and **author-owned ineffective validation**. Do not attribute the check bug to den. |
| byte-sized-emi/nix-config | `8df6aa42d1bb` | [`modules/auto-update.nix:20`](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/auto-update.nix#L20)/[`modules/auto-update.nix:21`](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/auto-update.nix#L21) use head after filtering by service name, without a local missing/multiple-provider check. | **Consumer robustness gap.** Not a failed pipe primitive. |

**Den action implication:**

- Ship paired producer/pipe/consumer examples that show the provenance entry shape.
- Provide reusable exactly-one/optional/many selection helpers with source-aware errors.
- Explore cycle/context tracing for cross-host config thunks. Clearly distinguish declaration over-approximation from
  a proven evaluation dependency cycle.
- Diagnose misuse. Do not claim that provenance itself is generally broken.

### 5. Battery defaults and class-routing conventions are not always discoverable during migration

**Recurrence:** 5 repositories: ivokun/kebun, arichtman/nix, byte-sized-emi/nix-config, elianiva/dotfiles,
Le0-dot/config.nix. This is mostly ergonomics and extension demand. It is weaker evidence of bugs than themes 1–2.

| Repository | Revision | What the source shows | Classification |
|---|---|---|---|
| ivokun/kebun | `1038ddc22989` | [`modules/users.nix:20`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L20)–[`modules/users.nix:23`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L23) deliberately avoids primary-user, because its networkmanager group is inappropriate for an iwd host. [`modules/users.nix:2`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L2)–[`modules/users.nix:6`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L6) explains that it uses _module.args because HM extraSpecialArgs belongs to the battery/osConfig. | **Intentional alternative policy and documented migration workaround.** Not misuse. |
| arichtman/nix | `a33136e4580d` | [`modules/den.nix:2`](https://github.com/arichtman/nix/blob/a33136e4580dd700bdf822e7a7314b475fbd0f11/modules/den.nix#L2) records uncertainty about importing den. [`modules/hosts.nix:21`](https://github.com/arichtman/nix/blob/a33136e4580dd700bdf822e7a7314b475fbd0f11/modules/hosts.nix#L21) complains about manually assigning the HM class. | **Author confusion.** Not proof that the assignment should be unnecessary. |
| elianiva/dotfiles | `44d6d212ab1d` | [`modules/_lib/identity.nix:18`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/_lib/identity.nix#L18) explicitly mirrors define-user's platform→home mapping. | **Local duplicated convention.** Reuse of the battery is an option only if its larger contract fits. |
| Le0-dot/config.nix | `4171c4b9f1f2` | [`modules/policies/define-user.nix:3`](https://github.com/Le0-dot/config.nix/blob/4171c4b9f1f2ad0dbcab61f829cea31135064057/modules/policies/define-user.nix#L3) supplies a systemManager branch alongside define-user at [`modules/policies/define-user.nix:12`](https://github.com/Le0-dot/config.nix/blob/4171c4b9f1f2ad0dbcab61f829cea31135064057/modules/policies/define-user.nix#L12). | **Normal new-class extension.** It shows where a class-aware extension recipe would help. |
| byte-sized-emi/nix-config | `8df6aa42d1bb` | Source-verified supporting instance. [`modules/den.nix:47`](https://github.com/byte-sized-emi/nix-config/blob/8df6aa42d1bbcc42b6a2b82447a26a340ce62655/modules/den.nix#L47) asks whether to add host-aspects. | A question about routing conventions, **not evidence that a missing include already broke that configuration**. |

**Den action implication:**

- Make battery side effects and ownership visible in a compact table: account creation, privilege/groups, HM class
  activation, host-aspects and reserved argument bridges.
- Show how to replace only one policy decision.
- Show how to extend account handling for another class.
- Explain the existing knobs before you broaden defaults that some adopters explicitly reject.

### Boundaries and caveats

- **Upstream reproduction candidates.** The strongest are standalone scope identity collisions, diamond list
  duplication, namespace strict round-tripping and freeform forwarding contribution loss. Each remains an
  author-reported source observation here. None was executed or confirmed against current upstream den.
- **Themes overlap deliberately.** One configuration can reveal both context and merge issues. Do not sum the
  recurrence counts into a count of broken repositories.
- **Legitimate extensions.** Constructor overrides, reserved settings keys, custom classes and manual argument passing
  are legitimate extensions. They become API/documentation signals when they repeat. Their existence alone is not a
  defect.
- **Excluded as den friction:** stale READMEs, hardware rfkill fixes, private repositories, unrelated runtime bugs and
  ordinary overrideable presets. For example, the Btrfs/Bluetooth/locale policy examples in reviews do not justify
  upstream den bug claims.
- **Heterogeneous sources.** The sources are at different revisions and den pins. A workaround can be obsolete
  upstream. The action implications are investigation/documentation proposals, not promises of an unimplemented
  feature.

## Reviewed public target inventory

All 98 public entries have source-led census records. The included public counts cover 93 entries, after the audit
excludes Yen, with-inputs and three namespace libraries.

How the table is built:

- The counts come from the reviewed declarations, not from the mechanical mentions or the earlier lower bounds in
  [Platform and extension coverage](#platform-and-extension-coverage-historical).
- Grouping deduplicates repositories by id, and targets by `(id, target key)`. Rows split by kind/class/system.
- Architecture rows overlap at repository level.
- Home and package rows do not add machines.
- [Census coverage](/census/coverage.tsv) distinguishes partial package inventories from genuinely missing/private
  inventories.

| target kind | class | declared system | repositories | known declared targets |
|---|---|---|---:|---:|
| home | homeManager | aarch64-darwin | 7 | 7 |
| home | homeManager | aarch64-linux | 4 | 7 |
| home | homeManager | x86_64-linux | 21 | 30 |
| host | darwin | aarch64-darwin | 31 | 40 |
| host | darwin | x86_64-darwin | 1 | 1 |
| host | esphome | esp32-idf | 1 | 1 |
| host | ios | aarch64-ios | 1 | 1 |
| host | nixOnDroid | aarch64-linux | 2 | 2 |
| host | nixbsd | x86_64-freebsd | 1 | 1 |
| host | nixos | aarch64-linux | 18 | 27 |
| host | nixos | unknown | 1 | 2 |
| host | nixos | x86_64-linux | 80 | 248 |
| host | systemManager | x86_64-linux | 1 | 1 |
| package | nvf | unknown | 1 | 1 |
| package | nvim | aarch64-darwin | 1 | 1 |
| package | nvim | aarch64-linux | 1 | 1 |
| package | nvim | x86_64-linux | 1 | 1 |
| package | package | aarch64-darwin | 4 | 5 |
| package | package | aarch64-linux | 5 | 12 |
| package | package | x86_64-darwin | 1 | 1 |
| package | package | x86_64-linux | 9 | 17 |

Software adoption and per-repository breadth are in [the complete census summary](/census/summary/). See also
the [source evidence](/census/software.tsv), the [target inventory](/census/targets.tsv) and the
[breadth](/census/breadth.tsv) files.

- The census distinguishes AeroSpace on Darwin, Niri/Hyprland on NixOS, editor frontends, multiplexers and shells.
- Configured/default, enable-only, installation-only and unresolved selections remain distinguishable.
- The counts concern declared configuration. They do not show successful evaluation, runtime use or distinct humans.

## Platform and extension coverage (historical)

This section is retained evidence from mechanical signals. It includes the excluded Yen.

- **Scope: 98/98 public entries.** The selection is only `extract/<id>.json` → `source == "public"`.
- **Classification.** The matching review front matter classifies **91/98 as den configs** and **7/98 as
  non-configs**.
- **Excluded:** local/archive entries, sini and all pilot artifacts. No scores are included.
- **Counting.** Every count is a set of repository IDs. It is never a sum of occurrences, hosts or services.
- **Overlap.** Categories overlap. Do not add the platform, class, operations and tooling totals.
- **Citations.** Source citations below are relative to each repository root at its reviewed revision.

### Exact mechanical signals

**These columns measure source mentions/signals, not actual instantiated support.** The first denominator is always
the 98 public entries. The second is the 91 classified configs. The final column is the contribution from the 7
non-config entries.

| Signal | Public /98 | Configs /91 | Non-configs /7 | Exact predicate |
|---|---:|---:|---:|---|
| system:x86_64-linux | 94 | 87 | 7 | `systems_mentioned[key] > 0` |
| system:aarch64-linux | 54 | 50 | 4 | `systems_mentioned[key] > 0` |
| system:x86_64-darwin | 20 | 18 | 2 | `systems_mentioned[key] > 0` |
| system:aarch64-darwin | 45 | 42 | 3 | `systems_mentioned[key] > 0` |
| flag:darwin | 48 | 45 | 3 | `platform_flags[key] == true` |
| flag:standalone_home | 24 | 23 | 1 | `platform_flags[key] == true` |
| flag:wsl | 12 | 12 | 0 | `platform_flags[key] == true` |
| flag:microvm | 3 | 3 | 0 | `platform_flags[key] == true` |
| extension:microvm | 7 | 6 | 1 | `extensions[key] > 0` |
| customclasses_extracted | 8 | 7 | 1 | `den_classes_declared` nonempty |
| extension:terranix | 4 | 3 | 1 | `extensions[key] > 0` |
| extension:nixidy/argocd | 7 | 7 | 0 | `extensions[key] > 0` |
| extension:kubernetes | 1 | 0 | 1 | `extensions[key] > 0` |
| extension:containers | 25 | 25 | 0 | `extensions[key] > 0` |
| extension:deploy-rs | 16 | 14 | 2 | `extensions[key] > 0` |
| extension:colmena | 7 | 6 | 1 | `extensions[key] > 0` |
| extension:nixos-anywhere | 13 | 11 | 2 | `extensions[key] > 0` |
| extension:topology | 1 | 1 | 0 | `extensions[key] > 0` |
| secrets | 58 | 56 | 2 | `secrets` nonempty |

`flag:aarch64_linux` gives the same 54/98, 50/91, 4/7 counts as `system:aarch64-linux`. It is not an independent
confirmation.

Exact-input-name signals:

| Exact member of `inputs` | Public /98 | Configs /91 | Non-configs /7 |
|---|---:|---:|---:|
| nix-on-droid | 3 | 3 | 0 |
| droidspaces | 1 | 1 | 0 |
| agenix | 11 | 11 | 0 |
| agenix-rekey | 4 | 4 | 0 |
| sops-nix | 47 | 45 | 2 |
| deploy-rs | 12 | 11 | 1 |
| terranix | 2 | 2 | 0 |
| microvm | 3 | 3 | 0 |

Source files and cross-checks:

- The source files are `extract/<id>.json:1` (one JSON record each). They are cross-checked against the `<id>` front
  matter.
- Example: `extract/vic/yen.json:1` contains many extension signals, but `vic/yen` classifies the repository as
  non-config.
- `corpus.jsonl` was not mixed with local/archive records. It is an alternate mechanical corpus, not evidence of
  successful instantiation.

### Reviewed lower bounds: targets/configuration, not successful instantiation

An evaluated-output census is **unavailable**: this synthesis ran no Nix evaluations. The table gives deliberately
curated, named **lower bounds**. They come from reviews plus source declarations/consumers at their extract revision.

- They establish static declared/wired target or configuration presence.
- They do not establish successful evaluation, builds, deployment, current maintenance or exhaustive support.
- All members are inside the 91-config subset. So the same numerator applies to `/98` and `/91`.
- Empty verified membership means unknown/unestablished. It does not mean zero actual support.
- Each repo appears once per category.

| Inspected category | Source-backed lower bound /98 (also /91) | Named membership and evidence |
|---|---:|---|
| x86_64-linux | ≥10 | `EzT32/nixos` ([`modules/den.nix:14`](https://github.com/EzT32/nixos/blob/aa287213a56e8bf8b4229f233ad8d7e240449319/modules/den.nix#L14)); `Steven-S1020/Nixos-Configuration` ([`modules/hosts/deimos/deimos.nix:6`](https://github.com/Steven-S1020/Nixos-Configuration/blob/89fd086f61a5e3dec8a8b46e9a48b07f3dac5d3c/modules/hosts/deimos/deimos.nix#L6)); `SuNNjek/nixos-config` ([`modules/hosts.nix:4`](https://github.com/SuNNjek/nixos-config/blob/f40297e9d045387227869245163e7e2b6c7799f9/modules/hosts.nix#L4)); `ivokun/kebun` ([`modules/aspects.nix:219`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L219)); `nolvyn/nixos` ([`modules/aspects/hosts/weebmachine/weebmachine.nix:3`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/weebmachine/weebmachine.nix#L3)); `pdarulewski/dotfiles` ([`modules/hosts/nuno/default.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/nuno/default.nix#L2)); `phucisstupid/dotfiles` ([`modules/hosts/linux/main.nix:7`](https://github.com/phucisstupid/dotfiles/blob/0e80243bb07bb53e2cb1d118d8dfc7f127ea0b6c/modules/hosts/linux/main.nix#L7)); `repparw/nix` ([`modules/entities.nix:4`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/entities.nix#L4)); `rhedgeco/nix-config` ([`modules/hosts/hedgebox.nix:2`](https://github.com/rhedgeco/nix-config/blob/fd875038e37fd1ab893ae25695fde8a9992cea47/modules/hosts/hedgebox.nix#L2)); `sm-f/nix` ([`modules/den.nix:8`](https://github.com/sm-f/nix/blob/23820eea5e00f8b1d7faab4a9c3ce43603f78b52/modules/den.nix#L8)) |
| aarch64-linux | ≥7 | `Aor-Li/Infra` ([`modules/inventory.nix:41`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/inventory.nix#L41)); `augustocdias/nixos` ([`modules/hosts.nix:14`](https://github.com/augustocdias/nixos/blob/494e352fa63d971d36e54641c6d8293ebed1dd92/modules/hosts.nix#L14)); `clemak27/homelab` ([`modules/hosts/hosts.nix:3`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/hosts/hosts.nix#L3)); `cfrenette/nixos-config` ([`modules/hosts.nix:10`](https://github.com/cfrenette/nixos-config/blob/af711691cde33c23754da2d6dc81a7ae52bc5e7c/modules/hosts.nix#L10)); `loystonpais/lunar` ([`modules/hosts.nix:32`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/hosts.nix#L32)); `mio-19/config-public` ([`modules/hosts.nix:31`](https://github.com/mio-19/config-public/blob/a269164a1be6a90eecb533f54d362e2d2bdef629/modules/hosts.nix#L31)); `repparw/nix` ([`modules/entities.nix:19`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/entities.nix#L19)) |
| aarch64-darwin | ≥10 | `Aor-Li/Infra` ([`modules/inventory.nix:22`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/inventory.nix#L22)); `motheki/nix` ([`modules/inventory/hosts.nix:4`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/inventory/hosts.nix#L4)); `mrbandler/nix` ([`modules/hosts/hermes.nix:2`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/modules/hosts/hermes.nix#L2)); `nolvyn/nixos` ([`modules/aspects/hosts/astraeus/astraeus.nix:3`](https://github.com/nolvyn/nixos/blob/e0fd0f9f0537a28b68ee802a75051f719a2af203/modules/aspects/hosts/astraeus/astraeus.nix#L3)); `pdarulewski/dotfiles` ([`modules/hosts/akari/default.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/akari/default.nix#L2)); `phucisstupid/dotfiles` ([`modules/hosts/phucs-MacBook-Air/main.nix:7`](https://github.com/phucisstupid/dotfiles/blob/0e80243bb07bb53e2cb1d118d8dfc7f127ea0b6c/modules/hosts/phucs-MacBook-Air/main.nix#L7)); `quasi-coherent/nix-config` ([`modules/my/configurations.nix:4`](https://github.com/quasi-coherent/nix-config/blob/52971feef21f5769354ae2359dbc598d2623aab4/modules/my/configurations.nix#L4)); `raphaelladinig/dotfiles` ([`modules/hosts/default.nix:3`](https://github.com/raphaelladinig/dotfiles/blob/f29658d31d046b1dc155bb57d00f8d7155a59a2d/modules/hosts/default.nix#L3)); `trash-panda-v91-beta/dots.factory` ([`modules/den.nix:5`](https://github.com/trash-panda-v91-beta/dots.factory/blob/04ed8728916414ec0bbcfa4b35e3b14c91db8816/modules/den.nix#L5)); `scoiatael/dotfiles` ([`modules/aspects/lsair.nix:7`](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lsair.nix#L7)) |
| x86_64-darwin | ≥1 | `pdarulewski/dotfiles` ([`modules/hosts/inazuma/default.nix:2`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/hosts/inazuma/default.nix#L2)) |
| standalone_home | ≥13 | `Aor-Li/Infra` ([`modules/inventory.nix:63`](https://github.com/Aor-Li/Infra/blob/87405e2c8b133c2c341a50a0aebeb7fd915db507/modules/inventory.nix#L63)); `Erastos/nixos-dotfiles` ([`parts/hosts.nix:8`](https://github.com/Erastos/nixos-dotfiles/blob/f2336347f41da991f4e371e10cd01864109b4687/parts/hosts.nix#L8)); `KGB33/.dotfiles` ([`modules/den.nix:6`](https://github.com/KGB33/.dotfiles/blob/851fb5b43c9e57a1fc5dfff6169b33b960a40932/modules/den.nix#L6)); `adanoelle/fern` ([`modules/hosts.nix:12`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L12)); `andreshungbz/nixconfig` ([`modules/homes/andreshung.nix:4`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/homes/andreshung.nix#L4)); `arichtman/nix` ([`modules/hosts.nix:5`](https://github.com/arichtman/nix/blob/a33136e4580dd700bdf822e7a7314b475fbd0f11/modules/hosts.nix#L5)); `danielgafni/nixos` ([`modules/den.nix:114`](https://github.com/danielgafni/nixos/blob/26f03bc416ad2535ff4cdf52a1d8cb9ead4b8fd6/modules/den.nix#L114)); `elianiva/dotfiles` ([`modules/hosts.nix:25`](https://github.com/elianiva/dotfiles/blob/44d6d212ab1deb2b7285a83244ff15aa20e32869/modules/hosts.nix#L25)); `quasi-coherent/nix-config` ([`modules/my/configurations.nix:3`](https://github.com/quasi-coherent/nix-config/blob/52971feef21f5769354ae2359dbc598d2623aab4/modules/my/configurations.nix#L3)); `scoiatael/dotfiles` ([`modules/aspects/lsair.nix:8`](https://github.com/scoiatael/dotfiles/blob/b1b3cc10eef10161c924085b6946b7a9b1d32ad4/modules/aspects/lsair.nix#L8)); `SyahrulBhudiF/dotfiles` ([`modules/den.nix:5`](https://github.com/SyahrulBhudiF/dotfiles/blob/ba537827987edc4e00a574d1748d37a34a3b69ff/modules/den.nix#L5)); `vodfsh/nixos-config` ([`modules/entities.nix:7`](https://github.com/vodfsh/nixos-config/blob/a0ff916b0b31a66554323355f9557b7e4c223eff/modules/entities.nix#L7)); `talarys/den` ([`modules/users/talarys.nix:6`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/users/talarys.nix#L6)) |
| wsl | ≥10 | `Occhima/nix-conf` ([`modules/den/hosts.nix:26`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/hosts.nix#L26)); `acrobertson/infra` ([`modules/hosts/hodor.nix:8`](https://github.com/acrobertson/infra/blob/05a8582100fb93d1de94b5119cc5dddc86f4ba45/modules/hosts/hodor.nix#L8)); `anders130/dotfiles` ([`hosts/wsl/default.nix:9`](https://github.com/anders130/dotfiles/blob/470c551356c8ccc92421f2d863cc0c15058df035/hosts/wsl/default.nix#L9)); `cfrenette/nixos-config` ([`modules/hosts/wsl.nix:8`](https://github.com/cfrenette/nixos-config/blob/af711691cde33c23754da2d6dc81a7ae52bc5e7c/modules/hosts/wsl.nix#L8)); `eugencowie/dotfiles` ([`modules/hosts/inspiron-16.nix:4`](https://github.com/eugencowie/dotfiles/blob/64dbfad5d9ca500edd0043e51502172bac37d7d7/modules/hosts/inspiron-16.nix#L4)); `jasperro/dotfiles` ([`modules/hosts/tinkpet-wsl/tinkpet-wsl.nix:10`](https://github.com/jasperro/dotfiles/blob/37a402659597ba8c5de5fad89c5d4c91e5f58926/modules/hosts/tinkpet-wsl/tinkpet-wsl.nix#L10)); `jkopano/nixiak` ([`modules/wsl.nix:24`](https://github.com/jkopano/nixiak/blob/97bf0689bb4d587a51199058a7ee2c89f5d4c204/modules/wsl.nix#L24)); `klchen0112/dotfiles` ([`modules/hosts/wsl/default.nix:28`](https://github.com/klchen0112/dotfiles/blob/d47908159f3eb13c9056ce5a0620b875f67f4579/modules/hosts/wsl/default.nix#L28)); `talarys/den` ([`modules/hosts/void.nix:11`](https://github.com/talarys/den/blob/469df2c2de88614d17a0f557cb19eaaa18ed0415/modules/hosts/void.nix#L11)); `thomasgoulet/nixnites` ([`nix/hosts/oric.nix:4`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/hosts/oric.nix#L4)) |
| microvm_configured_guest_or_pipeline | ≥2 | `nazarewk-iac/nix-configs` ([`hosts/brys/default.nix:260`](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/hosts/brys/default.nix#L260)); `hmajid2301/nixicle` ([`modules/aspects/services/tangled.nix:156`](https://github.com/hmajid2301/nixicle/blob/ca0d927add737601fcc3c1a6a1cf84a497b0b9c0/modules/aspects/services/tangled.nix#L156)) |
| custom_class_use | ≥6 | `auscyber/dotfiles` ([`aspects/framework/esphome/default.nix:104`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/framework/esphome/default.nix#L104)); `JoonasKajava/nvf-config` ([`modules/nvf-integration.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L32)); `Le0-dot/config.nix` ([`modules/containers/schema.nix:36`](https://github.com/Le0-dot/config.nix/blob/4171c4b9f1f2ad0dbcab61f829cea31135064057/modules/containers/schema.nix#L36)); `r17x/universe` ([`nix/nvim.nix/default.nix:70`](https://github.com/r17x/universe/blob/f8bc64a503b4f09b8eb325d07a5e1b37e6a49cc7/nix/nvim.nix/default.nix#L70)); `sonntag/nix` ([`modules/nixible/playbooks.nix:66`](https://github.com/sonntag/nix/blob/816947c6a2707def93b5f5070e5420a6abac7bb1/modules/nixible/playbooks.nix#L66)); `Occhima/nix-conf` ([`modules/den/hosts.nix:6`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/hosts.nix#L6)) |
| device_classes_esphome_ios | ≥1 | `auscyber/dotfiles` ([`aspects/framework/mobile/default.nix:84`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/framework/mobile/default.nix#L84)) |
| nix_on_droid_target | ≥1 | `Occhima/nix-conf` ([`modules/den/hosts.nix:13`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/hosts.nix#L13)) |
| droidspaces_nixos_target | ≥1 | `loystonpais/lunar` ([`modules/hosts/vili/vili.nix:16`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/hosts/vili/vili.nix#L16)) |
| kubernetes_cluster_configuration | ≥1 | `clemak27/homelab` ([`modules/aspects/k3s/server.nix:8`](https://github.com/clemak27/homelab/blob/a8bb1c3f0fec737ab49636845df4d03374004057/modules/aspects/k3s/server.nix#L8)) |
| nixidy_argocd_manifest_target | none established; actual count unknown | none |
| explicit_terranix_configuration_call | ≥1 | `Keyruu/shinyflakes` ([`packages/tf.nix:12`](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/packages/tf.nix#L12)) |
| deploy_configuration | ≥3 | `auscyber/dotfiles` ([`aspects/tooling/deploy.nix:23`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/tooling/deploy.nix#L23)); `moxie0420/dotfiles` ([`modules/deploy-rs.nix:13`](https://github.com/moxie0420/dotfiles/blob/42df6003db8cf97408656e9fef28d66459c3c8eb/modules/deploy-rs.nix#L13)); `repparw/nix` ([`modules/deploy.nix:207`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/deploy.nix#L207)) |
| entity_driven_secret_wiring | ≥3 | `auscyber/dotfiles` ([`aspects/security/agenix-rekey.nix:263`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/security/agenix-rekey.nix#L263)); `soriPhoono/homelab` ([`modules/sops.nix:29`](https://github.com/soriPhoono/homelab/blob/c6599b697b933728d67088cf3ab9197a07d9d8f1/modules/sops.nix#L29)); `voidlily/dotfiles` ([`modules/agenix.nix:59`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L59)) |
| entity_driven_builders | ≥1 | `auscyber/dotfiles` ([`aspects/base/builders.nix:121`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/builders.nix#L121)) |
| entity_driven_deploy | ≥1 | `auscyber/dotfiles` ([`aspects/tooling/deploy.nix:23`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/tooling/deploy.nix#L23)) |

### Interpretation of extension bounds

| Bound | Interpretation |
|---|---|
| `custom_class_use` | It includes six demonstrated contracts: NVF, container runtimes, Nixvim, nixible playbooks, ESPHome/iOS and nix-on-droid. This is broader than nonstandard *host outputs*: editor/routed classes are not additional operating systems. The six are not an exhaustive custom-class census. |
| `device_classes_esphome_ios` | **One repo**, auscyber, with two classes. Do not count it twice. Its ESPHome target is explicit ([`aspects/hosts/dyson.nix:360`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/hosts/dyson.nix#L360)). iOS supplies an explicit instantiator/output ([`aspects/hosts/iphone.nix:44`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/hosts/iphone.nix#L44)). |
| `nix_on_droid_target` | A dedicated den class/output in Occhima ([`modules/den/hosts.nix:6`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/den/hosts.nix#L6)). Lunar's Droidspaces target is a NixOS module import on its ARM host instead (`modules/hosts/vili/vili.nix:16`). Android development packages or Waydroid enablement alone do not establish a nix-on-droid output. |
| MicroVM | The bound means declared guests or a configured guest-execution pipeline. It does **not** mean a standalone microvm den class. nazarewk declares `microvm.vms.nbt-1` (`hosts/brys/default.nix:260`). hmajid configures Spindle's microvm pipeline and resource limits (`modules/aspects/services/tangled.nix:156`). |
| Terranix | Keyruu directly calls the output constructor ([`packages/tf.nix:12`](https://github.com/Keyruu/shinyflakes/blob/021ee48343db2893c2a041a49690e92896352e82/packages/tf.nix#L12)) beside den. So this is not evidence of a terranix den class. icebluerabbit has a network entity ([`modules/inventory.nix:88`](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/inventory.nix#L88)), Terranix fragments ([`modules/infra/options.nix:110`](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/infra/options.nix#L110)) and an imported external network adapter ([`modules/dendritic.nix:7`](https://github.com/icebluerabbit/nixos/blob/21a704b338c359686fa4b1a9d45ac3cdb81ba81d/modules/dendritic.nix#L7)). We did not trace the complete adapter-to-output instantiation, so it is not added to the constructor lower bound. |
| Kubernetes | clemak configures a k3s server/agents through den namespace aspects (`modules/aspects/k3s/server.nix:8`, `modules/hosts/hl-server.nix:11`). This is a NixOS cluster configuration, not a nixidy/ArgoCD manifest output. This limited verification established no such manifest target. |
| Deployment | The bound includes both generated and manually named deploy nodes. auscyber maps generated NixOS configurations ([`aspects/tooling/deploy.nix:23`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/tooling/deploy.nix#L23)). moxie names theHub directly (`modules/deploy-rs.nix:13`). repparw adds named activation overrides ([`modules/deploy.nix:207`](https://github.com/repparw/nix/blob/b2a680435a4e1c3451e76b73ed361f064029ab88/modules/deploy.nix#L207)). Do not label all three as automatically generated from den host data. |
| Secrets | Secret-tool signals do not prove per-aspect generators/rekey automation. The three verified examples differ. auscyber routes/generated scoped credentials ([`aspects/security/agenix-rekey.nix:263`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/security/agenix-rekey.nix#L263), [`aspects/base/celler/_lib.nix:180`](https://github.com/auscyber/dotfiles/blob/96be028eaba642d74c7e1ed19db00fe4b41356ca/aspects/base/celler/_lib.nix#L180)). sori maps source paths from identities (`modules/sops.nix:33`, `modules/sops.nix:42`). voidlily derives OS/HM rekey directories ([`modules/agenix.nix:59`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/agenix.nix#L59)). We did not check runtime secret decryption availability. |

### Correction examples and common overclaims

| Overclaim | Example and evidence |
|---|---|
| **ARM mention ≠ ARM host** | motheki has a Darwin inventory ([`modules/inventory/hosts.nix:4`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/inventory/hosts.nix#L4)) and an ARM Linux builder setting ([`modules/aspects/features/linux-builder.nix:6`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/aspects/features/linux-builder.nix#L6)). Both legitimately produce architecture mentions, with different target meanings. fern explicitly parks its ARM machine ([`adanoelle/fern/modules/hosts.nix:29`](https://github.com/adanoelle/fern/blob/060cd42a3d02a833bcd63a4148df09c18fc7810a/modules/hosts.nix#L29); the repo prefix is shown here only to identify its clone). |
| **Darwin mention ≠ Darwin host** | redxtech's extract has Darwin strings (`extract/redxtech/nixfiles.json:1`), but the described fleet is three Linux systems ([`redxtech/nixfiles/readme.md:9`](https://github.com/redxtech/nixfiles/blob/f0611199ba4295b2e7cdb9a9b1adad9fbfd0fca9/readme.md#L9)). We infer no Darwin target from that mechanical signal. |
| **Standalone flag can miss a real declaration** | quasi has `den.homes` in its inventory ([`quasi-coherent/nix-config/modules/my/configurations.nix:3`](https://github.com/quasi-coherent/nix-config/blob/52971feef21f5769354ae2359dbc598d2623aab4/modules/my/configurations.nix#L3)), but its extracted standalone flag is false (`extract/quasi-coherent/nix-config.json:1`). The verified bound is not limited to flag-positive entries. |
| **MicroVM signals vary sharply** | Lunar's occurrence is an interface matching string, not a VM target ([`loystonpais/lunar/modules/hosts/roglaptop/roglaptop.nix:84`](https://github.com/loystonpais/lunar/blob/5f836c9e4a1c3076e95f7df3969a77da051b6b2e/modules/hosts/roglaptop/roglaptop.nix#L84)). Occhima exposes an imported host-module feature ([`Occhima/nix-conf/modules/nixos/virtualisation/microvm/config.nix:11`](https://github.com/Occhima/nix-conf/blob/201ebbb670748352f2ac67f0e0a4c9775c7a5099/modules/nixos/virtualisation/microvm/config.nix#L11)), but no guest is established here. r17x labels its module an example and documents a non-working nested-host limitation ([`r17x/universe/nix/configurations/nixos/vm.nix:1`](https://github.com/r17x/universe/blob/f8bc64a503b4f09b8eb325d07a5e1b37e6a49cc7/nix/configurations/nixos/vm.nix#L1), [`r17x/universe/nix/configurations/nixos/vm.nix:5`](https://github.com/r17x/universe/blob/f8bc64a503b4f09b8eb325d07a5e1b37e6a49cc7/nix/configurations/nixos/vm.nix#L5)). |
| **All seven nixidy/argocd signals inspected are CLI packages/comments,** not manifest outputs | KGB33 ([`KGB33/homelab/nixos/nix/devshell.nix:19`](https://github.com/KGB33/homelab/blob/6ee44f24e022c95d0f8010fa63616e5366d20dbf/nixos/nix/devshell.nix#L19)), danielgafni ([`danielgafni/nixos/modules/aspects/users/dan.nix:67`](https://github.com/danielgafni/nixos/blob/26f03bc416ad2535ff4cdf52a1d8cb9ead4b8fd6/modules/aspects/users/dan.nix#L67)), eldios ([`eldios/dotfiles/modules/aspects/dev/_cli/packages_common_cli.nix:66`](https://github.com/eldios/dotfiles/blob/ce9d9573891ec0460a23da535166ab6455c0586e/modules/aspects/dev/_cli/packages_common_cli.nix#L66)), nazarewk ([`nazarewk-iac/nix-configs/modules/den/aspects/dev-k8s.nix:128`](https://github.com/nazarewk-iac/nix-configs/blob/a1a10f5c82721c402c8df10edd58145c8fc6f106/modules/den/aspects/dev-k8s.nix#L128)), pdarulewski ([`pdarulewski/dotfiles/modules/features/cli.nix:27`](https://github.com/pdarulewski/dotfiles/blob/97a47bb048adbc576160d1ee04de55698a0064a0/modules/features/cli.nix#L27)), thomasgoulet ([`thomasgoulet/nixnites/nix/features/infra.nix:23`](https://github.com/thomasgoulet/nixnites/blob/54d53d7979ed9e712aa725c5ca06dfce98398691/nix/features/infra.nix#L23)), voidlily ([`voidlily/dotfiles/modules/dev/k8s.nix:16`](https://github.com/voidlily/dotfiles/blob/ef20abb997bd0c7cd5b127834dfcd18f959fc4dc/modules/dev/k8s.nix#L16)). |
| **Custom declaration extraction is incomplete** | Joonas' vim→NVF class bridge is explicit ([`JoonasKajava/nvf-config/modules/nvf-integration.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L32)), but the extract's declared-class list is empty (`extract/JoonasKajava/nvf-config.json:1`). Schema extensions alone do not count as class targets. |
| **Declared output ≠ public reproducibility** | nifoc imports a private module tree unconditionally ([`nifoc/dotfiles/flake.nix:9`](https://github.com/nifoc/dotfiles/blob/387a13d9abfe831aac5e8b27d9c567d3d4fbe337/flake.nix#L9)). A private SSH git submodule supplies it ([`nifoc/dotfiles/.gitmodules:3`](https://github.com/nifoc/dotfiles/blob/387a13d9abfe831aac5e8b27d9c567d3d4fbe337/.gitmodules#L3)). That is a source/access prerequisite, separate from runtime secret decryption. mrbandler's README distinguishes active Darwin from unported Linux ([`mrbandler/nix/README.md:13`](https://github.com/mrbandler/nix/blob/6869a203c3fc4e605eaebefc2c760b7096b8fc66/README.md#L13)). |

### Non-config entries: denominator and contamination

These seven entries remain in the historical mechanical-evidence denominator **98**. They are outside the config
denominator **91**. Yen, with-inputs and the three namespace libraries are now excluded from current corpus counts.
The namespace libraries have a separate [library-audit track](/libraries/). All seven rows below remain
historical classification evidence.

| Entry | Classification | Page |
|---|---|---|
| `FastTrackStudios/task` | application packaging; the den example is inactive | [FastTrackStudios/task](/configs/fasttrackstudios/task/); see its §1 source citations |
| `adanoelle/garden-shell` | exported aspect/package library | [adanoelle/garden-shell](/libraries/adanoelle/garden-shell/); see its §1 source citations |
| `crocuda/crocuda.nixos` | exported server modules and consumer templates | [crocuda/crocuda.nixos](/libraries/crocuda/crocudanixos/); see its §1 source citations |
| `crocuda/normal.nixos` | exported desktop modules and consumer templates | [crocuda/normal.nixos](/libraries/crocuda/normalnixos/); see its §1 source citations |
| `denful/with-inputs` | input-resolution library with den templates | `denful/with-inputs`; see its §1 source citations |
| `fmway/infra` | Clan-primary infrastructure; the den hosts are explicitly debug/fake | [fmway/infra](/configs/fmway/infra/); see its §1 source citations |
| `vic/yen` | logic/fleet library with documentation fixtures | `vic/yen`; see its §1 source citations |

Do not read `den_fork_vic` as "this repository is a fork of den". That mechanical field records the input owner/pin
convention. The seven classifications above come from reviews, not from that flag.

### Measurement procedure and limits

- All work ran outside the clone directories.
- Trusted inline Python standard-library code read JSON/front matter, formed ID sets and calculated counts.
- Read-only `git -C <clone> rev-parse HEAD` verified all 91 config revisions.
- Probes used `rg --files`, `rg -n` and numbered static file reads.
- No Nix commands, repository code, clone setup, decryption, staging or commits ran.

Reproduction core:

```python
public = [json.loads(p.read_text()) for p in Path("extract").glob("*.json")
          if json.loads(p.read_text()).get("source") == "public"]
assert len(public) == 98
# Per metric, construct {e["id"] for e in public if predicate(e)}.
# Split that set using reviews/<id>.md is_den_config front matter.
# systems_mentioned.get(key, 0) > 0; platform_flags.get(key, False) is True;
# extensions.get(key, 0) > 0; bool(den_classes_declared); bool(secrets).
```

The lower bounds are not estimates of the remainder. An unverified target stays unknown. The source-led census
supersedes these platform lower bounds as its inventory becomes complete.

## Starter-template candidates

These are teaching sources to adapt. They are not claims that it is safe or reproducible to copy the whole
repository.

| use | source | reason and required adaptation |
|---|---|---|
| Cross-platform baseline | amatos/magnanix | It explains class-specific contributions and immutable-account prerequisites ([`modules/den/base.nix:39`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L39), [`modules/den/base.nix:49`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/base.nix#L49)). Replace the host identities and the checkout default ([`modules/den/repo-dir.nix:11`](https://github.com/amatos/magnanix/blob/7675475f050939b2606e5c4d0d0205c25ac18cfd/modules/den/repo-dir.nix#L11)). |
| Namespaces plus standalone HM | andreshungbz/nixconfig | Public/private namespace split ([`modules/den.nix:17`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/den.nix#L17)) and an explicit standalone home ([`modules/homes/andreshung.nix:4`](https://github.com/andreshungbz/nixconfig/blob/bdee3f6ec030ca92984814833e25c6f262c197bf/modules/homes/andreshung.nix#L4)). Replace the identity and hardware. Do not teach the declared-but-unverified firewall plumbing as a live dataflow example. |
| Small Darwin feature/profile/inventory layout | motheki/nix | Capability-only workstation profile ([`modules/aspects/profiles/workstation.nix:4`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/aspects/profiles/workstation.nix#L4)) and typed inventory projection ([`modules/inventory/access.nix:8`](https://github.com/motheki/nix/blob/e75e72ed08ccee4b62b4c2ac3aaa60b026eafef3/modules/inventory/access.nix#L8)). Add an introductory explanation of these boundaries. Do not confuse inventory visibility with authorization. |

A community library and a starter serve different needs:

- Tiny Bluetooth and audio leaves teach selection and class targeting.
- Settings traversal, custom classes, cross-host fact routing and operations are optional advanced lessons.
- A small clean config should not inherit a fleet's policies only because it has fewer aspects.

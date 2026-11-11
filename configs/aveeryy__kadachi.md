# aveeryy__kadachi

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/aveeryy__kadachi.md)

- Upstream: [aveeryy/kadachi](https://github.com/aveeryy/kadachi)
- Reviewed revision: [`ba03c6ede780`](https://github.com/aveeryy/kadachi/commit/ba03c6ede7801b46182399a78bbec1f041920e95)
- Author: aveeryy
- Score: **54.0 / 100**, rank 33 of 103 ranked configs. D 8 · I 8 · S 5 · R 5 · P 4 · L 2 · V 2 · O 7 · B 5 · X 2. Shortlists: showcase, library units (3).
- Summary: Showcase for the scoped cross-host Syncthing pipeline and explicit merge semantics. Library shortlist names closed namespace-rebindable units; starter withheld for sparse docs, private credentials and concrete settings/boundary defects.

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
This is a real den configuration despite zero extracted aspects: four namespaces are imported and host/user schema selects aspects from hosts (`dendritic.nix:28`, `defaults/misc.nix:12`). Generated import-tree scans the repository while excluding lib and flake.nix (`dendritic.nix:34`).

## 2. Common patterns
- namespace: adachi, kasane, megurine and hosts replace the literal den.aspects prefix (`dendritic.nix:28`).
- den.default includes define-user, host-aspects and mutual-provider via angle-bracket refs (`defaults/misc.nix:23`).
- provides tree: AMD CPU exposes a separate KVM contribution (`aspects/megurine/has/amd-cpu.nix:9`).

## 3. Novel patterns
The schema resolves each user aspect through the selected host’s users subtree, placing per-host identity composition under the host namespace (`defaults/misc.nix:16`).

Obsidian emits per-host vault paths through syncthingFolders (`aspects/kasane/programs/obsidian.nix:110`); a collectAll policy selects matching usernames with device IDs (`aspects/kasane/services/syncthing.nix:67`, `aspects/kasane/services/syncthing.nix:70`), is attached by the service aspect (`aspects/kasane/services/syncthing.nix:111`), and feeds generated Syncthing folders (`aspects/kasane/services/syncthing.nix:172`). This is active cross-host data flow, not just namespace organization.

## 4. Library candidates
- podman · `aspects/adachi/services/podman.nix:3` · **B**, rebind/register namespace; inputs standard NixOS config/pkgs; owns pruning, Docker socket, DNS and nftables-aware trusted interface selection (`aspects/adachi/services/podman.nix:11`, `aspects/adachi/services/podman.nix:16`).
- autofirma-firefox · `aspects/kasane/programs/autofirma.nix:12` · **B**, register/rebind namespace and retain declared autofirma-nix input; parameterized Firefox profile-name provider owns PKCS11 path from nixpkgs OpenSC (`aspects/kasane/programs/autofirma.nix:18`); actual minimal caller at `hosts/totsugeki/user.nix:26`.
- amd-cpu · `aspects/megurine/has/amd-cpu.nix:3` · firmware-sensitive microcode and opt-in kvm-amd provider · inputs: NixOS/nixpkgs, megurine namespace · parameterization: none; reads standard firmware enable option (`aspects/megurine/has/amd-cpu.nix:7`) · **B**, rebind namespace; provider keeps virtualization optional (`aspects/megurine/has/amd-cpu.nix:10`).

## 5. den friction
No verified den-specific friction in the namespace and entity-selection wiring (`dendritic.nix:28`, `defaults/misc.nix:12`).

## 6. Docs and complexity
Docs **2**: README defers documentation with Soon, though schema wiring and hardware modules carry comments (`README.md:8`, `dendritic.nix:27`). Complexity **4**: four namespaces and dynamic host/user aspect selection (`dendritic.nix:28`, `defaults/misc.nix:14`, `defaults/misc.nix:18`).

## 6a. Defects and scoring notes

- **S / moderate:** Syncthing folderOverrides accepts strings, while merge/filter consumption expects records with path/devices (`aspects/kasane/services/syncthing.nix:81`, `aspects/kasane/services/syncthing.nix:143`, `aspects/kasane/services/syncthing.nix:176`). Shared phone/network/client/player identities remain outside entity settings (`aspects/kasane/services/syncthing.nix:39`, `aspects/adachi/services/adguardhome.nix:93`, `lib/minecraft.nix:13`); grouped coverage is on S card.
- **P / moderate:** Hyprlock uses lib.optionals condition lib.mkOrder 1 list without grouping; false returns [] and then attempts to call that list (`aspects/kasane/desktop/hyprlock.nix:74`). False is the schema default (`aspects/kasane/desktop/config.nix:48`); the two current desktop hosts explicitly set true, so no selected-host failure is asserted (`hosts/mizuki/system.nix:10`, `hosts/totsugeki/system.nix:9`).
- **R / moderate:** Virtualisation grants libvirt rather than the pinned native libvirtd group (`aspects/adachi/programs/virtualisation.nix:15`, `flake.lock:749`); the [exact pinned native module](https://github.com/NixOS/nixpkgs/blob/55bfb4d7437bd4e09ab7cba58a43bd68eb310044/nixos/modules/virtualisation/libvirtd.nix#L443) creates libvirtd. The intended group grant misses that group; no evaluation or permission-failure result is asserted. Fastfetch references an unprovided personal logo (`aspects/kasane/programs/fastfetch.nix:11`). No extra deduction for an honest embedded-HM requirement or README baseline coverage.

## 7. Template notes
Useful advanced namespace layout; the mechanical zero is not evidence of absent den usage (`dendritic.nix:24`, `defaults/misc.nix:25`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Live cross-host folder channel: selected mizuki/totsugeki users include Obsidian and Syncthing (`hosts/mizuki/user.nix:16`, `hosts/mizuki/user.nix:23`, `hosts/totsugeki/user.nix:23`, `hosts/totsugeki/user.nix:33`) and declare device IDs (`hosts/mizuki/system.nix:33`, `hosts/totsugeki/system.nix:38`). Obsidian emits vault names, emitting host membership and per-host paths (`aspects/kasane/programs/obsidian.nix:110`); service includes a pipe.collectAll policy restricted to matching username/non-null device (`aspects/kasane/services/syncthing.nix:67`, `aspects/kasane/services/syncthing.nix:111`); consumer merges and selects host paths, then filters membership (`aspects/kasane/services/syncthing.nix:143`, `aspects/kasane/services/syncthing.nix:172`). Recursive merge explicitly deduplicates lists and resolves scalar collisions by last value (`lib/default.nix:96`). A second local quirk routes Git aliases into Zsh (`aspects/kasane/programs/git.nix:47`, `defaults/quirks.nix:3`, `aspects/kasane/zsh.nix:45`). 8 interpolates one substantial cross-host architecture plus a simpler local channel; malformed folder records are not validated, and separate WireGuard host iteration does not add routed-policy credit (`aspects/adachi/networking/kadachi-wg.nix:118`). Score **8**; confidence **high**.

### I

Scope · pros · cons/coverage: Four explicit namespaces organize system, user, hardware and host ownership (`dendritic.nix:28`); schema selects host and matching user branches (`defaults/misc.nix:14`, `defaults/misc.nix:18`), while per-host includes retain choices (`hosts/mizuki/user.nix:4`). Optional KVM is a provider, not forced by AMD microcode (`aspects/megurine/has/amd-cpu.nix:9`). 8 reflects these clean boundaries with a broad shared user/desktop baseline (`aspects/kasane/user.nix:14`, `aspects/megurine/is/desktop.nix:14`) rather than every concern independently documented/tested. Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Typed network, display, service-domain and backup contracts carry real host differences (`aspects/adachi/networking/config.nix:24`, `aspects/kasane/desktop/config.nix:3`, `aspects/adachi/services/config.nix:15`, `aspects/adachi/services/backups.nix:41`). Contract 5, rather than 7+, because Syncthing folderOverrides is attrsOf str but the consumer requires folder records (`aspects/kasane/services/syncthing.nix:81`, `aspects/kasane/services/syncthing.nix:143`, `aspects/kasane/services/syncthing.nix:176`). Verified grouped leaks 23: domain1, network sets2, DHCP clients5, private upstream1, interface selector1, external phone identity1, backup root1, shared author key/identity1, shared storage root1, Minecraft account IDs9 (`lib/constants.nix:3`, `aspects/adachi/services/adguardhome.nix:38`, `aspects/adachi/services/adguardhome.nix:65`, `aspects/adachi/services/adguardhome.nix:93`, `aspects/kasane/services/syncthing.nix:39`, `aspects/kasane/services/syncthing.nix:53`, `aspects/kasane/user.nix:34`, `aspects/adachi/services/koito.nix:31`, `lib/minecraft.nix:13`). Raw inventoried values exceed 30 before grouping; coverage cap 5, S=min(5,5). Public DNS/application presets, named host facts, overrideable Git email default and explicit secrets input contract are excluded. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":5,"distinct_leaks":23}}
```

### R

Scope · pros · cons/coverage: Complete Podman and AutoFirma/Firefox-PKCS11 integrations have closed native bodies under a standard registered namespace (`aspects/adachi/services/podman.nix:16`, `aspects/kasane/programs/autofirma.nix:18`), and AutoFirma has a real profile-name consumer (`hosts/totsugeki/user.nix:26`). Namespace rebinding makes these useful B units, anchor 5; the HTTP/backup suite additionally requires fleet schema and kadachi-lib (`lib/http.nix:33`, `lib/default.nix:33`). Fastfetch selects a personal logo file absent from the supplied assets, so that leaf is incomplete (`aspects/kasane/programs/fastfetch.nix:11`); no hidden editor source is credited as a reference (`defaults/nvim.nix:3`). Score **5**; confidence **medium**.

### P

Scope · pros · cons/coverage: The explicit scope is x86_64 Linux (`dendritic.nix:46`); optional WSL/Jovian projections guard presence of their native options (`defaults/classes.nix:11`, `defaults/classes.nix:36`), and WSL owns its import (`aspects/megurine/is/wsl.nix:10`). 4, below honest-scope baseline 5, because Hyprlock false/default branch calls the list returned by lib.optionals as a function (`aspects/kasane/desktop/hyprlock.nix:74`, `aspects/kasane/desktop/config.nix:48`). Current mizuki/totsugeki explicitly set true (`hosts/mizuki/system.nix:10`, `hosts/totsugeki/system.nix:9`); this is a disabled-setting boundary defect, not a claimed observed host failure. Embedded-HM osConfig coupling matches the visible scope (`aspects/kasane/services/syncthing.nix:158`). Score **4**; confidence **high**.

### L

Scope · pros · cons/coverage: README documentation is Soon (`README.md:8`); namespace meanings are explained (`README.md:19`) and individual leaves have useful descriptions (`aspects/megurine/is/steam-deck.nix:9`), but the default schema/projection and cross-host folder architecture have no newcomer walkthrough (`defaults/misc.nix:12`, `aspects/kasane/services/syncthing.nix:67`). Anchor 2: no wiring guide, rather than a size penalty. Score **2**; confidence **high**.

### V

Scope · pros · cons/coverage: No source-visible checks/CI or positive/negative composition fixture accompanies the generated import-tree output (`dendritic.nix:34`); README supplies no check workflow (`README.md:8`). Baseline 2. The guarded class definitions and declared types are defensive implementation, not tests (`defaults/classes.nix:11`, `aspects/adachi/networking/config.nix:24`); static reading makes no passing-evaluation claim. Score **2**; confidence **high**.

### O

Scope · pros · cons/coverage: Per-aspect secrets are emitted with host/user-derived paths and consumed by Syncthing (`aspects/kasane/services/syncthing.nix:115`, `aspects/kasane/services/syncthing.nix:158`), Miniflux templates (`aspects/adachi/services/miniflux.nix:19`, `aspects/adachi/services/miniflux.nix:36`) and base-user creation (`aspects/kasane/user.nix:26`, `aspects/kasane/user.nix:33`). Backup configuration derives archive names/repositories and service data paths from host/native facts (`lib/default.nix:32`, `aspects/adachi/services/forgejo.nix:61`, `aspects/adachi/services/backups.nix:41`); rebuild aliases interpolate host.name into NH targets (`defaults/nix.nix:34`, `aspects/kasane/zsh.nix:45`). 7 credits multiple derived operational concerns, with no visible comprehensive deploy/install/builder generator; credentials remain an explicit external input (`defaults/sops.nix:3`), not a reason to deny the live emissions. Score **7**; confidence **high**.

### X

Scope · pros · cons/coverage: Jovian, WSL and Noctalia classes forward into NixOS/HM option paths (`defaults/classes.nix:7`, `defaults/classes.nix:18`, `defaults/classes.nix:32`). Those are native host/home configuration, baseline 2; ordinary package forwarding for the separate editor profile is not a Den-driven non-host evaluation contract (`defaults/nvim.nix:12`). Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Selected/max-depth census yields 3.5 points, diversity grade 3: Zsh/Starship plus Hyprland, with external Neovim installation depth (`aspects/kasane/zsh.nix:18`, `aspects/kasane/zsh.nix:49`, `hosts/mizuki/user.nix:12`, `defaults/nvim.nix:12`). Complete reference inventory below has 13 app/integration units, grade 7, B=5. Libvirt-manager is excluded because its intended access group is misspelled (`aspects/adachi/programs/virtualisation.nix:15`, `flake.lock:749`). Standard namespace registration/rebinding is declared, not an outside fleet router (`dendritic.nix:28`); every counted body owns its packages/native wiring or explicit command/profile argument. Exclude bare enable/package leaves, MIME mapping helpers, custom-schema consumers, outside helper/asset/package dependencies, and broad inseparable multimedia/desktop bundles (`aspects/megurine/has/bluetooth.nix:4`, `aspects/kasane/programs/libreoffice.nix:6`, `aspects/kasane/programs/multimedia.nix:9`, `aspects/kasane/theme.nix:84`, `aspects/kasane/services/syncthing.nix:34`). Score **5**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":3.5,"diversity_grade":3,"reference_grade":7,"reference_units":[{"name":"ddcutil-i2c","evidence":"aspects/adachi/hardware/i2c.nix:7"},{"name":"ugreen-led-controller","evidence":"aspects/adachi/hardware/ugreen-led-controller.nix:69"},{"name":"fail2ban","evidence":"aspects/adachi/services/fail2ban.nix:8"},{"name":"podman","evidence":"aspects/adachi/services/podman.nix:16"},{"name":"printing-discovery","evidence":"aspects/adachi/services/printing.nix:7"},{"name":"samba","evidence":"aspects/adachi/services/samba.nix:6"},{"name":"autofirma-firefox","evidence":"aspects/kasane/programs/autofirma.nix:18"},{"name":"steam-mangohud","evidence":"aspects/kasane/gaming/steam.nix:7"},{"name":"kitty","evidence":"aspects/kasane/programs/kitty.nix:8"},{"name":"intel-graphics-microcode","evidence":"aspects/megurine/has/intel-cpu.nix:12"},{"name":"lanzaboote","evidence":"aspects/megurine/requires/secure-boot.nix:12"},{"name":"greetd-autologin","evidence":"aspects/adachi/system/greetd-autologin.nix:7"},{"name":"openssh-defaults","evidence":"defaults/ssh.nix:10"}]}}
```

**Total:** 54.0/100. **Shortlists:** showcase yes; library podman, autofirma-firefox, amd-cpu; starter no. Showcase for the scoped cross-host Syncthing pipeline and explicit merge semantics. Library shortlist names closed namespace-rebindable units; starter withheld for sparse docs, private credentials and concrete settings/boundary defects.

Overall pros:
- Live same-user cross-host folder policy with per-host paths and explicit merge behavior (`aspects/kasane/services/syncthing.nix:67`, `lib/default.nix:96`).
- Host differences use typed display/network/service contracts (`aspects/kasane/desktop/config.nix:3`, `aspects/adachi/networking/config.nix:24`).
- Secrets and backups derive actual service/user paths (`aspects/kasane/services/syncthing.nix:115`, `aspects/adachi/services/forgejo.nix:61`).

Overall cons / scope limits:
- Folder override type and record consumer disagree (`aspects/kasane/services/syncthing.nix:81`, `aspects/kasane/services/syncthing.nix:143`).
- Hyprlock false/default boundary applies a list as a function (`aspects/kasane/desktop/hyprlock.nix:74`).
- Shared client/player identity data and missing personal logo limit direct reuse (`aspects/adachi/services/adguardhome.nix:93`, `lib/minecraft.nix:13`, `aspects/kasane/programs/fastfetch.nix:11`).
- Documentation remains Soon and provides no check workflow (`README.md:8`).

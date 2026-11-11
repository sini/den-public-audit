# andreshungbz__nixconfig

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/andreshungbz__nixconfig.md)

- Upstream: [andreshungbz/nixconfig](https://github.com/andreshungbz/nixconfig)
- Reviewed revision: [`bdee3f6ec030`](https://github.com/andreshungbz/nixconfig/commit/bdee3f6ec030ca92984814833e25c6f262c197bf)
- Author: andreshungbz
- Score: **54.5 / 100**, rank 31 of 103 ranked configs. D 5 · I 8 · S 5 · R 5 · P 8 · L 5 · V 3 · O 5 · B 6 · X 2. Shortlists: starter, library units (1).
- Summary: Useful cross-platform namespace starter and application reference collection; entity-derived presentation is demonstrated, while the prepared firewall channel is not a live data-flow showcase.

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
Feature stacks live in named namespaces, with separate host and standalone-home inventories as the README explains (`README.md:3`). Den imports pkt and test namespaces with different visibility (`modules/den.nix:17`).

## 2. Common patterns
- namespace: pkt is exported while test is private (`modules/den.nix:17`, `modules/den.nix:18`).
- den.default includes define-user and mutual-provider via angle-bracket refs (`modules/defaults.nix:5`, `modules/defaults.nix:7`).
- homes (standalone HM): the same user profile is declared for two Linux architectures (`modules/homes/andreshung.nix:4`).

## 3. Novel patterns
The standalone identity explicitly replaces a user unavailable on some systems, sharing namespaced terminal/development stacks across architectures (`modules/homes/andreshung.nix:3`, `modules/homes/andreshung.nix:8`).

The networking aspect declares a firewall quirk and consumes its ports (`modules/aspects/desktop/components/nixos/networking.nix:3`, `modules/aspects/desktop/components/nixos/networking.nix:19`), but no emitter was verified in the reviewed tree. Treat this as prepared plumbing rather than established structured data flow.

## 4. Library candidates
- bluetooth · `modules/aspects/desktop/components/nixos/bluetooth.nix:2` · enables BlueZ and powers adapters on at boot · inputs: NixOS/nixpkgs plus a pkt namespace binding · parameterization: none (`modules/aspects/desktop/components/nixos/bluetooth.nix:5`) · **B**, rename/rebind pkt to the consumer namespace.

## 5. den friction
No verified den-specific friction in namespace, schema and standalone-home wiring (`modules/den.nix:17`, `modules/schemas.nix:3`, `modules/homes/andreshung.nix:4`).

## 6. Docs and complexity
Docs **4**: structure, installation and management commands are explained (`README.md:3`, `README.md:19`, `README.md:118`). Complexity **3**: shared stacks and architecture-specific homes without bespoke forward machinery in the reviewed entry points (`modules/homes/andreshung.nix:4`, `modules/defaults.nix:5`).

## 6a. Defects and scoring notes

- **S · moderate:** shared application configuration embeds account identity/checkout and physical-output assumptions instead of obtaining all of them through its consumer contract (`modules/aspects/apps/git.nix:15`, `modules/aspects/desktop/components/nix.nix:31`, `modules/aspects/desktop/niri/settings/outputs.nix:10`, `modules/aspects/desktop/noctalia-v5/config.toml:658`). Grouped coverage is recorded on the S card.
- Unused collector plumbing, documented architecture guards and lack of automated tests are anchor-coverage limits, not additional defects (`modules/aspects/desktop/components/nixos/networking.nix:3`, `modules/vm/vm.nix:12`, `modules/vm/vm.nix:16`).

## 7. Template notes
A useful namespace/standalone-HM teaching template; replace identities and hardware as the installation guide directs (`README.md:19`, `modules/homes/andreshung.nix:3`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Host identity selects Starship colors with a default fallback (`modules/aspects/apps/starship/starship.nix:8`, `modules/aspects/apps/starship/starship.nix:16`), meeting the entity-to-native-setting anchor5. The firewall collector has a consumer but no producer in the source tree (`modules/aspects/desktop/components/nixos/networking.nix:3`, `modules/aspects/desktop/components/nixos/networking.nix:19`); it receives no live-channel credit. Score **5**; confidence **high**.

### I

Scope · pros · cons/coverage: Application leaves and explicit stack includes separate workstation and terminal concerns (`modules/aspects/stacks/terminal.nix:5`, `modules/aspects/stacks/dev-tools.nix:5`). Cross-platform Bitwarden encapsulates the SSH-agent environment with installation (`modules/aspects/apps/bitwarden.nix:8`). Grade8 between ordinary boundaries5 and fully explicit contracts9: Flatpak still relies on an import supplied by the broader desktop stack (`modules/aspects/stacks/desktop-apps.nix:20`). Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract5: class functions receive actual user/host parameters (`modules/aspects/apps/kitty.nix:5`, `modules/aspects/apps/starship/starship.nix:7`), but shared Git/SSH embed identity and Noctalia embeds account paths (`modules/aspects/apps/git.nix:15`, `modules/aspects/apps/ssh.nix:23`, `modules/aspects/desktop/noctalia-v5/config.toml:658`). Grouped leaks4: identity/account1, checkout root1 (`modules/aspects/desktop/components/nix.nix:31`), physical output DP-1 and DP-2 two adaptations (`modules/aspects/desktop/niri/settings/outputs.nix:10`, `modules/aspects/desktop/niri/settings/outputs.nix:17`). Raw occurrences exceed these four groups; the Noctalia update command also repeats the checkout root (`modules/aspects/desktop/noctalia-v5/config.toml:618`). Coverage6 cap; S=min(5,6). Optional Starship fallback colors and ordinary timezone preferences are not charged. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":4}}
```

### R

Scope · pros · cons/coverage: The namespace exports independently selectable leaves (`modules/den.nix:17`, `modules/aspects/desktop/components/nixos/bluetooth.nix:2`) and the README identifies feature/host boundaries (`README.md:3`), meeting light adaptation5. No minimal external consumer contract is demonstrated; the existing Bluetooth candidate needs namespace rebinding (`modules/aspects/desktop/components/nixos/bluetooth.nix:5`). Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Concrete Linux and Darwin hosts plus two-architecture standalone homes have explicit class arms (`modules/hosts/kangaroo/kangaroo.nix:9`, `modules/hosts/hyena/hyena.nix:4`, `modules/homes/packet.nix:4`). Installation examples cover all three consumers (`README.md:22`, `README.md:56`, `README.md:85`). Grade8: strong documented scopes above narrow5, but no automated cross-platform check accompanies the examples; the runnable VM is x86-only by explicit guard (`modules/vm/vm.nix:12`). Score **8**; confidence **high**.

### L

Scope · pros · cons/coverage: The README teaches the directory-to-aspect/stack/host mapping and gives concrete installation and management examples (`README.md:3`, `README.md:28`, `README.md:120`), anchor5. It does not explain quirk producer/consumer design; the prepared collector is visible only in source (`modules/aspects/desktop/components/nixos/networking.nix:3`). Score **5**; confidence **high**.

### V

Scope · pros · cons/coverage: A documented VM launch builds the actual selected kangaroo configuration, with bounded VM resources (`README.md:9`, `modules/vm/vm.nix:19`, `modules/vm/vmvariant.nix:13`). Grade3 gives modest credit above unchecked2 for a reproducible manual smoke target; no assertions, outcome tests or CI invocation are present in that target (`modules/vm/vm.nix:16`). Score **3**; confidence **high**.

### O

Scope · pros · cons/coverage: Den inventory feeds nh.denPackages (`modules/aspects/desktop/components/nix.nix:8`), meeting one fact-derived operations concern5. Installation remains documented per-host commands, not an inventory-driven deploy/install/secrets pipeline (`README.md:36`, `README.md:71`). Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: The visible targets are standard NixOS, Darwin and standalone Home Manager (`modules/hosts/kangaroo/kangaroo.nix:9`, `modules/hosts/hyena/hyena.nix:4`, `modules/homes/packet.nix:4`), baseline2. The VM is an ordinary host smoke wrapper (`modules/vm/vm.nix:19`), not a distinct non-host module contract. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Enabled selection-verified census diversity6 gives grade5. Complete reference units19 below give grade7, hence B6. This includes real application/device integrations (DDCUtil installs its tool, enables I2C and grants access; Wireshark enables capture backends and group access), and several-resource Sunshine startup/capability/firewall/uinput wiring (`modules/aspects/desktop/components/nixos/ddcutil.nix:7`, `modules/aspects/apps/wireshark.nix:8`, `modules/aspects/apps/sunshine.nix:9`). Pixie is counted once as its asset-owning helper, not again as the SDDM include bundle (`modules/aspects/desktop/components/nixos/login/sddm/themes/pixie/pixie.nix:25`). Bare/token Btop, BlueZ, Ghostty, Zellij, HeadsetControl (package plus one udev resource, `modules/aspects/apps/headsetcontrol.nix:12`) and package bundles are excluded (`modules/aspects/apps/btop.nix:7`, `modules/aspects/apps/ghostty.nix:11`, `modules/aspects/apps/zellij.nix:16`). Niri/Noctalia require hardware/account adaptation, Kitty requires an externally installed Fish, Flatpak its stack import, and Git/SSH author identity, so none are complete reference units here (`modules/aspects/desktop/niri/settings/outputs.nix:10`, `modules/aspects/desktop/noctalia-v5/config.toml:658`, `modules/aspects/apps/kitty.nix:30`, `modules/aspects/stacks/desktop-apps.nix:20`, `modules/aspects/apps/git.nix:15`). Score **6**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":6.0,"diversity_grade":5,"reference_grade":7,"reference_units":[{"name":"DaVinci Resolve","evidence":"modules/aspects/apps/davinci-resolve.nix:10"},{"name":"Devenv shell hooks","evidence":"modules/aspects/apps/devenv.nix:16"},{"name":"Fastfetch","evidence":"modules/aspects/apps/fastfetch.nix:23"},{"name":"Helix","evidence":"modules/aspects/apps/helix.nix:10"},{"name":"Keyd keyboard mapping","evidence":"modules/aspects/apps/keyd.nix:10"},{"name":"Nautilus","evidence":"modules/aspects/apps/nautilus.nix:9"},{"name":"OpenRazer","evidence":"modules/aspects/apps/openrazer.nix:9"},{"name":"PostgreSQL","evidence":"modules/aspects/apps/postgresql/postgresql.nix:10"},{"name":"Starship","evidence":"modules/aspects/apps/starship/starship.nix:30"},{"name":"Wireshark","evidence":"modules/aspects/apps/wireshark.nix:9"},{"name":"Dock","evidence":"modules/aspects/desktop/components/darwin/dock.nix:5"},{"name":"Finder","evidence":"modules/aspects/desktop/components/darwin/finder.nix:5"},{"name":"ScreenCapture","evidence":"modules/aspects/desktop/components/darwin/screencapture.nix:5"},{"name":"PipeWire RAOP","evidence":"modules/aspects/desktop/components/nixos/pipewire.nix:15"},{"name":"Breeze cursor integration","evidence":"modules/aspects/desktop/components/nixos/cursors/breeze.nix:6"},{"name":"DDCUtil I2C access","evidence":"modules/aspects/desktop/components/nixos/ddcutil.nix:8"},{"name":"Bitwarden SSH agent","evidence":"modules/aspects/apps/bitwarden.nix:9"},{"name":"Sunshine streaming access","evidence":"modules/aspects/apps/sunshine.nix:9"},{"name":"Pixie SDDM theme","evidence":"modules/aspects/desktop/components/nixos/login/sddm/themes/pixie/pixie.nix:25"}]}}
```

**Total:** 54.5/100. **Shortlists:** showcase no; library bluetooth; starter yes. Useful cross-platform namespace starter and application reference collection; entity-derived presentation is demonstrated, while the prepared firewall channel is not a live data-flow showcase.

Overall pros:
- Explicit application/stack boundaries (`modules/aspects/stacks/terminal.nix:5`).
- Linux, Darwin and standalone-home installation recipes (`README.md:22`, `README.md:56`, `README.md:85`).
- Actual selected-host VM smoke target (`modules/vm/vm.nix:19`).

Overall cons / scope limits:
- Shared account/output assumptions need adaptation (`modules/aspects/apps/git.nix:15`, `modules/aspects/desktop/niri/settings/outputs.nix:10`).
- Collector has no verified producer (`modules/aspects/desktop/components/nixos/networking.nix:19`).
- VM entry provides no assertion or CI execution contract (`modules/vm/vm.nix:16`).

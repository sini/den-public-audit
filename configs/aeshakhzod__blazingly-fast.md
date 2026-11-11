# aeshakhzod__blazingly-fast

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/aeshakhzod__blazingly-fast.md)

- Upstream: [aeshakhzod/blazingly-fast](https://github.com/aeshakhzod/blazingly-fast)
- Reviewed revision: [`2c2fb84d6b39`](https://github.com/aeshakhzod/blazingly-fast/commit/2c2fb84d6b397a4d35c7af318d1a672294ab398a)
- Author: aeshakhzod
- Score: **41.0 / 100**, rank 86 of 103 ranked configs. D 2 · I 8 · S 5 · R 5 · P 5 · L 1 · V 2 · O 5 · B 6 · X 2. Shortlists: library units (1).
- Summary: Clear application/profile organization and one derived operational export; ordinary package-class plumbing receives no D/X credit, and author paths/unavailable secret assets limit transfer.

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
Generated flake-parts/import-tree loads host/profile/feature modules (`flake.nix:1`, `flake.nix:4`). Two Linux hosts compose hardware batteries and workhorse profiles, while defaults also define Darwin/HM behavior (`modules/hosts/qoravoy/default.nix:2`, `modules/defaults.nix:3`).

## 2. Common patterns
- host-aspects is selected on the host schema alongside hostname (`modules/defaults.nix:20`).
- den.default includes inputs-prime, self-prime and custom autocomplete (`modules/defaults.nix:14`).
- Parametric hardware/storage batteries are selected per host (`modules/hosts/qoravoy/default.nix:12`, `modules/hosts/qoravoy/default.nix:14`).

## 3. Novel patterns
A suspend override redirects the system suspend command to suspend-then-hibernate, supplying an explicit delay policy in the same battery (`modules/batteries/hibernation.nix:4`, `modules/batteries/hibernation.nix:15`).

## 4. Library candidates
- hibernation · `modules/batteries/hibernation.nix:2` · replace systemd suspend with suspend-then-hibernate and a 30-minute delay · inputs: Linux NixOS, systemd; consumer must provision working hibernation/swap · parameterization: none (`modules/batteries/hibernation.nix:8`) · **B**, expose delay and distinguish provisioning prerequisites from the command override (`modules/batteries/hibernation.nix:15`).

## 5. den friction
No verified den-specific friction in reviewed defaults/host wiring (`modules/defaults.nix:20`, `modules/hosts/qoravoy/default.nix:6`). Some editor aspects depend on inputs whose declarations are commented out, a configuration completeness issue (`modules/aspects/editors/doom-emacs/default.nix:10`, `modules/aspects/editors/doom-emacs/default.nix:66`).

## 6. Docs and complexity
Docs **1**: README gives intent and inspirations without setup/structure guidance (`README.md:3`, `README.md:7`). Complexity **3**: multiple host profiles plus hardware and user classes, without verified cross-host data routing (`modules/hosts/qoravoy/default.nix:7`, `modules/defaults.nix:24`).

## 6a. Defects and scoring notes

- **S · moderate:** shared code requires adapting six author groups: ACME identity, key directory, checkout, encrypted gitlink asset, domain and personal website origin (`modules/aspects/homelab/defaults.nix:12`, `modules/aspects/secrets/sops.nix:7`, `modules/aspects/editors/astronvim/default.nix:5`, `.gitmodules:3`, `modules/aspects/homelab/services/matrix.nix:3`, `modules/aspects/homelab/services/website.nix:11`).
- **R · moderate:** optional integrations refer to undeclared inputs; Doom/Lem/Xinux cannot be reused as complete units without restoring those declarations (`modules/aspects/editors/doom-emacs/default.nix:10`, `modules/aspects/editors/doom-emacs/default.nix:66`, `modules/aspects/editors/lem/default.nix:23`, `modules/aspects/desktop/xinux.nix:41`).
- **L · moderate:** root README supplies no adoption/feature-selection procedure (`README.md:3`).
Btrfs/Docker storage policy is not an additional forced defect (`modules/batteries/btrfs.nix:10`).

## 7. Template notes
Useful small battery/profile examples, but stale editor integrations and checkout assumptions need attention before reuse (`modules/aspects/editors/doom-emacs/default.nix:10`, `modules/aspects/editors/astronvim/default.nix:5`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Package-class bodies produce three editor tools (`modules/aspects/packages/json-tool-lsp.nix:3`, `modules/aspects/packages/kanata-lsp.nix:3`, `modules/aspects/packages/wit-cli.nix:3`); Zed includes them and reads self-prime packages (`modules/aspects/editors/zed/default.nix:8`, `modules/aspects/editors/zed/default.nix:37`). Exact pinned Den65c9 package-to-flake schema route was source-read (pin `flake.lock:28`; immutable source https://raw.githubusercontent.com/denful/den/65c9fd40e958109f5a352c1a93ae8254bf1ed29f/modules/policies/flake.nix). Formal ruling gives this channel no D credit: exporting compiled packages then looking them up is build plumbing, not structured configuration-data flow. Other visible feature bodies set options directly (`modules/aspects/profiles/workhorse.nix:3`), so D is baseline2. Score **2**; confidence **medium**.

### I

Scope · pros · cons/coverage: Application leaves and named profiles keep feature ownership clear (`modules/aspects/profiles/workhorse.nix:3`, `modules/aspects/editors/zed/default.nix:7`); host-specific hardware stays with its host (`modules/hosts/qoravoy/default.nix:26`). Eight approaches isolated9, with a broad workhorse profile selecting several editors and environments (`modules/aspects/profiles/workhorse.nix:17`). Btrfs also choosing a Docker storage driver is related storage policy (`modules/batteries/btrfs.nix:10`), not automatically an isolation defect. Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Dock entries/username and parametric hardware/disk batteries expose useful variation (`modules/aspects/desktop/darwin-dock.nix:27`, `modules/batteries/nixos-hardware.nix:2`, `modules/batteries/disko.nix:2`), contract5. Six grouped adaptations remain: shared ACME identity (`modules/aspects/homelab/defaults.nix:12`); fixed author key-directory root (`modules/aspects/secrets/sops.nix:7`); checkout root reused by editor/shell helpers (`modules/aspects/editors/astronvim/default.nix:5`, `modules/aspects/env/zsh.nix:40`); unavailable encrypted gitlink asset (`modules/aspects/secrets/sops.nix:8`, `.gitmodules:3`); aes.uz domain/subdomains (`modules/aspects/homelab/services/matrix.nix:3`); personal website source (`modules/aspects/homelab/services/website.nix:11`). Repeated raw paths/domain references group once, coverage6 cap gives min5. The unpopulated submodule could reveal additional coupling and lower coverage; it does not justify null. Score **5**; confidence **low**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":6,"distinct_leaks":6}}
```

### R

Scope · pros · cons/coverage: Hibernation is a small native policy unit with explicit systemd override and delay (`modules/batteries/hibernation.nix:4`, `modules/batteries/hibernation.nix:15`), requiring the prerequisite/parameter work described in §4, grade5. Optional Doom, Lem and Xinux integrations refer to inputs whose declarations are commented out (`modules/aspects/editors/doom-emacs/default.nix:10`, `modules/aspects/editors/doom-emacs/default.nix:66`, `modules/aspects/editors/lem/default.nix:4`, `modules/aspects/desktop/xinux.nix:3`). They are incomplete reuse units, not proof that all active hosts fail. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Both actual hosts are x86_64 Linux (`modules/hosts/qoravoy/default.nix:2`, `modules/hosts/waffle/default.nix:2`); host-specific hardware selection is explicit (`modules/hosts/qoravoy/default.nix:14`). Honest narrow5. Darwin arms exist (`modules/defaults.nix:3`, `modules/aspects/env/zsh.nix:49`), but no declared Darwin host demonstrates that larger profile; they do not establish cross-platform9. Score **5**; confidence **high**.

### L

Scope · pros · cons/coverage: README states intent and lists inspirations (`README.md:3`, `README.md:7`) without activation or feature-selection instructions. This is1 for missing onboarding, despite readable source profile lists (`modules/aspects/profiles/workhorse.nix:3`). Score **1**; confidence **high**.

### V

Scope · pros · cons/coverage: The dev shell installs statix/deadnix and formatters (`modules/shell.nix:19`); the VM package launches one literal host (`modules/vm.nix:9`). Neither is an asserted fixture or invoked configuration test, baseline2. A package explicitly disables its own checks (`modules/aspects/packages/wit-cli.nix:21`); no passing status is inferred. Score **2**; confidence **high**.

### O

Scope · pros · cons/coverage: NH packages derive from den.lib.nh.denPackages (`modules/nh.nix:4`), reaching one entity-driven operational concern5. SOPS uses a fixed author key root and external gitlink asset (`modules/aspects/secrets/sops.nix:7`), while the VM helper names qoravoy (`modules/vm.nix:9`); broader deploy/install/secret provisioning is not shown as generated inventory. Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: Ordinary NixOS/HM/Darwin arms remain the target configuration scope (`modules/defaults.nix:2`, `modules/defaults.nix:3`, `modules/defaults.nix:11`). The packages class builds tools consumed by Zed (`modules/aspects/packages/json-tool-lsp.nix:3`, `modules/aspects/editors/zed/default.nix:37`), ordinary flake output scaffolding rather than a new non-host target/module contract; baseline2. Score **2**; confidence **medium**.

### B

Scope · pros · cons/coverage: Census enabled verified breadth is7points, diversity5. Twelve complete substantive references below include a packaged native keyboard mapping (`modules/aspects/desktop/keyboard.nix:6`), native mouse config (`modules/aspects/desktop/mouse.nix:33`) and installed editor presets. Plain packages/bare flags are excluded (`modules/aspects/communication/matrix.nix:4`, `modules/aspects/env/podman.nix:5`); Wezterm has one cosmetic setting (`modules/aspects/env/wezterm.nix:8`). Floorp needs another aspect NUR overlay (`modules/aspects/www/floorp.nix:24`, `modules/aspects/env/nur.nix:7`), Zed needs package projection plus global self-prime setup (`modules/aspects/editors/zed/default.nix:37`, `modules/defaults.nix:16`), and out-of-store/private integrations fail self-contained reference scope. Reference7 and diversity5 yield B6. Score **6**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":7,"diversity_grade":5,"reference_grade":7,"reference_units":[{"name":"desktop.darwin-dock","evidence":"modules/aspects/desktop/darwin-dock.nix:2"},{"name":"desktop.gnome","evidence":"modules/aspects/desktop/gnome.nix:2"},{"name":"desktop.keyboard","evidence":"modules/aspects/desktop/keyboard.nix:2"},{"name":"desktop.mouse","evidence":"modules/aspects/desktop/mouse.nix:3"},{"name":"desktop.plasma","evidence":"modules/aspects/desktop/plasma.nix:2"},{"name":"editors.emacs","evidence":"modules/aspects/editors/emacs/default.nix:2"},{"name":"editors.vscode","evidence":"modules/aspects/editors/vscode.nix:2"},{"name":"env.alacritty","evidence":"modules/aspects/env/alacritty.nix:2"},{"name":"env.docker","evidence":"modules/aspects/env/docker.nix:2"},{"name":"env.starship","evidence":"modules/aspects/env/starship.nix:2"},{"name":"gaming.steam","evidence":"modules/aspects/gaming/steam.nix:2"},{"name":"www.thunderbird","evidence":"modules/aspects/www/thunderbird.nix:2"}]}}
```

**Total:** 41.0/100. **Shortlists:** showcase no; library hibernation; starter no. Clear application/profile organization and one derived operational export; ordinary package-class plumbing receives no D/X credit, and author paths/unavailable secret assets limit transfer.

Overall pros:
- Application leaves compose into readable profiles (`modules/aspects/profiles/workhorse.nix:3`).
- Hardware/storage batteries take explicit parameters (`modules/batteries/nixos-hardware.nix:2`, `modules/batteries/disko.nix:2`).
- NH packages derive from Den outputs (`modules/nh.nix:4`).

Overall cons / scope limits:
- Editor links assume a fixed checkout (`modules/aspects/editors/astronvim/default.nix:5`).
- SOPS key material comes from an external SSH submodule (`modules/aspects/secrets/sops.nix:8`, `.gitmodules:3`).
- Optional editor input declarations are commented out (`modules/aspects/editors/doom-emacs/default.nix:66`).

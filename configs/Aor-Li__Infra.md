# Aor-Li__Infra

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/Aor-Li__Infra.md)

- Upstream: [Aor-Li/Infra](https://github.com/Aor-Li/Infra)
- Reviewed revision: [`87405e2c8b13`](https://github.com/Aor-Li/Infra/commit/87405e2c8b133c2c341a50a0aebeb7fd915db507)
- Author: Aor-Li
- Score: **66.5 / 100**, rank 5 of 103 ranked configs. D 7 · I 8 · S 5 · R 9 · P 8 · L 8 · V 3 · O 5 · B 7 · X 2. Shortlists: showcase, library units (2).
- Summary: Showcase for the live typed-settings policy and its defensive declaration linter; library for the independently specified settings unit plus workspace adapter. Starter withheld: native workspace/cluster/keyboard constants still need review.

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
Inventory declares Linux, Darwin and standalone home entities with distro/role/virtualization data (`modules/inventory.nix:14`, `modules/inventory.nix:22`, `modules/inventory.nix:63`). README explains the generated flake and dendritic organization (`README.md:9`).

## 2. Common patterns
- den.default includes settings-injection policy and define-user (`modules/aspects/default/default.nix:13`, `modules/aspects/default/default.nix:22`).
- define-user+primary-user and host-aspects are selected through default/user layers (`modules/aspects/default/default.nix:22`, `modules/aspects/entity/users/aor/default.nix:4`, `modules/aspects/entity/users/aor/default.nix:8`).
- homes (standalone HM): cluster identity has a separate inventory entry (`modules/inventory.nix:63`).

## 3. Novel patterns
A shared user/home adapter derives workspace-relative out-of-store links from store paths and entity repoRoot, so moving a module preserves its workspace counterpart (`modules/aspects/default/home.nix:22`, `modules/aspects/default/home.nix:30`, `modules/aspects/default/home.nix:38`).

## 4. Library candidates
- aspect-settings · `modules/meta/aspect-settings/default.nix:15` · **A**, typed per-aspect settings mirrored into host/user/home entities, validated and injected into native contexts; inputs Den/lib plus owned `_lib/tree.nix` and `_lib/lint.nix`; reserve settings, import the module, include settings-injection, then use the explicit declaration/entity/consumer example (`modules/meta/aspect-settings/default.nix:6`, `modules/aspects/default/default.nix:13`).
- workspace-links · `modules/aspects/default/home.nix:18` · supplies lib.owner and workspace-relative symlink/path helpers · inputs: inputs.self, lib, HM; entity fullname/email/repoRoot fields · parameterization: fn args owner plus entity options (`modules/aspects/default/home.nix:22`, `modules/aspects/default/home.nix:26`) · **B**, extract the adapter and parameterize fallback checkout name.

## 5. den friction
Author-reported workarounds: reserve settings before traversing the aspect tree to avoid recursive option functors (`modules/meta/aspect-settings/default.nix:22`); defer validation into the settings submodule to avoid host/aspect recursion (`modules/meta/aspect-settings/_lib/lint.nix:8`); use a static Mac aspect because parametric expansion duplicated native lists (`modules/aspects/trait/system/platform/mac.nix:2`). These are documented extension/API interactions, not independently reproduced Den bugs.
The standalone-home comments warn that settings must be placed on the entity, not its aspect (`modules/aspects/entity/homes/aor@philo/default.nix:10`); this documents a context boundary that can surprise users.

## 6. Docs and complexity
Docs **5**: architecture/inventory guide plus comments explain store-to-workspace translation (`README.md:7`, `README.md:28`, `modules/aspects/default/home.nix:13`). Complexity **4**: role/distro facts and unified embedded/standalone owner adapters (`modules/inventory.nix:15`, `modules/aspects/default/home.nix:38`).

## 6a. Defects and scoring notes

- **S / moderate:** Native VSCode workspace roots bypass owner.repoRoot (`modules/aspects/trait/dev/editor/vscode/settings.json:32`, `modules/aspects/trait/dev/editor/vscode/settings.json:282`, `modules/aspects/trait/dev/editor/vscode/settings.json:372`); shared keyboard mappings and Clash helpers retain physical/institution-specific identifiers (`modules/aspects/trait/desktop/input/karabiner/config/karabiner.json:8`, `modules/aspects/trait/desktop/input/karabiner/config/karabiner.json:25`, `modules/aspects/trait/network/proxy/clash-script.js:17`, `modules/aspects/trait/network/proxy/netsel.py:262`). Grouped inventory and cap are on S card. No additional verified defect: repoRoot fallback is explicitly overrideable (`modules/meta/schema/identity.nix:25`), and workspace link inputs have a documented repository-path precondition (`modules/aspects/default/home.nix:13`).

## 7. Template notes
Good for learning entity facts and reusable identity plumbing; its README explicitly distinguishes embedded HM from standalone homes (`README.md:5`, `modules/inventory.nix:61`).

## 8. Scorecard

### D

Scope · pros · cons/coverage: Typed settings are actually routed: Tobimune produces neverSleep (`modules/inventory.nix:54`), the default includes settings-injection (`modules/aspects/default/default.nix:13`), policy.resolve injects home.settings or host.settings (`modules/meta/aspect-settings/default.nix:62`), and native NixOS/Darwin consumers apply it (`modules/aspects/trait/system/power/sleep.nix:18`, `modules/aspects/trait/system/power/sleep.nix:41`). Standalone-home XDG values take the same channel (`modules/aspects/entity/homes/aor@philo/default.nix:23`, `modules/aspects/trait/system/xdg.nix:23`); Rex maps tunnel entries into Darwin agents (`modules/aspects/trait/dev/shell/multiplexer/rex.nix:79`). Missing context throws explicitly (`modules/meta/aspect-settings/default.nix:66`); this is one useful context-injection architecture, without a second cross-entity reduction or explicit duplicate-record contract, hence interpolation 7 rather than 9. Score **7**; confidence **high**.

### I

Scope · pros · cons/coverage: Inventory, entity choices, feature-local inputs and native modules have clear boundaries (`modules/inventory.nix:14`, `modules/flakes/README.md:25`, `modules/aspects/trait/network/proxy/clash.nix:1`). The settings mirror prunes non-settings branches and skips structural/class keys (`modules/meta/aspect-settings/_lib/tree.nix:19`, `modules/meta/aspect-settings/_lib/tree.nix:39`). Broad shell selection still deliberately groups three shells (`modules/aspects/trait/dev/shell/shell.nix:30`); 8 interpolates strong separation with a custom three-file framework rather than a tested generic interface. Score **8**; confidence **high**.

### S

Scope · pros · cons/coverage: Identity and checkout variation have typed overrideable entity fields (`modules/meta/schema/identity.nix:10`, `modules/meta/schema/identity.nix:25`), consumed by owner/workspace adapters (`modules/aspects/default/home.nix:22`, `modules/aspects/default/home.nix:26`): contract 7. Native files bypass those contracts: VSCode embeds 35 workspace roots (eight change groups: checkout, two monorepos, project root, two NFS roots, home identity and macOS project; `modules/aspects/trait/dev/editor/vscode/settings.json:32`, `modules/aspects/trait/dev/editor/vscode/settings.json:142`, `modules/aspects/trait/dev/editor/vscode/settings.json:282`, `modules/aspects/trait/dev/editor/vscode/settings.json:342`, `modules/aspects/trait/dev/editor/vscode/settings.json:372`); two keyboard identifier pairs (`modules/aspects/trait/desktop/input/karabiner/config/karabiner.json:8`, `modules/aspects/trait/desktop/input/karabiner/config/karabiner.json:25`), two institutional domains (`modules/aspects/trait/network/proxy/clash-script.js:17`), cluster probe host (`modules/aspects/trait/network/proxy/netsel.py:262`) and subscription-selection pair (`modules/aspects/trait/network/proxy/netsel.py:36`). Raw inventoried values 42, grouped changes 13: coverage capped 5; S=min(7,5). Public caches, ordinary preferences and named entity settings are excluded. Score **5**; confidence **medium**.

```score-evidence
{"S":{"contract_design":7,"leak_coverage":5,"distinct_leaks":13}}
```

### R

Scope · pros · cons/coverage: The aspect-settings unit supplies typed option-tree construction, validation and scoped injection in three owned files (`modules/meta/aspect-settings/default.nix:17`, `modules/meta/aspect-settings/_lib/tree.nix:47`, `modules/meta/aspect-settings/_lib/lint.nix:25`). Its minimal declaration/entity/consumer example is explicit (`modules/meta/aspect-settings/default.nix:6`), with Den/lib inputs and reservation documented (`modules/meta/aspect-settings/default.nix:15`, `modules/meta/aspect-settings/default.nix:28`); the real default policy installation is shown (`modules/aspects/default/default.nix:13`). This substantial A unit reaches 9; individual application leaves needing config.lib.repo or settings are not silently treated as standalone (`modules/aspects/trait/dev/editor/vscode/vscode.nix:70`). Score **9**; confidence **high**.

### P

Scope · pros · cons/coverage: Real Linux, Darwin and standalone-home contexts are declared (`modules/inventory.nix:14`, `modules/inventory.nix:22`, `modules/inventory.nix:63`), with native class implementations for sleep and guarded standalone Nix configuration (`modules/aspects/trait/system/power/sleep.nix:17`, `modules/aspects/trait/system/power/sleep.nix:40`, `modules/aspects/trait/nix/conf.nix:60`). WSL imports guard absent virtual-host fields (`modules/aspects/trait/system/platform/wsl.nix:15`). 8 reflects these concrete boundaries without claiming a tested platform matrix; inventory contains no selected WSL target (`modules/inventory.nix:14`). Score **8**; confidence **high**.

### L

Scope · pros · cons/coverage: README explains generated flake, inventory and bootstrap (`README.md:9`, `README.md:28`, `README.md:45`); dependency placement has an explicit worked rule (`modules/flakes/README.md:25`, `modules/flakes/README.md:38`). Settings comments teach declaration, value placement, scope priority and lazy missing-context failure (`modules/meta/aspect-settings/default.nix:6`, `modules/meta/aspect-settings/default.nix:46`, `modules/meta/aspect-settings/default.nix:63`). 8 interpolates substantial composition teaching with no executable tutorial fixture: lint guidance is a runtime error/example, not a tutorial test (`modules/meta/aspect-settings/_lib/lint.nix:65`). Score **8**; confidence **high**.

### V

Scope · pros · cons/coverage: README offers deadnix/statix/nixfmt recipes (`README.md:54`); the settings linter rejects bad declaration leaves (`modules/meta/aspect-settings/_lib/lint.nix:25`, `modules/meta/aspect-settings/_lib/lint.nix:65`). That is runtime defensive validation, with no source-visible positive/negative fixture or CI selection of it. 3 credits static-check instructions above the no-check baseline, not the comment claiming an earlier experiment (`modules/meta/aspect-settings/_lib/lint.nix:5`). Score **3**; confidence **medium**.

### O

Scope · pros · cons/coverage: Entity repoRoot is converted into the HM workspace root (`modules/meta/schema/identity.nix:25`, `modules/aspects/default/home.nix:22`, `modules/aspects/default/home.nix:28`) and actually consumed as NH flake plus cleanup policy (`modules/aspects/trait/nix/tool/nh.nix:7`). This is one Den-fact-derived operations concern, anchor 5. Sops config derives optional default file locations but does not itself declare secret entries (`modules/aspects/trait/security/secrets/secrets.nix:53`, `modules/aspects/trait/security/secrets/secrets.nix:79`); bootstrap chooses existing flake outputs rather than deriving additional deployment policy (`scripts/bootstrap.sh:38`). Score **5**; confidence **high**.

### X

Scope · pros · cons/coverage: The evaluated targets are ordinary NixOS, Darwin and HM (`modules/inventory.nix:14`, `modules/inventory.nix:22`, `modules/inventory.nix:63`), anchor 2. Rex tunnel generation is native Darwin launchd configuration (`modules/aspects/trait/dev/shell/multiplexer/rex.nix:79`), not a distinct non-host evaluated module/output contract. Score **2**; confidence **high**.

### B

Scope · pros · cons/coverage: Census selected/max-depth inventory gives 11 points, diversity grade 7 (`modules/aspects/trait/dev/editor/editor.nix:13`, `modules/aspects/trait/dev/shell/shell.nix:30`, `modules/aspects/entity/users/aor/default.nix:12`). Complete reference inventory below: 11 units, reference grade 7, B=7. Each owner contains a coherent preset or actual integration, including Yazi archive backend+directory-changing shell hooks and nix-index database+shell wiring. Excluded package/cask-only leaves, bare Helix/Niri/Fzf enables, shared-settings consumers, mutable-link leaves requiring outside config.lib.repo, and Starship whose base07 palette is supplied by the separate theme (`modules/aspects/trait/dev/editor/helix/helix.nix:3`, `modules/aspects/trait/dev/editor/vscode/vscode.nix:70`, `modules/aspects/trait/dev/shell/prompt/starship/powerline.toml:27`, `modules/aspects/trait/system/theme.nix:1`). No includer or per-app Stylix fragment is counted separately. Score **7**; confidence **high**.

```score-evidence
{"B":{"diversity_points":11.0,"diversity_grade":7,"reference_grade":7,"reference_units":[{"name":"obsidian","evidence":"modules/aspects/trait/app/obsidian.nix:5"},{"name":"fcitx5","evidence":"modules/aspects/trait/desktop/input/fcitx5.nix:9"},{"name":"aerospace","evidence":"modules/aspects/trait/desktop/session/compositor/aerospace.nix:12"},{"name":"claude-program-status","evidence":"modules/aspects/trait/dev/ai/claude/claude.nix:34"},{"name":"clang-toolchain","evidence":"modules/aspects/trait/dev/lang/clang.nix:48"},{"name":"tmux","evidence":"modules/aspects/trait/dev/shell/multiplexer/tmux.nix:22"},{"name":"ghostty","evidence":"modules/aspects/trait/dev/shell/terminal/ghostty.nix:14"},{"name":"yazi","evidence":"modules/aspects/trait/dev/shell/util/yazi/yazi.nix:9"},{"name":"nix-runtime","evidence":"modules/aspects/trait/nix/conf.nix:16"},{"name":"nix-index","evidence":"modules/aspects/trait/nix/tool/nix-index.nix:9"},{"name":"stylix","evidence":"modules/aspects/trait/system/theme.nix:12"}]}}
```

**Total:** 66.5/100. **Shortlists:** showcase yes; library aspect-settings, workspace-links; starter no. Showcase for the live typed-settings policy and its defensive declaration linter; library for the independently specified settings unit plus workspace adapter. Starter withheld: native workspace/cluster/keyboard constants still need review.

Overall pros:
- Live entity→policy→native settings path, including explicit missing-context behavior (`modules/meta/aspect-settings/default.nix:62`, `modules/aspects/trait/system/power/sleep.nix:18`).
- Complete generic settings unit with minimal declaration/value/consumer example (`modules/meta/aspect-settings/default.nix:6`).
- Concrete Darwin/standalone-HM guards and actual targets (`modules/inventory.nix:22`, `modules/aspects/trait/nix/conf.nix:60`).

Overall cons / scope limits:
- Native workspace roots and institutional routing require edits outside the owner contract (`modules/aspects/trait/dev/editor/vscode/settings.json:32`, `modules/aspects/trait/network/proxy/clash-script.js:17`).
- Static-check recipes and runtime lint have no source-visible regression fixtures (`README.md:54`, `modules/meta/aspect-settings/_lib/lint.nix:65`).
- Operations derive NH workspace selection, while secrets remain optional defaults rather than traced emit/consume entries (`modules/aspects/trait/nix/tool/nh.nix:7`, `modules/aspects/trait/security/secrets/secrets.nix:53`).

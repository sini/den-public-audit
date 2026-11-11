# ivokun/kebun

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/ivokun/kebun.md)

- Upstream: [ivokun/kebun](https://github.com/ivokun/kebun)
- Reviewed revision: [`1038ddc22989`](https://github.com/ivokun/kebun/commit/1038ddc22989c43931a147959c64395efb6b661f)
- Author: ivokun
- Score: **54.0 / 100**, rank 33 of 103 ranked configs. D 5 · I 7 · S 6 · R 5 · P 5 · L 9 · V 6 · O 3 · B 5 · X 2. Shortlists: showcase.
- Summary: D useful direct capability contract capped5; I migration boundary remains; S guarded interface limited by six groups; R useful presets; P narrow honest; L worked ADRs; V regression+assertions; O snapshot facts/manual operations; X ordinary exports; B seven units.

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

Den is evaluated directly with nixpkgs evalModules and returns config.flake ([`flake.nix:4`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/flake.nix#L4)). Migration wrappers turn existing NixOS modules into aspects while HM modules remain imported into the user class ([`modules/aspects.nix:24`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L24), [`modules/users.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L60)).


## 2. Common patterns.

- host-aspects composition: one sharedHostAspects list captures common host concerns ([`modules/aspects.nix:12`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L12)).
- parametric aspect (fn args): host-base config receives host and config ([`modules/aspects.nix:44`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L44)).
- define-user: user creation is included separately from explicit groups and shell ([`modules/users.nix:14`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L14)).


## 3. Novel patterns.

Typed kebun.host capabilities reach HM via osConfig instead of hostname matching ([`modules/aspects.nix:57`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L57)), preserving the existing module boundary during migration.


## 4. Library candidates.

None verified as a self-contained community aspect in the inspected sources.


## 5. den friction.

Package outputs require an explicit flakeOutputs.packages import to avoid one freeform package definition silently winning ([`modules/den.nix:10`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/den.nix#L10)). User comments avoid primary-user because of unwanted networkmanager membership ([`modules/users.nix:20`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L20)), and use _module.args because HM extraSpecialArgs is reserved ([`modules/users.nix:2`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L2)).


## 6. Docs and complexity.

Docs 5: README explains entities, capability routing and migration ADRs ([`README.md:14`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L14)); source explains argument boundaries and rejected battery behavior ([`modules/users.nix:2`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L2), [`modules/users.nix:20`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L20)). Complexity 4: two hosts share wrapper aspects, typed capabilities and a large HM import boundary ([`README.md:3`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L3), [`modules/aspects.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L60), [`modules/users.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L60)).


## 6a. Defects and scoring notes.

- S · moderate: six grouped shared adaptations remain, enumerated in S, including printer/LAN/NFS/tailnet and identity/locale ([`modules/aspects/printing.nix:32`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/printing.nix#L32), [`modules/aspects/networking.nix:112`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/networking.nix#L112), [`home/features/shell.nix:137`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/shell.nix#L137)).
- I · minor: named user imports legacy broad shell/editor modules mixing app concerns and identity, making app reuse require separation ([`modules/users.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L60), [`home/features/editors.nix:77`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L77), [`home/features/shell.nix:131`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/shell.nix#L131)).
Explicit x86 single-user bridge and historical pre-install ADR are narrow scope/chronology, not additional defects.

## 7. Template notes.

Excellent migration reference, though a clean starter should reduce compatibility wrappers and personal desktop integration ([`modules/aspects.nix:1`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L1), [`README.md:11`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L11)).

## 8. Scorecard.

### D
Scope: host capabilities and user facts reaching plain modules. Pros: typed isLaptop/monitorsLua facts feed HM through osConfig; host users derive Snapper allowlist ([`modules/aspects.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L60), [`home/common.nix:14`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/common.nix#L14), [`modules/aspects.nix:175`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L175), [`modules/aspects/snapper.nix:21`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/snapper.nix#L21)). Cons: deliberate module-argument bridge/direct schema consumption, no custom fact policy/pipe ([`modules/users.nix:85`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L85)). Literal5 useful data contract capped5. Score **5**; confidence **medium**.

### I
Scope: migration wrappers and legacy HM modules. Pros: hosts compose shared concerns and import only own machine facts ([`modules/aspects.nix:201`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L201), [`modules/aspects.nix:210`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L210)). Cons: one named user owns a long untouched HM import boundary; shell/editor files combine independent apps and personal settings ([`modules/users.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L60), [`home/features/shell.nix:131`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/shell.nix#L131), [`home/features/editors.nix:77`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L77)). Interpolated7 above5 shared ownership, below9 fully feature-isolated contributions. Score **7**; confidence **medium**.

### S
Scope: typed capabilities and legacy settings. Pros: typed defaults, descriptions and memory-sync enrollment/runtime-secret assertions are purposeful ([`modules/aspects.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L60), [`modules/aspects.nix:115`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L115), [`modules/aspects.nix:153`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L153)). Contract7 above5 coherent guarded interface, below9 consistently applied surface. Cons: six grouped shared adaptations: printer, LAN route set, NFS server address, tailnet domain, owner identity/default UUID, household locale ([`modules/aspects/printing.nix:29`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/printing.nix#L29), [`modules/aspects/networking.nix:15`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/networking.nix#L15), [`modules/aspects/networking.nix:112`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/networking.nix#L112), [`home/features/shell.nix:137`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/shell.nix#L137), [`home/features/editors.nix:82`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L82), [`modules/aspects.nix:100`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L100), [`home/features/fish.nix:13`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/fish.nix#L13)). Coverage6; all aliases/identity occurrences grouped; min(7,6)=6. Score **6**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":6,"distinct_leaks":6}}
```

### R
Scope: complete plain HM presets behind Den migration. Pros: Helix, MPV and terminals have coherent nonidentity settings with tracked palette asset ([`home/features/helix.nix:10`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/helix.nix#L10), [`home/features/mpv.nix:25`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/mpv.nix#L25), [`home/features/kitty.nix:7`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/kitty.nix#L7)). Cons: §4 has no polished independent Den unit; broad legacy modules require untangling identities/capability schema ([`home/features/opencode-memory.nix:11`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/opencode-memory.nix#L11), [`home/features/editors.nix:82`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L82)). Literal5 useful reusable configurations, not9 documented A-aspect. Score **5**; confidence **medium**.

### P
Scope: deliberately x86 NixOS workstation/HM migration. Pros: machine facts separated and unsupported activation explicitly warned ([`modules/aspects.nix:204`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L204), [`README.md:49`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L49)). Cons: fixed legacy system/username bridge and host schema dependencies do not promise generic standalone HM ([`modules/users.nix:85`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/users.nix#L85), [`home/features/opencode-memory.nix:11`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/opencode-memory.nix#L11)). Literal5 honest narrow scope; fixed bridge alone is not an actual portability failure. Score **5**; confidence **medium**.

### L
Scope: architecture and authoring/operator docs. Pros: README maps ownership/commands, ADR works through host capability producer/consumer and third-host procedure ([`README.md:28`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L28), [`README.md:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L60), [`docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md:63`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md#L63), [`docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md:124`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md#L124)). Cons: historical ADR still describes pre-install Ume whereas README gives later live status, requiring chronology awareness ([`docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md:146`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md#L146), [`README.md:8`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L8)). Literal9 comprehensive worked explanation; historical status is not a current deployment defect. Score **9**; confidence **medium**.

### V
Scope: targeted regression plus configuration assertions. Pros: actual wrapped screenshot/clipboard paths have deterministic observable checks; sync enrollment/runtime paths have assertions ([`modules/omarchy-capture-check.nix:29`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/omarchy-capture-check.nix#L29), [`modules/omarchy-capture-check.nix:42`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/omarchy-capture-check.nix#L42), [`modules/aspects.nix:157`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L157)). Cons: no general Den capability negative-context fixture; documented migration build comparisons are historical evidence ([`docs/adr/0013-adopt-den-aspect-oriented-framework.md:54`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/docs/adr/0013-adopt-den-aspect-oriented-framework.md#L54)). Interpolated6 beyond5 one meaningful regression, below9 composition boundary coverage. Nothing executed. Score **6**; confidence **medium**.

### O
Scope: derived state access and manual rebuild workflow. Pros: host users drive snapshot permissions and safe snapshot directory creation refuses nonempty replacement ([`modules/aspects.nix:175`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L175), [`modules/aspects/snapper.nix:21`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/snapper.nix#L21), [`modules/aspects/snapper.nix:75`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/snapper.nix#L75)). Cons: rebuild/install is operator-driven, no Den-derived deploy/builder/secret inventory ([`README.md:39`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L39), [`home/backup.nix:19`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/backup.nix#L19)). Interpolated3 for one derived operational concern above2, below5 deployment automation. Score **3**; confidence **medium**.

### X
Scope: ordinary NixOS/HM plus diagrams/packages. Pros: diagrams derive actual host/user projections ([`modules/diagrams.nix:22`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/diagrams.nix#L22), [`modules/diagrams.nix:124`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/diagrams.nix#L124)). Cons: exports are ordinary package plumbing, not evaluated non-host Den classes ([`modules/diagrams.nix:307`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/diagrams.nix#L307)). Baseline2. Score **2**; confidence **medium**.

### B
Scope: selected census applications and whole complete presets. Pros: seven listed presets own app settings plus tracked palette; MPV owns scripts ([`home/features/mpv.nix:25`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/mpv.nix#L25), [`home/features/ghostty.nix:7`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/ghostty.nix#L7)). Cons: multi-app identity-bound editor/shell modules, external OS Fcitx activation, Btop without owned package, Omarchy session-dependent units and fleet memory schema excluded ([`home/features/editors.nix:82`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L82), [`home/features/fcitx5.nix:7`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/fcitx5.nix#L7), [`home/features/btop.nix:10`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/btop.nix#L10), [`home/features/sleep-lock.nix:39`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/sleep-lock.nix#L39), [`home/features/opencode-memory.nix:11`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/opencode-memory.nix#L11)). Several files of one app counted once; no isolated inner fragments invented. Score **5**; confidence **medium**.
B_div: 7 points → 5; B_ref: 7 units → 5; half-up mean → 5.
```score-evidence
{"B":{"diversity_points":7,"diversity_grade":5,"reference_grade":5,"reference_units":[{"name":"helix","evidence":"home/features/helix.nix:6"},{"name":"ghostty","evidence":"home/features/ghostty.nix:9"},{"name":"kitty","evidence":"home/features/kitty.nix:14"},{"name":"mpv","evidence":"home/features/mpv.nix:8"},{"name":"fastfetch","evidence":"home/features/fastfetch.nix:9"},{"name":"starship","evidence":"home/features/starship.nix:8"},{"name":"alacritty","evidence":"home/features/terminals.nix:18"}]}}
```

Total: **54.0/100**. Shortlists: showcase true; library_units []; starter false.

Overall pros:
- Typed capability ownership ([`modules/aspects.nix:60`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects.nix#L60)).
- Worked migration/third-host docs ([`docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md:124`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/docs/adr/0017-model-multiple-hosts-with-host-owned-hardware.md#L124)).
- Real screenshot regression checks ([`modules/omarchy-capture-check.nix:42`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/omarchy-capture-check.nix#L42)).

Overall cons / limits:
- Shared printer/server assumptions (§6a S; [`modules/aspects/printing.nix:32`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/modules/aspects/printing.nix#L32)).
- Legacy personal shell/editor boundary (§6a I; [`home/features/editors.nix:77`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/home/features/editors.nix#L77)).
- Mostly manual activation ([`README.md:46`](https://github.com/ivokun/kebun/blob/1038ddc22989c43931a147959c64395efb6b661f/README.md#L46)).

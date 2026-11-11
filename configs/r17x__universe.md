# r17x__universe

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../README.md#how-to-read-a-scorecard).

[Index](../README.md) · [Ranking](../RANKING.md) · [Census notes](../census/configs/r17x__universe.md)

- Upstream: [r17x/universe](https://github.com/r17x/universe)
- Reviewed revision: [`f8bc64a503b4`](https://github.com/r17x/universe/commit/f8bc64a503b4f09b8eb325d07a5e1b37e6a49cc7)
- Author: r17x
- Score: **62.5 / 100**, rank 10 of 103 ranked configs. D 7 · I 9 · S 7 · R 5 · P 5 · L 7 · V 8 · O 6 · B 3 · X 5. Shortlists: showcase, library units (1).
- Summary: Live runtime/test routing D7 with implicit collision semantics; typed profile S7; meaningful GPG reference; actual class bridge X5; extensive semantic tests V8; derived DNS/secrets operations.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../method/RUBRIC.md).

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

Flake-parts imports a custom den assembly that resolves flake and flake-parts scopes directly (`flake.nix:6`, `nix/den/default.nix:36`). Beyond system/home classes, the same aspect graph supplies Nixvim configurations and runtime theme metadata (`nix/nvim.nix/default.nix:65`, `nix/den/aspects/runtime.nix:14`).


## 2. Common patterns.

- quirks + policies: runtime metadata is exposed by a default pipe policy (`nix/den/default.nix:72`, `nix/den/default.nix:97`).
- custom schema/classes: nixvim is a named class and resolved per host (`nix/den/default.nix:70`, `nix/nvim.nix/default.nix:70`).
- define-user+primary-user: default includes also derive shell from user metadata (`nix/den/default.nix:81`).


## 3. Novel patterns.

Terminal aspects emit runtime theme variants (`nix/den/aspects/terminal.nix:155`); pipe.from runtime/expose routes them (`nix/den/default.nix:101`) to a consumer that writes a user manifest (`nix/den/aspects/runtime.nix:20`, `nix/den/aspects/runtime.nix:38`). This is verified structured dataflow rather than a marker declaration.


## 4. Library candidates.

- runtime-manifest · `nix/den/aspects/runtime.nix:3` · serializes runtime-switchable theme data and installs manifest · HM/nixpkgs, runtime quirk and colors namespace · fn args · B: document/parameterize colors and output path.


## 5. den friction.

Custom module discovery excludes outputs.nix and then manually resolves outputs (`nix/den/default.nix:10`, `nix/den/default.nix:60`); this is deeply coupled framework assembly, with compatibility risk beyond ordinary flakeModule usage.


## 6. Docs and complexity.

Docs 4: README names the framework and embeds aspect/runtime diagrams (`README.md:62`, `README.md:78`, `README.md:96`); integration source explains class boundaries and serialization (`nix/den/default.nix:70`, `nix/den/aspects/runtime.nix:14`). Complexity 5: custom output resolution, class evaluation and runtime dispatch share one graph (`nix/den/default.nix:36`, `nix/nvim.nix/default.nix:65`, `nix/den/aspects/runtime.nix:20`).


## 6a. Defects and scoring notes.

- S · minor: three grouped shared adaptations remain: fixed RG/eR17 cache-push destinations and repository secret source (`nix/den/aspects/shell.nix:89`, `nix/den/aspects/shell.nix:90`, `nix/den/aspects/secrets.nix:34`).
- R · minor: ghds iterates repo but passes undefined r to gh repo delete, so helper does not consume its requested repo argument (`nix/den/aspects/shell.nix:324`, `nix/den/aspects/shell.nix:325`).
No duplicate runtime payload or unsupported-platform failure is asserted from static coverage alone.

## 7. Template notes.

A standout runtime-dataflow demonstration; teach the runtime emitter/pipe/consumer separately from the custom den loader (`nix/den/aspects/terminal.nix:155`, `nix/den/default.nix:101`, `nix/den/aspects/runtime.nix:20`).

## 8. Scorecard.

### D
Scope: live runtime and test-class routes. Pros: Ghostty emits named variants, runtime policy exposes the quirk, HM serializes/installs the manifest (`nix/den/aspects/terminal.nix:155`, `nix/den/default.nix:101`, `nix/den/aspects/runtime.nix:20`). Feature tests also route from subtree into flake-parts nix-unit (`nix/den/classes/tests.nix:30`). Cons: nameless records are skipped and listToAttrs gives implicit collision behavior, without a checked manifest contract (`nix/den/aspects/runtime.nix:20`). Score7: real cross-scope policy routes, capped below8 by missing/duplicate semantics. Score **7**; confidence **medium**.

### I
Scope: feature ownership versus personal profile. Pros: machine selection composes feature providers; typed user/host data stays in r17 profile (`nix/den/aspects/machine.nix:4`, `r17.nix:3`, `nix/den/schema/profile.nix:93`). Cons: custom assembly must resolve framework internals directly (`nix/den/default.nix:60`). Literal9 coherent ownership; custom assembly is a maintenance boundary, not an inherent defect. Score **9**; confidence **medium**.

### S
Scope: profile/user/host interfaces and generated application settings. Pros: typed caches/workspaces/builder plus null-guarded host effects feed consumers (`nix/den/schema/types.nix:3`, `nix/den/schema/types.nix:13`, `nix/den/schema/profile.nix:118`). Contract7 beyond5: substantial typed domain, but service/mail payloads remain freeform (`nix/den/schema/types.nix:137`, `nix/den/schema/profile.nix:46`). Cons: three grouped shared adaptations remain: two fixed cache-push hostnames and repository secret-file location (`nix/den/aspects/shell.nix:89`, `nix/den/aspects/shell.nix:90`, `nix/den/aspects/secrets.nix:34`). Profile identity/cache/workspace values are entity-owned, not leaks. Coverage8; min=7. Score **7**; confidence **medium**.
```score-evidence
{"S":{"contract_design":7,"leak_coverage":8,"distinct_leaks":3}}
```

### R
Scope: independent app reference envelopes. Pros: GPG identity includes its own agent/user/pinentry/smartcard pieces (`nix/den/aspects/identity.nix:3`). Runtime manifest is a useful §4 B extraction with explicit dependency needs (`nix/den/aspects/runtime.nix:14`). Cons: terminal, editor, mail and shell depend on custom user/color/runtime schema, rather than complete standalone presets (`nix/den/aspects/terminal.nix:112`, `nix/den/aspects/editor/default.nix:27`, `nix/den/aspects/shell.nix:32`). Literal5 useful extraction/reference, not packaged9. Score **5**; confidence **medium**.

### P
Scope: two actual ARM Darwin hosts and editor exports. Pros: inherited host systems and class instantiation are explicit; DNS is guarded by host data (`r17.nix:119`, `nix/den/schema/profile.nix:95`, `nix/den/aspects/network.nix:59`). Cons: Linux package keys alias the Darwin host editor rather than independently constructing Linux configurations (`nix/nvim.nix/default.nix:78`); README broader cross-platform wording is not proof (`README.md:55`). Literal5 honest verified boundary, no platform-count bonus. Score **5**; confidence **medium**.

### L
Scope: architecture teaching. Pros: README describes Den and embeds a feature graph; schema explains profile projection (`README.md:62`, `README.md:78`, `nix/den/schema/profile.nix:110`). Cons: graph is substantially stronger than a concise worked new-host/runtime-producer walkthrough (`README.md:69`, `nix/den/default.nix:97`). Score7 between5 orientation and9 complete authoring route. Score **7**; confidence **medium**.

### V
Scope: actual expected-value and negative-context tests. Pros: guard fixtures verify both include and exclusion, fanout/user shape has expected results, and host feature checks consume actual resolved configs (`nix/den/tests/default.nix:100`, `nix/den/tests/default.nix:140`, `nix/den/classes/tests.nix:42`). Cons: no verified fixture covers manifest duplicate/missing names (`nix/den/aspects/runtime.nix:20`). Score8: broad targeted semantic fixtures beyond5, below9 contract-edge coverage; static only. Score **8**; confidence **medium**.

### O
Scope: profile-derived operational effects. Pros: profile injects trusted user/keys/caches into builder; DNS selection renders daemon config and checks readiness; secrets feed ordered identity generation (`nix/den/schema/profile.nix:97`, `nix/den/aspects/network.nix:68`, `nix/den/aspects/secrets.nix:59`). Cons: builder feature tests explicitly expect disabled state, so configured builder metadata is not counted as a live running builder; cache-push aliases still name hosts (`nix/den/tests/default.nix:34`, `nix/den/aspects/shell.nix:89`). Score6: multiple derived operational concerns, below9 full lifecycle. Score **6**; confidence **medium**.

### X
Scope: evaluated nonhost module family. Pros: host-resolved nixvim modules are fed through evalNixvim and exported as configured editor packages (`nix/nvim.nix/default.nix:33`, `nix/nvim.nix/default.nix:65`). Cons: process-compose profile mapping is ordinary service plumbing, and editor aliases do not prove more target families (`nix/den/aspects/services.nix:8`, `nix/nvim.nix/default.nix:78`). Literal5 one real nonhost class bridge. Score **5**; confidence **medium**.

### B
Scope: census maximum-depth diversity and full independent application envelopes. Pros: GPG identity is a coherent complete integration with owned included pieces (`nix/den/aspects/identity.nix:3`, `nix/den/aspects/identity.nix:39`). Cons: Starship uses custom color argument, terminal uses user workspace/font schema, desktop depends on custom overlay/assets, editor resolves fleet host; none counted as independent app units (`nix/den/aspects/shell.nix:160`, `nix/den/aspects/terminal.nix:242`, `nix/den/aspects/desktop.nix:128`, `nix/den/aspects/editor/default.nix:27`). Tools provider is a mixed multiapp body, not separately counted per attr (`nix/den/aspects/shell.nix:208`). Score **3**; confidence **medium**.
B_div: 5 points → 3; B_ref: 1 units → 2; half-up mean → 3.
```score-evidence
{"B":{"diversity_points":5,"diversity_grade":3,"reference_grade":2,"reference_units":[{"name":"gpg-identity","evidence":"nix/den/aspects/identity.nix:3"}]}}
```

Total: **62.5/100**. Shortlists: showcase true; library_units ['runtime-manifest']; starter false.

Overall pros:
- Runtime metadata follows a real producer/route/consumer chain (`nix/den/default.nix:101`).
- Typed profile projection owns identity and host effects (`nix/den/schema/profile.nix:93`).
- Positive and negative policy fixtures inspect resolved contexts (`nix/den/tests/default.nix:100`).

Overall cons / limits:
- Manifest collision/missing-name contract remains implicit (`nix/den/aspects/runtime.nix:20`).
- Many presets require fleet-specific color/user schema (`nix/den/aspects/terminal.nix:112`).
- Fixed host cache-push aliases need manual adaptation (§6a S; `nix/den/aspects/shell.nix:89`).

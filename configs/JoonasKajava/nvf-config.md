# JoonasKajava/nvf-config

About this page: this is the review of one config at one pinned revision. The header below gives the score and the shortlists. The numbered sections follow in the same order on every page, and section 8 is the scorecard. For the terms, see the [glossary](../../GLOSSARY.md). For a guide to the scorecard, see [how to read a scorecard](../../README.md#how-to-read-a-scorecard).

[Index](../../README.md) · [Ranking](../../RANKING.md) · [Census notes](../../census/configs/JoonasKajava/nvf-config.md)

- Upstream: [JoonasKajava/nvf-config](https://github.com/JoonasKajava/nvf-config)
- Reviewed revision: [`9674a20a5632`](https://github.com/JoonasKajava/nvf-config/commit/9674a20a5632ac2987f082465f0f298bb472ac9d)
- Author: JoonasKajava
- Score: **partial: 44.5 of 90 applicable** (not ranked). D 6 · I 9 · S 5 · R 5 · P 5 · L 3 · V 2 · O – · B 2 · X 5. Shortlists: showcase, library units (1).
- Summary: Showcase the explicit typed-merge class adapter, not editor breadth; a B integration unit is reusable, while undocumented packaging/context prerequisites prevent starter selection.

Citations are `path:line` in the upstream repository at the reviewed revision. Read the method in [method/RUBRIC.md](../../method/RUBRIC.md).

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
This is a custom editor configuration genuinely driven by den, not merely an unused dependency: the default package resolves den.aspects.nvf ([`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)). A custom vim class maps many feature fragments into NVF’s vim options ([`modules/nvf-integration.nix:18`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L18), [`modules/nvf-integration.nix:36`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L36)).

## 2. Common patterns
- custom schema/classes: vim forwards into nvf with mapModule nesting ([`modules/nvf-integration.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L32), [`modules/nvf-integration.nix:41`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L41)).
- forward uses the active aspect-chain as its source ([`modules/nvf-integration.nix:42`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L42)).
- Feature fragments contribute to one editor aspect ([`modules/config/languages/nix.nix:5`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L5), [`modules/config/utility/wakatime.nix:2`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/utility/wakatime.nix#L2)).

## 3. Novel patterns
nestUnderVim recursively preserves import structure and function arguments, letting NVF option types merge plugins instead of den freeform shallow merging ([`modules/nvf-integration.nix:19`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L19), [`modules/nvf-integration.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L24)).

## 4. Library candidates
- nvf-integration · [`modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12) · turns vim-class aspects into an NVF Neovim package · inputs: den, nvf, nixpkgs lib/pkgs · parameterization: fn args pkgs/vimAspect/ctx ([`modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12)) · **B**, preserve mapModule adapter and clarify the currently unused context hook ([`modules/nvf-integration.nix:50`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L50)).

## 5. den friction
The author explicitly reports shallow freeform merges overwriting lazy.plugins when forwarding into vim, and implements a top-level typed merge adapter ([`modules/nvf-integration.nix:20`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L20), [`modules/nvf-integration.nix:23`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L23)).

## 6. Docs and complexity
Docs **2**: root README is a TODO ([`README.md:1`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/README.md#L1)), but the core adapter carefully explains its merge workaround ([`modules/nvf-integration.nix:19`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L19)). Complexity **4**: custom class forwarding, argument mirroring and recursive import adaptation ([`modules/nvf-integration.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L24), [`modules/nvf-integration.nix:36`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L36)).

## 6a. Defects and scoring notes

- **S · moderate:** /etc/nixos checkout, joonas user and nixos-desktop host are three distinct consumer facts fixed in shared nixd expressions ([`modules/config/languages/nix.nix:29`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L29), [`modules/config/languages/nix.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L32)). Raw/grouped count3; upstream schemas and plugin names excluded.
- **R · minor:** ctx is accepted but the sole proposed scope injection is commented, so callers cannot rely on advertised context adaptation ([`modules/nvf-integration.nix:18`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L18), [`modules/nvf-integration.nix:50`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L50)).
- **L · moderate:** README remains TODO without a package/adaptation recipe ([`README.md:1`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/README.md#L1)).

## 7. Template notes
Strong custom-class and merge-semantics reference; document the packaging API and replace machine-specific nixd expressions before publishing as an editor template ([`modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12), [`modules/config/languages/nix.nix:29`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L29)).

## 8. Scorecard

### D

Scope · pros · cons/coverage: vim fragments ([`modules/config/general.nix:3`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/general.nix#L3), [`modules/config/utility/wakatime.nix:3`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/utility/wakatime.nix#L3)) → forward vim→nvf ([`modules/nvf-integration.nix:36`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L36)) → resolve and NVF package ([`modules/nvf-integration.nix:54`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L54), [`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)). mapModule preserves imports/args and delegates duplicate option merging to NVF ([`modules/nvf-integration.nix:19`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L19), [`modules/nvf-integration.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L24)). Routed single-consumer channel exceeds 5; missing/context behavior is not validated, so 6 rather than 8–9. Score **6**; confidence **medium**.

### I

Scope · pros · cons/coverage: App features are separated by language/editor/UI concern ([`modules/config/languages/nix.nix:5`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L5), [`modules/config/utility/wakatime.nix:2`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/utility/wakatime.nix#L2)) while adapter and package construction have separate owners ([`modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12), [`modules/den.nix:11`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L11)). Fits one-editor scale and 9 ownership; one shared editor identity is appropriate here, not an unrelated bundle. Score **9**; confidence **high**.

### S

Scope · pros · cons/coverage: Contract 5: typed NVF module semantics permit feature variation ([`modules/nvf-integration.nix:23`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L23)), but shared nixd expressions fix a consumer checkout/user/host ([`modules/config/languages/nix.nix:29`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L29), [`modules/config/languages/nix.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L32)). Three raw/grouped constants → coverage9 with no count cap; min(5,9)=5. Score **5**; confidence **high**.

```score-evidence
{"S":{"contract_design":5,"leak_coverage":9,"distinct_leaks":3}}
```

### R

Scope · pros · cons/coverage: B nvf-integration unit accepts pkgs/aspect/context and contains its NVF dependency ([`modules/nvf-integration.nix:7`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L7), [`modules/nvf-integration.nix:12`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L12)). One actual consumer ([`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)) demonstrates packaging. Unused ctx hook ([`modules/nvf-integration.nix:50`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L50)) needs clarification: useful B/5, not a fully explicit A contract. Score **5**; confidence **high**.

### P

Scope · pros · cons/coverage: Package set is supplied by perSystem and forwarded to NVF ([`modules/den.nix:19`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L19), [`modules/nvf-integration.nix:14`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L14)). Native clipboard package assumes a Linux desktop ([`modules/config/general.nix:15`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/general.nix#L15)); no broader guarantee or boundary fixtures verified. Honest scoped package support earns5, not a platform-count bonus. Score **5**; confidence **medium**.

### L

Scope · pros · cons/coverage: README is TODO ([`README.md:1`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/README.md#L1)), but adapter explains the shallow/typed merge choice and exact mechanism ([`modules/nvf-integration.nix:19`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L19)). Interpolate3 above placeholder2 for useful internal teaching; no entry-to-consumer setup path supports5. Score **3**; confidence **high**.

### V

Scope · pros · cons/coverage: Package output gives a concrete evaluation surface ([`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)); adapter documents the motivating overwrite ([`modules/nvf-integration.nix:20`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L20)). No relevant check/CI invocation found in the inspected module/entry inventory. Baseline2, not a failing build claim. Score **2**; confidence **medium**.

### O

Scope · pros · cons/coverage: Only a package is constructed ([`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)); there are no host/home entities to operate. Package-only editor configuration is not_applicable under the host/home ruling. Score **null**; confidence **high**.

### X

Scope · pros · cons/coverage: Custom vim/nvf target bridge produces a real application module-system artifact ([`modules/nvf-integration.nix:32`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L32), [`modules/nvf-integration.nix:54`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L54), [`modules/nvf-integration.nix:13`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L13)). One non-host target with a clear merge contract meets5; no several-target claim or operational double credit. Score **5**; confidence **high**.

### B

Scope · pros · cons/coverage: Census has one substantive selected Neovim package → 1 point/B_div2. All feature fragments belong to that one editor; plugins/languages do not become separate complete applications ([`modules/config/general.nix:3`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/general.nix#L3)). The assembled editor embeds author nixd targets ([`modules/config/languages/nix.nix:29`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L29)), so B_ref2 with no qualifying complete nonidentity unit; mean2. Score **2**; confidence **medium**.

```score-evidence
{"B":{"diversity_points":1,"diversity_grade":2,"reference_grade":2,"reference_units":[]}}
```

**Total:** 44.5/90; score null, missing O. **Shortlists:** showcase yes; library nvf-integration; starter no. Showcase the explicit typed-merge class adapter, not editor breadth; a B integration unit is reusable, while undocumented packaging/context prerequisites prevent starter selection.

Overall pros:
- Real custom-class route produces Neovim ([`modules/nvf-integration.nix:36`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L36), [`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)).
- Recursive adapter preserves typed import merging ([`modules/nvf-integration.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L24)).
- One-app concern files have clear ownership ([`modules/config/languages/nix.nix:5`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L5)).

Overall cons / scope limits:
- S: nixd still names one operator/host ([`modules/config/languages/nix.nix:29`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/config/languages/nix.nix#L29)).
- R: context hook is unused ([`modules/nvf-integration.nix:50`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/nvf-integration.nix#L50)).
- L/V: TODO entry and no check definitions at package construction ([`README.md:1`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/README.md#L1), [`modules/den.nix:24`](https://github.com/JoonasKajava/nvf-config/blob/9674a20a5632ac2987f082465f0f298bb472ac9d/modules/den.nix#L24)).

---
title: "Challenge the scoring categories before ranking configs"
---

Status: proposal for maintainer decision, 2026-11-10. This review challenges the seven-category /70 draft; it does not assign corpus scores.

The seven-category sum should not be locked. It rewards some mechanisms twice, lets excellent prose compensate for weak data flow, and conflates three different selections: community showcases, reusable aspects, and beginner templates. Keep a common evidence profile, make data flow the largest single influence on showcase selection, and select library/template exemplars separately. The maintainer's preference for intelligent quirks is a defensible showcase preference; it is not a universal definition of a good small configuration.

All source observations below are static. A test definition establishes an intended check, never a passing check. “Not observed” is not “absent.” File references use `<clone id>/<path>:<line>`, relative to each repository at its reviewed revision. Revisions are the matching `extract/<id>.json` revisions:

| clone id | revision |
|---|---|
| byte-sized-emi/nix-config | 8df6aa42d1bb |
| auscyber/dotfiles | 96be028eaba6 |
| DylanRJohnston/nixos | 505097f4d0fd |
| JoonasKajava/nvf-config | 9674a20a5632 |
| SyahrulBhudiF/dotfiles | ba537827987e |
| Keyruu/shinyflakes | 021ee48343db |
| adanoelle/fern | 060cd42a3d02 |
| adanoelle/garden-shell | e9c3a6b47faf |
| mio-19/config-public | a269164a1be6 |
| ~theutz/flake | 3ede31e7a4e9 |

## Contents

- [1. Orthogonality: merge fluency into composition; keep portability separate from reuse](#1-orthogonality-merge-fluency-into-composition-keep-portability-separate-from-reuse)
- [2. Missing evidence: add verification intent; keep inventory and novelty outside the sum](#2-missing-evidence-add-verification-intent-keep-inventory-and-novelty-outside-the-sum)
- [3. Revised seven-category evidence profile and observable anchors](#3-revised-seven-category-evidence-profile-and-observable-anchors)
- [4. Weighting: one data-flow category, not three correlated bonuses](#4-weighting-one-data-flow-category-not-three-correlated-bonuses)
- [5. Three uses require three selections; smallness is not a defect](#5-three-uses-require-three-selections-smallness-is-not-a-defect)
- [6. Calibration anchors and dissent for the maintainer](#6-calibration-anchors-and-dissent-for-the-maintainer)

## 1. Orthogonality: merge fluency into composition; keep portability separate from reuse

| Draft category | Verdict | Boundary to enforce |
|---|---|---|
| quirks and data flow | Keep and sharpen | Score coherent producer→route→consumer behavior and handling of missing/ambiguous facts, not references or API count. |
| composition hygiene | Keep; absorb den fluency | Split into layout/isolation and settings/variation: one judges concern boundaries, the other judges configurable properties. Credit routing correctness once under the dimension it serves. |
| den fluency | Remove as a separate number | Native APIs are evidence about composition, not another reward for the same includes/batteries. A legitimate workaround is not automatically poor fluency. |
| portability | Keep, rename platform boundaries | Score adaptation at platform boundaries and accuracy of support claims. Separate supported coverage from quality. |
| reusability | Keep, narrow to reuse contracts | Can someone import an aspect without inheriting the author's identity, hostnames, private modules and unrelated defaults? This differs from running it on macOS. |
| readability and docs | Keep, assess task completion | Can a reader trace a feature and add a host/user? README length and comment count are not quality. |
| scale handled clearly | Remove as a separate number | Treat scale as context for composition/docs: necessary complexity can be clear; host count never earns points itself. |

A single-platform aspect can have an excellent reuse contract. Conversely, a feature containing both `darwin` and `homeManager` may still carry the author's Git identity. Dylan's Git aspect demonstrates that distinction: `DylanRJohnston/nixos/modules/git.nix:19` covers OS installation and `:25` HM, while `:28` fixes a personal identity. Count this as platform separation with a reuse limitation, not two deductions for the same limitation.

Do not penalize a workaround once under fluency, again under composition, and again under complexity. Joonas documents a shallow-merge problem and adapts modules through `forward` to preserve option merging (`JoonasKajava/nvf-config/modules/nvf-integration.nix:19`, `:24`, `:36`). That is a useful integration idea with a version-sensitive dependency, not evidence of three independent quality failures.

## 2. Missing evidence: add verification intent; keep inventory and novelty outside the sum

Add **verification intent and maintenance boundaries** as a seventh dimension. Look for relevant positive/negative assertions and whether the check definitions cover the composition being recommended. Dylan defines enabled expectations and a disabled failure case beside dark-mode composition (`DylanRJohnston/nixos/modules/darkmode.nix:30`, `:40`, `:46`), plus a same-user/two-host projection check (`modules/host-aspects-test.nix:230`). These deserve recognition that formatting alone cannot earn. Static inspection cannot certify that CI runs or that any check passes.

Keep these as separate fields, with citations and explicit evidence states:

- Inputs/secrets prerequisites: public/private/local inputs; required checked-in assets; encrypted versus absent files; runtime credentials versus evaluation-time reads. Missing runtime credentials do not prove an evaluation blocker. The public/stub warning in `mio-19/config-public/README.md:15` is a reason to inspect the sweep target, not a low architecture score by itself.
- Verified test results and recency: measured result/revision/date, separate from tests-present. A recent commit does not establish maintenance quality; a stable small aspect does not become worse because it needed no recent edit.
- Novelty/standout idea: a cited explanation, independent of the numeric total. The nvf merge adapter above can be notable despite sparse onboarding documentation (`JoonasKajava/nvf-config/README.md:1`).
- Support coverage: actual instantiated targets separately from packages mentioned, test fixtures and commented hosts. Fern explicitly parks Asahi because of placeholders and x86-only packages (`adanoelle/fern/modules/hosts.nix:29`); it should receive honesty credit, not active ARM-support credit.
- Formatting/lint: useful verification evidence, but no standalone category. A formatter cannot prove correct routing or reusable boundaries.

Host/user variation belongs explicitly in composition. Fern reuses the same user aspect for a differently named standalone login and supplies its own package set and extra arguments (`adanoelle/fern/modules/hosts.nix:12`, `:18`, `:21`). That is more informative than a count of batteries.

## 3. Revised seven-category evidence profile and observable anchors

Use seven named scores, each 1–10, plus confidence and applicability. Treat 2, 5 and 9 as anchors; interpolate only with a written reason. A 9 is supported design within a stated scope, not proof of runtime success. The table describes proposed grading rules; only cited examples are measured source observations.

| Category | 2 anchor | 5 anchor | 9 anchor |
|---|---|---|---|
| **D: structured data flow** | Direct settings without a traced shared contribution, or declarations with no demonstrated producer/consumer; no claim that the config is incorrect. | One live emit→consume channel with limited routing/validation; fixed-name lookups remain. | Multiple useful consumers derive configuration from declared facts through attached policies, with explicit semantics for absent/duplicate contributions and scope boundaries. Show full chains; declarations alone earn no extra credit. |
| **I: layout and isolation of concerns** | One shared module mixes unrelated capabilities or a change requires edits across copied host trees. | Named features and includes localize most changes; some broad bundles remain. | Feature ownership and includes/provides boundaries are clear; optional concerns remain optional, independent features compose without incidental imports, and the layout fits the actual scale. |
| **S: settings and variation contracts** | Shared aspects embed author-specific identity, paths or endpoints that a second host/user must patch in source. | Most expected variation is explicit through args/schema/module options; a few personal constants or constructor overrides remain. | Real host/user differences flow through small documented settings contracts with sensible defaults, validation and context-aware consumers. Optional/absent contexts are handled; a second consumer changes settings rather than shared source. |
| **R: reuse contract** | Importing the feature brings personal identity, private assets or unrelated global defaults with no documented override. | A useful unit needs a small, identified parameterization or namespace rebind: grade B. | At least one substantial grade-A unit has explicit inputs, parameters, assets, platform contract and a minimal consumer example. Candidate count alone does not raise this score. |
| **P: platform boundaries** | Claimed support crosses unguarded platform assumptions, or promised targets are contradicted by active wiring. | Honest narrow support with local platform assumptions; or several platforms with manual exceptions. | Platform-specific modules are selected cleanly, unsupported uses fail clearly or are excluded, and representative boundary checks/examples exist for the claimed scope. Coverage breadth is reported separately. |
| **L: explanation and navigation** | Placeholder or operation-only docs; no short route from entry point to feature selection. | Explains entry/wiring and how to add a host/user/feature, with a small worked example. | Teaches composition, routing and prerequisites through runnable-in-principle examples and local explanations; clearly separates default path from advanced internals. No reward for volume alone. |
| **V: verification intent and maintenance boundaries** | No relevant checks found in the inspected scope; critical assumptions implicit. This is a coverage observation, not a failing-test claim. | Check definitions exercise representative outputs and document prerequisites; CI invocation can be traced statically. | Focused checks cover enabled/disabled behavior, context variation, collisions/missing data, and platform boundaries where applicable; commands and revision expectations are clear. Passing status remains separate. |

Examples pin how to apply these anchors:

- **D, middle rather than top:** byte-sized-emi emits ntfy endpoint data (`modules/stacks/ntfy.nix:3`), collects/transforms it (`modules/fleet.nix:20`, `:22`), and consumes it in update notifications (`modules/auto-update.nix:20`). This is real flow. The `builtins.head` lookups at `:20` and `:21` leave missing/duplicate producer behavior implicit, so a full chain alone does not justify 9.
- **D, upper-end evidence to inspect:** auscyber publishes cache facts (`aspects/base/celler/server.nix:169`), collects them (`aspects/base/celler/push.nix:298`), and uses them to derive HM configuration (`:532`, `:538`). Cross-scope exposure is explicit at `:307`. This supports depth; it does not by itself establish that every channel has robust conflict handling.
- **I/S, middle:** a compact standalone-home entry and explicit module list are easy to follow (`SyahrulBhudiF/dotfiles/flake.nix:40`, `:43`). The bespoke nixGL compatibility overlay (`modules/den.nix:12`) is complexity to explain, not an automatic Den-fluency penalty.
- **R, upper-end opportunity but not a free 9:** garden-shell deliberately exports a namespace (`adanoelle/garden-shell/modules/namespace.nix:4`), but its bundle also owns mutable settings and session restarts (`modules/aspects/shell.nix:30`, `:40`). Review the adoption contract. A library is still `is_den_config: false`; score its reusable units separately from corpus host rankings.
- **P, middle:** Fern handles NixOS plus a standalone Ubuntu home with explicit constructor overrides (`adanoelle/fern/modules/hosts.nix:4`, `:12`, `:21`). The parked ARM host at `:29` limits coverage without contradicting active support.
- **L, low versus middle:** Joonas's README is a TODO (`JoonasKajava/nvf-config/README.md:1`); Dylan explains structure and links ADRs (`DylanRJohnston/nixos/README.md:40`, `:46`). Rich internal comments should be credited, but they do not replace an entry-level usage path.
- **V, upper-end evidence:** Dylan's positive/negative aspect expectations and two-host context test above are stronger evidence than a bare formatter. Confirm how they are exported/invoked before assigning 9; no checks were executed here.


### Separate layout from settings without counting one defect twice

I recommend the two categories. Dylan's Git feature is isolated under `arc.base._.git` (`DylanRJohnston/nixos/modules/git.nix:18`), yet its shared body fixes the author's name/email (`:28`). The first fact supports I; the second limits S. Moving the constants into settings improves S without moving a file or changing I. A reusable name/email contract could also improve R, but the same defect must not be charged a full deduction in all three categories: assign it one primary cost category, and describe the adoption effect in R without another penalty unless an independent reuse defect exists.

Settings expressiveness is **not option count**. Function args, entity attributes, quirks and ordinary module options can all express a good contract. Not every port, package name or standard path needs a new setting. A deliberate opinionated default is acceptable when the advertised consumer can override it; a leaked personal value is a defect when the intended second consumer must edit shared implementation. Require the concrete variation use case before prescribing an option. Otherwise the score would reward unnecessary framework and punish a useful tiny preset.

Weigh D twice either I or S for showcase selection if a sum is required. Keep I and S individually visible for starter selection, where simplicity plus obvious variation can matter more than cross-host flow. Under §6a, record each observed defect as source reference, primary cost category, severity and effect on a concrete consumer. A moderate S defect does not automatically imply moderate I, R and P defects.

### Can reviewers independently reproduce the number?

Not exactly from these anchors alone. “Clear,” “substantial,” and “light parameterization” still need judgment. Publish the evidence and the vector; do not present a one-point total difference as a measurement of quality.

Require a small evidence card per score: scope inspected; cited positive evidence; cited limitation; confidence (high/medium/low). For D, record producer, attached route, consumer, and missing/duplicate behavior. An untraced channel is **unknown**, not a verified zero. If applicability is genuinely absent, record `not_applicable` with the reason; do not silently substitute a high score or renormalize totals across different scopes.

Before all 98 are scored, independently rescore a small set spanning an advanced fleet, a tiny standalone home, an aspect library, a stale README and a custom class adapter. A difference over two points in a category triggers discussion of evidence/anchor wording, not averaging. This review has not run that calibration exercise.

## 4. Weighting: one data-flow category, not three correlated bonuses

Splitting quirks into “declare,” “emit/consume,” and “route” gives the same channel up to three rewards and encourages ceremonial plumbing. A declaration without a consumer is not a third of an intelligent architecture. Keep one D score whose evidence requires the whole chain. I and S each get their own lens because a clean feature boundary can still conceal a hard-coded property; their distinction is tested below.

For **community showcases**, recommend D as the primary sorting key, then the other scores and the written standout judgment. This directly expresses the maintainer's priority and avoids allowing docs to buy back missing flow.

If a single additive score is mandatory, use a named, explicitly policy-based showcase index:

`showcase = 2D + I + S + R + P + L + V`, maximum 80.

D then weighs twice any other dimension, not more than all six combined. If “weighted most” means non-compensable, the maintainer must also choose a D eligibility floor; duplication alone cannot achieve that. Do not invent an eligibility cutoff or award tiers before seeing the calibration set.

An unweighted sum is simpler, but it fails the stated data-flow priority and lets correlated categories dominate. Merely adding categories changes existing awards without changing any configuration. Under the earlier /40 thresholds, preserving the platinum proportion exactly would require ceiling(70×35/40) = **62**, not 61; in either case, proportional scaling preserves arithmetic, not the meaning of an award.

## 5. Three uses require three selections; smallness is not a defect

Do not use a showcase award as the admission rule for a starter template or an aspect library.

- **Showcase:** traced data flow, clean variation, a supported scope and a clear explanation of the standout. Quirk sophistication is a legitimate selection preference here.
- **Library:** select cited grade-A/B units by adoption cost, explicit dependencies, and parameter contracts. A low-scoring whole repo may contain an excellent small unit. A namespace-exporting library should remain discoverable even though excluded from den-config counts.
- **Starter:** favor a short entry-to-output path, minimal prerequisites, clear host/user variation, and truthful platform boundaries. Provide one minimal host/user template and one optional contribution/policy extension. A standalone HM example can be good without pretending to be a fleet.

A tidy single-user configuration naturally needs little or no cross-host flow. Its low D score means “limited showcase evidence for this preference,” not “bad configuration.” Never add gratuitous quirks to improve a beginner template's total. Syahrul's explicit one-home module list (`SyahrulBhudiF/dotfiles/flake.nix:40`) illustrates the value of a small path; its nixGL workaround (`modules/den.nix:12`) also shows why small file count alone cannot settle beginner suitability.

Keep scale as scope, not an achievement metric. A clear two-host composition can score well on I/S/L; a large framework must justify its machinery. This also prevents penalizing small configs once for low flow, once for few platforms, and once for small scale.

## 6. Calibration anchors and dissent for the maintainer

**Theutz as about 8 in every category is not supported.** Its data-flow and integration ideas are strong: casks are emitted by `theutz/modules/aspects/omniwm.nix:8`, consumed by `modules/aspects/homebrew.nix:6`, and defined by `modules/quirks/casks.nix:2`; class routing appears in `modules/deploy.nix:14`. But the current review records doc_quality 1 and no README ([~theutz/flake](/configs/theutz/flake/), §6). It cannot simultaneously anchor an 8 on beginner explanation under the proposed L anchors. The review itself is not a source file in the clone; it is evidence of the audit's existing judgment, pending the maintainer's anchor update.

The maintainer may keep **32 as a holistic calibration judgment** under the four-lens model. That does not justify distributing 8/8/8/8, nor multiplying 8 by every newly introduced category. Calibrate the vector first; let any index follow it. Do not tune dimensions until a preferred repo lands on a predetermined total.

The maintainer now explicitly says sini/nix-config has strong layout/isolation but includes leaked hard-coded properties and incomplete settings contracts. The pattern study has since landed, and a targeted static read at `96d3ea2c004254e416cd814413ef0c3f6986021e` confirms the distinction: `../sini/nix-config/modules/den/aspects/roles/workstation.nix:3` is an isolated include-only role; `modules/den/aspects/core/nix/nix.nix:8` declares build-budget settings consumed at `:49`, while the same aspect fixes a fleet-specific cache URL at `:67`. The cache is public-read according to its comment at `:66`; the limitation is a personal default embedded in shared code, not a private-input finding. Treat sini as an upper reference for I, while allowing actual deductions under S, D or any other lens. I have not independently scored its whole vector. Do not reserve a perfect score in advance, and do not preserve an earlier requested D=10 if source defects contradict that anchor. A top reference is allowed an uneven vector.

Dissent I would preserve even if the maintainer chooses /70 awards:

1. More Den APIs do not mean better architecture. Keyruu's explicit provenance failure (`Keyruu/shinyflakes/modules/policies/services-collect.nix:22`) is valuable feedback alongside real collection (`:23`), not grounds to discard the design or reward unexamined API use.
2. A single leaderboard cannot faithfully select both a clever fleet and a first lesson. Keep the three use-specific shortlists even if there is one headline total.
3. Static reviews support evidence-backed judgments, not claims of correctness, successful CI, secret availability or cross-platform execution. Keep sweep flags and measured eval outcomes separate.
4. Anchors must be falsifiable. If no amount of missing docs could lower theutz's docs lens, it is a preference label, not a scoring category.

Maintainer decision needed: adopt these seven categories or retain the draft seven; decide whether D is a primary sorting key or a weighted term; and approve separate showcase/library/template selections. Then pilot the anchors before retrofitting scores across the corpus. Existing §1–7 reviews remain useful whichever scoring policy wins.

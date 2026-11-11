---
title: "Per-config review rubric"
---

One file per config: `<id>`, where `<id>` is the directory name used in `extract/<id>.json`. The work is
static reading only. Never run `nix`, never evaluate or build, and never execute repo code. Configs with IFD,
private inputs or missing secrets are reviewed like any other.

Start from `extract/<id>.json`, which holds the mechanical facets: den surfaces and batteries, aspects, inputs,
platforms and regression flags. Don't recount what it already holds. The review adds the judgement it can't make,
and it corrects it where it's wrong. If an extracted fact is wrong, say so under `extract_corrections`.

Every claim cites `path:line` from the clone at the rev in the extract.

## Front matter (YAML, required; aggregated by script)

```yaml
id: <id>
rev: <rev from extract>
is_den_config: true | false        # false = library, template, fork of den, or den barely used
layout: aspect-per-feature | host-centric | user-centric | namespace | policy-driven | flat | mixed
doc_quality: 1-5                   # 1 none · 3 README explains structure · 5 README + per-aspect docs/comments that teach
complexity: 1-5                    # 1 single host, few aspects · 3 several hosts/users, shared aspects · 5 fleet, policies, custom schema/classes
template_worthy: no | partial | yes
scores:                            # Famitsu-style: one 1-10 reviewer per category (§8); null + reason if not_applicable
  D: 1-10   # structured data flow (quirks/pipes/policies), counted twice
  I: 1-10   # layout & isolation of concerns
  S: 1-10   # settings & variation contracts
  R: 1-10   # reuse contract
  P: 1-10   # platform boundaries
  L: 1-10   # explanation & navigation
  V: 1-10   # verification intent & maintenance boundaries
  O: 1-10   # operations: deploy (colmena/deploy-rs), secrets pipeline, install/bootstrap, builders — driven by den data
  B: 1-10   # breadth: application diversity + number of reference-quality aspects (from census + §4)
  X: 1-10   # integrations: den driving other module systems/outputs as classes (terranix, k8s/nixidy/argocd, microvm…)
confidence: {D: high|medium|low, I: …, S: …, R: …, P: …, L: …, V: …, O: …, X: …}
score: <2D+I+S+R+P+L+O+B+½V+½X, max 100, one decimal>  # award tiers deliberately undefined until the pilot calibrates
shortlists: {showcase: true|false, library_units: [<§4 names graded A/B>], starter: true|false}
notable: true | false              # a shortlist hit, or one standout idea worth showing the den community
score_basis: <one line: what moved each category>
library_candidates: <count of entries in §4>
regression:                        # extra to the extract's regression_flags; [] if none
  ifd_sources: [<input or path:line>]
  private_inputs: [<input>]
  missing_secrets: [<path>]
  other_blockers: [<free text>]
extract_corrections: [<free text>]
```

## Body (headings in this order; keep each tight)

1. **Shape.** Two or three sentences: how the repo is organized and how den is wired in: flake-parts, npins,
   with-inputs, import-tree, namespaces.
2. **Common patterns.** Bullets of recognizable den idioms used, each with `path:line`. Use these names where
   they fit: `define-user+primary-user`, `host-aspects`, `mutual-provider`, `forward`, `den.default includes`,
   `parametric aspect (fn args)`, `provides tree`, `namespace`, `policies`, `custom schema/classes`, `quirks`,
   `angle-bracket refs`, `homes (standalone HM)`, `os-class`.
3. **Novel patterns.** Anything not on that list, or a list idiom used in an unusual way. Give each `path:line`
   and one line on why it's interesting or what problem it solves.
4. **Library candidates.** Self-contained aspects worth generalizing for a community library. Per entry: aspect
   name · path · what it configures · required inputs · how it's parametrized (none / fn args / options) ·
   reuse grade A (drop-in), B (needs light parametrizing) or C (idea only).
5. **den friction.** Workarounds, TODO/FIXME mentioning den, re-implemented batteries, misuse. These are signals
   for den itself. Give `path:line`.
6. **Docs and complexity.** The basis for the two scores.
6a. **Defects and scoring notes.** Record concrete defects as you read, each with `path:line`, the category it
   should cost, and its severity (minor / moderate / major). Typical defects:
   - hard-coded properties leaked into a shared aspect: hostnames, usernames, paths, IPs, ports, emails;
   - a value that should be a setting or option but is fixed inline;
   - concerns that aren't isolated: one aspect doing several unrelated things, or a host file carrying reusable logic;
   - per-host copy-paste;
   - a quirk declared but never consumed;
   - a secret or a private path assumed in a shared aspect.
   These notes feed the scorecard. A score must be explainable from §2-6a; don't deduct for anything not listed here.
   The anchor configs have defects too, so list them for the anchors as well.
7. **Template notes.** What a new den user would learn from this repo, or why it's a bad first example.

8. **Scorecard.** One reviewer per category scores 1-10 against the anchors below. Anchors are at 2, 5 and 9;
   interpolate only with a written reason. Each category gets an **evidence card**: scope inspected · pros
   (`path:line`) · cons (`path:line`) · confidence. Each §6a defect costs **one** primary category only; note
   any knock-on effect without deducting twice. An untraced claim is *unknown*, not zero. Record
   `not_applicable` with a reason rather than inventing a score. Size is context, not merit: a small, clean
   config is never penalized for being small.

   | cat | 2 | 5 | 9 |
   |---|---|---|---|
   | **D data flow** | settings set directly; quirk declarations with no traced producer/consumer | one live emit→consume channel; limited routing/validation; fixed-name lookups remain | several consumers derive config from declared facts via policies/pipes, with explicit semantics for missing/duplicate contributions and scope; full chains shown. Ceremonial quirks earn nothing |
   | **I layout/isolation** | one module mixes unrelated capabilities, or a change needs edits across copied host trees | named features and includes localize most changes; some broad bundles | clear feature ownership and includes/provides boundaries; optional concerns stay optional; layout fits scale |
   | **S settings/variation** | shared aspects embed author identity, paths or endpoints a second host/user must patch | most variation is explicit via args/schema/options; a few personal constants remain | real host/user differences flow through small documented settings contracts with defaults and validation; a second consumer changes settings, not shared source |
   | **R reuse contract** | importing a feature drags in identity, private assets or global defaults | a useful unit needs light parametrizing (grade B) | at least one substantial grade-A unit with explicit inputs, params and platform contract, plus a minimal consumer example; count alone doesn't raise R |
   | **P platform boundaries** | claimed support crosses unguarded platform assumptions | honest narrow support, or several platforms with manual exceptions | platform-specific modules selected cleanly; unsupported uses fail clearly; boundary checks/examples for the claimed scope |
   | **L explanation** | placeholder or operation-only docs; no route from entry point to feature selection | explains wiring and how to add a host/user/feature | teaches composition, routing and prerequisites with examples; separates the default path from internals; volume isn't rewarded |
   | **V verification** | no relevant checks in scope (an observation, not a failing claim) | checks exercise representative outputs; CI invocation traceable | focused checks for enabled/disabled, context variation, collisions/missing data, platform boundaries; passing status kept separate |
   | **O operations** | deploy/secrets/bootstrap done outside den (scripts, hand-kept host lists) or absent though the fleet needs it | one operational concern driven by den: e.g. deploy nodes generated from den hosts, or secrets emitted per aspect | deploy targets, secrets provisioning (emitted via quirks, rekey/generators), install/bootstrap and builders all derive from den host/user data with no hand-kept duplicate lists; per-host overrides are settings. Keeping secrets *out of* shared aspects is an S matter, not O |
   | **X integrations** | den drives only NixOS/HM; other systems configured beside it | one non-NixOS target as a den class with a clean contract (terranix, k8s manifests, microvm guest…) | several targets are first-class den classes fed by the same aspects/quirks as hosts (e.g. terranix + nixidy/argocd + microvm), with clear ownership; trivial classes (devshell/treefmt wrappers) earn little |
   | **B breadth** | see the B rule below | see the B rule below | see the B rule below |

   **Total:** `2D+I+S+R+P+L+O+B+½V+½X = N/100` (one decimal). Then list the three shortlists (§9) and 3-5 overall pros and cons.

   **Rulings (pilot, 2026-11-10):**
   - **not_applicable arithmetic.** Set that category to `null` and record its reason. Front matter then carries
     `score: null`, `score_partial` (the sum of the known terms, not renormalized), `max_applicable` (100 minus the
     weight of the null terms) and `missing: [<cats>]`. Never substitute a 2, and never rescale to /100.
   - **Applicability is not evidence availability (maintainer ruling).** Null and `not_applicable` are only for a category that genuinely does not apply to what the repo is. Private or unavailable inputs never justify null: score the visible code against the anchors with confidence `low`, state what is hidden and which way it could move the score. S is never null. X is never null because it has baseline 2. B is null only for a pure library with no aspects at all; otherwise B_div is computed from the census and B_ref counts only visible complete units. O is null when there is no host and no home, regardless of repo_kind; package-only program profiles qualify. Do not shrink a private config's denominator to its best-evidenced subset.
   - **D without quirks.** Facts stored in schema/entity attributes and read through the context args
     (`{ host, user }`) by consumers that derive config from them form a live emit→consume channel, so they can
     reach 5. Cross-host data gathered by iterating `den.hosts` without a policy or pipe is also capped at 5.
     Reaching a peer by literal name (`den.hosts.<sys>.<name>.…`) is a fixed-name lookup: score ≤ 4 unless a
     routed channel exists elsewhere. Scores of 6 and up need routing through policies or pipes.
   - **X baseline.** darwin, standalone home-manager and other standard OS/home targets are P (platform
     boundaries), not integrations. Using only those scores X = 2. X credits non-host targets driven as den
     classes, such as terranix, k8s/nixidy, microvm guests and droid.
   - **Operational classes are O only.** A custom den class that projects host data into deploy, secrets or
     bootstrap tooling (a `deploy` class feeding deploy-rs, colmena nodes, a rekey class) is credited under O, never
     also under X; one mechanism earns one category. X is for target families whose artifacts are not host
     operations: cloud/infrastructure (terranix), cluster manifests (k8s/nixidy/argocd), guests (microvm), devices
     or other OSes (droid, ESPHome, iOS).

   **Calibration rulings, from pilot gap reconciliation (two independent reviewers, 2026-11-10):**
   - **S is the weaker of two grades.** Contract design is how good the settings mechanism is. Leak coverage
     counts the *distinct* author-specific constants (identity, domains, IPs, paths, endpoints) inlined in
     shared aspects: ≤3 → no cap · 4-10 → cap 6 · 11-30 → cap 5 · more than 30 → cap 4. The S score is the
     lower of the two. Report both grades in the S card.
   - **I for bundles and libraries.** A feature that also performs unrelated side effects (session restarts,
     mutable user state, global defaults beyond its feature) caps I at 6. A hostless library is judged on its
     own module boundaries, with no credit for absent host trees and no penalty for them.
   - **R anchors made concrete.** R2 = no unit a second user could adopt without rewriting its body. R5 = at least
     one unit adoptable by changing ≤3 identified values or arguments. R9 = as written (grade-A unit plus a
     consumer example).
   - **O applicability.** O is `not_applicable` only for repos with no host and no home at all (including package-only program profiles,
     regardless of repo_kind). Every config with ≥1 host or home is scored. A single home activated by hand with no fleet
     scores the baseline 2; that's honest, not a defect. O credits only operations that derive from den data. A
     terranix or deploy tree that never reads den hosts earns nothing.
   - **Weights (maintainer, 2026-11-10):** D ×2; I, S, R, P, L, O and B ×1; V and X ×½. Reviewers still score every
     category 1-10 against the same anchors; only the total weights them.
   - **`max_applicable`** subtracts the null term's weighted maximum: D 20, V and X 5 each, the others 10. A null O
     gives max 90.
   - **B rule.** B is the mean of two sub-grades, rounded half up. Report both in the B card.
     - **B_div, diversity:** a fixed count over the repo's census record. Each family that is selection-verified
       counts 1 if `configuration_depth: substantive` and 0.5 if `enable-only` or installed-only (`none`); each
       named optional peer counts the same way. **Dedup:** each required family and each named peer
       contributes once, at the maximum depth credit across its hosts and implementations, never summed.
       Continuous bands on the total: ≤3 → 2 · ≤5 → 3 · ≤8 → 5 · ≤11 → 7 · >11 → 9.
     - **B_ref, reference aspects:** count, by reading, the aspects that are complete, self-contained references
       for their application: a substantive configuration, no leaked author identity, and the app usable from
       the aspect alone. Bands: ≤2 → 2 · ≤5 → 4 · ≤10 → 5 · ≤19 → 7 · >19 → 9.
       The B card must **list every counted unit** (aspect name · `path:line`). The count is that list, never
       §4's curated nominations and never the census family count. Several files of one app count once.
       Include-only bundles, profiles and role aspects that only `includes` other aspects don't count.
     - No domain is required. A strong desktop-only exemplar can score high; servers aren't mandatory. B is the
       one place breadth is credited, so don't penalize narrow configs elsewhere.
   - **L absence.** No README and no docs at all = 1. A placeholder or operation-only README = 2.
   - **V without CI.** In-tree checks that no CI or recipe invokes cap V at 6. CI that runs only a formatter adds
     nothing.
   - **D partial semantics.** Documented, deliberate merge semantics such as "last wins, by design" count as
     explicit and can reach 9. Silently taking the head of a list, or dropping duplicates without a warning,
     caps D at 7.

   **Scoring rulings (corpus scoring, 2026-11-10):**
   - **Counting distinct leaks (S).** Count what a second user would have to change *once*:
     - a registered domain and all its subdomains = 1;
     - a host's addresses or CIDRs = 1 per host or network;
     - a repo-path root = 1;
     - a username or identity = 1;
     - a cache URL plus its key = 1;
     - a hostname used as a default = 1 per hostname.

     Report the grouped count, and note the raw count beside it.
   - **"Usable from the aspect alone" (B_ref).** An aspect that emits a *standard resource quirk* (persist,
     secrets, firewall and similar) and relies on a collector for it still counts. The library will supply those
     collectors as the standard quirk suite. An aspect that needs a *fleet-specific* aspect, role or schema to
     function does not count.

   - **D and den's default quirk collection.** A quirk emitted by aspects and consumed by another aspect through
     den's built-in quirk collection *is* routed data flow; it isn't capped like schema traversal. Several
     independent live quirk channels, each with a traced producer and consumer, can reach 7. Reaching 8 or 9 needs
     cross-scope routing through policies or pipes (`pipe.from`/`collect`/`expose`/…) across hosts, environments
     or users, plus explicit missing/duplicate semantics. The cap of 5 still applies to non-quirk channels: schema
     facts through context args, or iterating `den.hosts` without a policy.

   - **B_ref threshold: substantive-useful, not any setting.** A unit counts when it's a coherent preset or a real
     integration:
     - several related settings, keybinds or plugins that together shape the app;
     - or integration behavior that's actually wired (for example fzf shell and key bindings, an editor's
       LSP/formatter set).

     A token tweak (`enable` plus one cosmetic or single preference, like `theme_background = false` or one
     default volume) does not count. This is stricter than the census `configuration_depth: substantive`, which
     still drives B_div.
   - **Resource-only units.** `enable` or a package plus *one* standard resource (a persist path, or one secret, or
     one port) is a token unit and doesn't count. Its resource inventory is still worth recording for the library
     harvest. A unit counts as a real integration when it wires *several* resources into a working service (for
     example state persisted, secrets provisioned, firewall or ports opened, a user or group created), or when it
     combines a resource with a real app preset.

   - **Package plumbing is neither D nor X.** Aspects that emit packages through den's default packages→`flake.packages`
     route, consumed via `self'.packages`, are build plumbing:
     - X stays at baseline 2: a package output is not a non-host target family;
     - D gains nothing: a package lookup is not structured-fact flow;
     - good packaging can earn I or R.

     X credit starts only when a den class drives a *distinct module system or output contract*, for example an
     nvf/nixvim module bridge evaluated as its own class, terranix, or k8s manifests. Score that X on the
     contract's depth, not on the package count.

   - **O and hand-kept secret recipients.** Per-aspect secret emission (aspects own their secret entries and
     consumers) is one den-driven operational concern and qualifies for O5, even when recipients or keys are
     enrolled by hand (`.sops.yaml`, a manual key file). Hand-kept recipient or target lists limit only the upper
     band: O8-9 requires provisioning (recipients, rekey and generators) derived from den data with no hand-kept
     list. A generic self-deploy service with fixed remotes (e.g. comin) is not a second derived concern.

   - **Namespaced units.** An otherwise complete aspect registered under a standard den namespace (e.g.
     `adachi.services._.podman`) counts for B_ref. Standard namespace registration or rebinding is an extraction
     contract, not a dependency, and units that need rebinding to adopt are grade B. A unit that needs a fleet
     schema, a custom class router or an unrelated bridge doesn't count.

9. **Shortlists** are separate from the total. A high total doesn't admit a repo to a shortlist.
   - **showcase:** D leads, then the other categories plus a written standout judgment.
   - **library_units:** §4 units graded A/B by adoption cost, explicit dependencies and parameter contract. A
     low-scoring repo can contribute.
   - **starter:** a short entry-to-output path, minimal prerequisites, clear host/user variation, honest platform
     scope. Never reward added machinery.

   Anchors: The reference pattern study is the upper reference for I, O and X. It has real deductions elsewhere (maintainer:
   leaked hard-coded properties, incomplete settings contracts), so no perfect vector is reserved for it. theutz is
   **not** a fixed anchor (maintainer ruling, 2026-11-10). The maintainer's 8 was a rough read of its code and its breadth of
   application coverage. Score it as measured. Application breadth is now scored as B, from census evidence. Scores are
   provisional until the pilot (§10) passes.

10. **Pilot.** Before scoring the corpus, two independent reviewers score a pilot set. A category gap greater than
    2 triggers a fix to the anchor wording, not an average.

Keep each review under roughly 120 lines. Breadth across the corpus matters more than depth on one repo.

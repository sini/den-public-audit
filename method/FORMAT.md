# Machine-checked score accounting

Use the current RUBRIC.md. The validator is stdlib-only: no package installation, network access or repository execution. Front matter may use the documented YAML scalar/map/list subset or a JSON object (JSON is valid YAML). Unsupported YAML constructs fail explicitly.

Every scored review has all ten scores and confidence values: D, I, S, R, P, L, V, O, X, B. Keep other review metadata. Remove obsolete `award: TBD`; award tiers are undefined. Null categories have a front-matter reason, for example:

```yaml
not_applicable: {O: "Pure hostless library; no host or home operations to assess"}
score: null
score_partial: 42.5
max_applicable: 90
missing: [O]
```

The numbers above illustrate the shape, not a calibrated score. Non-null totals use `2D+I+S+R+P+L+O+B+0.5V+0.5X`, to one decimal. The null-term maximum is D 20, V/X 5, all others 10; never renormalize. Shortlists contain `showcase` and `starter` booleans and a `library_units` list of existing §4 A/B unit names. `notable` is a boolean; `score_basis` explains the vector.

Under §8 use a `### D` ... `### B` heading for each category, with scope, cited pros/cons, score and confidence. The S card contains this exact fenced-block type and key shape:

```score-evidence
{"S":{"contract_design":5,"leak_coverage":5,"distinct_leaks":12,"raw_leaks":18}}
```

S is the lower grade. The leak count also enforces the rubric cap: 4–10 constants caps coverage at 6, 11–30 at 5, more than 30 at 4. Explain which distinct leaked constants were counted, with source evidence; file length or occurrence count is not the measure.

The B card contains a separate accounting block:

```score-evidence
{"B":{"diversity_points":4.5,"diversity_grade":3,"reference_grade":2,"reference_units":[{"name":"audio","evidence":"modules/audio.nix:4"}]}}
```

The array is the enumerated list of every counted reference unit: unique aspect name and real clone-relative `path:line`. Empty lists are valid. Several files of one app count once; bundles/profiles that only include other aspects do not count. Complete self-contained substantive units must be read in source; §4 nominations are not an exhaustive inventory.

Diversity points are independently recomputed from enabled, selection-verified census rows: each required family and each named optional peer contributes once, maximum across implementations/targets, 1 for substantive or 0.5 for enable-only/installation-only. Diversity bands are ≤3→2, ≤5→3, ≤8→5, ≤11→7, otherwise 9. Reference bands by array length are ≤2→2, ≤5→4, ≤10→5, ≤19→7, otherwise 9. B is the mean of these grades, rounded half up.

All deductions belong in §6a with one primary category each. Source citations refer to the manifest revision. Tools validate accounting and cited bounds; reviewers must verify meaning, selection and completeness in actual source.


## Applicability versus missing evidence

Private or unavailable evidence does not permit null: score visible code with low confidence and describe the hidden scope and possible direction of change. S and X must be numeric. O is null when there is no host and no home, regardless of repo_kind; package-only program profiles qualify. B null is limited to a pure library with no aspects: its B accounting block must explicitly state `aspects_present: false`, supply cited `scope_evidence: ["path:line"]`, retain the computed diversity fields, and use an empty `reference_units` list. This is a source-reviewed absence assertion, not an inference from an empty software list. All category confidence values remain high/medium/low, even when applicability itself is certain and the score is null.

Grouped S counts follow RUBRIC.md: domain/subdomains, one host or network address set, one repo-path root, one identity, one cache URL/key pair, or one default hostname is each one adaptation group. Include the raw count as a note (the optional `raw_leaks` accounting field can carry it). Standard resource-quirk collectors do not disqualify B reference units; fleet-specific roles, schemas and aspects do.

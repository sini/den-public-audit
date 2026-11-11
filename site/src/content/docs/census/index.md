---
title: "Census files"
---

This folder holds the census: the record of which software each config selects, and which machine roles it has. This
index is for readers who want the raw data behind the census summary. It gives one line for each file, and the
columns of each TSV.

## Contents

- [Start here](#start-here)
- [TSV files](#tsv-files)
- [Per-config census notes](#per-config-census-notes)

## Start here

- [summary.md](/census/summary/): the census summary. It gives the coverage, software selections, window managers by
  platform, host roles and per-repository application breadth, with an explanation above each table.
- [CENSUS.md](/method/census/): the census contract. It defines the tiers, states, modes and counting rules
  that every file here uses.

## TSV files

Every TSV is tab-separated with one header row. The per-repository files cover published configs only. Each of them
starts with the same identity columns: `repo`, `source`, `rev` (the reviewed revision), `repo_kind` (where present)
and `included`. `repo` is the upstream `owner/repo` of the config, the same name that its page uses.

| file | one row per | other columns |
|---|---|---|
| [software.tsv](/census/software.tsv) | software contribution in a config | `item`, `variant`, `tier`, `state`, `mode`, `configuration_depth`, `platform`, `targets`, `users`, `definition_evidence`, `selection_evidence`, `explanation` |
| [targets.tsv](/census/targets.tsv) | declared target (host, home or package) | `key`, `kind`, `name`, `system`, `class`, `users`, `evidence`, `roles`, `notes` |
| [roles.tsv](/census/roles.tsv) | role of one target | `target`, `role`, `certainty` (explicit or inferred), `evidence`, `reason` |
| [coverage.tsv](/census/coverage.tsv) | config | `reviewed`, `inventory_complete`, `targets`, `checked_items`, `unresolved_items`, `notes` |
| [breadth.tsv](/census/breadth.tsv) | config | `selected_families`, `required_families`, `configured_families`, `installation_only_families`, `substantive_families`, `enable_only_families`, `optional_peers`, `selected_family_names`, `optional_peer_names` |
| [repo-counts.tsv](/census/repo-counts.tsv) | aggregate count | `source`, `item`, `platform`, `deployment`, `measure`, `repos`, `host_targets`, `home_targets`, `package_targets`, `user_contexts` |

`repo-counts.tsv` has no per-repository rows. It holds the aggregate counts over all included configs, and the
`measure` column names the tier and mode that a row counts.

## Per-config census notes

- [configs/](https://github.com/sini/den-public-audit/tree/main/census/configs/): one page per published config. Each page links to the config's review page. It has four
  sections:
  1. the project and revision;
  2. the software selected, with its traces;
  3. the defined software and alternatives;
  4. the roles.

---
title: "Source-led adoption and machine-role census, version 1.1"
---

The manifest is `manifest.tsv` (id, source, path, rev). Review **actual source bodies and their selection paths** at that revision. Search is navigation; scripts validate and aggregate reviewed evidence. Never evaluate Nix, run clone code, activate direnv, or treat a package/input/string match as adoption. Read from outside clone directories. For `not-git`, read the manifest working tree and retain that revision marker.

There are two disjoint review lanes: one reviewer owns the 98 public rows; a second owns the 10 local, 11 archived and one anchor row. One shared schema and vocabulary applies to both. Changes to this contract must be coordinated before changing records.

## Contents

- [Deliverables and ownership](#deliverables-and-ownership)
- [Required software families](#required-software-families)
- [Record schema](#record-schema)
- [Software tiers, state and mode](#software-tiers-state-and-mode)
- [What selected means in Den](#what-selected-means-in-den)
- [Machine roles and counting units](#machine-roles-and-counting-units)
- [Readable notes](#readable-notes)
- [Validator and aggregator obligations](#validator-and-aggregator-obligations)
- [Derived deployment and application breadth](#derived-deployment-and-application-breadth)
- [Configuration depth (required in schema 1.1)](#configuration-depth-required-in-schema-11)
- [Included corpus and retained exclusions](#included-corpus-and-retained-exclusions)
- [macOS selection union](#macos-selection-union)
- [Library harvest constraints](#library-harvest-constraints)

## Deliverables and ownership

- `census/records/<id>.json`: one source-led evidence record per manifest row, authored by its assigned reviewer. This is the authoritative census input.
- `census/notes/<id>.md`: readable project findings with the four sections below. It may be rendered from the reviewed JSON, but the interpretation and selection traces must be authored by a reviewer.
- `tools/census.py`: validate records and source citations; render TSVs and summary from those records. It does **not** infer software adoption or host roles from regex matches.
- Generated `census/software.tsv`, `census/targets.tsv`, `census/roles.tsv`, `census/repo-counts.tsv`, `census/coverage.tsv`, `census/breadth.tsv`, `census/excluded.tsv` and `census/summary.md`. All tables retain source tags; report overall and per-source counts.

Files remain uncommitted until validated. Only the assigned controller commits, with explicit paths. Partial runs must state reviewed/missing record counts and must not call an unreviewed project a negative finding.

## Required software families

| group | item identifiers |
|---|---|
| window managers/desktops | aerospace, yabai, niri, hyprland, sway, gnome, kde |
| editors | neovim, vscode, emacs, helix, zed |
| multiplexers | tmux, zellij |
| shells | zsh, fish, nushell, bash |
| prompts | starship |

These 19 families must be checked in every review. Keep variants: neovim may be raw, nixvim, nvf or another named frontend; vscode may be vscode or vscodium; kde includes Plasma. Do not count nixvim/nvf input pins alone as a configured editor. A standalone configured editor package output is a package target, not a managed host.

Optional peers encountered while reading may use `other_wm`, `other_editor`, `other_multiplexer`, `other_shell`, `other_prompt`, with `variant` naming the software. Their presence can be reported; the required-family coverage claim does not establish exhaustive absence of all peers. Terminal emulators are not multiplexers merely because they have tabs.

## Record schema

Use UTF-8 JSON and the literal field names/types below. No score fields.

```json
{
  "schema_version": "1.1",
  "id": "manifest-id",
  "source": "public",
  "rev": "manifest-revision-or-not-git",
  "reviewed_by": "reviewer-a",
  "review_complete": true,
  "repo_kind": "config",
  "inspected_paths": ["flake.nix", "modules/hosts.nix", "modules/desktop/niri.nix"],
  "inventory_complete": true,
  "inventory_notes": "How inventory was followed; dynamic portions or omissions.",
  "targets": [{
    "key": "host:x86_64-linux:atlas",
    "kind": "host",
    "name": "atlas",
    "system": "x86_64-linux",
    "class": "nixos",
    "users": ["alice"],
    "evidence": ["modules/hosts.nix:3"],
    "roles": [{"role": "desktop", "certainty": "explicit", "evidence": ["modules/hosts.nix:7"], "reason": "Selects roles.workstation."}],
    "notes": "Inventory and user/profile interpretation."
  }],
  "software": [{
    "item": "niri",
    "variant": "niri",
    "tier": "selection-verified",
    "state": "enabled",
    "mode": "configured",
    "configuration_depth": "substantive",
    "platform": "nixos",
    "targets": ["host:x86_64-linux:atlas"],
    "users": ["alice"],
    "definition_evidence": ["modules/desktop/niri.nix:4"],
    "selection_evidence": ["modules/hosts.nix:7", "modules/roles/workstation.nix:6"],
    "explanation": "Host selects workstation, which includes niri; the NixOS class enables it. Explain any guards."
  }],
  "references": [{"item": "hyprland", "evidence": ["flake.nix:18"], "explanation": "Input only; no live configuration found in the inspected scope."}],
  "coverage": {
    "checked_items": ["aerospace", "yabai", "niri", "hyprland", "sway", "gnome", "kde", "neovim", "vscode", "emacs", "helix", "zed", "tmux", "zellij", "zsh", "fish", "nushell", "bash", "starship"],
    "not_found": ["aerospace", "yabai", "hyprland", "sway", "gnome", "kde", "neovim", "vscode", "emacs", "helix", "zed", "tmux", "zellij", "zsh", "fish", "nushell", "bash", "starship"],
    "unresolved_items": [],
    "notes": "A negative means no live definition found within the inspected source scope, not proof of runtime absence."
  },
  "notes": {
    "project": "What the project configures and how its aspects are organized.",
    "selection": "Host/user/default/policy wiring and why these software choices apply.",
    "software": "Notable alternatives, frontend variants, installation versus configuration, shell availability versus login choice.",
    "roles_and_limits": "Machine purpose, explicit versus inferred roles, unknowns and prerequisites."
  }
}
```

`repo_kind`: `config`, `library`, `template`, `den-fork`, `mixed`, `unknown`. Preserve library/template entries in the corpus but distinguish their definitions from deployed selections. Fixtures, example trees and documentation snippets are not managed targets unless the root configuration actually selects them.

`kind`: `host`, `home`, `package`. Keys are unique within the record; use `<kind>:<system>:<name>`. Use `unknown` for a genuinely unresolved system/class, with explanation. A standalone home is not an additional physical machine; a package output is not a host. Do not enumerate an unknown dynamic host set as a single fake host. Set `inventory_complete: false` and explain what remains unresolved.

Citations are repo-relative `path:line`, at `rev`; list each path separately, with positive integer line numbers. No basename shorthand, line ranges or prose punctuation inside citation strings. `inspected_paths` names real source files read; a hit list alone does not satisfy review.

## Software tiers, state and mode

- `defined`: a live configuration/install contribution exists, but the reviewer has not established that a declared target selects it. Include its definition evidence; keep targets empty unless the definition's scope is itself clear. This is availability in source, not adoption.
- `selection-verified`: follow a concrete declared target through selected aspects/imports, defaults, providers or policies to the software contribution, including platform/conditional guards. Supply a nonempty target list, definition evidence and selection evidence. This is static configuration reachability, not proof of successful evaluation, activation or runtime use.
- `ambiguous`: a relevant contribution exists, but dynamic selection, conditions, patched APIs, external/private modules or unresolved context prevent a defensible selection conclusion. Explain the unresolved step. An ambiguous row is not a zero or a verified selection.

`state`: `enabled`, `disabled`, `conditional`, `unknown`. An explicit false/disabled configuration never contributes to enabled-adoption totals. A condition is only enabled when the reviewed target's facts resolve it; otherwise use ambiguous/conditional.

`mode`: `configured`, `installed`, `default`. `configured` requires actual settings/enable wiring or supplied native configuration files; `installed` means package/cask selection alone; `default` requires explicit default-session/login-shell/editor selection. Installing a WM/editor/shell does not make it the default. A package can have multiple rows if modes differ, but aggregation deduplicates family/repo or family/target.

`platform`: `nixos`, `darwin`, `home-linux`, `home-darwin`, `home-unknown`, `other-os`, `package`, `unknown`. This is where that contribution applies, not merely the system mentioned by an input. Do not report Home Manager on generic Linux as NixOS.

The required families must each appear in software, coverage.not_found, or coverage.unresolved_items. `unresolved_items` is a list of item identifiers; explain each unresolved case in coverage.notes or an ambiguous software row. Do not put a family in not_found when a live definition was found. Input-only references may coexist with not_found, because inputs are not configuration definitions.

## What selected means in Den

Read the actual aspect body, including native config assets where the body imports them. A complete trace usually connects inventory → host/profile includes → user/feature → class contribution. Account for:

- `den.hosts` block declarations and helper-built inventories, not just dotted assignments.
- `den.default` and schema includes; determine the target/class receiving them rather than assuming every key affects every user.
- User aspects and host-qualified home aspects. Do not infer user configuration from host inclusion without verifying `host-aspects`, `mutual-provider`, explicit forwarding, or equivalent policy wiring.
- `provides` trees, namespaces, path-derived aspect names, angle-bracket refs, exclusions and custom class routes. A provider's existence does not mean it was selected.
- Conditions in class functions, `mkIf`, platform arms and settings/profile switches. Follow values far enough to decide; preserve ambiguity when that requires evaluation.
- Non-Den legacy imports that the selected aspect delegates to. These still count when their import path and configuration are clear.

A row may reference several targets only when the same contribution/mode/platform trace holds for each. Separate rows when selection/state differs. `users` lists declared user names reached by this row; use an empty list for system scope or unresolved users and explain which. Never infer a default shell merely from `programs.<shell>.enable`.

## Machine roles and counting units

Roles are nonexclusive: `server`, `laptop`, `desktop`, `wsl`, `vm`, `darwin`. Normalize workstation to desktop and explain the source term. A desktop may also run server workloads; VM and WSL describe execution environment, not physical form. Record unknown purpose in target notes; do not invent a role to fill a table.

- `explicit`: source or project documentation identifies the role, a selected named role/profile states it, a clearly named inventory entry states it, or an explicit WSL/guest/Darwin class/import establishes it. Cite the declaration and selection where relevant.
- `inferred`: hardware model, chassis declaration, battery/lid configuration, or coherent workload evidence supports a role without an explicit role declaration. State the inference and its basis. GUI enablement alone does not prove laptop versus desktop; SSH alone does not prove server. Hypervisor software on a host does not make that host a VM.

Report distinct repository counts and distinct **declared host target** counts separately. Deduplicate host counts by `(repo id, target key)`, and role counts by that key plus role. Publish explicit and inferred role totals separately; they can overlap across roles but must not double-count one target within the same role. Homes/packages remain separate target tables and never inflate machine totals.

Do not call repositories or Unix account names unique human users. Optional user-context counts use `(repo, target key, username)` and remain explicitly labeled configured contexts. Repo frequency is a configuration-adoption measure, not a survey of distinct people or running machines.

## Readable notes

Each `notes/<id>.md` has: (1) Project and inspected revision; (2) software selected and the host/user traces; (3) defined/disabled/ambiguous alternatives; (4) machine roles, inference basis and remaining unknowns. Cite actual source locations. Link the matching record. Explain surprising combinations rather than only emitting a list of hits.

## Validator and aggregator obligations

`tools/census.py` must validate:

1. IDs/source/revision match manifest; records are unique; missing reviews remain missing. Resolve all source citations and inspected paths at the recorded Git revision, or the recorded non-Git working tree.
2. Required fields/types/vocabulary, all 19 families checked or explicitly unresolved, and positive line bounds. Require explanations/evidence for every adoption/role claim.
3. Selection-verified rows have real target keys and selection evidence; disabled/conditional/unknown rows cannot inflate enabled totals. References alone never become software rows automatically.
4. Host roles have valid certainty/basis; homes/packages do not count as physical hosts. Report incomplete inventories and per-source coverage.
5. Deterministic TSV rendering and deduplication. Separate selection-verified configured/default, selection-verified installation-only, defined, ambiguous and disabled counts. A multi-WM/editor repo can count in several families; rows are not mutually exclusive.

The tool cannot prove the reviewer's semantic judgment. Require source-reading spot checks, including positive/negative controls: comments/input-only pins, disabled alternatives, a provider never selected, a standalone home, helper-built hosts, and a real default/host-aspects selection chain. Tests use synthetic fixtures or recorded source data and never execute clone code. Count summaries link back to records/notes so users can challenge them.

## Derived deployment and application breadth

Aggregation distinguishes the contribution platform from its selected target: Home Manager software attached to a NixOS host contributes to deployment=nixos; a standalone Linux home contributes to deployment=home-linux. This derives from reviewed target kinds and classes, without changing evidence records or assuming a host for a standalone home. Use deployment=darwin for AeroSpace on macOS and deployment=nixos for Niri versus Hyprland on NixOS.

`breadth.tsv` and the per-project summary table count distinct required families with enabled, selection-verified evidence, out of 19. Configured/default families and installation-only families are separate; multiple implementations or hosts do not inflate the family count. Optional peers retain their names and a separate count. Breadth describes observed application coverage, never quality or unique people. Ambiguous selections are excluded, and incomplete inventories remain explicit.

## Configuration depth (required in schema 1.1)

Every software row carries `configuration_depth`: `enable-only`, `substantive`, or `none`. Set it by reading the aspect body and any supplied native configuration, never from names. `none` means installation-only (`mode=installed`); the other modes require either `enable-only` or `substantive`. Bare enable wiring and selecting a default without further settings are `enable-only`; meaningful application settings, integrations or supplied native configuration are `substantive`. Retain the existing `mode`: a default shell can have either depth. Explain the distinction and cite the inspected configuration. This field describes even unselected definitions, without promoting them to adoption.

## Included corpus and retained exclusions

The maintainer-directed id table in `EXCLUDED.md` is the exclusion authority. Keep original `source` provenance in manifest and records; moved-clone paths remain recorded in the manifest. The validator checks every manifest evidence record, including excluded entries. Rendering reads the table (CLI `--exclusions`, default audit-root `EXCLUDED.md`) and excludes those ids from all corpus aggregates and the main breadth/role/platform summary. The current evidence set is 120 entries; the included corpus is 108, with twelve excluded.

Raw `software.tsv`, `targets.tsv`, `roles.tsv`, `coverage.tsv` and `breadth.tsv` retain evidence for all manifest entries and carry an `included` flag. Filter this flag before making corpus totals. `repo-counts.tsv` already contains only included entries. `excluded.tsv` and the summary appendix retain excluded ids, reasons and source links; they never enter headline counts. In particular, excluded `gwenodai-nixos` cannot double-count included `Gwenodai/nixos`.

## macOS selection union

The derived `deployment=macos` axis combines declared Darwin host targets and standalone homes whose declared system ends in `-darwin`, for every software family. It deduplicates repositories across both kinds while retaining separate host/home target counts. The narrower `deployment=darwin` axis continues to mean OS-host class Darwin. Thus a standalone Darwin Home Manager AeroSpace configuration counts toward macOS software selection without creating a machine. Generic Linux standalone homes still do not imply NixOS.

## Library harvest constraints

Maintainer ruling, 2026-11-10: lucasshiva, a config whose source is no longer public and two configs whose source is no longer public are included census and aspect-library sources. No license was found for lucasshiva or a config whose source is no longer public: re-implement ideas independently or obtain the author's permission; do not copy their code verbatim. Census inclusion and reuse grades do not grant copying permission.

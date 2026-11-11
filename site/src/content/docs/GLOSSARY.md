---
title: "Glossary"
---

This glossary defines the terms that the audit docs use. It is for every reader of the audit, and most of all for
readers who are new to den. Each term has one meaning, and every doc in this repository uses it with that meaning.

The first section paraphrases den's own glossary. The second section defines the terms of this audit. For den's
original wording, see [den's glossary](https://github.com/denful/den/blob/main/docs/src/content/docs/reference/glossary.mdx).

## Contents

- [den terms](#den-terms): [aspect](#aspect) · [battery](#battery) · [class](#class) · [context](#context) ·
  [entity](#entity) · [entity kind](#entity-kind) · [freeform](#freeform) · [includes](#includes) ·
  [parametric](#parametric) · [policy](#policy) · [provides](#provides) · [provider](#provider) ·
  [resolution](#resolution)
- [Audit terms](#audit-terms): [category](#category) · [census](#census) · [census family](#census-family) ·
  [config](#config) · [configuration depth](#configuration-depth) · [defect](#defect) ·
  [evidence card](#evidence-card) · [excluded repo](#excluded-repo) · [namespace library](#namespace-library) ·
  [partial total](#partial-total) · [published config](#published-config) · [reference unit](#reference-unit) ·
  [review](#review) · [scorecard](#scorecard) ·
  [selection-verified / defined / ambiguous](#selection-verified--defined--ambiguous) · [shortlist](#shortlist) ·
  [total](#total) · [withheld config](#withheld-config)

## den terms

These terms come from den. The definitions paraphrase den's glossary. Each one links to the den doc that explains
the term.

### aspect

An aspect is a named, composable attribute set. It holds one module for each class (for example `nixos`,
`homeManager` or `darwin`), an `includes` list and nested aspects (`den.aspects.<aspect>.<name>`). The aspect is
den's main unit of organisation. One aspect groups related configuration for many module systems under one name.

See [Aspects](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/aspects.mdx).

### battery

A battery is a reusable provider that den ships under `den.batteries`. Its aliases are `den.provides` and `den._`.
Batteries do common configuration tasks, for example user creation, hostname setup and home environment integration.

See [Batteries](https://github.com/denful/den/blob/main/docs/src/content/docs/reference/batteries.mdx).

### class

A class is a Nix module evaluation domain: `nixos`, `darwin`, `homeManager`, `hjem`, `maid`, `user`, `os` or a
custom class. The class sets which module system evaluates the configuration. A class is not an entity kind.

See [Aspects](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/aspects.mdx).

### context

A context is the data shape that flows through the resolution pipeline, for example `{ host }`, `{ host, user }` or
`{ home }`. A context is a real function argument that carries entity references. It is not a NixOS module argument
(`{ config, pkgs, lib, ... }`), and it is not `_module.args`.

See [Context pipeline](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/context-pipeline.mdx).

### entity

An entity is a typed data declaration: a host, a user or a home. An entity carries metadata (name, system, class)
and freeform attributes. Aspects and policy resolve functions can read these attributes.

See [Entities](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/entities.mdx).

### entity kind

The entity kind is the type of an entity: `host`, `user` or `home`. You can add custom kinds with `den.schema`.
Entity kinds control policy dispatch. An entity kind is not a class.

See [Entities](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/entities.mdx).

### freeform

Freeform attributes are attributes on an entity that have no declared option. They are arbitrary key-value data, and
aspects read them through the context. With freeform attributes, an entity can carry ad-hoc metadata without a schema
change.

See [Entities](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/entities.mdx).

### includes

`includes` is a list of aspect references on an aspect or a stage. It declares dependencies: "this aspect needs
these other aspects, resolved with it". All the includes together make a directed acyclic graph (DAG).

See [Aspects](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/aspects.mdx).

### parametric

A parametric aspect is a context-aware function. Its argument shape sets when it applies. For example,
`{ host }: ...` runs only in host contexts, and `{ host, user }: ...` runs only in user contexts. Den reads the
function arguments and dispatches automatically, so a bare function in `includes` needs no wrapper. The explicit
`den.lib.parametric` wrapper is deprecated.

See [Parametric aspects](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/parametric.mdx).

### policy

A policy is a context-driven function that declares a directed edge between entity kinds. It takes a context, for
example `{ host, ... }` or `{ host, user, ... }`, and returns a list of effects (includes, routes, provides). A
policy fires when the scope context satisfies its argument signature. Policies are about entity topology, not about
stages.

See [Policies](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/policies.mdx).

### provides

`provides` has two different meanings:

| where | meaning |
|---|---|
| on an aspect | `provides` (alias `_`) is the legacy namespace for nested aspects. It is still necessary for the cross-entity keys `to-users`, `to-hosts` and `<host>` on a user aspect. You write other nested aspects directly. |
| at the top level | `den.provides` is an alias for `den.batteries`, the reusable providers that den ships. |

See [Aspects](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/aspects.mdx) and
[Batteries](https://github.com/denful/den/blob/main/docs/src/content/docs/reference/batteries.mdx).

### provider

A provider is an aspect for reuse through `includes`. The batteries (`den.batteries.*`) are the built-in providers,
but any aspect can be a provider.

See [Batteries](https://github.com/denful/den/blob/main/docs/src/content/docs/reference/batteries.mdx).

### resolution

Resolution is the process that makes the final module for an entity. It walks the aspect graph of the entity,
applies parametric dispatch and collects the modules for each class. The result is a final NixOS, Home Manager or
Darwin module. The fx pipeline drives resolution.

See [Context pipeline](https://github.com/denful/den/blob/main/docs/src/content/docs/explanation/context-pipeline.mdx).

## Audit terms

These terms belong to this audit. The [README](/) and the [method docs](/method/) use them.

### category

A category is one scored dimension of a config. Each category gets a score from 1 to 10. There are ten categories:

| letter | category |
|---|---|
| D | data flow |
| I | layout and isolation |
| S | settings contracts |
| R | reuse |
| P | platform boundaries |
| L | explanation |
| V | verification |
| O | operations |
| B | breadth |
| X | integrations |

### census

The census is the record of which software each config selects, and which machine roles it has. See the
[census summary](/census/summary/).

### census family

A census family is one of the 19 software groups that the census checks, for example window managers, editors and
shells. See the [census contract](/method/census/).

### config

A config is a den configuration repo that declares its own hosts or homes. The audit names each config by its
upstream `owner/repo`, as the forge spells it, for example `Keyruu/shinyflakes` or `~theutz/flake`. Its review page
is `configs/<owner>/<repo>.md`, without the sr.ht `~`. The census TSVs name it in their `repo` column.

### configuration depth

The configuration depth tells how much a config configures one piece of software. It has three values:

| value | meaning |
|---|---|
| substantive | the config supplies meaningful settings, integrations or native configuration files |
| enable-only | the config only enables the software, or only selects it as a default |
| installed-only | the config only installs the package; the census data records this as `none` |

### defect

A defect is a cited problem that costs exactly one primary category. Each review lists its defects in section 6a.

### evidence card

An evidence card covers one category in a review. It gives the scope, the pros and the cons (each with a
`path:line` citation), the score and the confidence.

### excluded repo

An excluded repo is not a den config. It can be a clone, a duplicate, a library or a superseded repo. An excluded
repo is not scored. See [method/EXCLUDED.md](/method/excluded/).

### namespace library

A namespace library is a repo that exports a den aspect namespace for others, and has no machines of its own. See
[libraries/](/libraries/).

### partial total

A partial total is a total with one category not applicable. A partial total is not rescaled, and it is not
ranked.

### published config

A published config is a config with a page in this audit. There are 103 published configs. See the
[list of config pages](/configs/).

### reference unit

A reference unit is an aspect that is complete and self-contained for one application. It owns its activation and
has no leaked identity. Reference units count toward category B.

### review

A review is the page for one config. It gives the shape, the patterns, the library candidates, the den friction,
the defects and the scorecard.

### scorecard

The scorecard is section 8 of a review. It has one evidence card per category, plus the total. The README shows
[how to read a scorecard](/#how-to-read-a-scorecard).

### selection-verified / defined / ambiguous

These three values tell whether a config selects a piece of software:

| value | meaning |
|---|---|
| selection-verified | a traced den selection path selects the software |
| defined | the config declares the software, but never selects it |
| ambiguous | static reading cannot decide whether the config selects the software |

### shortlist

A shortlist is a list judged apart from the total. There are three shortlists: showcase, starter and library units.

### total

The total is the weighted sum of the category scores, out of 100: 2D + I + S + R + P + L + O + B + ½V + ½X.

### withheld config

A withheld config is scored and counted, but has no page, because its source is no longer public. There are
5 withheld configs.

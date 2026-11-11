---
title: "Excluded repositories"
---

This page lists the excluded repos: repos found during collection that are not scored. It is for readers who look
for a repo and can't find its page. It tells how each repo was checked, and why it was left out.

## Contents

- [How a repo was excluded](#how-a-repo-was-excluded)
- [Excluded repos](#excluded-repos)
- [Included configs whose source is no longer public](#included-configs-whose-source-is-no-longer-public)

## How a repo was excluded

Some repositories found during collection were reviewed, but do not count toward the corpus totals and have no page
here. Each was checked for unique value first: the distinctive patterns from its review were searched for across
the rest of the corpus. A repo was excluded when all its patterns appeared elsewhere, or when it is not a den
configuration.

## Excluded repos

Each row gives one excluded repo and the reason for its exclusion.

| repository | why excluded |
|---|---|
| gwenodai-nixos | an older clone of the same upstream as `Gwenodai/nixos`, which is the newer copy and is included |
| vic/yen | a den-derived engine and fleet library, not a config: no hosts or homes |
| denful/with-inputs | not a config: den's input-helper library |
| crocuda/crocuda.nixos | an aspect namespace library, not a config; [audited separately](/libraries/crocuda/crocudanixos/) |
| crocuda/normal.nixos | an aspect namespace library, not a config; [audited separately](/libraries/crocuda/normalnixos/) |
| adanoelle/garden-shell | an aspect namespace library, not a config; [audited separately](/libraries/adanoelle/garden-shell/) |
| slashfiles | superseded by `theutz`, the same author's newer repo, so including both would count one person twice |
| a config whose source is no longer public | a den host's `mainModule` handed to a non-den flake builder; the pattern also appears in three included configs |
| a config whose source is no longer public | an installer ISO as a den host; installer hosts appear in 18 included configs |
| a config whose source is no longer public | no novel pattern |
| a config whose source is no longer public | not a config: a den bug-reproduction template |
| a config whose source is no longer public | demoted by the maintainer |

## Included configs whose source is no longer public

Three included configs whose source is no longer public stay in the corpus totals, the score distributions and
the census. They have no page, row or citation here.

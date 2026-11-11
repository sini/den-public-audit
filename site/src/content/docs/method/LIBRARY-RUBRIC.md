---
title: "Aspect namespace library rubric"
---

> **Adopted revision (2026-11-10):** use the categories, anchors and unit inventory in
> `LIBRARY-RUBRIC-REVIEW.md` §"Revised categories" and §"Q weight and the inventory". They supersede the draft
> table below.
> - The categories are E, N, K, Q, C, U and T. Q counts twice, so the total is out of 80.
> - Breadth is not scored. It's published as a per-unit inventory with unit kinds (application,
>   integration-adapter, constructor, tool), so a theme adapter isn't counted as an app preset.
> - Q8-9 is **provisional** until a minimal standard resource-protocol design pointer is frozen. Until then,
>   score the semantics shown in source and mark target-suite fit as provisional.
> - Two additional judgments per library: *consumer-ready as published* and *useful rewrite prior art*.
> - Pilot the 3 libraries with two independent readers before expanding.

(The original draft follows for reference.)

Scope: repos that export a den aspect namespace for others to import and run no machines of their own
(`LIBRARIES.md`). These repos are the prior art for the community aspect library, and the questions are the ones
a library *consumer* asks. Static reading only, at the manifest rev, with every claim cited `path:line`.

## Categories (1-10 each, anchors at 2 / 5 / 9)

| cat | question | 2 | 5 | 9 |
|---|---|---|---|---|
| **E export contract** | Can a consumer import it and know what they get? | no stable entry point; the consumer must read internals | a documented flake/namespace entry; aspects reachable by name; some internal leakage | an explicit, versioned export (namespace + flake module); a stable aspect index; internals kept private |
| **N namespace hygiene** | Does it stay in its lane? | writes global den state (`den.default`, foreign namespaces, global options) on import | mostly self-contained; a few global defaults | nothing applies unless the consumer includes it; no global side effects; no collisions |
| **K parametrization** | Can a second user adapt it without forking? | author identity, paths and endpoints hard-coded | args/options for most variation; a few fixed choices | small documented settings contracts with defaults; identity always supplied by the consumer |
| **Q resource contract** | Does it declare what it needs from the host? | persist, secrets, firewall and users configured directly and silently | some resources via quirks or options, the rest direct | every persisted path, secret, port and user is emitted through standard resource quirks a consumer can collect |
| **U consumer docs** | Can someone adopt it from the docs? | none, or "my dots" | a README with install and an aspect list | per-aspect docs, a worked consumer example, and the prerequisites stated |
| **T tests / examples** | Is consumption exercised? | none | a test template that instantiates a consumer | checks covering include/exclude, parametrization and platform boundaries for the exported aspects |
| **D dependency surface** | What does adopting it drag in? | many unpinned or overlapping inputs, a fork of den, or private inputs | a moderate input set, mostly follows-able | a minimal input set; follows-friendly; no den fork; no private inputs |
| **W breadth of units** | How much reusable value? | ≤3 complete units | 6-10 complete units | >19 complete, self-contained units (the config rubric's B_ref threshold applies) |

Total = E + N + K + Q + U + T + D + W, out of 80. No category is weighted, since every one matters for adoption.
Q is the one that matters most for our rewrite plan: the community library rewrites onto a standard quirk suite,
so a library already shaped that way is the closest to adoptable.

## Output

`<id>` per library: §1 shape, §2 the export contract as a consumer sees it, §3 notable patterns
(path:line), §4 units (name · path:line · resources touched · grade A/B/C), §5 defects (path:line, one primary
category), §6 scorecard (evidence card per category), §7 lessons for our library.

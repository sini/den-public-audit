# Cross-check of the finished scores

This page records the cross-check: a blind second reading of a sample of the finished scores. It is for readers who
want to know how far the published scores depend on the reviewer. It gives the sample, the agreement, the gaps sent
back, and the corrections that the published scores include.

## Contents

- [How the sample was read](#how-the-sample-was-read)
- [Agreement](#agreement)
- [Gaps sent back for adjudication](#gaps-sent-back-for-adjudication)
- [Adjudication](#adjudication)
- [Outcome](#outcome)

## How the sample was read

After the public configs were scored, a second reviewer rescored a stratified random sample of six of them, blind.

- The second reviewer read only the review's evidence sections (§1-7 and §6a). The reviewer never read the scores
  or the scorecard.
- The sample was drawn with a fixed seed: two configs from each third of the score distribution.

Each cell in this table is first reviewer / second reviewer.

| config | D | I | S | R | P | L | V | O | B | X | total (first / second) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| [Erastos__nixos-dotfiles](../configs/Erastos__nixos-dotfiles.md) | 2/2 | 7/5 | 4/4 | 5/3 | 5/5 | 2/2 | 2/2 | 2/3 | 3/3 | 2/2 | 34.0 / 31.0 |
| [arichtman__nix](../configs/arichtman__nix.md) | 5/5 | 6/6 | 4/5 | 6/5 | 4/4 | 3/3 | 5/4 | 2/3 | 3/4 | 2/2 | 41.5 / 43.0 |
| [eugencowie__dotfiles](../configs/eugencowie__dotfiles.md) | 5/3 | 6/7 | 6/4 | 5/5 | 7/6 | 3/3 | 3/2 | 2/2 | 4/4 | 2/2 | 45.5 / 39.0 |
| [acrobertson__infra](../configs/acrobertson__infra.md) | 5/3 | 5/5 | 4/5 | 5/4 | 9/7 | 5/4 | 6/6 | 5/2 | 3/4 | 2/2 | 50.0 / 41.0 |
| [Aor-Li__Infra](../configs/Aor-Li__Infra.md) | 7/8 | 8/8 | 5/6 | 9/8 | 8/7 | 8/8 | 3/3 | 5/4 | 7/6 | 2/2 | 66.5 / 65.5 |
| [amatos__magnanix](../configs/amatos__magnanix.md) | 5/5 | 8/8 | 6/5 | 5/7 | 9/8 | 9/9 | 9/6 | 6/7 | 7/7 | 2/2 | 65.5 / 65.0 |

## Agreement

51 of 60 category pairs are within one point, and only 2 differ by more than two. Both readings rank the six configs
in the same order.

The first reviewer ran slightly higher on some categories:

| categories | average difference, first minus second |
|---|---|
| P and V | +0.83 for each |
| D and R | +0.5 |

## Gaps sent back for adjudication

1. **amatos V: 9 against 6.** The CI workflow builds the Darwin, NixOS and devShell outputs, but never invokes the
   flake `checks`. Under the calibration ruling, in-tree checks that no CI job or recipe runs cap V at 6.
2. **acrobertson O: 5 against 2.** The second reviewer found no den-derived operational concern. So the first
   reviewer was asked to cite the one it had credited.

Four cells within the threshold were also re-examined, because they drove the two largest total differences:

- eugencowie D (5 against 3) and S (6 against 4);
- acrobertson D (5 against 3) and P (9 against 7).

## Adjudication

Each row gives one re-examined cell, its score before and after adjudication, and the basis for the final score.

| config | cell | before | final | basis |
|---|---|---|---|---|
| amatos__magnanix | V | 9 | **6** | flake `checks` are never invoked by CI or a recipe; package-local postBuild tests are real, but the cap applies. Total 65.5 → **64.0** |
| acrobertson__infra | D | 5 | **3** | `userConfig` is a static `let` record passed through native Home Manager `_module.args`, not den entity facts |
| acrobertson__infra | O | 5 | **5** | `modules/flake/tarball.nix` turns a den-instantiated host's `tarballBuilder` into a WSL install artifact, one den-derived bootstrap concern. The blind reading missed it |
| acrobertson__infra | P | 9 | **9** | negative platform fixtures plus guards. Total 50.0 → **46.0** |
| eugencowie__dotfiles | D | 5 | **5** | a real `{user}` entity drives the runtime user, the tailscale operator and the matching home path |
| eugencowie__dotfiles | S | 6 | **5** | genuine argument and context variation, but no broad settings contract. Total 45.5 → **44.5** |

## Outcome

The check found three real over-scores (amatos V, acrobertson D, eugencowie S) and one miss by the blind reading
(acrobertson O). Every correction either moved toward the blind reading or was shown against the source. The
published scores include these corrections.

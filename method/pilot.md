# Scoring pilot

This page records the scoring pilot: the calibration step before the corpus was scored. It is for readers who want
to know how far two independent reviewers agree under the rubric. It also tells how the rubric anchors changed.

## Contents

- [What the pilot did](#what-the-pilot-did)
- [Agreement](#agreement)
- [Final pilot vectors](#final-pilot-vectors)

## What the pilot did

Before the corpus was scored, two independent reviewers scored seven calibration configs. Each reviewer read the
source against the draft rubric, blind to the other's scores.

- The draft had nine categories. Application breadth (B) was added after the pilot, from census evidence.
- The set includes the reference anchor, a hostless library and configs from across the score range.

## Agreement

In the first blind pass, 48 of 61 category pairs were within one point, and 4 differed by more than two.

The rubric treats a gap of more than two as a defect in the anchor wording. It does not average the gap away. Each
such gap was traced to an ambiguous anchor, and the anchor was rewritten. The rewrites are the calibration rulings in
[RUBRIC.md](RUBRIC.md) §8:

- S as the weaker of a contract grade and a leak-count grade;
- the I cap for bundles;
- concrete R anchors;
- O applicability;
- the partial-total arithmetic.

Both reviewers then rescored only the gap cells under the new wording.

After reconciliation, 53 of 62 category pairs are within one point, and 0 differ by more than two.

## Final pilot vectors

Each cell is reviewer A / reviewer B. A dash means not applicable.

These are pilot vectors under the draft rubric, not the published scores. The corpus scores add B and apply the
final weights, and they were written after the pilot.

| config | D | I | S | R | P | L | V | O | X |
|---|---|---|---|---|---|---|---|---|---|
| [sini__nix-config](../configs/sini__nix-config.md) | 9/8 | 9/9 | 5/5 | 5/6 | 8/8 | 6/7 | 6/6 | 9/8 | 9/9 |
| [theutz](../configs/theutz.md) | 6/6 | 7/7 | 3/5 | 5/5 | 5/7 | 1/1 | 2/2 | 7/6 | 2/2 |
| [auscyber__dotfiles](../configs/auscyber__dotfiles.md) | 9/8 | 7/9 | 6/7 | 4/5 | 7/8 | 7/7 | 8/8 | 8/8 | 7/9 |
| [DylanRJohnston__nixos](../configs/DylanRJohnston__nixos.md) | 5/5 | 7/9 | 5/5 | 6/5 | 7/9 | 5/5 | 8/9 | 5/5 | 2/2 |
| [SyahrulBhudiF__dotfiles](../configs/SyahrulBhudiF__dotfiles.md) | 2/2 | 4/5 | 2/2 | 3/5 | 5/5 | 2/2 | 2/2 | 2/2 | 2/2 |
| [adanoelle__garden-shell](../libraries/adanoelle__garden-shell.md) | 2/2 | 5/6 | 3/5 | 5/5 | 4/5 | 5/5 | 3/4 | –/– | 2/2 |
| [Keyruu__shinyflakes](../configs/Keyruu__shinyflakes.md) | 7/7 | 7/8 | 5/6 | 3/5 | 5/5 | 4/3 | 4/5 | 4/5 | 3/2 |

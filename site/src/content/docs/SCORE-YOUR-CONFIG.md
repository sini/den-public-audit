---
title: "Score your own config"
---

You can score your own den config with the same rubric as the survey. Use an AI coding agent that can read your
repository. This page gives you a prompt to paste into the agent, then tells you how to read the result and how to
share it with us.

A self-score is a useful estimate, but it is not an official score. The survey scores were made by two independent
reviewers and checked blind. Your agent works alone, so its result can differ from ours by a point or two in a
category.

## Contents

- [What you need](#what-you-need)
- [The prompt](#the-prompt)
- [How to read the result](#how-to-read-the-result)
- [Compare with the survey](#compare-with-the-survey)
- [Share your score or add your config](#share-your-score-or-add-your-config)

## What you need

- An AI coding agent that can read files in your repository and fetch web pages.
- A checkout of your config at the commit that you want scored. The agent cites that commit.
- About the same reading time as a careful code review. A large config takes longer.

The agent only reads files. It must not evaluate, build or run your config. That keeps the scoring the same as the
survey's, and it keeps your machine safe from anything the agent misreads.

## The prompt

Open your agent in the root of your config repository, then paste this prompt. Replace nothing; the agent finds your
commit by itself.

````text
Score this den configuration with the den configuration audit rubric. Static reading only:
do not run nix, do not evaluate, build or run anything from this repository.

Read these documents first. They are the rules:
- Rubric (categories, anchors, rulings, weights):
  https://raw.githubusercontent.com/sini/den-public-audit/main/method/RUBRIC.md
- Scorecard format:
  https://raw.githubusercontent.com/sini/den-public-audit/main/method/FORMAT.md
- Census contract (how to decide which software a host actually selects; used for category B):
  https://raw.githubusercontent.com/sini/den-public-audit/main/method/CENSUS.md
- Terms (den terms and audit terms; use them exactly):
  https://raw.githubusercontent.com/sini/den-public-audit/main/GLOSSARY.md
- Two calibrated example reviews, to copy the structure and the level of evidence:
  https://raw.githubusercontent.com/sini/den-public-audit/main/configs/Occhima/nix-conf.md
  https://raw.githubusercontent.com/sini/den-public-audit/main/configs/sini/nix-config.md

Then:
1. Record the commit you read: `git rev-parse HEAD`. Cite every claim as a repo-relative path:line at that commit.
2. Write the review sections in the order the example reviews use: shape, common patterns, novel patterns,
   library candidates, den friction, defects (each defect costs exactly one category), then the scorecard.
3. Score the ten categories D, I, S, R, P, L, V, O, B, X from 1 to 10 against the rubric anchors and rulings.
   For every category, write an evidence card: scope, pros (path:line), cons (path:line), score, confidence.
   - D needs a traced chain: producer, route, consumer, and what happens to missing or duplicate values.
   - S is the lower of the settings-contract grade and the leak grade; count distinct leaked constants.
   - B is the mean of a diversity grade and a reference-unit grade; list every counted reference unit.
   - Use "not applicable" only where the rubric allows it, and say why.
4. Compute the total: 2D + I + S + R + P + L + O + B + ½V + ½X, out of 100, to one decimal.
5. Say which shortlists the config fits (showcase, starter, library units) and why.
6. Finish with the three places where the rubric was hardest to apply.

Do not quote secrets. If you find credential material, say only that it exists and where it should be removed.
````

## How to read the result

- **The total** is out of 100. The survey median is about 50, and the top configs score in the high 60s and 70s.
  See [the ranking](/ranking/).
- **The ten category scores** tell you more than the total. A low score with a clear con is the most useful line in
  the scorecard, because it names a change you can make.
- **D (data flow) counts twice.** It rewards configs that move structured data between aspects through den quirks,
  pipes and policies, instead of hard-coding values.
- **The defects** each cost one category. Fixing a defect is the most direct way to raise a score.
- **Confidence** is the agent's own estimate. Treat a low-confidence category as a question to check, not as a
  result.

[How to read a scorecard](/#how-to-read-a-scorecard) walks through one real scorecard, line by line.

## Compare with the survey

If your config is already in the survey, open its page from the [config index](/configs/) and compare the
two scorecards category by category. A difference of one point is normal. A difference of three or more usually means
that one of the two readings missed a file. The evidence cards show which one.

The survey read each config at one fixed revision. If you changed your config since then, the two scorecards measure
different code.

## Share your score or add your config

We welcome both. See [CONTRIBUTING.md](/contributing/) for the steps. In short:

- **Add your config to the survey:** open an issue with the repository URL and the commit you want reviewed.
  Attach your self-score if you have one; it helps the review, but the survey score comes from our own reading.
- **Dispute a finding:** open an issue that names the page and the finding, with a link to the source line.

---
title: "Contributing"
---

This repository is a point-in-time survey of den configurations. You can add your config, correct a finding, remove
your config, or report a security concern. This page tells you how to do each one.

Every page here is generated from the maintainers' working files. For this reason, a pull request that edits a page
cannot be merged directly. Open an issue instead, and we apply the change at the source, so that it survives the next
export.

## Contents

- [Add your config to the survey](#add-your-config-to-the-survey)
- [Score your own config first](#score-your-own-config-first)
- [Request a correction](#request-a-correction)
- [Remove your config](#remove-your-config)
- [Report a security concern](#report-a-security-concern)
- [What we do not accept](#what-we-do-not-accept)

## Add your config to the survey

A config can join the survey if it is a public repository that declares its own den hosts or homes. A library that
only exports an aspect namespace is welcome too; it is reviewed on the [library track](/libraries/).

Open an issue with:

1. the repository URL;
2. the commit that you want reviewed (a full commit hash, not a branch);
3. optionally, your self-score from [Score your own config](/score-your-config/).

We read the config at that commit with the same rubric and the same checks as every other config. Your self-score
helps us find things faster, but the survey score comes from our own reading. The new page then appears in the
[config index](/configs/) and the [ranking](/ranking/).

## Score your own config first

You do not need to wait for us. [Score your own config](/score-your-config/) gives you a prompt for an AI coding
agent that scores your config with this rubric. It is also a good way to find quick improvements.

## Request a correction

Open an issue that names:

- the config (its page under `configs/`);
- the finding that you dispute, quoted or linked;
- why it is wrong, with a link to the source line if you can.

A finding that is wrong at the reviewed revision is fixed, and the score is recomputed if it moves. A finding that
was right at the reviewed revision but has since been fixed upstream is noted, but not rescored, because every config
was read at one revision. To be rescored at a newer revision, request a re-review the same way as a new config.

## Remove your config

Open an issue that asks us to remove your config. You do not need to give a reason. We remove the page, its census
notes and its rows. Its scores may stay in aggregate counts.

## Report a security concern

If you find credential material or other sensitive data on any page here, do not quote it in a public issue. Open an
issue that only says which page is affected, and ask for a private contact.

## What we do not accept

- Requests to change a score without a cited reason. A score changes when its evidence changes.
- Reviews of private repositories. The survey only publishes reviews of public code.

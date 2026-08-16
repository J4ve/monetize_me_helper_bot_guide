# Contributing

## What this repository is

This repository is the **published guide** for the Monetize Me Helper Discord bot — nothing more.

- `README.md` **is the site.** The whole guide lives in that one file, and it is exactly what readers see at <https://j4ve.github.io/monetize_me_helper_bot_guide/>.
- `_config.yml` is the GitHub Pages configuration (title, description, theme).
- There is no application code, no build step, no dependencies, and no tests. The entire product is Markdown.

**The bot itself lives in a separate repository and runs on its own server.** Nothing you change here affects how the bot behaves. This repo only describes it.

## Making a change

1. Branch off `main`.
2. Edit `README.md`.
3. Open a pull request.
4. On merge, the change is live.

Step 4 is the one to slow down on.

## Merging to `main` is publishing

There is **no staging environment and no preview**. GitHub Pages builds from the `main` branch at the repository root, so the moment a PR merges, the public page changes and the next community member to open the guide reads your text. Treat the PR review as the last check there will be — because it is.

After merging, open the live site and confirm your change actually appears.

That last step is not paranoia. Until 2026-08-14 the Pages site was configured to serve a **stale branch** rather than `main`, so months of merged corrections never reached readers — the repository looked correct while the published guide stayed wrong. Pages now serves `main`, and checking the live page is how anyone would catch a repeat.

## Accuracy is the main risk

The guide documents a bot whose source is elsewhere and whose live behaviour can move ahead of what is written here.

**Check any claim about the bot's behaviour against the bot before publishing it.** Do not infer it from the surrounding guide text — the guide has been wrong before, and those errors persisted for months. Existing wording is not evidence; it is the thing being checked.

If you cannot verify a behaviour, say so in the PR rather than guessing.

## What belongs in the guide

`README.md` is user-facing documentation for **community members**, not engineers. It covers:

- The bot's commands and what they do
- Badge types and how the competitions work
- The rules people need to follow: entries, approvals, periods, leaderboards

Write it for someone in the Discord who wants to know what to type and what will happen.

## What does not belong in the guide

Developer, deployment, or repository detail — how the site is published, how to branch, how to review, anything about the bot's implementation. That is what this file is for. Put it here instead.

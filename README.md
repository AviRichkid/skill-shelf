# 📚 Skill Shelf

A one-page directory of the Claude Code skills and plugins our team actually has installed — grouped by the plugin they came with, with a second tab surfacing what's trending in the wider ecosystem.

**Live site:** https://avirichkid.github.io/skill-shelf/

Descriptions are in Hebrew for the team; skill names, plugin names, and links stay in English/code form since that's how you'd reference or install them.

## What's in it

- **מדף הסקילים (Skill Shelf tab)** — every skill from the plugins we have installed, grouped under its plugin (currently [Superpowers](https://github.com/obra/superpowers-marketplace) and [Ponytail](https://github.com/DietrichGebert/ponytail)), each with a one-line Hebrew explanation and a link to where to get it.
- **חם החודש (Trending tab)** — a hand-curated, occasionally-refreshed top 5 of things that gained real traction across the Claude Code ecosystem recently (new standards, popular skills/plugins), each tagged with who it's most useful for.

## Updating it

This is a single static `index.html` — no build step, no server, no database. To add or change a skill:

1. Open `index.html`.
2. Find the `skills` array near the top of the `<script>` block.
3. Add/edit an entry: `{ name, description, group, link }`.
4. Commit and push to `master` — GitHub Pages redeploys automatically within a minute or two.

Or just ask Claude to do it and push the change for you.

The `TRENDING` array right below `skills` works the same way, but is meant to be refreshed periodically (it's a snapshot, not a live feed) rather than added to indefinitely.

## Stack

Plain HTML/CSS/JS, no dependencies, no framework. Fonts loaded from Google Fonts (Fraunces / IBM Plex). Hosted for free on GitHub Pages.

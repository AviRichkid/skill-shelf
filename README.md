# 📚 Skill Shelf

A one-page directory of the Claude Code skills and plugins our team actually has installed — grouped by the plugin they came with, with a second tab surfacing what's trending in the wider Claude ecosystem.

**Live site:** https://avirichkid.github.io/skill-shelf/

UI labels and skill descriptions are in plain Hebrew for the team; skill/plugin names and links stay in English since that's how you'd reference or install them.

## What's in it

- **רשימת כלים (Skill list tab)** — every skill from the plugins we have installed, grouped under its plugin (currently [Superpowers](https://github.com/obra/superpowers-marketplace) and [Ponytail](https://github.com/DietrichGebert/ponytail)), each with a one-line Hebrew explanation and a link to where to get it. Searchable, and anyone with the link can add a new entry directly via the **"הוסף כלי חדש"** button (no login).
- **חם החודש (Trending tab)** — a top-5 of things that gained real traction across the Claude Code ecosystem recently, each tagged with who it's most useful for. Refreshed automatically every Sunday 7am Israel time by a scheduled Claude Code routine (see [Automation](#automation)).
- **Light/dark toggle** and a **feedback button** (footer) that opens the visitor's email app pre-addressed to the maintainer.

## How data is stored

This is a static `index.html` with no server — but the skill list isn't hardcoded anymore. It's backed by a free **Firebase Firestore** database, written to directly from the page's client-side JS:

- Reading and adding skills works for any visitor, no login (matches the "anyone with the link, no friction" goal).
- The `firebaseConfig` block visible in `index.html` (including the `apiKey`) is **not a secret** — Firebase's web SDK config is designed to be public in client-side code; see [Firebase's own docs on this](https://firebase.google.com/docs/projects/api-keys). The actual access boundary is the **Firestore Security Rules** (open read/write, scoped only to the `skills` collection — nothing else). As defense-in-depth, the API key is also restricted in Google Cloud Console to only work from `avirichkid.github.io`.
- If you ever see junk/spam entries: open the [Firebase console](https://console.firebase.google.com) → Firestore Database → Data → `skills` collection, and delete the bad document directly.

## Updating it

- **Adding/editing a skill**: just use the "הוסף כלי חדש" button on the live page — no repo edit needed.
- **Changing layout, copy, or styling**: edit `index.html` directly (plain HTML/CSS/JS, no build step) and push to `master` — GitHub Pages redeploys automatically within a minute or two. Or ask Claude to do it and push the change for you.
- **The `TRENDING` array**: updated automatically weekly (see below), but can also be edited by hand the same way.

## Automation

A scheduled Claude Code cloud routine runs every **Sunday at 7:00 AM Israel time**, researches what's newly trending in the Claude Code / Skills / MCP ecosystem, rewrites the 5 entries in the `TRENDING` array in `index.html`, and pushes the change directly to `master`.

Note: the routine's cron schedule is fixed in UTC and does not auto-adjust for Israel's daylight-saving clock change (late October / late March) — it may drift by an hour around those dates until manually adjusted.

## Stack

Plain HTML/CSS/JS, no framework, no npm/build step. Fonts: Rubik + Heebo (Hebrew-covered) + JetBrains Mono, via Google Fonts. Icons: Phosphor. Data: Firebase Firestore (free tier). Hosted free on GitHub Pages.

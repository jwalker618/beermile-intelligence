# 🍺 Bermondsey Beer Mile

A fun, mobile-first companion app for a Saturday crawl down the Bermondsey Beer Mile.
It's a single self-contained web page — no build step, no backend, works offline.

## Features

- **🍺 Venue guide** — every brewery/taproom in a suggested west→south walking route, with
  what they're known for, a Maps link, and a tick-off checklist with a progress bar.
- **📓 Drink logger** — log who drank what (venue, beer, style, size, ABV, rating).
  Auto-calculates alcohol units and ticks off the venue.
- **🎲 Games of chance** — "whose round is it?" spinner, dice, coin flip, and a beer-style roulette.
- **🎯 Fun** — Beer Mile Bingo, a random dare draw, and photo challenges.
- **📊 Stats** — running tally of drinks/units/pints, a per-person leaderboard, and end-of-day highlights.

The whole crew can use it: add everyone under **Crew** (top-right). Everything is saved
in the browser on each phone — there's no shared server, so each person tracks their own data.

> ⚠️ Venue hours and line-ups change often. Treat the guide as a starting point and check
> Maps / each taproom on the day. Drink responsibly and pace yourself. 💧

## Using it

**Easiest:** open the deployed GitHub Pages link on your phone and "Add to Home Screen"
(it installs as an app and works offline once loaded). Share the link with the group.

**No internet at all:** download `index.html` and open it directly in your phone's browser.
Everything works as a plain file (the offline service worker is the only part that needs hosting).

## Deploying to GitHub Pages

A workflow is included at `.github/workflows/static.yml`. One-time setup:

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Push to the deploy branch (or run the workflow manually from the **Actions** tab).

The workflow publishes the site automatically. The Pages URL appears in the workflow run
summary and under Settings → Pages.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app (HTML + CSS + JS inline) |
| `manifest.webmanifest` | PWA manifest (installable) |
| `sw.js` | Service worker for offline use |
| `icon.svg` | App icon |
| `.github/workflows/static.yml` | GitHub Pages deploy workflow |

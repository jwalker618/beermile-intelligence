# 🍺 Bermondsey Beer Mile

A fun, mobile-first companion app for a Saturday crawl down the Bermondsey Beer Mile.
It's a single self-contained web page — no build step, works offline, and can optionally
sync the whole crew live via a free Firebase room (see **Group sync setup**).

## Features

- **🍺 Venue guide** — every brewery/taproom in a suggested west→south walking route, with
  what they're known for, a Maps link, and a tick-off checklist with a progress bar.
- **📓 Drink logger** — log who drank what (venue, beer, style, size, ABV, rating).
  Auto-calculates alcohol units and ticks off the venue.
- **🎲 Games of chance** — "whose round is it?" spinner, dice, coin flip, and a beer-style roulette.
- **🎯 Fun** — Beer Mile Bingo, a random dare draw, and photo challenges.
- **📊 Stats** — running tally of drinks/units/pints, a per-person leaderboard, and end-of-day highlights.
- **🟢 Group sync (optional)** — enter a shared room code and the whole crew shares one live
  log, crew list and leaderboard across phones (Firebase free tier; see setup below).

The whole crew can use it: add everyone under **Crew** (top-right). By default everything is
saved in the browser on each phone. Turn on **Group sync** (below) to share **one live
session** across all your phones — same crew, same drink log, same leaderboard, updating in
real time.

> ⚠️ Venue hours and line-ups change often. Treat the guide as a starting point and check
> Maps / each taproom on the day. Drink responsibly and pace yourself. 💧

## Group sync setup (Firebase) — ~5 minutes, free

Without this, each phone keeps its own data. With it, everyone who enters the same **room
code** shares one live session. It uses Firebase's free tier.

1. Go to **<https://console.firebase.google.com>** and **Add project** (any name, e.g.
   `beer-mile`). You can skip Google Analytics.
2. In the left menu open **Build → Realtime Database → Create database**. Pick a location
   (Europe is fine), and start in **Test mode** for now → **Enable**.
3. Make the room data readable/writable. In **Realtime Database → Rules**, paste this and
   **Publish** (open access, fine for a one-day event with a non-obvious code):
   ```json
   { "rules": { "rooms": { "$room": { ".read": true, ".write": true } } } }
   ```
4. Get your keys: **Project settings** (⚙️ top-left) → scroll to **Your apps** → click the
   **Web** icon `</>` → register an app (nickname `web`, no hosting needed). Copy the
   `firebaseConfig` object it shows you.
5. Paste it into `index.html` — find `const FIREBASE_CONFIG = {` near the top of the
   `<script>` and replace the commented block with your real values. It should look like:
   ```js
   const FIREBASE_CONFIG = {
     apiKey: "AIza…",
     authDomain: "beer-mile.firebaseapp.com",
     databaseURL: "https://beer-mile-default-rtdb.europe-west1.firebasedatabase.app",
     projectId: "beer-mile",
     appId: "1:…:web:…"
   };
   ```
   (The important one is `databaseURL` — sync switches on automatically once it's present.)
6. Commit & push. On the day, everyone opens the app, taps **Crew** → enters the **same room
   code** (e.g. `BEERMILE`), and you're all sharing live. 🍻

These keys are safe to put in client code — that's how Firebase web apps work; the Rules
above scope access to room data only. If you ever want it locked down further, ping me.

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

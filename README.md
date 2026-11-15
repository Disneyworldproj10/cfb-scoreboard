# CFB Scoreboard

A standalone college football scoreboard for **ACC** and **AP Top 25** games, built as a single-page app (no build step). It talks directly to the ESPN college football scoreboard API.

Styled as a **Glance-style LED matrix** on a **1920×720 (8:3)** panel: black unlit-dot cabinet, pixel typography, team-colored abbreviations, a scrolling bottom ticker, and a flashing TOUCHDOWN / FIELD GOAL marquee. The rotating spotlight fills the viewport with no scrolling (away team left, scores center, home team right). Controls auto-hide so the display reads like a real sign. It also scales to other sizes, including phones (portrait stack, landscape 3-column) and can be installed as a PWA.

## Open locally

```bash
python3 -m http.server 8080
# then visit http://127.0.0.1:8080/
```

Direct ESPN fetches work in the browser (`Access-Control-Allow-Origin: *`). A `proxy.py` helper is included only as a fallback and is not required.

## Features

- Tabs: All (ACC ∪ Top 25, deduped), ACC, Top 25
- Rotating spotlight (default) and a card grid (horizontal rows on wide/short screens)
- Auto-refresh every 10 seconds, with a last-updated time and manual Refresh
- Score-change celebrations (TOUCHDOWN, FIELD GOAL, and others), queued if several games score
- Alerts toggle (on by default) and optional Web Audio sting (off by default)
- Demo: press **T** to simulate a touchdown and field goal, or add `?demo=1`

## Add to Home Screen (iPhone)

Open the site in Safari → Share → Add to Home Screen. The app uses `apple-mobile-web-app-capable`, a 180×180 apple-touch-icon, and a standalone dark `manifest.json`.

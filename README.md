# CFB Scoreboard

A standalone college football scoreboard for **ACC** and **AP Top 25** games, built as a single-page app (no build step). It talks directly to the ESPN college football scoreboard API.

Styled as a **Glance-style LED matrix**, with the primary layout targeting an **iPhone** (393×852 / 430×932 portrait, and 852×393 landscape). Portrait stacks the away and home teams with large LED scores, a status strip, and a scrolling ticker at the bottom. Landscape keeps a compact 3-column board. The display fills the screen in standalone / Add to Home Screen mode (`viewport-fit=cover`, `100dvh`, safe-area insets, black-translucent status bar). Swipe left or right to change games; tap to show or hide controls. Wider screens, including **1920×720 (8:3)**, keep the three-column spotlight (away left, scores center, home right). Controls auto-hide so the display reads like a real sign.

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

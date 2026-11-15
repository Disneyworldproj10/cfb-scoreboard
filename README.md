# CFB Scoreboard

A standalone college football scoreboard for **ACC** and **AP Top 25** games, built as a single-page app (no build step). It talks directly to the ESPN college football scoreboard API.

Styled as a **Glance-style LED matrix**. The board is fully fluid: it reads the actual window size and `devicePixelRatio`, then picks a layout from the aspect ratio — tall (portrait stacked), near-square, wide (3-column), or ultra-wide (3-column with larger logos, e.g. 1920×720, 2560×1080). LED dot pitch is derived from the available space so the sign fills the monitor without scrolling, from an iPhone (393×852 / 430×932 and landscape) through 1366×768, 1080p, 1440p, and 4K. Canvases are sized at CSS pixels × DPR with an integer device-pixel pitch so type, scores, and logos stay sharp. The layout reflows on resize, orientation change, fullscreen, and DPR changes. Ticker height/speed and the TOUCHDOWN overlay scale with the screen. Standalone / Add to Home Screen mode uses `viewport-fit=cover`, safe-area insets, and a black-translucent status bar. Swipe left or right to change games; tap to show or hide controls. Controls auto-hide so the display reads like a real sign.

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

# CFB Scoreboard

A standalone LED scoreboard for **NCAA football**, **NCAA men's basketball**, the **NFL**, and **MLB**, built as a single-page app (no build step). It talks directly to the ESPN site APIs.

Open **Settings** (gear) to turn sports on or off and to filter each one: Top 25 and conferences for NCAA sports, divisions/conferences for the NFL and MLB, plus searchable favorite teams. A game appears if it matches any selected filter. The default view is unchanged from before: NCAA football, ACC and AP Top 25. Choices are saved in the browser.

Styled as a **Glance-style LED matrix**. The board is fully fluid: it reads the actual window size and `devicePixelRatio`, then picks a layout from the aspect ratio — tall (portrait stacked), near-square, wide (3-column), or ultra-wide (3-column with larger logos, e.g. 1920×720, 2560×1080). LED dot pitch is derived from the available space so the sign fills the monitor without scrolling, from an iPhone (393×852 / 430×932 and landscape) through 1366×768, 1080p, 1440p, and 4K. Scores, names, status, and the ticker are drawn as a finer LED matrix (about 2× the previous dot density, integer device-pixel pitch) so letterforms stay the same size but look sharper. Team logos are the official ESPN images (500px, dark-background variant when available), smoothly scaled, not dot-matrix. In wide and ultra-wide layouts each score sits with its own team, separated by a clear dash, so 7 and 14 cannot be read as 714. The layout reflows on resize, orientation change, fullscreen, and DPR changes. Ticker height/speed and the TOUCHDOWN overlay scale with the screen. Standalone / Add to Home Screen mode uses `viewport-fit=cover`, safe-area insets, and a black-translucent status bar. Swipe left or right to change games; tap to show or hide controls. Controls auto-hide so the display reads like a real sign.

## Open locally

```bash
python3 -m http.server 8080
# then visit http://127.0.0.1:8080/
```

Direct ESPN fetches work in the browser (`Access-Control-Allow-Origin: *`). A `proxy.py` helper is included only as a fallback and is not required.

## Features

- Settings (gear): turn on NCAA Football, NCAA Men's Basketball, the NFL, and/or MLB. Preferences persist in `localStorage`.
- NCAA filters: AP Top 25, conference multi-select (from ESPN standings), and searchable favorite teams. Default for football is ACC + Top 25, so the board matches the previous ACC/Top 25 view.
- NFL and MLB filters: All games, conference (AFC/NFC or AL/NL) and division multi-select, and favorite teams.
- A game appears if it matches any selected filter for an enabled sport.
- Tabs: All, plus one tab per enabled sport with live counts.
- Only enabled sports are fetched (every 10 seconds). Games merge into one rotation with a small sport tag (CFB, CBB, NFL, MLB) on the status line.
- Rotating spotlight (default) and a card grid (horizontal rows on wide/short screens)
- Auto-refresh every 10 seconds, with a last-updated time and manual Refresh
- Football scoring celebrations (TOUCHDOWN, FIELD GOAL, and others), queued if several games score. Basketball basket changes do not fire the overlay. An MLB run silently jumps that game to the front.
- Basketball status shows half and clock; baseball shows inning and outs. A sport with no games (off-season or a failed fetch) shows an LED `NO GAMES` / `ERROR` line.
- Alerts toggle (on by default) and optional Web Audio sting (off by default)
- Demo: press **T** to simulate a touchdown and field goal, or add `?demo=1`

## Add to Home Screen (iPhone)

Open the site in Safari → Share → Add to Home Screen. The app uses `apple-mobile-web-app-capable`, a 180×180 apple-touch-icon, and a standalone dark `manifest.json`.

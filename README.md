# 🏒🏀 NHL + NBA Playoffs Wallpaper Generator

A single-file browser app that generates a live, updating desktop wallpaper showing the full 2026 NHL Stanley Cup Playoffs and NBA Playoffs brackets — complete with team logos, series scores, per-game results, and automatic winner progression.

---

## Features

- **Full bracket layout** — Round 1 → Round 2 → Conference Finals → Championship, with the Finals card centered between East and West
- **Live scores via ESPN** — pulls real series wins and per-game scores directly from ESPN's public API (no API key required)
- **Auto winner promotion** — when a team wins a series, they automatically advance into the correct next-round slot
- **Per-game score log** — each series card shows a compact game-by-game breakdown (e.g. `G1 BUF 4–2 BOS`, `G2 OT`)
- **Team logos** — all 30+ teams rendered using ESPN's CDN logo URLs
- **Smart export** — detects your primary monitor's resolution and OS at download time:
  - Exports a JPEG at your screen's exact native resolution
  - **Windows/Linux**: reserves 48px at the bottom for the taskbar
  - **macOS**: reserves menu bar height at the top (scales with Retina/HiDPI)
- **No scrollbars** — the bracket scales to fill 90% of your browser window, centered, with no overflow

---

## Usage

1. Download `playoffs-wallpaper-2026.html`
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. Click **↻ Update Scores** to fetch the latest series results from ESPN
4. Click **⬇ Download JPEG** — the button label shows your detected resolution (e.g. `2560×1440`)
5. Set the downloaded JPEG as your desktop wallpaper using **Fill** mode

> **Tip:** Repeat step 3 each morning during the playoffs to keep scores current. Winner promotion happens automatically — teams advance through the bracket as they win series.

---

## Wallpaper Settings

| Monitor | Recommended fit mode |
|---|---|
| 2560×1440 (primary) | Fill |
| 1920×1200 (laptop) | Fill |
| Any 16:9 monitor | Fill |
| 16:10 monitor | Fill (slight crop) or Fit (small bars) |

**Windows:** Right-click desktop → Personalize → Background → set each monitor to **Fill** individually by right-clicking each thumbnail.

**macOS:** System Settings → Wallpaper → set to **Fill Screen**.

---

## How It Works

The file is entirely self-contained HTML/CSS/JS with no build step or dependencies beyond two CDN scripts loaded at runtime:

- **[html2canvas](https://html2canvas.hertzen.com/)** — renders the bracket DOM to a canvas for JPEG export
- **[Barlow / Barlow Condensed](https://fonts.google.com/specimen/Barlow)** — typography (loaded from Google Fonts)

Score updates call ESPN's unofficial public scoreboard API:
```
https://site.api.espn.com/apis/site/v2/sports/hockey/nhl/scoreboard?seasontype=3
https://site.api.espn.com/apis/site/v2/sports/basketball/nba/scoreboard?seasontype=3
```
These endpoints are open, require no authentication, and work directly from the browser.

---

## Bracket Structure

```
NHL (top half)
  East: Atlantic + Metropolitan divisions
  West: Central + Pacific divisions

NBA (bottom half)
  East: Seeds 1–8
  West: Seeds 1–8
```

Each half flows:

```
R1 (4 series) → R2 (2 series) → Conf. Final (1 series) → [Championship] ← Conf. Final ← R2 ← R1
```

---

## Updating for Future Seasons

The first-round matchups are hardcoded in the `D` object near the top of the script. At the start of a new playoff year, update the team names and seeds in that object. ESPN score fetching and winner promotion will handle the rest automatically.

---

## License

MIT — do whatever you want with it.

# Moon Lander — Publish Package

A playable browser game (canvas + HTML) plus its visual-design spec document. **No build step, no dependencies, no server code** — everything in this folder runs as-is as a static site.

## What Claude Code should do

Publish this folder to GitHub Pages:

1. Create a new public repo (e.g. `moon-lander`) and push the contents of this folder to its root.
2. Enable GitHub Pages: Settings → Pages → Deploy from branch → `main` / root
   (or `gh api repos/{owner}/{repo}/pages -X POST -f 'source[branch]=main' -f 'source[path]=/'`).
3. Verify the live URL:
   - `https://<owner>.github.io/moon-lander/` → the game (index.html)
   - `https://<owner>.github.io/moon-lander/spec/Moon%20Lander%20Visual%20Identity.dc.html` → the design spec

Do **not** run these files through a bundler, minifier, or framework scaffold. They are self-contained HTML documents that load `support.js` (a small runtime, included) from the same directory via a relative path. Keep every file next to its sibling `support.js` and keep the exact filenames — the spec document links to `Moon%20Lander%20Prototype.dc.html` by name.

## Files

| File | What it is |
|---|---|
| `index.html` | The game, ready to serve as the site root (identical to the file below) |
| `Moon Lander Prototype.dc.html` | The game under its original name (the spec's ▶ LAUNCH button links to this) |
| `support.js` | Runtime the HTML files require — must sit in the same folder |
| `spec/Moon Lander Visual Identity.dc.html` | Design spec: two art directions (Flight Manual + Terminator Line), animated HUD mockup, palette, FX, accessibility notes |
| `spec/support.js` | Same runtime, needed by the spec document |

External requirement: Google Fonts (Jost, IBM Plex Mono) load from `fonts.googleapis.com` at runtime. Offline, text falls back to system fonts; everything else works.

## The game (for the repo description / testing)

Classic lunar-lander: land both feet on a pad within limits.

- **Controls:** click the page for keyboard focus → any key to start → `← →` RCS rotate, `↑` / `Space` main engine, `R` re-fly, `Enter` next site
- **Landing limits:** V/S ≤ 2.5 m/s · H/S ≤ 1.5 m/s · tilt ≤ 8°
- **Scoring:** 1 000 base × pad multiplier (×1 teal / ×3 gold) + fuel % × 20
- 3 craft per game, seeded terrain per site, wraparound edges

Suggested repo description: *"Moon Lander — a browser lunar-lander game. Arrow keys + space. No install, no build."*

## If asked to port it later (not part of publishing)

The HTML here is a working prototype, high-fidelity to its spec. If the user later wants a production port (React, canvas engine, native), treat `spec/Moon Lander Visual Identity.dc.html` as the source of truth — section 1a "Flight Manual" is the primary direction and defines the exact palette, HUD layout, chip logic (● GO ≤ 80 % of limit / ▲ CAUTION 80–100 % / ✕ EXCEED), craft construction, FX timing, and terminal-screen scoring math. Key tokens: bg `#081420→#143049`, ink `#E9F2F9`, vellum `#8FB0C9`, gold `#D9A544`, teal `#2FE6A6`, amber `#FFB020`, red `#FF4D5E`; type = Jost (labels, tracked caps) + IBM Plex Mono (tabular telemetry).

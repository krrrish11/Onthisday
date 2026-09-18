# Field Sketchbook — On This Day

A single-file HTML app that shows Wikipedia's "On This Day" historical events, births, deaths, and holidays, styled as a hand-drawn field sketchbook.

**Status:** temporary / working notes — not final documentation.

---

## Files

- `design-5-field-sketchbook.html` — the main/active build (all features below)
- `design-1-archive-ledger.html` — dark slate-teal archive style (earlier exploration)
- `design-2-almanac-poster.html` — warm cream torn-calendar style (earlier exploration)
- `design-3-terminal-console.html` — command-line/CRT style (earlier exploration)
- `design-4-editorial-timeline.html` — minimalist vertical timeline (earlier exploration)

Only `design-5-field-sketchbook.html` has the full feature set (magnifier, detail pages, index). The others are style explorations from earlier and are not being actively maintained.

## How it works

- No backend, no build step. Pure HTML/CSS/JS in one file.
- Data source: Wikipedia's public REST API, fetched client-side.
  - List view: `https://en.wikipedia.org/api/rest_v1/feed/onthisday/all/{mm}/{dd}`
  - Detail view (richer summary): `https://en.wikipedia.org/api/rest_v1/page/summary/{title}`
- Fonts loaded from Google Fonts (Caveat, Literata, Inter).
- Requires internet access to fetch data — won't show anything meaningful offline.

## Features implemented

- Month/day picker + "Today" button
- Tabs: Events / Births / Deaths / Holidays
- Plates (cards) for each entry, sketchbook-styled (torn corner, hand-drawn border, slight rotation)
- Editorial index sidebar — click an entry to scroll to its plate
- Draggable magnifying glass — grab it and drop it on a plate to zoom the text under it
- Click any plate → opens a **detail page** for that entry:
  - Full text, year, category
  - Extra summary + larger image fetched live from Wikipedia's summary API
  - Related-page chips
  - "Back to sketchbook" button
  - URL hash routing (`#events/9/17/3`) — browser back/forward works, links are shareable/refreshable
- Responsive layout (sidebar stacks on mobile, magnifier resizes)

## Known quirks (not bugs)

- On the **Births** tab, each entry's text often includes "(died ####)" in parentheses — that's Wikipedia's own phrasing, not a mix-up. The big year number shown always matches the active tab (birth year on Births, death year on Deaths).
- The magnifier is hover/drag-based, so on first load it needs a moment to find the `.plates` container before it positions itself correctly.

## Open items / possible next steps

- Strip the "(born ...)" / "(died ...)" parenthetical from plate text to reduce visual confusion (discussed, not yet done)
- Decide which of the 5 designs to keep as the final one, or merge features across them
- Optional: add a loading skeleton instead of the plain "Loading…" state message
- Optional: cache Wikipedia summary API responses (currently only the day-level `onthisday` response is cached, not individual page summaries)

## Running it

Just open the `.html` file directly in a browser — no server needed for local testing (some browsers may warn about `file://` + fetch(), in which case use a simple local server, e.g. `python -m http.server`).

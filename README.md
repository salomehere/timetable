# Timetable tracker

A tiny mobile page showing "Now / Next / Rest of day" from a timetable, with A/B week
rotation and term-date awareness. Pure static files — no server, no build step.

## Files

- `index.html` — the whole app (styling + logic).
- `data.json` — everything editable: the timetable, period times, term dates,
  A/B week anchor, inset days. Edit this file whenever anything changes; no
  code changes needed.

## Turning on GitHub Pages

The repo and files are already set up. Last step to make it a live link:

1. In this repo: **Settings → Pages → Build and deployment → Source**, choose
   "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
2. Wait ~1 minute, then the site is live at:
   `https://salomehere.github.io/timetable/`
3. Share that link — it works from any phone browser, no login needed.

## Updating the timetable later

Edit `data.json` directly on github.com (click the file → pencil icon →
commit). The site picks up changes within a minute (browser caching aside —
if it looks stale, do a hard refresh).

### What's in `data.json`

- `periods` — the fixed daily time slots (same every day).
- `timetable.A` / `timetable.B` — one array per weekday, matching the
  `periods` order 1:1. Use `null` for a free period.
- `weekAAnchorMonday` — a Monday that is definitely "Week A". Every week is
  worked out by counting forward/back from this date, alternating A/B.
- `terms` — start/end dates of each term. Outside these ranges the app shows
  "Out of term" instead of a timetable.
- `insetDays` — dates with no lessons even though it's term time.

## Notes on this build (2026/27 term dates)

The exact term boundaries and inset days were read off a scanned school
calendar image, which isn't 100% reliable to parse precisely (shading is
easy to misjudge). Worth a quick double-check against the school's official
term dates PDF:

- Term 1: Thu 3 Sep – Fri 16 Oct 2026
- Term 2: Mon 2 Nov – Fri 18 Dec 2026
- Term 3: Mon 4 Jan – Fri 12 Feb 2027
- Term 4: Mon 22 Feb – Thu 25 Mar 2027
- Term 5: Thu 8 Apr – Fri 21 May 2027
- Term 6: Tue 1 Jun – Fri 16 Jul 2027
- Inset days spotted: Tue 1 Sep 2026, Fri 27 Nov 2026 (there may be more not
  clearly visible in the scan)

If any of these are wrong, just fix the dates in `data.json` — no other
changes needed.

# Strive Internal Planning Calendar

A self-contained, single-file web calendar for tracking Strive's key dates: executive travel and
logistics, conference attendance, Bitcoin history, company milestones, and US holidays.

## How to open

**Live version:** https://danimontoya-strive.github.io/strive-planning-calendar/

That link is served by GitHub Pages from `main` and rebuilds automatically on every push, so it always
reflects the canonical version in this repo. Share it directly — no install or GitHub account needed.

To run it locally instead, open **`index.html`** in any modern browser. No build step and no
dependencies — everything (HTML, CSS, JS, data) is inline in the one file.

## Colour key

Listed in the order they appear everywhere in the app — chips, panels, and day cells all follow it.

| Colour | Type | Meaning |
|--------|------|---------|
| 🟢 Green | Attending | Conferences & events we are **confirmed** for |
| 🟠 Orange | Bitcoin Date | Significant Bitcoin anniversaries (genesis block, halvings, whitepaper day) |
| 🔴 Red | Potential | Conferences & events **under consideration** |
| 🟡 Yellow | Strive Milestone | Corporate milestones (going public / ASST, SATA daily-dividend launch) |
| 🔵 Blue | Holiday / OOO | US federal holidays & office closures |

## Four views

**Month** (the default) — one month's day grid beside that month's events. A strip along the top jumps
between months. Click a day to narrow the panel to it; click again to widen back out.

**Agenda** — every event for the year in one chronological list. Opens scrolled to today, dims what has
already passed, and draws a "Today" line.

**Year** — all 12 months at once. Click any month to open it.

**Travel** — the one to send an executive. Every upcoming trip across years (not just the selected
year), showing who is going, the fly-out/fly-back window, the hotel, and what is still unbooked. Filter
to one person to see only their travel. Ends with every open prep item in a single list, so the wider
team can see at a glance how to help.

`Today` in the header jumps back to now from anywhere.

## Features

- **Travel & logistics** — each trip carries its city and venue, and can hold a confirmed roster, travel
  dates, a hotel and a prep checklist. Anything not yet set is flagged rather than hidden, so an
  unbooked trip looks unbooked. Trips outside the US are badged **International**.
- **Conflict detection** — overlapping trips are flagged with the clashing event *and its city*, because
  "Las Vegas 13–16" and "New York 13–14" is only obviously impossible once both cities are visible.
- **Multi-day events** are single entries with a date range, rendered across every day they span
- **Filter chips** — click any colour in the legend to show or hide that category
- **Status toggle** — flip any conference between 🔴 Potential and 🟢 Attending
- **Export .ics** — download what is currently shown and import it into Outlook, Google or Apple
- **Search** across titles, notes, dates and types; press `/` to focus it
- Keyboard: `M` / `A` / `Y` / `R` switch view, `T` jumps to today, `←` / `→` step through months or years

## A note on saved changes

Marking a trip attending, adding an event, or filling in logistics saves **in your own browser only**.
Teammates opening the shared link will not see it, and neither will anyone else.

To put something on the calendar everyone sees, use **Copy for commit** in the logistics editor and send
it over — or edit the `events` array in `index.html` directly and push. The live link rebuilds from
`main` within a minute.

## Notes

- Conference dates were researched and verified where possible; a few are marked TBD pending confirmation.
- Two known items to confirm: BTC Hong Kong's third day (the public programme lists Aug 27–28), and
  whether the TrueNorth happy hour should move to Sep 28 to line up with the Bitcoin Treasuries Conference.

# Strive Internal Planning Calendar

A self-contained, single-file web calendar for tracking Strive's key dates: Bitcoin history, company milestones, conference attendance (confirmed + under consideration), and US holidays.

## How to open

Open **`strive-calendar-final.html`** in any modern browser. No build step and no dependencies — everything (HTML, CSS, JS, data) is inline in the one file.

## Color key

| Color | Type | Meaning |
|-------|------|---------|
| 🟠 Orange | Bitcoin Date | Significant Bitcoin anniversaries (genesis block, halvings, whitepaper day, etc.) |
| 🟡 Yellow | Strive Milestone | Corporate milestones (going public / ASST, SATA daily-dividend launch, analyst coverage) |
| 🟢 Green | Attending | Conferences & events we are **confirmed** for |
| 🔴 Red | Possible | Conferences & events **under consideration** |
| 🔵 Blue | Holiday / OOO | US federal holidays & office closures |

## Features

- **Multi-day events** are single entries with a date range — they render across every day they span
- **Filter chips:** click any color in the legend to show/hide that category (counts update per year)
- **Conflict detection:** overlapping travel commitments are flagged per month, and clashing days are marked `CLASH`
- **Status toggle:** flip any conference between 🔴 Possible and 🟢 Attending — colors update everywhere instantly
- **Saves automatically:** status changes and added events persist in the browser via `localStorage`
- **Suggested attendees:** each conference carries a recommendation for which executive should go and why
- Year navigation (← / → keys); inside a month view, ← / → move month to month
- Search across titles, notes, suggested attendees, dates, and types; press `/` to jump to search
- Full-screen month zoom, day-level detail, hover tooltips
- Add events (with optional end date) from the header or month view

## Notes

- Conference dates were researched and verified where possible; a few are marked TBD pending confirmation.
- Saved state lives in the browser it was saved in — it does not sync between people. For shared
  planning, edits should be made in the `events` array in the HTML and committed.
- Two known items to confirm: BTC Hong Kong's third day (public programme lists Aug 27–28), and
  whether the TrueNorth happy hour should move to Sep 28 to line up with the Bitcoin Treasuries Conference.

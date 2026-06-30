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

- Year navigation (arrows or ← / → keys) and full-screen month zoom
- Click a day for its event detail; hover for a quick tooltip
- Search across titles, notes, dates, and types
- Add new events from the header or month view
- **Status toggle:** flip any conference between 🔴 Possible and 🟢 Attending — the color updates everywhere instantly

## Notes

- Conference dates were researched and verified where possible; a few are marked TBD pending confirmation.
- Event additions and status toggles are currently in-session (reset on reload). Persistence can be added if needed.

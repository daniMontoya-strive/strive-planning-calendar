# Strive Internal Planning Calendar — project context

## What this is

A single-file web calendar tracking Strive's key dates for 2026–2027: Bitcoin history, company
milestones, conference attendance, and holidays. Built for the Strive team to read at a glance.

Everything (HTML, CSS, JS, and the event data) lives inline in **`index.html`**. No build step, no
dependencies, no backend. Open it in a browser and it works.

## Where it lives

| | |
|---|---|
| Local | `C:\Users\DaniMontoya\OneDrive - Strive\Desktop\Calendar Claude\index.html` |
| Repo | https://github.com/daniMontoya-strive/strive-planning-calendar (**public**) |
| Live | https://danimontoya-strive.github.io/strive-planning-calendar/ |

GitHub Pages serves `main` from the repo root and rebuilds on every push (~30–60s). The live URL is
what the team has been given — it must keep working, and it must stay at that address.

## ⚠️ Push after every change

**The repo is the canonical version. After completing any change, commit and push it.**

The owner's workflow is: ask for an edit here → it lands on the live URL. An unpushed change is an
invisible change. Verify the push landed (`git log origin/main..HEAD` should be empty) rather than
assuming it.

`gh` is installed and authenticated as `daniMontoya-strive`, so pushes need no prompts. It sits at
`C:\Program Files\GitHub CLI\gh.exe` and is in the machine PATH — if a fresh shell can't find plain
`gh`, call it by full path.

The repo is **public**. Anything committed is world-readable. Current content is deliberately
non-sensitive; keep it that way (no unannounced deal terms, personnel matters, or credentials).

## The five-colour system

This is the core of the design and the owner is specific about it. Each type maps to a CSS class that
sets `--c` (accent) and `--cd` (dim tint); components read those variables, so adding a type means
adding one class.

| Colour | `type` value | Meaning |
|---|---|---|
| 🟠 Bitcoin orange | `bitcoin` | Significant Bitcoin dates — genesis block, halvings, whitepaper day, Pizza Day, ETF approval |
| 🟡 Strive yellow | `milestone` | Strive corporate milestones — going public (ASST), SATA daily-dividend launch, product launches, major public announcements |
| 🟢 Green | `attending` | Conferences/events Strive is **confirmed** for |
| 🔴 Red | `possible` | Conferences/events **under consideration** |
| 🔵 Blue | `holiday` | US federal holidays and Strive office closures |

New conferences default to 🔴 `possible` until the owner confirms attendance.

## Event schema

Events are objects in the `events` array in `index.html`:

```js
{
  id: 221,                        // unique integer; 1-99 company, 100-199 holidays, 200+ conferences
  date: '2026-09-16',             // start (YYYY-MM-DD)
  end: '2026-09-17',              // OPTIONAL — omit for single-day events
  title: 'European Blockchain Convention 2026 — Barcelona',
  type: 'possible',               // one of the five above
  notes: 'Sep 16–17, Fira Barcelona Gran Via. ... WHY STRIVE: ...',
  rec: 'Ben Werkman (CIO) to lead on EU institutional capital; ...'   // OPTIONAL
}
```

**Conventions the owner expects:**

- `notes` for a conference should state dates + venue, what the event is, and a **`WHY STRIVE:`**
  clause explaining the strategic value — especially for reaching advisors/allocators with **SATA**,
  Strive's preferred stock paying dividends every business day (13% annualized). Red events end with
  "POSSIBLE — confirm attendance to move to Attending."
- `rec` is the **★ Suggested attendees** line: which executive should go and why.
- Research conference dates and details before adding — don't guess. Verify against the official site.

## The executives

- **Matt Cole** — CEO. Flagship stages, keynotes, sovereign/large-allocator relationships, top-advisor credibility.
- **Ben Werkman** — CIO. The SATA distribution workhorse: investment thesis, allocators, advisor and capital-markets audiences.
- **Jeff Walton** — CRO. Risk and regulatory-heavy venues, institutional risk conversations.

## The three views

`view` is one of `'month' | 'agenda' | 'year'`; `render()` dispatches on it. All three live inside the
same `#scroll` container and are shown/hidden by `setView()` — there is no full-screen overlay any more.

- **Month view** (default) — one month's day grid on the left, that month's events on the right, on a
  single screen. A month strip (`#monthBar`) above it jumps between months and shows per-month counts.
  Clicking a day narrows the panel to that day; clicking it again widens back to the whole month.
  The grid and the event panel each scroll independently, so the page itself does not scroll.
- **Agenda view** — chronological list, opens at today, past events dimmed, "Today" line, and an
  "Open month →" button on each month header.
- **Year view** — 12 month cards at once; clicking one switches to Month view for that month.

## Features already built

- **Multi-day events** render across every day they span with `↳` continuation markers; pill corners
  are squared mid-run so a trip reads as one continuous band, and re-rounded at week breaks.
- **Relative timing** — every event card carries a `Today` / `Tomorrow` / `In 3 weeks` / `Done` badge.
- **Conflict detection** — overlapping travel flagged per month; clashing days marked `CLASH`
- **Filter chips** — click a legend colour to show/hide that category
- **Status toggle** — flip any conference 🔴 Possible ⇄ 🟢 Attending (per-browser; see Gotchas)
- **Reset my changes** — appears in the toolbar only when local changes exist; clears them
- **Export .ics** — downloads everything currently shown, importable into Outlook/Google/Apple.
  All-day `DTEND` is exclusive (a 3-day event ends on day 4) and lines fold at 75 **octets**.
- **Search** across titles, notes, suggested attendees, dates, types (`/` focuses it)
- Keyboard: `←`/`→` step months in Month view and years elsewhere; `M`/`A`/`Y` switch view;
  `T` jumps to today; `/` focuses search; `Esc` clears the selected day or closes an overlay.

## Gotchas

- **⚠️ Never round-trip `index.html` through PowerShell `Get-Content`/`Set-Content`.** `Get-Content`
  reads the (BOM-less, UTF-8) file as Windows-1252 and `Set-Content -Encoding UTF8` writes it back
  double-encoded — every `—`, `★`, `⚠`, `↳` silently turns to mojibake. This already happened once.
  Use the Edit/Write tools, or explicit .NET: `[System.IO.File]::ReadAllText/WriteAllText` with
  `New-Object System.Text.UTF8Encoding($false)`. To detect it: the file should contain ~94 `—` and 0
  occurrences of `Â` or `â€`.
- **`localStorage` stores only type overrides (by id) and user-added events** — never the base
  `events` array. So deleting an event from the source removes it cleanly; a stale override for a
  deleted id is ignored harmlessly.
- **Saved state is per-browser and does not sync between people.** The UI now says this explicitly:
  the button reads "✓ Mark attending — for me", and a `.local-note` under it names what teammates
  actually still see. Keep that honesty if you touch `toggleBtn()` — the live link is shared, so a
  label implying a shared update genuinely misleads people.
- **Day grids must use `minmax(0,1fr)`, not `1fr`.** The event pills are `white-space:nowrap`, and
  plain `1fr` resolves to `minmax(auto,1fr)`, so long titles blow the columns out — day cells once
  reached 1449px inside a 526px container. Cells also need `min-width:0`.
- **The month view stacks below 1150px**, not 900px. Between those widths a 400px event panel starves
  the day grid to ~58px per column and titles truncate to two characters. Below 1150px the page also
  gets its scroll back (`.scroll.locked` reverts to `overflow-y:auto`).
- **The header wraps below 900px.** Three view buttons + Today + Add overflowed a phone header once
  the Month button was added; `Add Event` goes icon-only below 600px.
- **Future Proof Festival was deliberately removed** from September at the owner's request. Don't
  re-add it.
- The local folder is inside OneDrive. Fine on one machine; don't work from a second clone
  simultaneously, since OneDrive syncing `.git` can corrupt it.

## Open questions worth confirming

- **BTC Hong Kong** is entered as a 3-day event (Aug 27–29) but the public programme lists **Aug 27–28**.
- **TrueNorth happy hour** sits on Sep 22, while the Bitcoin Treasuries Conference it's tied to is
  **Sep 28** — should it move to line up?
- **Maxim Growth Summit** is entered Oct 13–14 per the owner; the 2025 edition ran Oct 22–23, so 2026
  dates need confirming. (Owner originally called it "Maximum Growth Summit.")
- **Bitcoin for Corporations 2027** uses the 2026 dates (Feb 24–25) as a placeholder.
- October is heavily overloaded with overlapping travel — the conflict panel flags it. Several
  advisor events (Forbes SHOOK, Schwab IMPACT) are still 🔴 and compete for the same people.

## Deliberately not done

- **A light theme.** Considered and skipped: 🟡 milestone yellow (`#FFD23F`) is unreadable on white,
  and darkening it to an amber collides with 🟠 bitcoin orange — which muddies the one thing the owner
  is most specific about. Revisit only with an explicit palette decision for all five colours.

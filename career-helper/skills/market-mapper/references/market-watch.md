# Market Watch: Weekly Update

**Purpose:** Keep an existing market map current with the least possible noise. Each run re-checks every organisation on the map, compares against the previous state, and reports only what has changed. The map file is updated in place; the dated update file is the short read.

---

## Step 1: Read the Previous State

Before any search:

1. Read `market-map.md`. If it does not exist, there is nothing to compare against: in conversation, offer to build one via Capability 1; in an unattended run (a scheduled task or `/career-helper:weekly-update`), report in one line that no market map was found and end the step without asking anything.
2. Note the posture, the signal window, the per-organisation last-checked dates, the current priorities, and the named decision makers.
3. Read the most recent file in `market-watch/` if one exists, so a signal reported last week is not reported again as new.
4. Read `applications/tracker.md` if it exists; an organisation the user is already applying to is flagged in the update rather than re-suggested as an angle.

The comparison baseline is the per-organisation last-checked date, not the date of the last update file. If a run was skipped, the window simply covers the gap. An organisation whose last-checked date is blank or `[UNKNOWN]` (for example one added on the board) gets a full signal-window check and its date set on this run.

---

## Step 2: Re-check Every Organisation

For each organisation on the map, run the signal pass from `company-mapping.md` Step 4, limited to material dated after that organisation's last-checked date:

- Careers page: fetch it and count live roles, noting any in the user's function; compare with the previous count where recorded
- News and press: search `"{organisation}" news` restricted to the gap period, plus regional press
- Companies House: new officer appointments or resignations, new charges, filed accounts, confirmation statements that change the registered office
- Contracts Finder and Find a Tender: awards naming the organisation
- Funding sources: rounds, grants, and acquisitions announced in the gap

Run organisations in parallel where the tooling allows. Record every new signal as one line with source URL and date seen, in the same taxonomy as the map (Hiring, Growth, Investment, Change).

Decision makers: re-fetch the leadership page or Companies House officers where the map has a named person. A departure or a new appointment in the relevant function is a Change signal and updates the map row.

---

## Step 3: Detect the Differences

Compare the fresh signals against the map and the previous update:

| Difference | What to report |
|:-----------|:---------------|
| New signal | One line, group, date, source. Only signals dated after the last-checked date, or first seen since it |
| Decision-maker change | Who moved, in which direction, the confirming source; the map row is updated |
| Priority change | Old priority, new priority, and the one signal that drove it |
| Gone quiet | Any organisation with no signals across this update and the previous one is listed as Quiet and offered for removal; never removed automatically |
| Suggested addition | An organisation surfaced during the search that fits the seed profile, with the signal that surfaced it; offered, never added without the user's yes |
| Already in play | Any organisation on the map that also appears in `applications/tracker.md`; note the stage and skip the angle |

A signal that was already on the map or in last week's update is not new. Re-reporting is the failure mode that makes a weekly update unreadable, so check before writing.

---

## Step 4: Write the Update

Use `market-watch-update-template.md`. Keep it to one screen for a normal week:

- Header: run date, gap period covered, posture
- What changed: new signals grouped by organisation, most significant first
- Priority changes and decision-maker changes
- Quiet organisations offered for removal, and suggested additions offered for adding
- Three suggested actions for the week, each tied to a signal and fitting the posture
- Coverage: what was unreachable this run

In dyslexia-friendly mode, number every organisation and every signal, signpost each section, keep each suggested action to one short sentence, and present each offered removal or addition as its own numbered decision; never bundle two decisions in one line.

If nothing changed, the update is a header, one line saying "No new signals across the {{N}} organisations on the map in the period {{start}} to {{end}}", the coverage line, and the footer. Do not manufacture observations to fill the page.

Save to `market-watch/{{YYYY-MM-DD}}-update.md`.

---

## Step 5: Roll Changes Into the Map

Update `market-map.md` in place so it stays the single current view:

1. Set the header "Last checked" to today's date
2. For each organisation: update the "Latest signal" and "Last checked" cells in the watchlist table; append new rows to the "Signals in window" table; update the decision-maker table where a person changed; update the priority and its reason
3. Do not remove organisations or add suggested ones until the user confirms; record the offer in the update file and leave the map unchanged on that point
4. Drop signals that have fallen outside the window from the watchlist "Latest signal" cell, but keep them in the organisation detail so history is not lost

If `market-map-board.html` exists, regenerate it from the updated map (see `market-map-board.md`) so the board never shows stale data, and say in the update that the board was regenerated. Edits made on the previous board and never exported are not lost: the regenerated board offers a recovery button that copies them as watchlist markdown.

Tell the user in one line that the map has been updated and the update file saved, using descriptions rather than filenames if dyslexia-friendly mode is on.

---

## Running on a Schedule

This capability is one step of `/career-helper:weekly-update`, which is built to run unattended on a Cowork schedule, and it also has a standalone prompt (routine 6 in the `/career-routines` library). Both tell the scheduled session to read the map, report only changes, apply nothing that needs a decision, and never invent a signal, a person, or a URL; keep those instructions if the prompt is edited.

`/career-routines` covers the setup, including the one thing that matters most: a Cowork task given a local workspace folder runs on the user's machine, which must be awake, while a task needing no local folder runs in the cloud. It also covers Claude Code Desktop, cron, and cloud Routines for people outside Cowork. Say "update my market map" by hand whenever you like; the delta logic is identical.

---

## What Not to Do

- Do not re-report a signal that is already on the map or in the previous update
- Do not remove or add organisations without the user's confirmation
- Do not turn a quiet week into a page of sector commentary
- Do not suggest angles for organisations already in the tracker; point to the tracker row instead
- Do not invent a signal, a person, a title, or a URL to make the update look productive

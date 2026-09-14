---
description: Run every recurring update in one go (tracker standup, follow-ups, market map, learnings) and save a dated report; built to run unattended on a schedule
---

# Career Helper - Weekly Update

You are running the recurring maintenance pass for someone's job search. This command exists so that one prompt, `/career-helper:weekly-update`, can be put on any scheduler (Claude Code Desktop scheduled task, Claude Cowork `/schedule`, a cloud Routine, or system cron) and keep the workspace current without anyone sitting at the keyboard.

## Unattended Operation

Assume nobody is watching. Apply these rules for the whole run:

1. **Never ask a question.** Do not use AskUserQuestion and do not wait for input. Where a decision is needed (remove a quiet organisation, add a suggested one, mark an application closed), record it under "Decisions waiting for you" in the report and leave the files unchanged on that point. One decision per numbered item, each with a plain "what to do" line; never two decisions in one item. This applies to everyone, not only in dyslexia-friendly mode.
2. **Never invent.** No applications, dates, contacts, signals, people, or URLs that the files or a cited public source do not support. A missing file is reported as missing, not filled in.
3. **Only touch what this command owns.** Write the dated report, update `market-map.md` and `market-map-board.html` through the market mapper's own update logic, and refresh the tracker's At a Glance counts. Do not rewrite a CV, cover letter, or plan.
4. **Read preferences first.** If `career-helper-preferences.md` exists, apply its accessibility settings to the report. Do not create the file if it is absent. With `dyslexia_friendly: true`: number every list, including the tracker and market map items; keep sentences short; signpost each section ("Section 2 of 6: follow-ups"); refer to files by description ("your market map", "this week's report in your updates folder"), never by path; repeat the organisation or role name in every line that mentions it, so nothing depends on remembering an earlier line; use no idioms or metaphors. Apply these only when the preference is set; the default report keeps its paths and its normal shape. With `colour_blind: true`, nothing changes: the report already uses text labels only.
5. **Keep it to one screen.** A quiet week is a short report. Do not pad.

## Steps

Work through these in order, skipping any whose input file does not exist and saying so in one line.

### 1. Tracker standup

Read `applications/tracker.md`. Report:
- Every active application with its next action, overdue actions first (next date in the past).
- Any application with no movement for more than two weeks.
- The three most important actions for the week, in order.

Refresh the At a Glance counts in the tracker if they no longer match the tables. Make no other change to the tracker.

### 2. Follow-ups due

Read any `applications/*/application-strategy.md`. List follow-ups due today or overdue, each with the step the strategy describes. If none, one line.

### 3. Market map update

If `market-map.md` exists, run the `/market-mapper` weekly update exactly as its `market-watch.md` reference describes: re-check every organisation since its last-checked date, report only what changed, and roll only the signal, decision-maker, last-checked, and priority changes into the map. Offered removals and additions are recorded in the update and in this report, never applied: the map's organisation list is unchanged until the user confirms. Save `market-watch/{{YYYY-MM-DD}}-update.md` (creating the `market-watch/` folder if it does not exist), and regenerate `market-map-board.html` if it exists (say so under "Files touched"; the regenerated board offers to copy any edits the user made on the previous board and never exported, so nothing is lost). If there is no market map, say so in one line and move on. Keep the posture recorded in the map. Put the headline changes (new Act now organisations, priority changes) in this report and point to the update file for the rest.

### 4. Learnings check

If `applications/learnings/` holds per-event notes newer than `applications/learnings/patterns.md` (or no patterns file exists and three or more notes do), say so and list it under "Decisions waiting for you" as an offer to synthesise. Do not synthesise unattended; the user should read their own patterns with you in the room.

### 5. Suggested next skill

From what the files show, suggest one next step using the same table `/career-helper:status` uses. One line.

## Report

Save the report to `updates/{{YYYY-MM-DD}}-weekly-update.md` (create the folder if needed) and also print it. Structure:

```markdown
# Weekly Update: {{YYYY-MM-DD}}

## Do first
1. {{Overdue or most important action, with the application or organisation it belongs to}}
2. ...
3. ...

## Tracker
{{Active applications and next actions; stalled applications; or "No tracker found"}}

## Follow-ups due
{{List, or "None due"}}

## Market map
{{Headline changes and a pointer to market-watch/{{date}}-update.md; or "No market map found"}}

## Decisions waiting for you
1. {{One decision, then on the next line: What to do: {{plain action}}}}
2. {{...}}
{{Or "None"}}

## Files touched
{{List, or "None"}}

*Generated using Career Helper. Found this helpful? Share your success story or suggest improvements at https://github.com/Zal4DW/career-helper*
```

If no Career Helper files exist at all, the report is one line saying so and pointing to `/career-helper:quick-start`.

## Scheduling This Command

In Claude Cowork, type `/schedule` in any task, paste `/career-helper:weekly-update` as the prompt, choose weekly on Monday, and choose your workspace folder. With a local folder the task runs on your machine, so pick a time the computer is normally awake; with no local folder it runs in the cloud. `/career-routines` tailors the prompt, records the routine in `routines.md`, reviews what is running, and covers scheduling outside Cowork (Claude Code Desktop, cron, cloud Routines).

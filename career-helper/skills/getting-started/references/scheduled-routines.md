# Scheduled Job-Search Routines

**Purpose:** Turn the job search from a series of one-off sessions into a living process that keeps itself moving. Claude can run a saved prompt on a schedule (daily, weekly, weekdays only, or on demand), with access to the Career Helper skills and your workspace folder each time. This guide explains where you can schedule, gives you the one command that does all the updating, and supplies ready-made prompts for narrower routines.

**Applies to:** Anyone using Career Helper with a workspace folder. The scheduler you use depends on where you run Claude; the prompts are the same everywhere.

---

## The Simplest Route: One Command

The plugin includes `/career-helper:weekly-update`, a single command that runs every recurring update in one pass and saves a dated report to `updates/`:

1. Tracker standup: overdue actions first, stalled applications, the three things to do this week
2. Follow-ups due from your application strategies
3. Market map update via `/market-mapper`: only what changed, map and board refreshed, offers recorded rather than applied
4. A check on whether your learnings notes are ready to synthesise
5. One suggested next skill

It is written to run unattended: it never asks a question, never invents, and lists any decision it could not take under "Decisions waiting for you". Put that one command on whichever scheduler you have (below), weekly on Monday morning, and you have the whole loop. Run it by hand whenever you like too.

---

## Where You Can Schedule

Four routes, in rough order of how easy they are for a Career Helper workspace. The plugin supplies the prompts; the scheduler is a feature of the surface you use, not of the plugin.

| Route | Runs where | Needs your machine on | Sees your workspace folder | Minimum interval | Plan |
|:------|:-----------|:----------------------|:---------------------------|:-----------------|:-----|
| 1. Claude Code Desktop local scheduled task | Your machine | Yes, app open and awake (missed runs catch up once on wake) | Yes | 1 minute | Any plan with Claude Code Desktop |
| 2. Claude Cowork `/schedule` | See note below | See note below | Yes | Daily, weekly, weekdays, or on demand | Paid plan (Pro, Max, Team, Enterprise) |
| 3. System cron or launchd running `claude -p` | Your machine | Yes, awake at the scheduled time | Yes | Any | Claude Code CLI with a login or API key |
| 4. Cloud Routine (claude.ai/code/routines) | Anthropic-managed cloud | No | No: it clones a GitHub repository, so your workspace would have to be a private repo | 1 hour | Pro, Max, Team, Enterprise |

### 1. Claude Code Desktop local scheduled task (recommended for most people)

In the Claude Desktop app's Code tab, open **Routines** in the sidebar, click **New routine**, and choose **Local**. Set the name, put `/career-helper:weekly-update` (or one of the prompts below) in the instructions, choose your workspace folder as the working folder, pick a permission mode (Accept edits lets it write files without stalling), and set the schedule to Weekly on Monday. You can also create one by asking Claude in any Desktop session: "set up a weekly task every Monday at 7:30 that runs /career-helper:weekly-update in this folder."

Run it once with **Run now** and approve any permission prompts with "always allow", so future runs do not stall waiting for you. Runs only happen while the app is open and the computer is awake; if the machine slept through Monday, Desktop runs one catch-up when it wakes. Runs appear under **Scheduled** in the sidebar so you can read what happened.

### 2. Claude Cowork `/schedule`

In Claude Cowork, type `/schedule` in the chat input, paste the prompt, and choose the cadence. Each run is its own session with the plugin's skills and your workspace folder. Cowork's help centre documents the current behaviour, including whether a task runs when your computer is off; this guide does not assume it does. Keep the same folder selected in every run.

### 3. System cron or launchd with the command line

Plugin commands work in headless mode, so a scheduler entry can be one line. From your workspace folder:

```bash
cd ~/career-helper-workspace && claude -p "/career-helper:weekly-update" --permission-mode acceptEdits --permission-prompts none
```

`--permission-mode acceptEdits` lets Claude write files without a prompt; `--permission-prompts none` tells it nobody is there to answer anything else (Claude Code 2.1.259 or later). Put that line in `crontab -e` as, for example, `30 7 * * 1 cd ~/career-helper-workspace && claude -p "/career-helper:weekly-update" --permission-mode acceptEdits --permission-prompts none >> updates/cron.log 2>&1`, or in a launchd plist on macOS. The machine must be awake at the time; cron does not catch up missed runs. Do not add `--bare`: it skips plugin discovery, so the command would not be found.

### 4. Cloud Routine

Cloud Routines run without your machine, but they only see a GitHub repository they clone at the start of each run, and they cannot write to your local folder. That suits a workspace you keep in a private repository and are comfortable having cloned into Anthropic's cloud environment each week; it does not suit a folder of CVs on your laptop. If you do use one, the routine's prompt is the same `/career-helper:weekly-update`, and the run's changes come back as a branch you merge. Create one at claude.ai/code/routines or with `/schedule` in the Claude Code CLI.

### Not a scheduler: `/loop`

Claude Code's `/loop` repeats a prompt while a session stays open and expires after seven days. It is for polling during a session, not for a weekly job-search routine.

---

## Ready-Made Routines

If you want narrower routines than the weekly update, copy a prompt below into whichever scheduler you use and set the cadence shown. Adjust the bracketed parts to your situation. Every prompt below is also safe to run unattended, provided you keep its "do not invent" line.

### 1. Monday job-search standup (weekly, Monday morning)

Reads your tracker and tells you what to do this week.

```text
Read applications/tracker.md in my workspace. Give me a short Monday standup:
1. Every active application and its next action, with anything overdue flagged first.
2. Any application that has had no movement for over two weeks.
3. The three most important things for me to do this week, in order.
Keep it to one screen. Do not invent any application or status that is not in the tracker.
```

Cadence: Weekly, Monday.

### 2. Weekly market and role monitor (weekly)

Watches the market for your target roles so you are not searching from scratch each time.

```text
Search for new job postings and relevant market news from the past seven days for
[your target role, e.g. "Head of Marketing"] in [your location/region]. Use the
career-navigator approach: cite sources with dates, and be honest about volume and
seniority. List up to eight roles worth a closer look, with a one-line reason each.
Save the summary to a dated file in my workspace. Do not pad the list to reach eight.
```

Cadence: Weekly.

### 3. LinkedIn posting reminder (weekly, aligned to your content calendar)

Keeps your personal-brand cadence on track without you having to remember it.

```text
Read my content calendar (personal-brand-content-plan.md or content-calendar.md) if
present in my workspace. Remind me what I planned to post this week and which content
pillar it belongs to. Suggest one specific post idea drawn only from my existing pillars
and notes. Do not invent achievements or claims about me.
```

Cadence: Weekly.

### 4. Application follow-up check (weekdays)

Catches the follow-ups that quietly slip.

```text
Read applications/tracker.md and any application-strategy.md files in my workspace.
Tell me which applications are due a follow-up today or are overdue, based on their
next dates. For each, remind me of the follow-up step from the application strategy.
If nothing is due, say so in one line. Do not invent dates or contacts.
```

Cadence: Weekdays.

### 5. Pre-interview prep nudge (on demand)

Set this up when an interview is booked, then trigger it the day before.

```text
I have an interview for [role] at [company] on [date]. Read the interview-prep file in
the matching applications folder. Give me a focused day-before checklist: the five
stories to have ready, the questions I planned to ask, and the logistics to confirm.
Keep it short and calm in tone.
```

Cadence: On demand.

### 6. Weekly market map update (weekly, Monday morning)

Keeps your ear to the ground on organisations like your employer without searching from scratch. Build the map first with `/market-mapper`; this routine only updates it.

```text
Read market-map.md in my workspace and the most recent file in market-watch/ if one
exists. Run the market-mapper weekly update: re-check every organisation on the map for
hiring, growth, investment, and change signals dated after its last-checked date, and
report only what has changed. Update the map file in place and save the update to
market-watch/ with today's date. Keep the posture recorded in the map (if it says
employed and discreet, suggest only following, reading, or commenting). Offer, but do
not apply, removals of quiet organisations or additions of new ones. If nothing changed,
say so in one line. Do not invent a signal, a person, a title, or a URL.
```

Cadence: Weekly, Monday, 07:30 or whenever you start your week.

---

## Adapting These

- **Accessibility.** If you use dyslexia-friendly mode, the scheduled prompts will produce numbered, short-sentence output because every skill checks `career-helper-preferences.md` on each run. Keep that file in your workspace folder.
- **Keep prompts honest.** Every routine above tells Claude not to invent applications, dates, or claims. Keep that instruction in if you edit a prompt; it is what stops a scheduled task from drifting into fabrication when a file is missing.
- **Start with one.** For most people that is `/career-helper:weekly-update`, which already contains the standup, the follow-up check, and the market map update. Add the narrower routines only if you want them at a different cadence.
- **Unattended runs cannot answer questions.** Any prompt you schedule should say what to do when a decision is needed: record it and move on. The weekly update does this by design.

---

*Scheduled Job-Search Routines v1.2 | Career Helper Plugin | Prosper AI Consulting, UK*

# Scheduling in Claude Cowork

**Purpose:** The setup steps, the rules that decide where a scheduled task runs, permissions, and troubleshooting for Career Helper routines in Claude Cowork on Claude Desktop, with an appendix for people running the plugin elsewhere.

**Applies to:** Claude Cowork on a paid plan (Pro, Max, Team, or Enterprise). Cowork's help centre article "Schedule recurring tasks in Claude Cowork" is the authority on current behaviour; where this guide and that article differ, the article wins.

---

## Create a Scheduled Task

1. In any Cowork task, type `/schedule` in the chat input, or click **Scheduled** in the left sidebar and create a new task there.
2. Give it a name you will recognise in the Scheduled list (for example, "Career weekly update").
3. Paste the prompt. For the weekly update, the whole prompt is `/career-helper:weekly-update`. For a narrower routine, paste the prompt from the library with its bracketed parts filled in.
4. Choose the cadence: daily, weekdays, weekly on a chosen day, or on demand.
5. Choose the folder, or leave it empty. This decides where the task runs (next section).
6. Save, then run it once straight away from the Scheduled list. Read the result, and approve anything it asks for so future runs do not stall.

**Dyslexia-friendly mode:** keep the steps above numbered, give them one at a time with a confirmation between each ("Step 2 of 6 done. Next: choosing the cadence."), ask the cloud-or-local question on its own with two short numbered options, and refer to the routine by its name ("your weekly update routine"), never by a filename or a prompt string. Troubleshooting is one likely cause per message, with the fix, not the whole table at once.

Each run is its own Cowork session with access to the same things a normal task has: connected tools, plugins, skills, and web research. Runs appear in the Scheduled list, where you can open one to see what it did.

---

## Where a Task Runs

Cowork runs a scheduled task remotely when it can, and on your computer when it must. The deciding factor is whether the task needs a folder on your computer.

| You choose | Where it runs | Your computer | What it can reach |
|:-----------|:--------------|:--------------|:------------------|
| No folder (or a workspace Cowork can reach from the cloud) | In the cloud | Can be off or asleep; Claude Desktop can be closed | Connected tools, plugins, skills, web research, files saved to your Claude account |
| A folder on your computer | On your machine | Must be on and awake, with Claude Desktop available | Everything above plus that folder |

### Desktop Cowork and cloud Cowork keep data differently

Career Helper works in both, but they persist your files differently, and routines depend on persistence:

- **Desktop Cowork with a local folder** is the most feature-rich option for keeping data. Every session, and every scheduled run given that folder, reads and writes the same files on disk. Last week's tracker, map, and reports are simply there.
- **Cloud Cowork** keeps the files Claude creates in that conversation's data store. To carry on a long-running piece of work with Career Helper in cloud Cowork, stay in the same conversation; start a new one and the earlier files are not there. Each scheduled run is its own new session, so a cloud-run routine cannot build on last week's files unless the workspace lives somewhere every session can reach, such as a connected drive. Check what your account offers.

So the honest default for the weekly update is: use Desktop Cowork, give the task your workspace folder, accept that it runs on your machine, and pick a time you are normally at your desk (Monday 07:30 is a poor choice if the laptop is in a bag until nine). A cloud-run routine is right for a task that needs only connectors and web research, such as a market monitor that saves nothing, or for a workspace kept on a connected drive. Do not move a folder of CVs to a shared or public location for the sake of a routine.

If a run you expected in the cloud instead waited for your machine, the task was given a local folder. That is the single most common reason a routine "did not run".

---

## Permissions and Unattended Runs

A scheduled run cannot ask you anything. Two consequences:

1. **Approve on the first run.** Run the task once by hand from the Scheduled list. If it needs permission to write files or use a tool, grant it then, so later runs do not stall waiting for an answer.
2. **Prompts must not need a decision.** Every Career Helper routine is written to record a decision rather than ask for one. The weekly update lists what it could not decide under "Decisions waiting for you" in its report. If you edit a prompt, keep that behaviour, and keep the "do not invent" line.

---

## Checking It Worked

- The weekly update writes `updates/{date}-weekly-update.md`; the market map update writes `market-watch/{date}-update.md` and refreshes `market-map.md`. A dated file is the proof a run happened.
- `/career-helper:status` reads `routines.md` and surfaces open decisions from the latest weekly update.
- Open the run in Cowork's Scheduled list to read what Claude actually did. A run that completed is not the same as a run that found anything; read the report.

---

## Troubleshooting

| Symptom | Most likely cause | Fix |
|:--------|:------------------|:----|
| No output file this week | The task has a local folder and the computer was asleep or Desktop was closed | Change the scheduled time to when you are at your desk, or move the workspace somewhere cloud-reachable |
| The run stalled or ended early | It needed a permission nobody was there to grant | Run it once by hand and approve what it asks for |
| Report says "no tracker found" or "no market map found" | The input file does not exist in the folder the task uses | Build the file first (`/career-navigator` tracker, `/market-mapper` map), or check the task points at the right folder |
| The same news reported every week as new | The prompt lost its "report only what changed" instruction, or the map's last-checked dates are not being updated | Restore the library prompt; run the market map update by hand once so the dates roll forward |
| Cloud-run routine reports "no tracker found" every week | Each scheduled run is a new session and cannot see files from an earlier cloud conversation | Run it from Desktop Cowork with your local folder, or keep the workspace on a connected drive every session can reach |
| Nothing at all runs | The task is paused, or the plan does not include scheduled tasks | Check the Scheduled list; check the plan |
| Cannot find `/schedule` | Not in a Cowork task, or the feature is not available on this account | Open Cowork and start a task first; check the help centre for plan availability |

---

## Outside Cowork

The prompts are identical; only the scheduler changes. Career Helper is designed for Cowork, so treat these as secondary routes.

### Claude Code Desktop local scheduled task

In the Claude Desktop app's Code tab, open **Routines** in the sidebar, click **New routine**, choose **Local**, put `/career-helper:weekly-update` in the instructions, select the workspace folder, pick a permission mode that allows file edits, and set the schedule. Runs on your machine with the folder; needs the app open and the computer awake; if it slept through, one catch-up run happens on wake. Run it once with **Run now** and choose "always allow" for any permission prompts.

### Command line with cron or launchd

Plugin commands work in headless mode, so one line does it:

```bash
cd ~/career-helper-workspace && claude -p "/career-helper:weekly-update" --permission-mode acceptEdits --permission-prompts none
```

`--permission-mode acceptEdits` allows file writes; `--permission-prompts none` tells Claude nobody can answer a prompt (Claude Code 2.1.259 or later). Do not add `--bare`, which skips plugin discovery. The machine must be awake; cron does not catch up missed runs. Example crontab line for Monday 07:30:

```text
30 7 * * 1 cd ~/career-helper-workspace && mkdir -p updates && claude -p "/career-helper:weekly-update" --permission-mode acceptEdits --permission-prompts none >> updates/cron.log 2>&1
```

### Cloud Routine

Cloud Routines (claude.ai/code/routines, or `/schedule` in the Claude Code CLI) run without your machine, but only clone a GitHub repository at the start of each run and cannot read a local folder. That suits a workspace kept in a private repository that you are comfortable having cloned each week, and nothing else. Minimum interval one hour; changes come back on a branch.

### Not a scheduler

Claude Code's `/loop` repeats a prompt while a session stays open and expires after seven days. It is for polling during a session, not for a weekly routine.

---

*Scheduling in Claude Cowork v1.0 | Career Helper Plugin | Prosper AI Consulting, UK*

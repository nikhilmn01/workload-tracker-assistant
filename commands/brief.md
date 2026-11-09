---
description: Morning brief - today, what is at risk, and the longest free window
argument-hint: ""
---

Follow the time-assistant skill's morning brief.

1. Call `week` with scope `today`.
2. If `firstRun` is true, run the skill's first run instead: in file mode say no data was found at `where`, in drive
   mode that nothing was found in their Google Drive yet, and get the person's OK to start fresh there, then ask the
   three questions and call `settings`.
3. Otherwise, in a few lines: today's load against the workday ceiling and hands-on against its ceiling; today's
   open tasks by keyword; every promise in `atRisk` with its due day; and the longest free window (the day, the
   minutes, work or life).
4. On a weekend or a day off, `work` is null (or `dayOff` is true): say today is not a workday and show the life row
   (`life`) instead when there is one, then the rest as above.
5. Call `time_debt`. Only when `owing` is true, add one line: what is owed, and an offer to take it back (the skill's
   time debt flow). Otherwise say nothing about debt.

Round every number. Never show refs or ids.

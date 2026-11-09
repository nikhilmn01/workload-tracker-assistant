---
description: Show the week - load, free windows, open tasks, promises at risk and time debt
argument-hint: "[today|week|nextweek|lastweek|month|lastmonth] [work|personal]"
---

Follow the time-assistant skill.

Call the workload-tracker `week` tool. Arguments given: $ARGUMENTS

- A period word (today, week, nextweek, lastweek, month, lastmonth) is the `scope`; the default is week.
- "work" or "personal" is the `area`; the default is all.

If `firstRun` is true, run the skill's first run instead.

Otherwise show it compactly, one row per day: the load against the workday ceiling, the free windows as separate
blocks (never summed), and the open tasks by a keyword from their titles. The view lists open tasks only. After the
days: every promise at risk with its due day, the longest free window, and any time debt owed.

Round every number. Never show refs or ids.

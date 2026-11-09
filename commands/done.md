---
description: Close finished work with what it really took, which recalibrates its work type
argument-hint: "<which task, in a few words>"
---

Follow the time-assistant skill. The task: $ARGUMENTS

1. Call `find_tasks` with a few words from it. If several match, ask which one by title and day. If none match, try
   fewer words, or say so.
2. Ask the person for the actuals: the hands-on hours it really took, and any waiting runs and minutes per run.
   Never guess them.
3. Call `done` with the task's ref and `actual` (`hours`, `runs`, `minutesPerRun`).
4. Say it is closed and what the work type's numbers are now (`workType` in the result). While the work type has
   under 3 samples, say it is still a rough guess.

`not-found` means it was already closed or removed. `stale` means the data changed: call `find_tasks` again and
retry with the fresh ref. Never say the ref.

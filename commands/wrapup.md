---
description: Evening wrap-up - close what got done with actuals, roll the rest over
argument-hint: ""
---

Follow the time-assistant skill's evening wrap-up.

1. Call `week` with scope `today`. It lists open tasks only.
2. Go through today's open tasks with the person, a few at a time. For each one that is finished, ask for the
   actuals (hands-on hours, waiting runs, minutes per run), then call `done`.
3. For the rest, propose rolling them to the next workday. Take it from the `week` rows (scope `week`, or `nextweek`
   near the end of the week): the first day after today whose row has `workday` true and `dayOff` false, never from
   your own date arithmetic. Say the plan in one line, and only on the person's yes call `move` for each. A
   `needs-yes` answer still needs its own yes: show the preview words and wait.
4. Refs go stale after any write: take each next task's ref from the last write result's `days`, or call `week`
   again.
5. Finish with how tomorrow looks, from the days in the `move` results or another `week` call, and any promise now
   at risk.

Never show refs or ids.

---
description: Can I take this? Finds where new work fits and what it costs, then offers to book it
argument-hint: "<what landed, with hours, waiting runs or a deadline if known>"
---

Follow the time-assistant skill. The request: $ARGUMENTS

1. Read the request for a title in the person's words, hands-on hours, waiting runs and minutes per run, the
   granularity, the area, and a deadline. Take the deadline's YYYY-MM-DD from the `week` rows (`day` and `when`),
   never from your own date arithmetic. Ask only for what you cannot reasonably infer.
2. Call `work_types` and choose the closest work type. If none is close, propose one with `add_work_type` (only with
   the person's OK).
3. Call `can_i_take` with `title`, `workType`, and whatever was given: `hours`, `waitingRuns`, `minutesPerRun`,
   `granularity`, `area`, `dueDay`.
4. Answer with the consequence, never a bare yes or no: the route and the day, then each option's own figures - a
   fit's before and after against the ceiling and whether it eats the reserve; a make room's moves by title only,
   with the day each moves to, and every late promise; a borrow's `overBy` and `debtAdded`; an over budget's `overBy`.
   Say "rough guess" when the work type has under 3 samples. With no options, say the binding constraint and the
   earliest day it could work.
5. Offer the choices, a fit first. Only on the person's yes to one, call `book` with its `optionId`. Make room and
   borrow come back `needs-yes` (or the client asks the person itself): show the preview words, wait for the
   person's own yes, then call again with `confirm`. Never split a make room into plain moves to avoid asking. Then
   say what it cost from the days in the result, and relay the message when it has `skipped`.
6. If someone else asked and it cannot be done as asked, call `draft_reply` with an `optionId` from the answer and
   offer the draft as it is; with no options, offer the answer's own `draft` instead. It never names another task;
   keep that rule if you reword it.

Never show refs, option ids or tokens.

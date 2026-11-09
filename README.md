# UKG Pro (Target) — Practical Notes for Team Members

Field notes from real requests (call-off coverage with sick time, availability change, multi-day time off). Focus: how to do it right the first time and how to verify it actually worked.

---

## Golden rule

**Never trust the screen where you made the change. Verify somewhere else.**

| What you did | Where to verify |
|---|---|
| Any request (time off, backfill, availability) | **Control Center → My Requests** → click the request → right panel |
| Hours / pay / sick or vacation balance | **Timecard** and **My Accruals** tile (Available Balance, Planned Takings, Taken to Date) |
| Schedule impact | **My Schedule** for the affected dates |

"Submitted" only means the request was received. Nothing changes in balances or the timecard until it is **Approved** (and sometimes not until an overnight recalculation).

---

## Date entry — the #1 source of failed requests

- **Use the date picker and press Done.** Typing a date often *looks* accepted but is not registered by the form.
- If you type a date, press **Tab** afterward.
- **If Next / Submit does nothing, the date was not accepted.** The error message ("Correct the errors in the required fields to continue") may not be visible on screen — the form fails silently.
- Closing the side panel discards the request **without warning**. If a confirmation toast ("We've received your time-off request") did not appear, it was not submitted.

---

## Covering a partial call-off with sick time (Backfill)

Scenario: shift partly covered by someone else; you want sick time for the remaining hours.

1. **Request time off** → Request type: **Backfill – Stores** ("benefit pay for a date in the past").
2. Pick the date with the picker → Done → Next.
3. Duration: **Hours**, Start time = start of the uncovered part, Duration = uncovered hours.
4. **Deduct from: Pay Hrs – Accrued Sick Time** (default is Vacation — change it).
5. Submit → confirm toast → check it appears under the date in My Schedule as **[Submitted] Backfill**.

Notes:
- A **Call Off** may already be auto-approved with paycode **Att – Absent – Other** for the full shift. Backfill adds sick pay but may not change that paycode — ask HR / ETL-HR to recode it so the day is not counted as an unexcused absence.
- Backfill is **not** auto-approved. Sick balance drops only after approval (watch **Planned Takings**).
- Check **Submission periods** on My Schedule — Backfill has its own submission window, separate from the "request period" shown in the form.
- Arizona earned paid sick time (A.R.S. § 23-374) cannot be counted as an absence leading to discipline.

---

## Availability change

- **Patterns must start on a Sunday.** The picker only allows Sundays, typically ~3 weeks out. Use the earliest one offered.
- Use **Show list** (not the graph) to see exact times per day.
- To change several days at once: check the days → **Edit availability** → set times → choose:
  - **Replace previously scheduled availability** — overwrite (usually what you want)
  - **Merge** — add to what is already there
- To block a day completely: Status = **Unavailable**, 12:00 AM – 12:00 AM.

### Overnight availability looks confusing — it is correct

UKG stores availability **per calendar day**. "1:00 PM – 2:00 AM" is split into:

```
Mon 1:00 PM ─────────── Tue 2:00 AM
  └ Mon: 1PM–12AM ┘└ Tue: 12–2AM ┘
```

So the list shows "12:00–2:00 AM + 1:00 PM–12:00 AM" for each day. The 12–2 AM piece is the **tail of the previous evening**, not an early start.

- Because the week starts on Sunday, Saturday's after-midnight tail may need an explicit **Sunday 12:00–2:00 AM** entry.
- A fully Unavailable day also cuts off the previous evening at midnight.
- On Review, the list shows +/- hours per day and total weekly hours before/after — check it before Submit.

---

## Time off for non-consecutive days

- Use **Add another date** to put several separate days in one request.
- The request list shows a **range** (e.g. "12/01 – 12/16") — this does **not** mean every day in between.
- The real days are in the right panel: **Requested Dates → Paycodes**.

---

## Housekeeping

- Old requests can stay in **Submitted** forever, sometimes with no approver. Cancel stale ones so managers aren't confused.
- Request types and windows (paid/unpaid scheduled time off, backfill, open shift claims) each have their own **submission period** — listed on the My Schedule page.

---

## Why it feels broken (for managers)

Most "UKG doesn't work" moments are **UI and configuration**, not failed transactions:

- Silent validation (no visible error, button just does nothing)
- Panels that discard input without warning
- Data shown the way the database stores it (per-day overnight splits, date ranges)
- Results that appear only after approval or overnight recalculation

The transaction usually went through — verify in Control Center / Timecard before re-entering, to avoid duplicates.

This page online: https://azwiki.github.io/ukg/ 

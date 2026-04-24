# skill.md
# WorkOS -- Email Skills
# Drafted by John Harden, Lemhi.AI (In Conjunction with Claude Code)
**Version:** 6.0 | Two skills defined: Morning Email and Nightly Wrap-Up Email.

All email is sent to the user's own email address (user_email in state.md Settings) via Microsoft Graph API.
No email is ever sent to anyone other than the user without explicit user instruction.

---

## SKILL 1: MORNING EMAIL

### When to Execute
Called automatically at the end of Morning Boot Sequence Step 14 (instructions.md Section 1).
Do not call this skill at any other time unless the user explicitly requests it.

### What to Pull
Read the following before composing:
- data.md ## Settings (name, timezone), ## Active Workstreams, ## Open Loops, ## Muted Task Types
- data.md ## Task Queue (Todo, In Progress, Blocked), ## Quick Todos, ## Agentic Queue
- data.md ## Task Library -- avg_completion_time_minutes for each task type (used for time estimates)
- data.md ## People -- VIP names, active delegations, anyone flagged in today's boot

### Subject Line Format
```
WorkOS Morning Boot — [DAY], [DATE] | [N] tasks · [N] new · [N] meeting preps
```
Example: `WorkOS Morning Boot — Monday, Apr 14 | 9 tasks · 3 new · 2 meeting preps`

### Body Structure
Clean HTML. Mobile-readable. Two parts delivered in this email: Step 1 (Intelligence Summary) then Step 2 (Priority Card Deck). Step 3 is delivered in Cowork only.

---

**Part 1 — Intelligence Summary**

Plain text block. Bullets only. Omit any section with nothing to report -- do not write 'None.'

```
WorkOS Morning Boot — [Day, Date]
Boot completed at [time] [timezone].

Files: state.md [OK/WARN] · tasks.md [OK/WARN] · library [OK/WARN] · people [OK/WARN]
[If any WARN: one-line note on what failed.]

Calendar shifts since yesterday
- [bullet per change: time moves, new events, cancellations, attendee changes]

Key signals overnight
- [bullet per notable item: agreements, alerts, decisions, commitments made in email/DM]
- [include: VIP appearances, stale delegations, people moved to stale, SOP updates]

Loops closed
- [open loops resolved by this boot's scan]

[N] tasks total — priority deck below.
```

---

**Part 2 — Priority Card Deck**

Rendered as an Adaptive Card. Five groups, always in this order. Hide empty groups entirely.

**Header:** Morning Priority Deck — [Day, Date]
**Subheader:** Pre-prioritized by Copilot. Edit any that need adjusting. [N] tasks total ([Y] carry-forward · [Z] meeting preps · [W] new).

Groups:
- **A — Today's Meetings** | Meeting preps sorted by start time
- **B — Overdue / Due Today** | Missed deadlines + same-day commitments
- **C — This Week** | Due by end of Friday
- **D — Active / No Deadline** | Open tasks, no firm date
- **E — Quick / Lightweight** | Sub-5-minute items, self-email extractions

Each task card:
- **[Task name]** (bold, action-oriented -- rewrite passive names)
- Workstream badge &nbsp;|&nbsp; People: [name, role/company]
- Badge: 🔴 Today/Overdue &nbsp;|&nbsp; 🟠 This week &nbsp;|&nbsp; 🔵 Informational &nbsp;|&nbsp; ⚪ TBD
- *Why now:* [one line -- reason it's on today's deck, not a description of the task]
- **NEW** (if not present in yesterday's task list)
- Priority: **High** / **Med** / **Low** / **Skip**
- ✏️ Draft ready (if AA-classed with a first pass prepared)

Priority logic applied before sending:
- High → today's meeting preps, overdue, 48-hr deadlines, already-committed actions
- Med → this-week deadlines, active partner/investor tasks, open loops 48h+
- Low → no-deadline tasks, FYI items, lightweight extractions
- Skip → no clear action, duplicates, noise (Copilot flags; user confirms in Cowork)

---

*Open Cowork · Tasks start immediately. Interrupt any time to redirect or adjust.*

---

### Graph API Call

Use CallGraph with method POST to send the email:
- Path: `/me/sendMail`
- Method: POST
- Body:
```json
{
  "message": {
    "subject": "[SUBJECT LINE]",
    "body": {
      "contentType": "HTML",
      "content": "[FULL HTML BODY]"
    },
    "toRecipients": [
      {
        "emailAddress": {
          "address": "[user_email from state.md Settings]"
        }
      }
    ]
  },
  "saveToSentItems": true
}
```

On success: log `morning_email_sent: true` in today's session log.
On failure: log the error. Announce to user in Cowork at next session: 'Morning email failed to send on [DATE]. Reason: [error].'
Do not retry automatically. Do not halt the boot on email failure.

---

## SKILL 2: NIGHTLY WRAP-UP EMAIL

### When to Execute
Called automatically at the user's configured nightly_wrap_time from state.md Settings.
Only runs if nightly_wrap is set to true in state.md Settings.
Can also be triggered manually by the user saying 'send wrap-up' or 'send nightly summary'.

### What to Pull
Read the following before composing:
- data.md ## Completed Tasks -- all tasks completed today (matching today's date in completed_at)
- data.md ## Task Queue -- current state (what is still active, blocked, or in progress)
- data.md ## Active Workstreams, ## Open Loops added today
- data.md ## People -- anyone added or updated today
- Logs/session-[today].md -- session summary and stats for the day

### Subject Line Format
```
WorkOS Wrap-Up | [DAY], [DATE] | [N] completed | [N] still in queue
```
Example: `WorkOS Wrap-Up | Monday, Apr 14 | 4 completed | 5 still in queue`

### Body Structure
Clean HTML. Shorter than the morning brief. Summary-focused, not action-focused.

---

**WORKOS NIGHTLY WRAP-UP**
[DAY OF WEEK], [DATE] &nbsp;|&nbsp; [USER TIMEZONE]
*Built by [John Harden](https://www.linkedin.com/in/john-harden/) &nbsp;|&nbsp; [Lemhi.ai](https://lemhi.ai/?ref=workos)*

---

**COMPLETED TODAY**
> If no tasks completed: 'No tasks completed today.'

| Task | Type | Workstream | How It Was Resolved |
|------|------|-----------|---------------------|
| [task name] | [type] | [workstream] | [resolution_notes from tasks-completed.md, truncated to 1 line] |

---

**STILL IN QUEUE**
Brief summary only -- no full task details.

- In Progress ([N]): [task names, comma-separated]
- Todo ([N]): [task names, comma-separated]
- Blocked ([N]): [task names and blocker, comma-separated]

---

**OPEN LOOPS ADDED TODAY**
> Only include if new Open Loops were added during today's sessions.

- [item] | [flag]

---

**SESSION STATS**
Tasks actioned today: [N created] | [N completed] | [N snoozed] | [N won't do] | [N delegated]
Library entries updated: [N]
People updates: [N added] | [N moved to stale] | [N reactivated]

---

**TOMORROW**
Highest priority task in queue: **[task name]** ([workstream])
First boot: 5am [timezone]

---

*Tomorrow's brief arrives at 5am. Open Cowork any time to work ahead.*

---

### Graph API Call

Use CallGraph with method POST to send the email:
- Path: `/me/sendMail`
- Method: POST
- Body:
```json
{
  "message": {
    "subject": "[SUBJECT LINE]",
    "body": {
      "contentType": "HTML",
      "content": "[FULL HTML BODY]"
    },
    "toRecipients": [
      {
        "emailAddress": {
          "address": "[user_email from state.md Settings]"
        }
      }
    ]
  },
  "saveToSentItems": true
}
```

On success: log `nightly_email_sent: true` in today's session log.
On failure: log the error. Announce to user at next Cowork session: 'Nightly wrap-up email failed on [DATE]. Reason: [error].'
Do not retry automatically.

---

## SHARED EMAIL RULES

- Both emails are sent only to the user's own email address (user_email in state.md Settings).
- Neither email ever sends to any other recipient without an explicit user instruction in that session.
- Both emails save to Sent Items (saveToSentItems: true) so the user has a searchable archive.
- HTML is the content type for both. Plain text fallback is not required.
- Neither skill modifies any WorkOS data file. Read-only access to all files.
- If user_email is not set in data.md ## Settings: do not attempt to send. Log the error. Prompt user to set their email in the next Cowork session.

---

*skill.md | WorkOS email skills | Version 6.0 | Called by instructions.md Morning Boot and Nightly Wrap-Up trigger*

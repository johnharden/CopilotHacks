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
- state.md -- Settings (name, timezone), Active Workstreams, Open Loops, Muted Task Types
- tasks.md -- full Task Queue (Todo, In Progress, Blocked), Quick Todos, Agentic Queue
- task-library.md -- avg_completion_time_minutes for each task type (used for time estimates)
- people.md -- VIP names, active delegations, anyone flagged in today's boot

### Subject Line Format
```
WorkOS | [DAY], [DATE] | [N] tasks | [N] drafts ready
```
Example: `WorkOS | Monday, Apr 14 | 7 tasks | 3 drafts ready`

### Body Structure
Compose as clean HTML email. Use headers, bullets, and minimal tables. No walls of text.
All section headers bold. Use horizontal rules between sections. Mobile-readable.

---

**WORKOS MORNING BRIEF**
[DAY OF WEEK], [DATE] &nbsp;|&nbsp; [USER TIMEZONE]
*Built by [John Harden](https://www.linkedin.com/in/john-harden/) &nbsp;|&nbsp; [Lemhi.ai](https://lemhi.ai/?ref=workos)*

---

**FILES LOADED**
State: [OK/WARN] &nbsp;|&nbsp; Tasks: [OK/WARN] &nbsp;|&nbsp; Library: [OK/WARN] &nbsp;|&nbsp; People: [OK/WARN]
> If any file shows WARN: include a one-line note explaining what was missing or failed.

---

**WORKSTREAMS**
[count] active &nbsp;|&nbsp; [count] stale &nbsp;|&nbsp; [count] completed since last boot
> List stale workstreams by name if any exist.

---

**TASKS FOR TODAY**
One row per task in the Todo column of tasks.md, ordered by priority.

| # | Task | Type | Workstream | Est. Time | AI First Pass |
|---|------|------|-----------|-----------|---------------|
| 1 | [task name] | [type] | [workstream] | [avg from library or --] | [one-line summary of first pass] |
| 2 | ... | | | | |

> For tasks on the never_auto_draft_list: AI First Pass column shows 'Requires your judgment.'
> For unknown task types: AI First Pass column shows 'First pass unverified -- review in Cowork.'
> Include In Progress and Blocked tasks below the Todo list as a separate short table if any exist.

---

**DRAFTS READY FOR REVIEW**
Tasks in the Agentic Queue with status Pending Review. These have a full draft waiting.

| Task | Type | Workstream | Draft Summary |
|------|------|-----------|---------------|
| [task name] | [type] | [workstream] | [one-sentence draft summary] |

> Footer: 'Open Cowork and say "open [task name]" to review any draft.'

---

**QUICK TODOS**
Human-Only tasks ready to execute with pre-printed steps.

For each Quick Todo:
- **[Task Name]** | Est: [time]
  1. [step 1]
  2. [step 2]
  [tool: [tool name] -- [URL] if requires_third_party]

---

**DELEGATED TASKS**
> Only include if active delegations exist.

| Task | Delegated To | Date | Days Out | Status |
|------|-------------|------|----------|--------|
| [task] | [person] | [date] | [N] days | [status] |

> Flag any row where Days Out >= 3 in bold as: **STALE -- follow up today**

---

**OPEN LOOPS**
> Only include if Open Loops exist in state.md.

| Item | Age | Flag |
|------|-----|------|
| [item] | [N days] | [UNKNOWN TASK TYPE / NEEDS DEFINITION / FOLLOW UP] |

---

**PEOPLE RADAR**
> Only include if VIPs appear in today's tasks OR stale delegations exist OR people were migrated to stale.

- VIPs in today's context: [name(s)]
- Stale delegations: [name -- task -- N days]
- Moved to stale today: [name(s)] (no interaction in 30+ days)

---

**MUTED TASKS**
> Only include if Muted Task Types exist. Keep brief.

[type] | muted [date] | suppressed [N] times &nbsp;&nbsp; (repeat per entry)
*Say "unmute [type]" in Cowork to restore.*

---

*Open Cowork to work through tasks interactively.*

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
- tasks-completed.md -- all tasks completed today (matching today's date in completed_at)
- tasks.md -- current Task Queue state (what is still active, blocked, or in progress)
- state.md -- Active Workstreams, Open Loops added today
- people.md -- anyone added or updated today
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
- If user_email is not set in state.md Settings: do not attempt to send. Log the error. Prompt user to set their email in the next Cowork session.

---

*skill.md | WorkOS email skills | Version 6.0 | Called by instructions.md Morning Boot and Nightly Wrap-Up trigger*

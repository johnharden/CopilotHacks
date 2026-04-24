# onboard.md
# WorkOS -- One-Time Onboarding Protocol
# Drafted by John Harden, Lemhi.AI (In Conjunction with Claude Code)
# Version: 6.0 | Run once. Never loaded again after Section 10 completes.

---

## SECTION 0: FILE PURPOSE

> [COPILOT INSTRUCTION -- READ BEFORE DOING ANYTHING ELSE]
> This file is the one-time WorkOS onboarding protocol.
> It is loaded only when no WorkOS data file exists and no prior onboarding has been completed.
>
> REQUIRED FILES FOR THIS SESSION -- both must be attached before proceeding:
>   1. instructions-v6.md  (operating rules and email skills -- you are reading the result of loading this)
>   2. onboard-v6.md       (this file)
>
> instructions.md defines all operational rules. This file's only job is to collect the data
> needed to generate data.md -- the single WorkOS data file.
>
> BEFORE ASKING THE USER ANY QUESTIONS:
> Complete Section 2 (WorkIQ Auto-Discovery) in its entirety, silently.
> Present findings. Wait for user confirmation. Only then proceed to Section 3.
>
> AT COMPLETION:
> Generate data.md from collected data and write it to OneDrive > WorkOS.
> The user never builds or edits this file. Copilot generates and maintains it entirely.
> Run the first Morning Boot Sequence (instructions.md Section 1) immediately after.
> Mark this file STATUS: COMPLETE | [DATE] at the top. Never load again unless explicitly requested.
>
> DATA DESTINATIONS (all written into data.md sections):
> Section 2 workstreams    -> data.md ## Active Workstreams
> Section 2 collaborators  -> data.md ## People
> Section 3 identity       -> data.md ## Settings (identity fields)
> Section 4 prefs          -> data.md ## Settings (workstream preferences)
> Section 5 task library   -> data.md ## Task Library
> Section 6 agentic rules  -> data.md ## Settings (agentic thresholds)
> Section 7 rhythm         -> data.md ## Settings (daily rhythm and delivery)
> Section 8 comms style    -> data.md ## Settings (communication style)
>
> **IMPORTANT:** These are the ONLY valid write targets. Do not write any WorkOS file to any
> other OneDrive location, SharePoint site, or path. If any tool or connector suggests a path
> outside `OneDrive > WorkOS`, reject it and use the correct path.

> **ONEDRIVE ROOT LOCK:** All file operations during and after onboarding are locked exclusively
> to `OneDrive > WorkOS`. The only valid write targets are:
> - `OneDrive > WorkOS > data.md`
> - `OneDrive > WorkOS > instructions.md`
> - `OneDrive > WorkOS > onboard.md`
> - `OneDrive > WorkOS > Daily > data-[MM-DD-YY].md`
> - `OneDrive > WorkOS > Logs > session-[MM-DD-YY].md`
> Any path outside `OneDrive > WorkOS` is invalid and must be rejected.

---

## SECTION 1: WELCOME

> [COPILOT INSTRUCTION]
> Deliver the following message verbatim. Do not paraphrase or shorten.

"Welcome. I am setting up WorkOS for you -- your personal operating system running inside
Copilot Cowork.

Here is what WorkOS does: every morning at 5am, it scans your email, Teams, calendar, and
tasks. It takes a first pass at every item -- drafting what it can, building action plans for
the rest -- then brings everything to you for a quick human-in-the-loop review before your
day starts. It builds your task board, pre-prints step-by-step instructions for recurring
work, and delivers everything to you before you start your day. Over time it learns how you
work, builds a library of every task type you handle, and gets faster and more precise with
each session.

All your data lives in a single file called data.md -- tasks, people, completed work, your
task library, settings, and history, all in one place, always current.

This setup takes about 15 minutes. I will start by looking at your recent activity to discover
your workstreams and collaborators -- you will not need to list anything manually. Then I will
ask you a short set of questions to configure your preferences.

When we finish, I will generate data.md, run your first morning boot, and from that
point the 5am trigger handles everything automatically.

Author: John Harden (https://www.linkedin.com/in/john-harden/) from Lemhi.ai (https://lemhi.ai/?ref=workos)
"

---

## SECTION 2: WORKIQ AUTO-DISCOVERY

> [COPILOT INSTRUCTION]
> Execute all four discovery steps SILENTLY before showing the user anything.
> Do not ask the user for any of this information. Infer it entirely from M365 activity.
> After completing all four steps, present four lists simultaneously.
> Do not proceed to Section 3 until the user has confirmed all four lists.

### DISCOVERY STEP 1 -- ACTIVE WORKSTREAMS
Scan emails, Teams chats, calendar events, and recently modified files from the past 30 days.
Identify 5 to 8 recurring named projects or initiatives. These are Workstreams -- project
containers, not topic tags. For each: infer name, estimated goal, current status.

Present as a markdown table:

| # | Workstream Name | Status | Estimated Goal |
|---|-----------------|--------|----------------|
| 1 | [AUTO-DISCOVERED -- CONFIRM OR EDIT] | Active | [INFERRED] |
| 2 | [AUTO-DISCOVERED -- CONFIRM OR EDIT] | Active | [INFERRED] |
| 3 | [AUTO-DISCOVERED -- CONFIRM OR EDIT] | Active | [INFERRED] |
| 4 | [AUTO-DISCOVERED -- CONFIRM OR EDIT] | Active | [INFERRED] |
| 5 | [AUTO-DISCOVERED -- CONFIRM OR EDIT] | Active | [INFERRED] |

### DISCOVERY STEP 2 -- TOP COLLABORATORS
Identify the top 8 to 10 people by interaction volume across email, Teams DMs, and calendar.
For each: name, inferred role, primary interaction channel. These seed data.md ## People.

Present as a markdown table:

| Name | Inferred Role | Primary Channel |
|------|---------------|-----------------|
| [AUTO-DISCOVERED] | [ROLE] | [Email / Teams / Calendar] |
| [AUTO-DISCOVERED] | [ROLE] | [Email / Teams / Calendar] |
| [AUTO-DISCOVERED] | [ROLE] | [Email / Teams / Calendar] |
| [AUTO-DISCOVERED] | [ROLE] | [Email / Teams / Calendar] |
| [AUTO-DISCOVERED] | [ROLE] | [Email / Teams / Calendar] |

### DISCOVERY STEP 3 -- RECENT TOPIC CLUSTERS
Extract the top 10 to 15 keywords or topic clusters from the past 14 days of activity.
These tune the morning task scanner.

Present as inline code tags:
`[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]` `[AUTO]`

### DISCOVERY STEP 4 -- CANDIDATE TASK LIBRARY SEEDS
Identify 3 to 5 obvious recurring task types from activity patterns.
These become candidates for the data.md ## Task Library bootstrap in Section 5.

Present as a bullet list:
- [AUTO-INFERRED RECURRING TASK TYPE]
- [AUTO-INFERRED RECURRING TASK TYPE]
- [AUTO-INFERRED RECURRING TASK TYPE]

> [COPILOT INSTRUCTION]
> After presenting all four lists, ask:
> "Here is what I found from your recent activity. Confirm, correct, or add anything I missed.
> I will wait until you confirm all four lists before moving on."

---

## SECTION 3: ROLE AND IDENTITY

> [COPILOT INSTRUCTION]
> This section is a free-form conversation. Do not ask rigid questions one at a time.
> Open with a single prompt and let the user answer however they want -- all at once,
> in fragments, or over a few back-and-forths. Your job is to extract the data you need
> from whatever they say and confirm your understanding at the end.
>
> Proposed considerations to surface in your opening prompt (present as a light list,
> not a form -- the user can address all, some, or none explicitly):
> - Name and job title
> - Company and what it does
> - What success looks like for them in the next 90 days
> - The top things only they can decide or own
> - Who they report to and who reports to them
> - Any ongoing partnerships, investors, customers, or external relationships worth tracking
>
> After the user responds, extract what you can and confirm:
> "Here is what I have for your identity profile: [summary]. Anything missing or off?"
> Fill gaps with targeted follow-up only for fields that are completely absent.
> Do not re-ask for anything the user already answered.
>
> Data destination: data.md ## Settings (identity fields)

---

## SECTION 4: WORKSTREAM PREFERENCES

> [COPILOT INSTRUCTION]
> Free-form conversation. Open with one prompt covering the whole topic.
> The user can answer as briefly or thoroughly as they want.
>
> Proposed considerations to surface:
> - How many active workstreams they want open at once (before you start asking to pause or archive)
> - How often they want workstream status reviewed -- daily, weekly, or only when they ask
> - What "done" means for a workstream -- milestone reached, date passed, or they tell you
> - How they prefer tasks organized -- by workstream swimlane, priority, or due date
>
> After the user responds, confirm what you heard:
> "Got it -- here is how I will manage your workstreams: [summary]. Does that match?"
> Follow up only on anything left completely unanswered.
>
> Defaults to apply if user does not address a field:
> - max_active_workstreams: 7
> - review_cadence: weekly
> - definition_of_done: manual declaration
> - kanban_style: swimlanes by workstream
>
> Data destination: data.md ## Settings (workstream preference fields)

---

## SECTION 5: TASK LIBRARY BOOTSTRAP

> [COPILOT INSTRUCTION]
> This section pre-populates data.md ## Task Library. It is the most important configuration section.
> Free-form conversation. Let the user describe their work naturally.
>
> Before opening the conversation, tell the user:
> "For anything you describe, I will check whether your organization already has a process
> document for it. If I find one, I will show you and ask whether you follow it or do it your
> own way. If I find nothing, I will capture how you do it. The library grows automatically
> with every task you complete -- you only need to seed it here."
>
> Then open with one prompt. Proposed considerations to surface:
> - The recurring things they do every week that feel routine or repetitive
> - Tasks that require logging into a specific tool or external platform (tool name + URL helpful)
> - Tasks they currently draft by hand that follow a predictable structure (agentic candidates)
> - Tasks that are frequently blocked waiting on someone else
> - What a "quick todo" looks like for them -- something done in under 5 minutes
>
> Let the user respond freely. Extract every distinct task type they mention.
> Then for each task type:
> STEP 1: Run WorkIQ SOP Discovery (instructions.md Section 5).
> STEP 2: Present the SOP result:
>   If SOP found: "I found a process document for [TASK TYPE]: [SOP NAME]. Do you follow this,
>                  or do you handle it differently?"
>   If no SOP: "No existing process found for [TASK TYPE]. Walk me through how you do it."
> STEP 3: Collect custom steps where needed. Keep this conversational -- let the user describe
>         the steps in plain language. You extract and structure them.
> STEP 4: Draft the full data.md ## Task Library with all entries, SOP fields, custom steps,
>         and Completion Learnings blocks initialized at zero.
> STEP 5: Present the drafted library for confirmation:
>   "Here is your initial Task Library based on what you described. [summary table].
>    Anything wrong, missing, or worth adjusting before I lock it in?"
> STEP 6: Do not write to data.md until the user confirms.
>
> Data destination: data.md ## Task Library

---

## SECTION 6: AGENTIC THRESHOLDS

> [COPILOT INSTRUCTION]
> Free-form conversation. The user does not need to know the internal field names.
> Open with context and a single prompt covering the topic.
>
> Context to share with the user before prompting:
> "By default I take a first pass at every task and bring it to you for review before anything
> happens. Nothing gets sent or acted on without your approval. I just need to know where to
> draw the lines -- some things I should never even attempt a draft for, and some things I can
> draft freely without asking first."
>
> Proposed considerations to surface:
> - What they want Copilot to NEVER attempt drafting or acting on, not even a first pass
>   (common examples to mention: investor communications, legal documents, anything requiring
>   a signature, financial commitments, personnel decisions, board-level emails)
> - What is safe to draft automatically without a pre-approval prompt
>   (common examples: internal recaps, email responses, meeting prep briefs, status updates,
>   research summaries, slide outlines, follow-up messages)
> - How confident Copilot should be before taking an agentic action -- HIGH means act only
>   when 90%+ certain, MEDIUM means 70%+ with explicit flags, LOW means draft everything
> - What Copilot should do when it encounters a task type it has never seen before -- ask first,
>   attempt a best-guess draft with a label, or mark it human-only and surface for later
>
> After the user responds, confirm:
> "Here is how I will handle agentic actions: [summary]. Does that match what you intended?"
> Follow up only on fields left completely unanswered.
>
> Defaults to apply if user does not address a field:
> - never_auto_draft_list: investor communications, legal documents, financial commitments, personnel decisions
> - safe_to_auto_draft_list: internal recaps, email responses, meeting prep briefs, status updates
> - agentic_confidence_threshold: MEDIUM
> - unknown_task_handling_rule: best-guess draft labeled uncertain
>
> Data destination: data.md ## Settings (agentic threshold fields)

---

## SECTION 7: DAILY RHYTHM

> [COPILOT INSTRUCTION]
> Free-form conversation. One prompt, let them describe their day.
>
> Proposed considerations to surface:
> - When they typically start their workday and their hard stop time
> - Their timezone
> - Any standing recurring meetings that should be excluded from task scanning
>   (fixed commitments -- Copilot will not generate prep tasks from them unless asked)
> - Whether they want a nightly wrap-up email in addition to the 5am morning brief, and if so, what time
>
> Note: the morning brief is always sent as an email to the user's own M365 account email.
> No other delivery surface is offered. Do not ask about this.
>
> After the user responds, confirm:
> "Here is your daily rhythm setup: [summary]. Anything to adjust?"
>
> Defaults to apply if user does not address a field:
> - workday_start: 8:00am
> - hard_stop: 6:00pm
> - nightly_wrap: false
>
> Data destination: data.md ## Settings (daily rhythm and delivery fields)

---

## SECTION 8: COMMUNICATION STYLE

> [COPILOT INSTRUCTION]
> Free-form conversation. One prompt. This is the most personal section -- let the user
> describe how they like to work with AI tools, what annoys them, what they value.
>
> Proposed considerations to surface:
> - Tone preference -- direct and brief, conversational, formal, or adaptive
> - How long responses should be by default
> - Anything Copilot should never do when communicating with them
>   (examples to offer if they draw a blank: over-explain, use filler phrases, bullet everything,
>   ask multiple questions at once, repeat what they just said back to them)
> - Formatting preference for task lists and documents -- tables and bullets, numbered lists,
>   prose, or mixed
> - Any specific people whose name appearing in any task or email should trigger an immediate
>   heads-up before anything else is processed (VIP trigger names -- these are never auto-migrated
>   to ## Stale People regardless of how often contact occurs)
>
> After the user responds, confirm:
> "Here is how I will communicate with you: [summary]. Anything to change?"
>
> Defaults to apply if user does not address a field:
> - tone: adaptive
> - response_length: adaptive
> - formatting: mixed
> - vip_trigger_names: none unless specified
>
> Data destination: data.md ## Settings (communication style fields)

---

## SECTION 9: INITIALIZATION CHECKLIST

> [COPILOT INSTRUCTION]
> Run through every item on this checklist with the user before proceeding to Section 10.
> Do not proceed to synthesis if any item is unconfirmed.
> If an item is not ready, tell the user exactly what needs to happen to resolve it first.

- [ ] Both required files are attached to this session: instructions-v6.md, onboard-v6.md
- [ ] Both files confirmed loaded: instructions-v6.md and onboard-v6.md
- [ ] Sections 2 through 8 completed -- user has engaged with each topic and confirmed the summary for each
- [ ] Active workstream list confirmed from Section 2 discovery
- [ ] Top collaborators list confirmed -- these seed data.md ## People
- [ ] Initial Task Library drafted, WorkIQ SOP Discovery run for every task type, confirmed by user
- [ ] NEVER attempt list confirmed (Section 6)
- [ ] SAFE to auto-draft list confirmed (Section 6)
- [ ] Unknown task type handling rule confirmed (Section 6)
- [ ] Daily rhythm confirmed -- morning brief email and nightly wrap preference set (Section 7)
- [ ] Nightly wrap preference confirmed (Section 7)
- [ ] Communication style and VIP trigger names confirmed (Section 8)
- [ ] User understands: people with no interaction in 30+ days are auto-migrated to data.md ## Stale People. VIPs and direct reports are exempt.
- [ ] User understands: data.md ## Completed Tasks is append-only and grows permanently -- completed tasks are never deleted.
- [ ] User understands: data.md ## Task Library is append-only and grows permanently with completion learnings after each task resolved.
- [ ] OneDrive > WorkOS folder exists or user confirms they will create it before first boot
- [ ] User confirms: Copilot generates and maintains data.md entirely. The file is never edited manually. Preference changes go through Copilot.
- [ ] User acknowledges: the 5am scheduled trigger in Copilot Cowork fires the boot chain automatically each morning once configured. No manual action required after initial setup.
- [ ] User confirms: all WorkOS files are stored exclusively in `OneDrive > WorkOS`. No files will be written to any other location.

---

## SECTION 10: SYNTHESIS AND HANDOFF

> [COPILOT INSTRUCTION]
> This section is Copilot's execution block. It is not a set of questions for the user.
> Execute all seven steps in order. Do not skip any step.

STEP 1 -- SYNTHESIZE PERSONA PROFILE
Compile all data collected from Sections 2 through 8 into a single structured persona block:
  Full name, title, company, company description
  90-day success definition
  Owned decisions and responsibilities
  Reporting structure
  Key external relationships and partnerships
  Confirmed workstream list with goals and status
  Workstream preferences (max, review cadence, definition of done, Kanban style)
  Full Task Library (all entries with SOP references, sop_steps, and custom_steps)
  NEVER attempt list
  SAFE to auto-draft list
  Confidence threshold
  Unknown task type handling rule
  Daily start time, hard stop, timezone
  Excluded standing meetings
  Delivery surface
  Nightly wrap preference and time
  Communication tone, response length, formatting preference
  Three never-dos
  VIP trigger names

STEP 2 -- CONFIRM WITH USER
Present the synthesized persona profile in a clean, readable format.
Ask: "Here is your WorkOS identity profile. Does this accurately represent how you work and
what you want from me? Say yes to proceed, or tell me what needs to change."
Wait for confirmation. Apply any corrections requested.
Do not proceed to Step 3 until the user explicitly says yes.

STEP 3 -- GENERATE data.md
Upon user confirmation, build data.md with all sections populated:
- ## Settings: all fields from Sections 3–8
- ## Active Workstreams: from Section 2 discovery, confirmed by user
- ## Archived Workstreams: empty
- ## Open Loops: empty
- ## Muted Task Types: empty
- ## Task Queue with Todo / In Progress / Blocked subsections: empty
- ## Quick Todos: empty
- ## Agentic Queue: empty
- ## Completed Tasks: header only, empty body
- ## Task Library: all entries from Section 5 with SOP fields, custom_steps, and Completion Learnings blocks initialized at zero
- ## People: all collaborators from Section 2 discovery with inferred fields (user confirms names and roles)
- ## Stale People: header only, empty body
Run WorkIQ SOP Discovery for any ## Task Library entries not yet scanned.
Verify data.md is correctly formed before writing.

STEP 4 -- WRITE ALL FILES TO ONEDRIVE
In this exact order:

Static system files first (read from session-attached copies):
  A. OneDrive > WorkOS > instructions.md  (write from the attached instructions-v6.md)
  B. OneDrive > WorkOS > onboard.md       (write from this file, with STATUS: COMPLETE | [DATE] prepended)

Data file:
  D. OneDrive > WorkOS > data.md          (the single data file generated in Step 3)

Archive and log folders:
  E. OneDrive > WorkOS > Daily > data-[today MM-DD-YY].md (first daily snapshot)
  F. Create OneDrive > WorkOS > Logs folder (do not write any log file yet -- first log written at end of first Morning Boot)
Confirm each write was successful before proceeding to Step 5.
If any write fails: stop, notify the user, and resolve before continuing.

STEP 5 -- RUN FIRST MORNING BOOT
Execute instructions.md Section 1 (Morning Boot Sequence) immediately.
This scans M365, detects tasks, takes an agentic first pass at each task, classifies and routes
each one, populates data.md ## Task Queue, builds ## Quick Todos with pre-printed steps, generates
agentic drafts, and delivers the first Morning Brief to the user's confirmed delivery surface.
The first session log is written at the end of this boot to OneDrive > WorkOS > Logs > session-[today MM-DD-YY].md.

STEP 6 -- DELIVER COMPLETION MESSAGE
Deliver the following message verbatim:

"Your WorkOS is live.

Here is what was just built:
  - data.md initialized and saved to OneDrive > WorkOS -- this single file holds everything:
    your settings, workstreams, live tasks, completed task log, task library, and people
  - Session logs write to OneDrive > WorkOS > Logs after each session
  - Your first morning boot just ran -- your task board, quick todos, and agentic first passes are ready
  - Every morning at 5am, your Copilot Cowork scheduled trigger fires this loop automatically

From this point forward, work exclusively here. I will track your tasks, learn your patterns,
take a first pass at everything before presenting it to you, and update data.md after every
session. Every new task type we encounter together gets added to ## Task Library so I never
have to ask you how to handle it twice. The library gets smarter with every task you complete.

You will never need to open onboard.md again."

STEP 7 -- MARK FILE COMPLETE
Add the following status tag to the very top of this file, above the title line:
  STATUS: COMPLETE | [DATE]
Do not load this file again in any future session unless the user explicitly requests it.

---

*onboard.md | WorkOS one-time onboarding | Version 6.0 | Run once | Do not delete*

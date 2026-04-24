# Coworker OS

**Your personal operating system inside Microsoft Copilot Cowork.**

Built by [John Harden](https://www.linkedin.com/in/john-harden/) at [Lemhi.ai](https://lemhi.ai/?ref=workos)

---

## What It Does

Coworker OS runs automatically inside Copilot Cowork. Every morning at 5am it scans your email, Teams, calendar, meeting transcripts, and task tools. It takes a first pass at everything it finds — drafting what it can, building action plans for the rest — then emails you a brief before your day starts. You review and approve in Cowork. Nothing gets sent or acted on without you.

Over time it learns how you work. Every task type you handle gets added to a living library. Every completion makes that library smarter.

---

## How It Works

Two files load into every Copilot Cowork session:

| File | Purpose |
|------|---------|
| `instructions-v6.md` | The operating brain. Defines every rule and email skills. Never edited. |
| `onboard-v6.md` | One-time setup. Run once, never again. |

One data file lives in OneDrive and is managed automatically:

| File | What Lives Here |
|------|----------------|
| `data.md` | Everything: settings, workstreams, tasks, completed tasks, task library, people, stale people, open loops, muted task types |

Session logs write to `OneDrive > WorkOS > Logs > session-[date].md` after each session.

---

## Daily Flow

1. **5am** — Boot runs automatically. Scans 8 sources. Takes a first pass at every task.
2. **Morning email** — Brief arrives in your inbox with tasks, drafts, and quick todos.
3. **You open Cowork** — Work through tasks interactively. Approve, edit, delegate, snooze, or won't-do each one.
4. **Session end** — data.md updated. Session logged.
5. **Nightly email** *(optional)* — Wrap-up summary of what got done and what's next.

---

## Setup

1. Clone or download this folder.
2. In a new Copilot Cowork session, attach two files: `instructions-v6.md` and `onboard-v6.md`.
3. Coworker OS will scan your M365 activity, ask a few free-form questions, and build your data files automatically.
4. Onboarding takes about 15 minutes. After that, the 5am trigger handles everything.

---

## Version

Current: **v6.0**

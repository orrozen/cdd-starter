---
name: update-design-log
description: Update the design log from a discussion. Turn a pasted meeting summary, chat thread or PR review into a new dated design-log entry, or append Implementation Results to an existing one. Use when the user says "update the design log", "log this decision", "write this up as a design log", or "add implementation results".
---

# Update design log

Turn a discussion the user pastes into a design-log change that follows the repo rules in `AGENTS.md`.

## 1. Find the project and the log

- Ask which project, unless it's clear. Read `projects/<project>/INTRO.md`.
- Grep `projects/<project>/design-log/` for the topic. Decide:
  - **No related log** → new entry.
  - **Related log, implementation not started** → edit that log's design sections.
  - **Related log, implementation started** → append `## Implementation Results`. Don't touch the sections above it.

## 2. Filter with the newcomer test

From the pasted text, keep only what a smart newcomer would undo without knowing why: decisions, rejected options and reasons, constraints, surprises. Drop status chatter, names of who said what, and anything already obvious from the code.

## 3. Write it

- **New entry:** copy `templates/design-log.md` to `design-log/YYYY-MM-DD-<short-slug>.md` (today's date). Fill Background, Problem, Q&A, Design, Trade-offs. Leave sections empty rather than invent content.
- **Q&A:** every question raised goes in, with its answer. Unanswered questions stay, marked `**A:** open`.
- **Implementation Results:** start with `_Appended YYYY-MM-DD. The design above is frozen._`, then what shipped, what changed and why, surprises, follow-ups.
- **Links, not copies:** reference tickets, designs and PRs by link. Don't paste their content.
- **Length:** about 80 lines at most. Move long detail to `dev/<slug>.md` and link it.

## 4. Check with the user

Show the diff. List anything you left out and why, and any open questions. Then remind the user to commit.

# AGENTS.md

This repo holds the **why** behind our code: decisions, trade-offs and incidents. Read it before you read source.

## Session start

1. Ask the user which project this session is about, unless they already said.
2. Read `projects/<project>/INTRO.md`.
3. Read `projects/<project>/design-log/`, newest first. Grep for the topic at hand instead of loading everything.
4. Only then open source files. If the code and a design log disagree, say so; don't silently pick one.

## Conventions

- **Newcomer test.** Log only what a smart newcomer would undo without knowing why.
- **Why before code.** Intro and design log come before any source file.
- **Argue in markdown.** No code before an approved design log. Keep each question in the file with its answer.
- **Append, never rewrite.** After implementation starts, add `## Implementation Results` below the design. Don't edit the design sections.
- **Short logs.** About 80 lines per log at most. Deep detail goes in `dev/`, linked.
- **Link, don't copy.** Tickets, designs and dashboards live in their own tools. Link to them.
- Design-log file names: `YYYY-MM-DD-<short-slug>.md`. Structure: see `templates/design-log.md`.

## After work

Before you finish, remind the user to:
1. Update the design log (new entry, or append Implementation Results).
2. Commit the change to this repo.

## Boundaries

Never:
- Copy ticket, spec or design-tool content into this repo. Link to it.
- Edit a design section after implementation has started. Append instead.
- Edit `system/` without first verifying the change against the code.
- Delete a question from a design log, even if it was answered "no".

## Doc index

| Path | What's there |
|------|--------------|
| `projects/<p>/INTRO.md` | What the project is, status, links |
| `projects/<p>/design-log/` | Dated decisions, with Q&A and results |
| `projects/<p>/dev/` | Deep technical detail, linked from logs |
| `projects/<p>/pm/`, `qa/`, `data/` | Product, test and data notes |
| `system/` | Architecture and glossary |
| `postmortems/` | One dated entry per incident |
| `templates/` | Design-log and postmortem templates |
| `skills/update-design-log/` | Skill: discussion to design-log entry |

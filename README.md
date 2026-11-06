# cdd-starter

**Give your AI agent the why, not just the how.** A minimal Context-Driven Development (CDD) starter.

Talk: AiDevTLV 2026 — "Why our agents got worse over six months — and the repo structure that fixed it"

## The idea

An agent only gets it when it knows **why**, not just **how**. The code already holds the how. What is missing is the onboarding a new teammate would get: the decisions, the trade-offs, the things you tried and dropped.

CDD puts that onboarding in a repo of decisions next to your code (or a folder inside it), in git.

- **Cheap on tokens.** The agent greps the slice it needs instead of loading whole wiki pages.
- **Stays up to date.** Your dev workflow (design → plan → execute → review) writes back to it, so it changes when the code changes.

## The four rules

1. **Newcomer test.** Log only what a smart newcomer, human or agent, would undo without knowing why.
2. **Why before code.** The agent reads the project intro and the design log before any source file.
3. **Argue in markdown.** No code before an approved design log. Questions stay in the file, with their answers.
4. **Append, never rewrite.** Once implementation starts, the design freezes. Add an "Implementation Results" section below it. Keep each log to about 80 lines and put the detail in `dev/`, linked.

## Layout

```
AGENTS.md                  how agents work in this repo (CLAUDE.md points here)
projects/<name>/
  INTRO.md                 what the project is, status, links
  design-log/              dated decisions: YYYY-MM-DD-<slug>.md
  dev/                     deep technical detail, linked from the design log
  pm/ qa/ data/            product, test and data notes
system/                    architecture and glossary, verified against the code
postmortems/               one dated entry per incident
templates/                 design-log and postmortem templates
skills/update-design-log/  a Claude Code skill that turns a discussion into a log entry
```

## Quickstart (one Sunday)

1. **Copy it.** Click "Use this template", or copy the files into a `/cdd` folder.
2. **Write one project.** Copy `projects/_example` to `projects/<your-project>`, fill in `INTRO.md`, and write one design log for the decision your team re-explains most often.
3. **Point your agent at it.** Keep `AGENTS.md` (and `CLAUDE.md`) at the root, then start your next task with "read the intro and design log first". After the task, update the log and commit.

## How to adopt

- **Separate repo.** Best when one team's decisions span several code repos. Clone it next to the code and add the path to each code repo's `AGENTS.md`.
- **A `/cdd` folder in a monorepo.** Best when the code lives in one place. Decisions get reviewed in the same PR as the code.

Either way: it's markdown in git. Review it like code.

## Using the skill

Copy `skills/update-design-log` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Then paste a meeting summary, chat thread or PR discussion and ask Claude to update the design log.

## License

MIT, see [LICENSE](LICENSE).

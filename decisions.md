# Decisions

## 2026-10-01: Install `jq` so the status line script can run as written
- Why: the script relies on `jq` to read session info. Installing it with Homebrew is one command and keeps the script identical to the course version.
- What we didn't pick: rewriting the script to use Python instead. That would drift from the shared course version and be harder to update.

## 2026-10-01: Turn the status line on for every project (user-level settings)
- Why: seeing how much of Claude's memory is in use matters in every project, not just this one.
- What we didn't pick: project-only settings, which would have to be set up again in each folder.

## 2026-10-01: Keep general rules in a user-level `~/.claude/CLAUDE.md`
- Why: lessons like "Notion links need a browser download" apply to every project.
- What we didn't pick: putting them in this project's CLAUDE.md. That file is the interview framework and is already over 200 lines.

# automate

Claude Code plugin that detects repetitive tasks and turns them into reusable scripts.

## What It Does

- **`/automate`** — Retrospective scan of claude-mem session history. Surfaces repeated manual sequences as automation candidates, lets you pick which to script.
- **`/automate:setup`** — One-time initialization. Adds the `## Automations` table to `~/.claude/CLAUDE.md` and creates `~/.claude/bin/` if missing.

## How It Works

A `## Automations` table in `~/.claude/CLAUDE.md` lists every available script with a description of when to use it. Claude reads this at session start and uses the scripts instead of doing the work manually.

In-session: when Claude is about to do a multi-step sequence it has seen before (via claude-mem), it asks if you want it scripted.

## Installation

```bash
claude plugin add-marketplace rubin-johnson https://github.com/rubin-johnson/automate
claude plugin install automate@rubin-johnson
```

Then run `/automate:setup` in a new session.

## Adding Scripts Manually

1. Write a script to `~/.claude/bin/<name>` (make it executable)
2. Add a row to the `## Automations` table in `~/.claude/CLAUDE.md`
3. If chezmoi-managed: `chezmoi re-add ~/.claude/bin/<name> ~/.claude/CLAUDE.md`

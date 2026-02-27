# automate

Claude Code plugin that detects repetitive tasks and turns them into reusable scripts.

## What It Does

- **`/automate`** — Retrospective scan of claude-mem session history. Surfaces repeated manual sequences as automation candidates, lets you pick which to script.
- **`/automate:setup`** — One-time initialization. Adds the `## Automations` table to `~/.claude/CLAUDE.md` and creates `~/.claude/bin/` if missing.
- **In-session detection** — When Claude is about to repeat a multi-step sequence it has seen before (via claude-mem), it asks if you want it scripted before doing it manually again.

## How It Works

A `## Automations` table in `~/.claude/CLAUDE.md` lists every available script with a description of when to use it. Claude reads this at session start and uses the scripts instead of doing the work manually.

```markdown
## Automations

Scripts in `~/.claude/bin/` — use these instead of doing the work manually.
When I notice a repeated multi-step sequence, I'll ask if you want it scripted.
Use `/automate` to review candidates from session history.

| Script | When to use | Usage |
|--------|-------------|-------|
| `chezmoi-sync` | After modifying any chezmoi-managed file | `chezmoi-sync <file>` |
| `token-log` | Log token usage for current session | `token-log <tokens> [notes]` |
```

## Requirements

- [Claude Code](https://claude.ai/code)
- [claude-mem](https://github.com/thedotmack/claude-mem) plugin (for session history analysis)

## Installation

```bash
claude plugin marketplace add rubin-johnson/automate
claude plugin install automate@rubin-johnson
```

Restart Claude Code, then run `/automate:setup` in a new session to initialize the `## Automations` section in your `~/.claude/CLAUDE.md`.

## Usage

**First time:**
```
/automate:setup
```

**After a few sessions, find automation candidates:**
```
/automate
```

**Add scripts manually:**
1. Write a script to `~/.claude/bin/<name>` (make it executable)
2. Add a row to the `## Automations` table in `~/.claude/CLAUDE.md`
3. If chezmoi-managed: `chezmoi re-add ~/.claude/bin/<name> ~/.claude/CLAUDE.md`

## License

MIT

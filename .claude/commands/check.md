<!-- AGENT-FACING — written for Claude Code, not for the vault owner. -->

# /check — Sanity Scan

You are running a vault health check. The owner may have typed `/check` or said something natural like "is everything okay", "sanity check my vault", "is anything broken". Either route runs the same flow.

Your job is to walk the vault, verify the things that should be true, and produce a short scannable report. Use traffic-light icons (✅ ⚠️ ❌) so the owner can see status at a glance.

## What to check

Run all checks. Don't stop at the first failure.

### 1. Is this actually a vault?

- ✅ if `CLAUDE.md` AND `README.md` exist at the current folder root
- ❌ if either is missing — stop here and report: "This doesn't look like a vault folder. Run `/check` from inside your second-brain folder (the one with CLAUDE.md and README.md)."

### 2. Has /setup been run?

Read README.md. Look at the "Your Vault Right Now" section.

- ✅ if `**Focus updated:**` shows a real date AND `**Your pillar:**` links to a file that exists in `pillars/`
- ⚠️ if some placeholders remain (`_(not set up yet)_`, `YYYY-MM-DD`) but a pillar file exists — partial setup
- ❌ if all placeholders still present — recommend running `/setup`

### 3. Pillar file

List `pillars/`. Filter out `_TEMPLATE.md`.

- ✅ if at least one non-template pillar file exists
- ❌ if only `_TEMPLATE.md` is there — recommend `/setup`

### 4. Global instruction file

Detect the OS, then check the expected path:
- Windows: `C:\Users\[username]\.claude\CLAUDE.md`
- Mac/Linux: `~/.claude/CLAUDE.md`

- ✅ if the file exists AND mentions this vault's path
- ⚠️ if the file exists but doesn't mention this vault — note it (might be set up for a different vault)
- ❌ if no file at that path — recommend running `/setup` and saying yes to the global file step, OR following `docs/global-instruction-file.md`

If the file exists but is named `global.md`, `Claude.md`, or anything other than exact `CLAUDE.md` (case-sensitive on Mac/Linux), flag as ❌ with: "Found a file but it's not named `CLAUDE.md` exactly. Claude Code only auto-loads `CLAUDE.md`. Want me to rename it?"

### 5. Slash commands present

Check `.claude/commands/` for all six canonical commands:
- `setup.md`
- `hello.md`
- `goodbye.md`
- `brief.md`
- `ingest.md`
- `check.md` (this file — should be present since you're running)

- ✅ if all 6 present
- ⚠️ if some missing — list them. Recommend `git pull` to get latest, or copy from the template repo.

### 6. Web Clipper templates

Check `docs/web-clipper/` for:
- `setup.md`
- `youtube-template.json`
- `x-post-template.json`
- `article-template.json`

- ✅ if all 4 present
- ⚠️ if some missing — recommend `git pull` to get latest

### 7. Vault structure (folders)

Check that these folders exist at root: `pillars/`, `raw/`, `wiki/`, `inbox/`, `decisions/`, `docs/`, `.claude/`.

- ✅ if all present
- ⚠️ if any missing — list them. They were in the template, so the owner may have deleted by accident.

### 8. Briefing freshness (informational, not a fail)

Check `wiki/briefings/` for the most recent briefing file.

- ✅ if a briefing exists and is less than 7 days old
- ℹ️ if 7+ days old — note: "Briefing is overdue. Want to run `/brief` now?"
- ℹ️ if no briefings yet — note: "No briefings yet — that's normal for a fresh vault. /brief will fire on its own when there's enough to summarize."

## Report format

Use this exact shape, keep it tight:

```
## Vault Health Report — [today's date]

**Vault:** [path]

✅ Vault structure (CLAUDE.md, README.md, all folders present)
✅ /setup has run — Focus updated 2026-04-17, pillar: [[pillars/yan-tutoring]]
✅ Pillar file exists — pillars/yan-tutoring.md
❌ Global instruction file missing — expected at C:\Users\yan\.claude\CLAUDE.md
✅ All 6 slash commands present
✅ Web Clipper templates ready
✅ Folder structure complete
ℹ️ No briefings yet (normal for fresh vault)

## Summary

1 issue found:
- Global instruction file missing. Run /setup and say yes to the global file step, or follow docs/global-instruction-file.md.

Otherwise the vault is in good shape.
```

If everything is ✅, the summary is: "Vault is healthy. Nothing to fix."

## Rules

- **Do everything in one pass.** The owner runs `/check` to get a single report, not a back-and-forth.
- **Be specific in failures.** Don't say "something is missing" — name the file and the path.
- **Plain language.** No jargon ("YAML", "frontmatter", "wikilinks").
- **Don't fix anything in /check.** This is read-only — diagnose, recommend, exit. Fixes happen in `/setup` or by the owner asking.
- **Don't lecture.** A 5-second scan, not a tutorial.

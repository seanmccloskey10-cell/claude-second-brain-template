# HELP.md — Diagnose-and-Fix Prompt

Something's not working. Don't try to debug it yourself.

**Paste the prompt below into Claude Code (in your vault folder) and press enter.** Claude runs through a diagnostic, fixes what it can, and tells you exactly what's broken if it can't.

---

## The diagnostic prompt — copy everything between the lines

---

```
Something is broken with my second brain vault. Please diagnose it.

Run through this checklist in order. Stop and tell me at the FIRST thing
that's wrong — don't try to fix everything silently. Just one fix at a
time, with my approval before each change.

1. Folder check — am I actually in a vault?
   - Confirm CLAUDE.md and README.md both exist at the current folder
     root. If either is missing, stop and tell me I'm in the wrong folder.
   - Confirm the .claude/ folder exists with at least: commands/setup.md,
     commands/hello.md, commands/goodbye.md, commands/brief.md.

2. Setup check — has the vault been customised?
   - Read the "Your Vault Right Now" section in README.md.
   - If you see "_(not set up yet)_" or "YYYY-MM-DD" placeholders, the
     wizard hasn't been run yet. Stop and offer to run setup (the user
     can say "let's get started" or type /setup — either works).

3. Pillar check — does at least one pillar exist?
   - List pillars/. If the only file is _TEMPLATE.md, no pillar has
     been created. Tell me to run setup or create one with you.

4. Global instruction file check (only if I asked you to set this up
   during setup)
   - On macOS / Linux: check ~/.claude/CLAUDE.md — does it reference my
     vault path?
   - On Windows: check C:\Users\<my-name>\.claude\CLAUDE.md — same check.
   - If it should exist but doesn't (or doesn't reference my vault), tell
     me. I might want to redo Step 6 of setup.

5. Voice-memo skill check (only if my .env contains Eleven_Labs= with a
   real key — not the placeholder)
   - Does .claude/skills/generate-voice-memo/generate.py exist?
   - Does .env exist at vault root with a non-placeholder
     Eleven_Labs= value?
   - Is python (or python3) installed and on PATH? Run python --version.
   - Run a dry-run check (no API call): can you read .env and confirm
     the key is non-empty?
   - If anything's missing, tell me which step.

6. Briefings folder check
   - Does wiki/briefings/ exist? If not, create it (it's where the
     weekly briefing is written).
   - Does wiki/briefings/audio/ exist? If not AND I have voice memo
     enabled, create it.

7. Recent activity check
   - Read log.md (if it exists). When did the last weekly briefing
     run? When was the last session note written? If both are over
     14 days, my vault may be stale — tell me so I can decide whether
     to run a catch-up briefing.

8. Folder hygiene check
   - Are there any non-.md files at the vault root that shouldn't be
     there? (.env is fine — that's expected.)
   - Are there any folders at the root that aren't in the standard list:
     .claude, .git, .obsidian, archive, decisions, docs, inbox, pillars,
     raw, wiki?
   - If anything looks weird, tell me and ask before touching it.

9. Last resort — share the symptoms
   If you've worked through 1-8 and everything looks structurally fine
   but the vault still isn't behaving, ask me:
   - "What were you doing when it broke?"
   - "What did you expect to happen?"
   - "What actually happened? (Any error messages? Paste them in.)"

Throughout: never delete files without my explicit approval. If
something's misconfigured, propose the fix in plain language and wait
for me to say "go" before you change anything. If I gave you something
ambiguous, ask one clarifying question — don't guess.

Begin.
```

---

## When to use this

- The setup wizard didn't finish, and you don't know what got created.
- You see strange template placeholders that won't go away.
- You added an ElevenLabs key but the briefing still doesn't produce audio.
- You set up the global instruction file but Claude doesn't know about your work when you open a different folder.
- Anything else "isn't working right" and you don't know where to start.

The diagnostic doesn't fix things behind your back. Every change waits for your approval. So pasting it is safe — even if you're not sure what's wrong.

## When NOT to use this

- You haven't run setup yet — start there instead. Either say *"hi, I'm new"* or type `/setup`.
- You haven't installed Claude Code yet — see [docs/install.md](docs/install.md).
- The problem is "Claude is being weird" without anything specific — try a fresh session first (close the terminal, re-open, `claude`).

## Reporting a bug

If the diagnostic confirms something is genuinely broken in the template (not your setup), open an issue at [github.com/seanmccloskey10-cell/claude-second-brain-template/issues](https://github.com/seanmccloskey10-cell/claude-second-brain-template/issues). Include:

- Which step of the diagnostic failed
- Your OS (macOS / Windows / Linux)
- Whether `/setup` had completed before the failure
- The exact error message, if any

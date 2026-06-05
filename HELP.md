# HELP.md — Diagnose-and-Fix Prompt

Something's not working. Don't try to debug it yourself.

**Paste the prompt below into Claude Code (in your vault folder) and press enter.** Claude runs through a diagnostic, fixes what it can, and tells you exactly what's broken if it can't.

---

## The diagnostic prompt — copy everything between the lines

---

```
Something is broken with my second brain vault. Please diagnose it.

You are troubleshooting for a non-technical owner. Work in plain
language. If you hit anything about install / OS / tooling you're not
sure of, READ docs/AGENT-FAQ.md before guessing or asking me — it
covers required software, Mac vs Windows differences, and common
gotchas.

HOW TO WORK THROUGH THIS:
- If I told you a specific symptom, jump to the matching section in
  PART B first, then run PART A if you still haven't found it.
- Otherwise run PART A (structure) top to bottom.
- Stop at the FIRST real problem. Don't fix everything silently. One
  fix at a time, in plain language, and wait for me to say "go" before
  you change anything.
- NEVER delete a file without my explicit approval.
- If something's ambiguous, ask ONE clarifying question — don't guess.

═══════════════════════════════════════════════════════════════════
PART A — STRUCTURE CHECK (is the vault itself set up correctly?)
═══════════════════════════════════════════════════════════════════

1. Folder check — am I actually in a vault?
   - Confirm CLAUDE.md and README.md both exist at the current folder
     root. If either is missing, stop — I'm in the wrong folder. Tell
     me to open the folder I cloned (the one with CLAUDE.md inside).
   - Confirm .claude/ exists with at least: commands/setup.md,
     commands/hello.md, commands/goodbye.md, commands/brief.md,
     commands/onboard.md.

2. Setup check — has the vault been customised?
   - Read the "Your Vault Right Now" section in README.md.
   - If you see "_(not set up yet)_" or "YYYY-MM-DD" placeholders, the
     wizard hasn't been run. Stop and offer to run it (I can say "let's
     get started" or type /setup). If I have a folder of my own notes,
     offer /onboard instead.

3. Pillar check — does at least one pillar exist?
   - List pillars/. If the only file is _TEMPLATE.md, no pillar has
     been created. Offer to run setup or create one with me.

4. Briefings folder check
   - Does wiki/briefings/ exist? If not, create it (where the weekly
     briefing is written).
   - Does wiki/briefings/audio/ exist? If not AND I have voice
     briefings enabled, create it.

5. Folder hygiene check
   - Non-.md files at root that shouldn't be there? (.env and
     .env.example are fine — expected.)
   - Folders at root NOT in the standard list: .claude, .git,
     .obsidian, decisions, docs, inbox, pillars, power-ups, raw, wiki.
   - If anything looks off, tell me and ask before touching it.

6. Recent activity check
   - Read log.md (if it exists). When did the last weekly briefing run?
     The last session note? If both are 14+ days old, the vault may be
     stale — tell me so I can decide on a catch-up briefing.

═══════════════════════════════════════════════════════════════════
PART B — SYMPTOM CHECK (structure is fine but something misbehaves)
═══════════════════════════════════════════════════════════════════

S1. "You don't know about my work when I open a DIFFERENT folder"
    (the #1 issue — the brain isn't following me everywhere)
    - This needs the global instruction file. Check:
      • Windows: C:\Users\<my-name>\.claude\CLAUDE.md
      • Mac / Linux: ~/.claude/CLAUDE.md
    - Does that file exist, AND does it name THIS vault's full path?
      • Missing → offer to create it (see power-ups/brain-follows-you.md
        or docs/global-instruction-file.md). 
      • Exists but points at a different/old path (e.g. I moved the
        vault) → offer to update the path.
    - Remind me: after creating/editing it, I must fully QUIT and
      reopen VS Code for it to take effect.
    - Test: open a different folder, start Claude, ask "what do you know
      about what I'm working on?" — a generic "hi" won't prove anything.

S2. "I see my files in VS Code but Obsidian shows nothing" (or vice versa)
    - Both apps must be opened on the SAME folder. In Obsidian:
      "Open folder as vault" → pick this exact vault folder. Tell me to
      check the folder name shown in Obsidian's top-left matches.

S3. "Web Clipper isn't saving into my vault"
    - Obsidian-the-app must be installed AND running — the clipper
      delivers files through Obsidian's URL handler. Open Obsidian.
    - Web Clipper Settings → vault name must match my Obsidian vault
      folder name exactly.
    - For YouTube specifically: I must click "Show transcript" on the
      video BEFORE clipping, or the transcript comes through empty.
    - Full setup: power-ups/web-clipper.md and docs/web-clipper/setup.md.

S4. "I added an ElevenLabs key but the briefing makes no audio"
    (only relevant if I want voice briefings — see power-ups/voice-briefings.md)
    - Does .claude/skills/generate-voice-memo/generate.py exist?
    - Does .env exist at vault root with a REAL Eleven_Labs= value
      (not the "your-elevenlabs-key-here" placeholder)?
    - Is python (or python3) installed and on PATH? Run python --version.
    - Dry-run (no API call): read .env and confirm the key is non-empty.
    - HTTP 401 → key invalid/revoked, generate a new one. HTTP 429 →
      monthly free-tier limit hit, wait for reset or upgrade.

S5. "git push fails / permission denied"
    - This is EXPECTED if the vault is still linked to the public
      template — I can't write to someone else's repo. It's also a sign
      /onboard Step 0 (which runs `git remote remove origin`) didn't
      run. Run `git remote -v`; if origin points at a
      claude-second-brain-template repo, offer to disconnect it so my
      brain is private and local-only. A personal vault should NEVER be
      pushed to a public repo.

S6. "I want to add a power-up but don't know how"
    - The power-ups live in power-ups/. Read power-ups/README.md for the
      menu, then the specific page (brain-follows-you, web-clipper,
      voice-briefings, ikigai) and walk me through it one step at a time.

S7. Last resort — share the symptoms
    If structure (Part A) is clean and nothing in Part B matches, ask me:
    - "What were you doing when it broke?"
    - "What did you expect to happen?"
    - "What actually happened? (Any error messages? Paste them in.)"

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

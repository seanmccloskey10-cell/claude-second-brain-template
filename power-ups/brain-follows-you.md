# Power-Up: Brain Follows You Everywhere

> **TL;DR:** By default your vault only works when the vault folder is open in VS Code. This power-up makes Claude read your vault at the start of **every session, in every folder** — so you can be building an app, writing an email, working on anything, and Claude already knows what you've been tracking. It takes 2 minutes and it's the single biggest upgrade. Add it right after setup.

## When to add it

**Early — ideally the moment setup finishes.** This is the power-up that turns "a folder I open when I remember to" into "an assistant that's always there." The setup wizard offers to do it for you; if you skipped it, this page is how you switch it on later.

## What it does

You create a small instruction file in a special location on your computer. Claude Code reads that file at the start of every session, in every folder. It tells Claude: *"Before you do anything, go read my vault."*

The result: you open any project on your computer, say hello, and Claude already knows what you've been working on. No re-explaining. No "let me give you context."

## How to set it up

### Option A — Let Claude do it (recommended)

In your vault folder, say:

> *"Set up the brain-follows-you power-up — make a global instruction file so you read my vault from any folder. Show me the file before you create it."*

Claude detects your OS, finds the right path, fills in your vault path, and shows you the file before writing it. Approve it and you're done.

### Option B — Do it yourself

1. Find the `.claude` folder in your user folder (create it if it's not there):
   - **Windows:** `C:\Users\[YOUR USERNAME]\.claude\`
   - **Mac:** `/Users/[YOUR USERNAME]/.claude/`

2. Create a file called `CLAUDE.md` inside that folder.

3. Paste this content and fill in the placeholders:

```markdown
# Global Instructions

## My Second Brain
I have a vault at `[YOUR VAULT PATH]` that stores everything about my work and thinking.

On every session start, before responding, read these two files:
1. `[YOUR VAULT PATH]/CLAUDE.md`
2. `[YOUR VAULT PATH]/README.md`

Do NOT read `mistakes-made.md` at session start — it's a write-only log. Durable lessons from past mistakes get promoted into CLAUDE.md as rules. The raw log is read during weekly briefings.

Don't announce that you've read them. Just use the context naturally.

## About Me
[Write one paragraph about yourself — who you are, what you're tracking]

## How I Like to Work
- I use voice-to-text, so fix obvious transcription errors without commenting
- Show me changes before making them
- Be concise — bullets over paragraphs
- Push back if I'm making a mistake

## Wrong-Folder Detection
If I say something that's clearly meant for my vault (e.g. *"hi I'm back"*, *"give me a briefing"*, *"process this article"*, *"is everything okay with my vault"*), or if I type any of `/setup`, `/hello`, `/goodbye`, `/brief`, `/ingest`, `/check`, AND you are NOT currently in my vault folder — stop and tell me:

> "You're not in your vault folder right now. Your vault is at `[YOUR VAULT PATH]`. Want me to help you switch to it? You can either close this Claude Code session and reopen it inside the vault folder, or run `cd [YOUR VAULT PATH]` in the terminal."

Do not try to run the workflow from the wrong folder — it will half-work or fail confusingly. Surfacing the folder mismatch immediately saves you from a debugging spiral.
```

## How to test it

This is the proof. Don't skip it.

1. Open a **completely different folder** in VS Code — an empty folder, another project, anything that isn't your vault.
2. Start Claude Code.
3. Ask, word-for-word: **"What do you know about what I'm working on?"**

- If Claude describes your priorities and your pillar → **it's working.** The brain follows you everywhere.
- If Claude says it doesn't know, or describes the new folder instead → the path in the file is wrong, or VS Code needs a full restart. Re-check the path and reopen VS Code.

Don't test with a plain *"hi"* — a generic greeting won't prove anything either way.

## Important notes

- **This file lives OUTSIDE your vault.** It's in a special folder Claude Code checks automatically. Don't move it.
- **If you move your vault folder,** update the paths in this file — otherwise Claude reads from the old location and finds nothing.
- **You can add more to this file over time.** Preferences, communication style, anything you want Claude to know in every session.
- **This only works in Claude Code** (the VS Code version). If you use Claude in the desktop app (Cowork), that has its own memory system — this file won't affect it.

## Cross-references

- [Power-ups menu](README.md) — the other upgrades
- [The technical template](../docs/global-instruction-file.md) — the same file, written agent-first
- [Capacity and compaction](../docs/concepts/capacity-and-compaction.md) — why a single instruction file beats re-explaining yourself

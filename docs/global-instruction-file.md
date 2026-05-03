# Make Your Brain Follow You Everywhere

By default, your vault only works when the vault folder is open in VS Code. This means if you're building an app, writing code, or working on anything else — Claude doesn't know about what you've been tracking.

There's a fix. It takes 2 minutes.

## What This Does

You create a small instruction file in a special location on your computer. Claude Code reads this file at the start of **every session, in every folder.** It tells Claude: "Before you do anything, go read my vault."

The result: you open any project on your computer, say hello, and Claude already knows what you've been working on.

## How to Set It Up

### Option A — Let Claude do it (recommended)

In your vault folder, give Claude this prompt:

> Create a file at [PATH BELOW] that tells you to read my vault at the start of every session. My vault is at [YOUR VAULT PATH]. Use the template from docs/global-instruction-file.md. Show me the file before you create it.

**The path depends on your computer:**
- **Windows:** `C:\Users\[YOUR USERNAME]\.claude\CLAUDE.md`
- **Mac:** `/Users/[YOUR USERNAME]/.claude/CLAUDE.md`

Replace `[YOUR USERNAME]` with your actual username on your computer.

### Option B — Do it yourself

1. Find the `.claude` folder in your user folder:
   - **Windows:** `C:\Users\[YOUR USERNAME]\.claude\`
   - **Mac:** `/Users/[YOUR USERNAME]/.claude/`

   If the folder doesn't exist, create it.

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

## How to Test It

1. Open a **completely different folder** in VS Code — an empty folder, anything that isn't your vault.
2. Start Claude Code.
3. Ask: **"What do you know about what I'm working on?"**

If Claude describes it → it's working. The brain follows you everywhere.
If Claude says it doesn't know → double-check the path in the file you just created.

## Important Notes

- **This file lives OUTSIDE your vault.** It's in a special folder that Claude Code checks automatically. Don't move it.
- **If you move your vault folder,** update the paths in this file. Otherwise Claude will try to read from the old location and find nothing.
- **You can add more to this file over time.** Preferences, communication style, anything you want Claude to know in every session.
- **This only works in Claude Code** (the VS Code version). If you use Claude in the desktop app (Cowork), that has its own memory system — this file won't affect it.

# Setup Guide — Starting from Scratch

This guide takes about 15 minutes. By the end, you'll have a working second brain.

## What You Need

| Tool | What it does | Cost |
|------|-------------|------|
| [VS Code](https://code.visualstudio.com/) | Where you work with Claude | Free |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Claude running in VS Code | Part of your Claude plan |
| [Obsidian](https://obsidian.md/) | Where you browse your vault | Free |
| A Claude plan (Pro, Max, or Team) | Powers everything | Your existing plan |

**You do NOT need an API key.** This runs entirely on your existing Claude subscription.

## Step 1 — Get the template (and understand what it is)

Two ways to do this. **Pick whichever feels easier — the result is the same.**

### Option A — Download ZIP (easiest, no git required)

1. Go to the GitHub page: https://github.com/seanmccloskey10-cell/claude-second-brain-template
2. Click the green **Code** button → **Download ZIP**
3. Extract the ZIP somewhere on your computer (e.g., your Documents folder)
4. Rename the extracted folder to something meaningful — your business name works well (`yan-tutoring`, `speechway-vault`, etc.)

### Option B — Git clone (if you already use git)

```
git clone https://github.com/seanmccloskey10-cell/claude-second-brain-template my-brain
```

Replace `my-brain` with whatever you want to call your vault.

---

> ⚠️ **Important — read this carefully.** The folder you just created **IS your vault.** Don't create a new empty folder alongside it. The cloned/extracted folder, with all its files inside, is what you'll use as your second brain. The placeholder content (in README.md, in `pillars/_TEMPLATE.md`) gets customized for you when you run `/setup` in Step 3. So if you see a `YYYY-MM-DD` placeholder or an empty section, that's normal — `/setup` fills it in.

## Step 2 — Open it in VS Code and start Claude Code

1. Open VS Code → **File → Open Folder** → select the folder from Step 1.
2. Open the terminal: **View → Terminal**. The keyboard shortcut is `` Ctrl+` `` on Windows/Linux, `` Cmd+` `` on Mac.
3. Connect to your Claude account (uses your existing plan, no API key):
   ```
   claude login
   ```
4. Start Claude Code:
   ```
   claude
   ```

Claude reads `CLAUDE.md` automatically. It now knows how to work with the vault.

## Step 3 — Run `/setup`

In the Claude chat, type:

```
/setup
```

Claude will walk you through a 5-10 minute wizard:
- Asks your name and what your business does
- Customizes your README with your actual focus
- Creates your first pillar file from the template
- Offers to set up the global instruction file (Step 4 below)

**The wizard handles all the customization for you.** You just answer questions. Claude shows you every change before it writes anything.

## Step 4 — Make the brain follow you everywhere

This is offered automatically by `/setup`, but worth understanding.

By default, Claude only knows about your vault when the vault folder is open in VS Code. With one small file in a special location, Claude reads your vault from **any** folder on your computer — so when you're working on something else, Claude still knows about your business.

If you said "yes" during `/setup`, this is already done. If you said "later" — see [global-instruction-file.md](global-instruction-file.md) when you're ready (2 min setup).

**To test it:** open any other folder in VS Code. Start Claude Code. Ask: *"What do you know about my business?"* If Claude describes your business, it's working everywhere.

## Step 5 — Open in Obsidian and run your first briefing

1. Open Obsidian. Choose **"Open folder as vault"** and select the same folder you opened in VS Code.

   Now you have two windows into the same brain:
   - **VS Code** — where you work with Claude (capture, ingest, brief)
   - **Obsidian** — where you browse your notes, follow links, see the big picture

2. Back in VS Code, run your first briefing:
   ```
   /brief
   ```

   If you've only just started, the briefing will be short — that's normal. It gets richer every week as you add more.

## What to Do This Week

1. **One thought per day** — open Claude Code, just say what's on your mind. 30 seconds, voice-transcribe if you can.
2. **Find one article** relevant to your business. Save it in `raw/` (or use the [Web Clipper](web-clipper/setup.md) for one-click capture). Tell Claude to process it.
3. **Wait for `/brief` to fire.** Claude tracks when your last briefing was and runs one automatically when it's time. Or run `/brief` yourself anytime.

That's the whole habit. A few minutes per day. The vault compounds.

## Optional: voice briefings

If you'd rather *listen* to your weekly briefing on a walk than read it, you can enable the optional voice-memo skill. It uses ElevenLabs (free tier — no credit card) to turn the briefing into an MP3.

Setup is 3 minutes. **It's entirely optional** — skip it if you'd rather just read.

→ See [docs/concepts/voice-briefings.md](concepts/voice-briefings.md) for the full setup walk-through.

---

## Common Issues

**"claude: command not found"**
Claude Code isn't installed yet. Follow the [install guide](https://docs.anthropic.com/en/docs/claude-code).

**"git: command not recognized" / "I don't have git installed"**
No problem — use Option A (Download ZIP) in Step 1. You don't need git at all to use this template. If you want git later for backups or version history, install [GitHub Desktop](https://desktop.github.com/) — it's the friendliest way in.

**"I see files in VS Code but not in Obsidian"**
Make sure you opened the same folder in both apps. In Obsidian: Open Vault → select the vault folder.

**"Claude isn't reading my vault context"**
Make sure you're in the vault folder when you start Claude Code. Check that `CLAUDE.md` exists in the root of your vault folder. If you want it to read from anywhere, set up the [global instruction file](global-instruction-file.md).

**"I cloned the repo but I'm not sure if I'm in my vault"**
Open the folder in VS Code. If you can see `CLAUDE.md`, `README.md`, and folders called `pillars/`, `raw/`, `wiki/` — you're in your vault. That folder, with everything in it, is your second brain.

**"The README has placeholders like `YYYY-MM-DD` — is something broken?"**
No, those are intentional. They get filled in by `/setup`. If you ran `/setup` and they're still there, run it again — it may have been interrupted.

**"I want to back up my vault"**
Your vault is just files on your computer. You can:
- Copy the folder to an external drive
- Create a private backup on GitHub (ask Claude to help you set this up)
- Use any backup tool you already have

Your data stays on your machine unless you choose to put it somewhere else.

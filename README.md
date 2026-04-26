# Your Second Brain

**Your AI forgets everything. This fixes that.**

> **👋 First time?** The folder you just cloned **IS your vault** — don't create a new empty folder alongside it. Open Claude Code in this folder and type **`/setup`** to get started. The wizard takes 5-10 minutes.

This is a system that gives Claude long-term memory about you and your business. Every time you start a new session — in any folder, on any project — Claude already knows who you are, what you're working on, and what matters to you.

No repeating yourself. No re-explaining your business. No starting from scratch.

## How It Works

Your vault is a folder of plain text files on your computer. Claude reads them at the start of every session. The more you add, the smarter it gets.

**You just talk to Claude.** Tell it what you're thinking, share an article, ask a question. Claude knows where things go and how to organize them — the instruction file it reads automatically tells it what to do.

The four commands worth knowing:

| Command | When | What it does |
|---|---|---|
| `/setup` | Once, at the start | First-run wizard — interviews you, customizes the vault, sets up the global brain |
| `/hello` | Start of each session | Briefs you on where you are and what's active |
| `/goodbye` | End of each session | Writes session notes so the next session picks up cleanly |
| `/brief` | Weekly (auto) | Full vault review with connections, blind spots, and one thing to focus on |

For everything else: **just talk to Claude.** Share a thought, paste an article, ask a question. Claude figures out where it goes.

## Three Habits

| Habit | What you do | How long |
|-------|------------|----------|
| **Capture** | Tell Claude a thought, share an article, talk about your business | 30 seconds – 10 minutes |
| **Review** | Claude runs `/brief` weekly — read the output | 5 minutes to read |
| **Feed** | One-click capture with [Web Clipper](docs/web-clipper/setup.md), then Claude processes it | 30 seconds capture, 2 min process |

Everything else is handled by Claude behind the scenes.

## What's Inside

```
your-vault/
├── README.md          ← This file (vault home page, customized by /setup)
├── CLAUDE.md          ← The instruction file Claude reads first
├── HANDOFF-PROMPT.md  ← Paste into Claude Code if you want the agent to set this up for you
├── HELP.md            ← Diagnose-and-fix prompt for when something breaks
├── .env.example       ← Optional API keys (ElevenLabs for voice briefings); copy to .env to enable
├── pillars/           ← Your business (the core — created by /setup)
├── raw/               ← Articles, PDFs, posts you've saved (originals, never edited)
├── wiki/              ← Your personal Wikipedia (Claude builds this from your sources)
│   ├── index.md       ← Table of contents (Claude maintains this automatically)
│   └── briefings/     ← Weekly briefings saved here
│       └── audio/     ← Optional MP3 voice briefings (if ElevenLabs key set)
├── inbox/             ← Quick thoughts, not yet sorted
├── decisions/         ← Business decisions with context
├── log.md             ← Activity log — what was ingested, when briefings ran
├── mistakes-made.md   ← Error log (write-only — durable lessons get promoted into CLAUDE.md)
├── SESSION-NOTES.md   ← Session-by-session log (created by your first /goodbye)
├── .claude/
│   ├── commands/      ← /setup, /hello, /goodbye, /brief, /ingest, /check
│   └── skills/        ← Optional skills (generate-voice-memo for the voice briefings)
└── docs/              ← Setup guides + concept docs
    ├── concepts/      ← Short explainers: three-layers-of-memory, the-four-commands, etc.
    └── web-clipper/   ← One-click capture: extension setup + 3 importable templates
```

## What This Costs

**Nothing extra for the core experience.** This runs on your existing Claude plan. No API key, no second bill.

**One optional add-on:** if you want your weekly briefing read aloud as an MP3 (so you can listen on a walk), you can plug in a free [ElevenLabs](https://elevenlabs.io) key in `.env`. Free tier covers ~3 audio briefings per month. Skip it if you'd rather just read the briefing — everything else works the same. See [docs/concepts/voice-briefings.md](docs/concepts/voice-briefings.md).

## Getting Started

### New here? Start with this

1. **Clone this repo** to your computer:
   ```
   git clone https://github.com/seanmccloskey10-cell/claude-second-brain-template my-brain
   ```
   *(Replace `my-brain` with whatever you want to call your vault.)*
2. **Open the cloned folder in VS Code** (File → Open Folder).
3. **Open the terminal** (View → Terminal).
4. **Connect to your Claude account:** `claude login`
5. **Start Claude Code:** `claude`
6. **Type `/setup`** and follow the wizard.

That's it. The `/setup` wizard interviews you about your business, customizes your vault, creates your first pillar, and offers to set up the global instruction file (so the brain follows you into every project).

For a more detailed step-by-step (with troubleshooting), see [docs/install.md](docs/install.md). Want to hand the whole setup off to your AI agent instead of doing it yourself? See [HANDOFF-PROMPT.md](HANDOFF-PROMPT.md) — paste it into Claude Code and the agent handles everything.

**New here? Read these short concept docs first** (each ~5 min):
- [docs/concepts/three-layers-of-memory.md](docs/concepts/three-layers-of-memory.md) — the boat / island / continent model
- [docs/concepts/the-four-commands.md](docs/concepts/the-four-commands.md) — what `/setup`, `/hello`, `/goodbye`, `/brief` actually do
- [docs/concepts/folder-grammar.md](docs/concepts/folder-grammar.md) — pillars, raw, wiki, inbox: which goes where
- [docs/concepts/capacity-and-compaction.md](docs/concepts/capacity-and-compaction.md) — why Claude needs `/hello` and `/goodbye` (the context-window problem)

### Already have a vault?

Give this prompt to Claude Code in your existing vault:

> Download https://github.com/seanmccloskey10-cell/claude-second-brain-template to a temporary folder — NOT inside my vault. Read the CLAUDE.md and docs/how-to-use.md from the downloaded template. Then look at my vault and help me add whatever I'm missing. Don't overwrite anything I already have. Show me every change before you make it.

## Now What? — Things You Can Say to Claude

Once `/setup` is done, you don't need to memorize any commands. You just talk. If you're not sure what to say, here's a list of starter prompts grouped by what you're trying to do:

**See [docs/things-you-can-ask.md](docs/things-you-can-ask.md).**

Examples from that doc:
- *"I had a thought about my pricing — can you save it?"*
- *"I saved an article to raw/ — can you read it and pull out what's useful?"*
- *"Based on everything in my vault, how should I approach raising my prices?"*
- *"Read my whole vault. What patterns do you see across my notes?"*

You don't need to use these exact words. Claude figures out what you mean.

## The Big Unlock: Your Brain Follows You Everywhere

By default, your vault only works when the vault folder is open. But there's a way to make Claude read your vault in *every* project you open — even unrelated ones.

**`/setup` will offer to do this for you.** If you want to do it manually, see [docs/global-instruction-file.md](docs/global-instruction-file.md).

**The test:** Open a completely different folder. Start Claude Code. Ask: *"What do you know about my business?"* If Claude describes your business, the brain is working everywhere.

## Your Vault Right Now

> 🛠️ **This section gets filled in when you run `/setup`.** After setup, it'll show your current priorities and link to your business pillar. Until then, it's intentionally empty.

**Focus updated:** _(run `/setup`)_

**Current priorities:**
- _(`/setup` will help you write 1-3 priorities here)_

**Your pillar:** _(`/setup` will create this and link it here)_

## Quick Rules

- File names: `lowercase-with-dashes.md`
- Dates: `2026-04-14`
- Link notes with `[[double brackets]]`
- One idea per file
- Never put passwords or API keys in the vault

## What This Is NOT

- Not a task manager — use your existing one
- Not a chat history archive — distill, don't dump
- Not a place for code — link to code, don't paste it
- Not finished — it grows with you

## Something Not Working?

See [HELP.md](HELP.md) — paste the diagnostic prompt into Claude Code and it'll walk through what's broken.

---

Free to use and share. Built by Sean McCloskey, inspired by Andrej Karpathy's LLM-wiki pattern.

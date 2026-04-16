# Your Second Brain

**Your AI forgets everything. This fixes that.**

This is a system that gives Claude long-term memory about you and your business. Every time you start a new session — in any folder, on any project — Claude already knows who you are, what you're working on, and what matters to you.

No repeating yourself. No re-explaining your business. No starting from scratch.

## How It Works

Your vault is a folder of plain text files on your computer. Claude reads them at the start of every session. The more you add, the smarter it gets.

**You just talk to Claude.** Tell it what you're thinking, share an article, ask a question. Claude knows where things go and how to organize them — the instruction file it reads automatically tells it what to do.

The one command worth knowing: **`/brief`** — a weekly briefing where Claude reads your entire vault, tells you what's changed, surfaces connections, and gives you one thing to focus on. **You don't have to remember to run it.** Claude tracks when your last briefing was and generates one automatically when it's time.

## Three Habits

| Habit | What you do | How long |
|-------|------------|----------|
| **Capture** | Tell Claude a thought, share an article, talk about your business | 30 seconds – 10 minutes |
| **Review** | Claude runs `/brief` weekly — read the output | 5 minutes to read |
| **Feed** | One-click capture with [Web Clipper](docs/web-clipper/setup.md), then `/ingest` in Claude | 30 seconds capture, 2 min process |

Everything else is handled by Claude behind the scenes.

## What's Inside

```
your-vault/
├── pillars/          ← Your business (the core)
├── raw/              ← Articles, PDFs, posts you've saved (originals, never edited)
├── wiki/             ← Your personal Wikipedia (Claude builds this from your sources)
│   ├── index.md      ← Table of contents (Claude maintains this automatically)
│   └── briefings/    ← Weekly briefings saved here
├── inbox/            ← Quick thoughts, not yet sorted
├── decisions/        ← Business decisions with context
├── log.md            ← Activity log — what was ingested, when briefings ran
├── mistakes-made.md  ← Error log (write-only — durable lessons get promoted into CLAUDE.md)
├── CLAUDE.md         ← The instruction file Claude reads first
├── .claude/
│   └── commands/     ← Slash commands: /brief (weekly review), /ingest (process raw)
└── docs/             ← Setup guides
    └── web-clipper/  ← One-click capture: extension setup + 3 importable templates
```

## What This Costs

**Nothing extra.** This runs on your existing Claude plan. No API key, no second bill.

## Getting Started

### I already have a vault

Give this prompt to Claude Code:

> Download https://github.com/seanmccloskey10-cell/claude-second-brain to a temporary folder — NOT inside my vault. Read the CLAUDE.md and docs/how-to-use.md from the downloaded template. Then look at my vault and help me add whatever I'm missing. Don't overwrite anything I already have. Show me every change before you make it.

If you're comfortable with git, you can also clone it:
```
git clone https://github.com/seanmccloskey10-cell/claude-second-brain my-brain-template
```

### Starting from scratch

See [docs/install.md](docs/install.md) for a step-by-step setup guide.

## The Big Unlock: Your Brain Follows You Everywhere

By default, your vault only works when the vault folder is open. But there's a way to make Claude read your vault in *every* project you open — even unrelated ones.

See [docs/global-instruction-file.md](docs/global-instruction-file.md) to set this up. It takes 2 minutes and it's the single most powerful feature of this system.

**The test:** Open a completely empty folder. Start Claude Code. Ask: *"What do you know about my business?"* If Claude describes your business, the brain is working everywhere.

## Your Vault Right Now

**Focus updated:** YYYY-MM-DD

**Current priorities:**
- [ ] ...
- [ ] ...

**Your pillar:** [[pillars/your-business]]

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

---

Free to use and share. Built by Sean McCloskey, inspired by Andrej Karpathy's LLM-wiki pattern.

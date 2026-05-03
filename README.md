# Your Second Brain

**Your AI forgets everything. This fixes that.**

> **👋 First time?** The folder you just cloned **is your vault** — don't create a new empty folder alongside it. Open Claude Code in this folder, run `claude`, and say something like *"hi, I'm new — let's get started"*. The setup wizard takes 5–10 minutes.

This is a system that gives Claude long-term memory about you and your work. Every time you start a new session — in any folder, on any project — Claude already knows who you are, what you're working on, and what matters to you.

No repeating yourself. No re-explaining your work. No starting from scratch.

You decide what your vault tracks. A business. A teaching practice. A research habit. Your studies. A portfolio of projects. A creative practice. The vault adapts to you — pillars (the trunks of your vault) reflect whatever you care about most.

## How It Works

Your vault is a folder of plain text files on your computer. Claude reads them at the start of every session. The more you add, the smarter it gets.

**You just talk to Claude.** Tell it what you're thinking, share an article, ask a question. Claude knows where things go and how to organise them.

### Two ways to use it (both work, pick whatever feels natural)

**Mode A — Just talk.** This is the default. Speak naturally, and Claude figures out what you want.

| What you say | What Claude does |
|---|---|
| *"Hi, I'm back"* | Reads your vault, briefs you on where you are |
| *"I'm done for tonight"* | Writes session notes for next time |
| *"Give me a briefing"* / *"What does my whole vault say?"* | Generates a weekly briefing — connections, blind spots, one thing to focus on |
| *"I read this article"* / paste a URL | Saves the source, processes it into your wiki |
| *"Is everything okay?"* | Runs a vault health check |
| *"I had a thought about X"* | Captures the thought into the right file |
| *"I just decided to drop a client"* | Logs the decision with context |

**Mode B — Slash commands.** If you prefer typing commands, every behaviour above also has a slash command: `/setup`, `/hello`, `/goodbye`, `/brief`, `/ingest`, `/check`. Same result, faster to type.

You'll find yourself drifting between both. That's fine. Both modes are first-class.

## Three Habits

| Habit | What you do | How long |
|-------|------------|----------|
| **Capture** | Tell Claude a thought, share an article, talk about your work | 30 seconds – 10 minutes |
| **Review** | Read the weekly briefing Claude generates | 5 minutes to read |
| **Feed** | One-click capture with [Web Clipper](docs/web-clipper/setup.md), then Claude processes it | 30 seconds capture, 2 min process |

Everything else is handled by Claude behind the scenes.

## What's Inside

```
your-vault/
├── README.md          ← This file (your vault home page, customised by setup)
├── CLAUDE.md          ← Instructions Claude reads automatically (you don't need to read this)
├── HANDOFF-PROMPT.md  ← Paste into Claude Code if you want the agent to set this up for you
├── HELP.md            ← Diagnose-and-fix prompt for when something breaks
├── .env.example       ← Optional API keys (ElevenLabs for voice briefings); copy to .env to enable
├── pillars/           ← The trunks — what you're tracking (created by setup)
├── raw/               ← Articles, PDFs, posts you've saved (originals, never edited)
├── wiki/              ← Your personal Wikipedia (Claude builds this from your sources)
│   ├── index.md       ← Table of contents (Claude maintains this automatically)
│   └── briefings/     ← Weekly briefings saved here
│       └── audio/     ← Optional MP3 voice briefings (if ElevenLabs key set)
├── inbox/             ← Quick thoughts, not yet sorted
├── decisions/         ← Decisions with context, so future-you knows why
├── log.md             ← Activity log — what was ingested, when briefings ran
├── mistakes-made.md   ← Error log (write-only — durable lessons get promoted into CLAUDE.md)
├── SESSION-NOTES.md   ← Session-by-session log (created the first time you wrap up)
├── .claude/
│   ├── commands/      ← Slash commands (the canonical workflow specs)
│   └── skills/        ← Optional skills (generate-voice-memo for the voice briefings)
└── docs/              ← Setup guides + concept docs (for you to read)
    ├── concepts/      ← Short explainers — what each part of the system is for
    └── web-clipper/   ← One-click capture: extension setup + 3 importable templates
```

## What This Costs

**Nothing extra for the core experience.** This runs on your existing Claude plan. No API key, no second bill.

**One optional add-on:** if you want your weekly briefing read aloud as an MP3 (so you can listen on a walk), you can plug in a free [ElevenLabs](https://elevenlabs.io) key in `.env`. Free tier covers ~3 audio briefings per month. Skip it if you'd rather just read — everything else works the same. See [docs/concepts/voice-briefings.md](docs/concepts/voice-briefings.md).

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
6. **Say** *"hi, I'm new — let's get started"* (or type `/setup`). Either way, the wizard kicks off.

That's it. The wizard interviews you about what you want to track, customises your vault, creates your first pillar, and offers to set up the global instruction file (so the brain follows you into every project).

For a more detailed step-by-step (with troubleshooting), see [docs/install.md](docs/install.md). Want to hand the whole setup off to your AI agent instead of doing it yourself? See [HANDOFF-PROMPT.md](HANDOFF-PROMPT.md) — paste it into Claude Code and the agent handles everything.

**New here? Read these short concept docs first** (each ~5 min):
- [docs/concepts/three-layers-of-memory.md](docs/concepts/three-layers-of-memory.md) — the boat / island / continent model
- [docs/concepts/the-four-rhythms.md](docs/concepts/the-four-rhythms.md) — the four rhythms that run the vault (setup, hello, goodbye, brief)
- [docs/concepts/folder-grammar.md](docs/concepts/folder-grammar.md) — pillars, raw, wiki, inbox: which goes where
- [docs/concepts/capacity-and-compaction.md](docs/concepts/capacity-and-compaction.md) — why Claude needs hello and goodbye (the context-window problem)

### Already have a vault?

Give this prompt to Claude Code in your existing vault:

> Download https://github.com/seanmccloskey10-cell/claude-second-brain-template to a temporary folder — NOT inside my vault. Read the CLAUDE.md and docs/ from the downloaded template. Then look at my vault and help me add whatever I'm missing. Don't overwrite anything I already have. Show me every change before you make it.

## Now What? — Things You Can Say to Claude

Once setup is done, you don't need to memorise any commands. You just talk. If you're not sure what to say, here's a list of starter prompts grouped by what you're trying to do:

**See [docs/things-you-can-ask.md](docs/things-you-can-ask.md).**

Examples:
- *"I had a thought about my pricing — can you save it?"*
- *"I saved an article to raw/ — can you read it and pull out what's useful?"*
- *"Based on everything in my vault, how should I approach raising my prices?"*
- *"Read my whole vault. What patterns do you see across my notes?"*

You don't need to use these exact words. Claude figures out what you mean.

## The Big Unlock: Your Brain Follows You Everywhere

By default, your vault only works when the vault folder is open. There's a way to make Claude read your vault in *every* project you open — even unrelated ones.

**Setup will offer to do this for you.** If you want to do it manually, see [docs/global-instruction-file.md](docs/global-instruction-file.md).

**The test:** Open a completely different folder. Start Claude Code. Ask: *"What do you know about what I'm working on?"* If Claude describes it, the brain is working everywhere.

## Your Vault Right Now

> 🛠️ **This section gets filled in during first-time setup.** After setup, it'll show your current priorities and link to your pillar. Until then, it's intentionally empty.

**Focus updated:** _(not set up yet)_

**Current priorities:**
- _(setup will help you write 1–3 priorities here)_

**Your pillar:** _(setup will create this and link it here)_

## Quick Rules

- File names: `lowercase-with-dashes.md`
- Dates: `2026-04-30`
- Link notes with `[[double brackets]]`
- One idea per file
- Never put passwords or API keys in the vault

## What This Is NOT

- Not a task manager — use your existing one
- Not a chat history archive — distil, don't dump
- Not a place for code — link to code, don't paste it
- Not finished — it grows with you

## Future Ideas

Documented but not built. Things you can adopt later, once you have a vault with real content in it:

- **The Ikigai interview** ([docs/concepts/ikigai-interview.md](docs/concepts/ikigai-interview.md)) — a structured self-interview rooted in the Japanese concept of *ikigai* (reason for being). Designed to surface the intersection of what you love, what you're good at, what the world needs, and what you can be paid for. Best used after a few months of vault use, when you have enough captured to reflect on.

## Something Not Working?

See [HELP.md](HELP.md) — paste the diagnostic prompt into Claude Code and it'll walk through what's broken.

---

Free to use and share. Built originally as a tool for non-technical people learning to use Claude productively.

# The Four Rhythms

> **TL;DR:** Four daily/weekly rhythms run the whole vault: **setup** (once, at the start), **hello** (at session start), **goodbye** (at session end), **brief** (weekly, often automatic). Two more — **ingest** and **check** — handle articles and sanity-checks. You don't need to memorise any of them. Talk to Claude in plain English; it'll figure out which rhythm you want. If you prefer typing slash commands (`/hello`, `/goodbye`, `/brief`, `/ingest`, `/setup`, `/check`), they all still work — both modes do the same thing.

## Two ways to use the vault

This vault has two layers, and **both work — pick whatever feels natural in the moment**:

**Speaking naturally (default).** You talk to Claude. Claude figures out what rhythm you want.
- *"Hi, I'm back"* → session start briefing
- *"I'm done for tonight"* → session end notes
- *"Give me a briefing"* → weekly review
- *"I read this article"* → article ingest
- *"Is everything okay?"* → vault sanity check

**Typing slash commands.** Faster if you know what you want.
- `/hello` `/goodbye` `/brief` `/ingest` `/setup` `/check`

You'll drift between both. That's expected. Both produce the same result.

## The four you'll actually use

### Setup — once, at the very start

The first-run wizard. Interviews you about what you want to track, customises your README, creates your first pillar file, and offers to set up the global instruction file (so Claude knows about your vault from any folder, not just the vault folder).

Takes 5–10 minutes. You only run it once.

**To trigger it:** say *"hi, I'm new"* or *"let's get started"* (or type `/setup`). If you've just cloned the repo, Claude will detect the fresh state and offer to start it on its own.

### Hello — at the start of each session

Reads your README, your CLAUDE.md, your most recent session notes, and the current state of your vault. Briefs you in 6–8 lines: what you've been working on, what's open, what's worth focusing on today.

This is the *"Claude already knows me"* moment. After a few weeks, the briefings get sharp.

**To trigger it:** say *"hi, I'm back"*, *"where am I"*, *"catch me up"* (or type `/hello`).

### Goodbye — at the end of meaningful sessions

Reviews what changed during the session. Writes a session note appended to `SESSION-NOTES.md`. Names what's incomplete or worth carrying forward. Gives the next *hello* something concrete to load.

You don't need this for short sessions where nothing changed. Run it when real work happened.

**To trigger it:** say *"I'm done"*, *"let's wrap up"*, *"stop for tonight"* (or type `/goodbye`).

### Brief — weekly, often automatic

A full vault review. Reads your pillars, wiki, decisions, recent raw items, and inbox. Surfaces:

- What's changed since last time
- Topics with the most movement
- Connections between ideas you might not see yourself
- One or two pushbacks (where Claude thinks you might be wrong)
- Open questions, unprocessed items
- Vault health (orphan pages, stale projects, anything weird)
- One thing to focus on this week
- An optional voice memo script (turned into MP3 audio if you've set up the [ElevenLabs key](voice-briefings.md))

Claude is instructed to fire this automatically if 7+ days have passed since the last briefing. You can also trigger it yourself anytime.

**To trigger it manually:** say *"give me a briefing"*, *"weekly review"*, *"what's the big picture"* (or type `/brief`).

## The two extras

### Ingest — when you share an article, post, or PDF

Reads the source fully. Compares it against your existing wiki to check for novelty. Saves the original to `raw/` (with frontmatter). Synthesises it into wiki pages. Updates `wiki/index.md`. Flags contradictions with anything you've previously captured. Marks the raw file as `processed: true`.

This is the [Karpathy raw → wiki pipeline](folder-grammar.md). It's how reading-time becomes vault-time.

**To trigger it:** paste a URL or wall of text, say *"I read this"* or *"process this"* (or type `/ingest`).

### Check — when something feels wrong

A read-only sanity scan. Verifies your README has been customised (no template placeholders left), your pillar file exists, the global instruction file is in place if you set it up, all commands are present, and the web-clipper templates haven't drifted. Returns a green/yellow/red report.

Run it when something doesn't feel right, or after a big change.

**To trigger it:** say *"is everything okay"*, *"sanity check my vault"*, *"is anything broken"* (or type `/check`).

## You don't need to memorise any of this

The whole vault is designed so you talk to Claude in plain English and Claude figures out what you want. The slash commands are a faster shortcut for people who like typing them. Either path leads to the same place.

If you forget what to say, just describe what you're trying to do. Claude is patient.

## Cross-references

- [Three layers of memory](three-layers-of-memory.md) — why these rhythms exist
- [Folder grammar](folder-grammar.md) — where each rhythm writes
- [Voice briefings](voice-briefings.md) — the optional audio version of the weekly briefing
- [Capacity and compaction](capacity-and-compaction.md) — why hello and goodbye matter even within a single project
- [Ikigai interview](ikigai-interview.md) — a future-mode reflective ritual, once your vault has data

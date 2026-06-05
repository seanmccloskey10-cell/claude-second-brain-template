<!-- AGENT-FACING — written for Claude Code, not for the vault owner. The owner does not need to read this file. Tone is directive and specific. The owner-facing copy is in README.md and docs/. -->

# Vault Instruction File

This file tells Claude how to work with the vault. Claude reads it automatically at the start of every session.

## What this vault is

A personal second brain for one person. It stores their context, decisions, knowledge, and lessons so Claude has memory across sessions.

The vault is the source of truth. The owner decides what to track — a business, a life area, a portfolio of projects, a thinking habit, a research practice. Pillars (the trunks of the vault) reflect whatever they care about. **Do not assume "their business"** — assume "what they are tracking."

## How the owner interacts with you

The owner has two modes available, and **both work**:

**Mode A — Natural language (default).** The owner talks normally: *"hi, I'm back"*, *"I read this article"*, *"let's wrap up"*, *"give me a briefing"*. You recognise the intent and run the matching workflow. **You do NOT need the owner to type a slash command for any of the standard workflows.**

**Mode B — Slash commands (still available).** Slash commands live in `.claude/commands/`. If the owner types `/hello`, `/goodbye`, `/brief`, `/ingest`, `/check`, or `/setup`, run the file directly. Some owners prefer commands; some prefer talking. Both are first-class.

The intents you recognise are mapped to slash command files below. **The slash command files are the canonical workflow specs.** When you recognise an intent — whether the owner typed the command or spoke naturally — read the corresponding file in `.claude/commands/` and follow it. Do not duplicate that workflow logic here; this file is for routing, not procedure.

## Session start protocol

Every session, before responding, read these two files:

1. This file (`CLAUDE.md`) — how to work with the vault
2. `README.md` — the owner's current focus and priorities

Then run these checks in order:

3. **First-time detection.** Has the vault been customised yet? Signals it has NOT:
   - README "Your Vault Right Now" section still contains placeholder values like `_(not set up yet)_` or `YYYY-MM-DD`
   - The only file in `pillars/` is `_TEMPLATE.md`
   - The owner's first message doesn't suggest they're already set up

   If the vault is fresh, **route to `.claude/commands/setup.md` and run it** before answering whatever else they asked. Their question may depend on the vault being set up.

   **If the owner mentions they have an existing folder of their own notes/documents to import, route to `.claude/commands/onboard.md` instead** — it bootstraps the vault from their folder rather than a blank-slate interview.

4. **Staleness gate.** Check the `Focus updated:` date in README. If more than 7 days old, ask the owner to update their priorities before doing anything else. (Skip if the vault is fresh — Step 3 covers it.)

5. **Briefing gate.** Check `wiki/briefings/` for the most recent briefing. If 7+ days have passed since the last one (or none exist), **route to `.claude/commands/brief.md` and run it** before doing other work. (Skip if the vault is fresh.)

6. **Structural glance.** While reading, note anything unexpected — folders that shouldn't exist, non-`.md` files at root, anything that looks wrong. Flag it.

7. Only read deeper files if the owner's question requires them — follow `[[wikilinks]]` to navigate, don't load everything.

Do not announce that you've read the files. Just use the context naturally.

**Do NOT read at session start:** `mistakes-made.md` is a write-only log. Durable lessons graduate into this CLAUDE.md as rules. The raw log is read during briefings and on demand.

---

## Intent → command routing

When the owner speaks, recognise the intent and run the matching slash command file. Phrases below are **examples**, not exact triggers — match the intent, not the literal words. The owner may use voice-to-text and produce messy sentences. Be charitable; ask one short clarifying question only if the intent is genuinely ambiguous.

| Intent | Sample phrasings | Run this file |
|---|---|---|
| **First-time setup** (vault is fresh — placeholders + only `_TEMPLATE.md` in `pillars/`) | "I just downloaded this", "what is this", "let's get started", "I'm new", first-time-detection at session start | `.claude/commands/setup.md` |
| **Bootstrap from an existing folder** (owner has their own notes/docs and wants the vault built from them) | "build my brain from this folder", "import my notes from [path]", "I have a folder about me", "populate the vault from my desktop" | `.claude/commands/onboard.md` |
| **Session start** | "Hi", "hi I'm back", "where am I", "where are we", "catch me up", "remind me what's active", "what was I doing" | `.claude/commands/hello.md` |
| **Session end** | "I'm done", "let's wrap up", "wrap up", "stop for tonight", "end session", "I have to go" | `.claude/commands/goodbye.md` |
| **Weekly briefing** | "Give me a briefing", "weekly review", "what's the big picture", "what does my whole vault say", "what am I missing", or briefing-gate fires automatically | `.claude/commands/brief.md` |
| **Source ingest** | A pasted URL, a wall of text, "I read this", "process this", "save this article", "look at this", "process raw/" | `.claude/commands/ingest.md` |
| **Health check** | "Is everything okay", "sanity check my vault", "is anything broken", "diagnose", "is my setup right" | `.claude/commands/check.md` |

If the owner explicitly types a slash command (`/hello`, `/goodbye`, etc.), just run that file. Do not require natural-language paraphrase.

For everything else (a thought, a question, a brain dump, a decision, a quick fact-check), use the general patterns under "How to handle what the owner gives you" below. You do not need a slash command for those.

---

## Folder map

| Folder | What goes here |
|---|---|
| `pillars/` | The trunks — one file per major area the owner wants to track. Start with one. |
| `raw/` | Original sources — articles, transcripts, posts. Never edited. |
| `wiki/` | Synthesised knowledge — turns raw sources into useful pages |
| `inbox/` | Quick capture — thoughts, ideas, anything not yet sorted |
| `decisions/` | Decisions with context, so future-them knows why |
| `docs/` | Setup guides and reference (for the owner, not for you) |
| `power-ups/` | Owner-facing guides to optional upgrades — brain-follows-you (global file), web-clipper, voice-briefings, ikigai. The vault works fully without any of them. |
| `.claude/commands/` | Canonical workflow specs (slash commands) |
| `.claude/skills/` | Optional capabilities the vault works fine without (e.g. voice memo) |

**Power-ups:** if the owner asks to "set up a power-up", "make my brain follow me everywhere", "add voice briefings", "set up the web clipper", or "do the ikigai thing", read the matching file in `power-ups/` (or `power-ups/README.md` for the menu) and walk them through it one step at a time.

**Onboarding from existing material:** `.claude/commands/onboard.md` now handles three shapes of starting material — (a) one folder/project, (b) little/no data → routes to the `/setup` interview, (c) notes scattered across the computer → a permissioned broad sweep of Desktop/Documents/Downloads. The git-detach (Step 0) and privacy pass (Step 2) are mandatory.

## File conventions

### Frontmatter

Every file starts with a block like this:

```yaml
---
title: Short descriptive name
type: pillar | wiki | decision | inbox | raw | briefing | index
status: active | dormant | archived
created: 2026-04-30
updated: 2026-04-30
tags: [relevant, tags]
---
```

### Naming
- Lowercase with dashes: `client-retention.md`, not `ClientRetention.md`
- Dates in ISO format: `2026-04-30`
- One concept per file — split if a file covers two topics

### Links between notes
- Use `[[double brackets]]`: `[[pillars/your-pillar]]`
- Every note should link to at least one other note
- A note without links is a bug — always connect it to something

## How to behave

### Always
- Read relevant vault files before answering questions
- Cite which vault file informed your answer
- Append to existing notes rather than replacing content
- Preserve the owner's exact words in "Owner's Take" sections
- Flag contradictions: old claim vs. new information
- Push back when the owner is making a mistake
- Show your work before writing — never change the vault without approval
- Be concise — bullets over paragraphs
- If you hit an install / setup / OS / tooling problem you're unsure about, read `docs/AGENT-FAQ.md` before guessing or asking the owner

### Never
- Overwrite the owner's words or paraphrase their voice
- Invent facts or data not in the vault
- Delete files without explicit permission
- Store passwords, API keys, tokens, or credentials — write "stored in [location]" instead
- Store sensitive personal information about people (clients, patients, students, family) without considering the privacy implications

## How to handle what the owner gives you (general patterns)

For the six routed intents above, run the matching slash command file. The patterns below cover everything else.

### When they share a thought or idea (quick capture)
1. Figure out where it belongs: append to an existing wiki page, add to the pillar file, or drop into `inbox/` if unsure.
2. Date-stamp it with their exact words: `- 2026-04-30 — "[their words]"`.
3. Show what you'd write and where. Get approval, then write it.
4. One clarifying question max. If it's clear, skip the question.
5. If it turns into 3+ paragraphs, switch to brain dump (below).

### When they want to talk things through (brain dump)
1. Ask one question at a time. Let them lead.
2. If it's their first time on a topic: "Tell me about it. What's going on, and what's on your mind?"
3. Let them talk. They're probably voice-transcribing — expect messy sentences. If they pause: "What else?" or "Keep going."
4. After they've dumped, reflect back what you heard. Ask: "Did I get that right?"
5. Pull on 2–4 threads with follow-up questions. One at a time.
6. Show what you'd capture and where. Get approval before writing.
7. Use their exact words in "Owner's Take" sections — never paraphrase.
8. Flag anything that contradicts an existing note.

### When they make a decision
1. Create a file in `decisions/` using `decisions/_TEMPLATE.md`.
2. Include: the decision, the context, alternatives considered, when to revisit.
3. Link from the relevant pillar or wiki page.
4. Append to `log.md`: `## [YYYY-MM-DD] decision | short-description`.

### When they ask a question
1. Read `wiki/index.md` to find relevant pages.
2. Read the relevant pages.
3. Synthesise an answer with citations: `[Source: wiki/page-name]`.
4. If the answer is reusable, offer to file it as a new wiki page.

### After every meaningful interaction — build the wiki automatically
The owner should never have to ask "can you update the wiki?" It happens as a side effect of normal conversation.
1. After capturing a thought, processing an article, or finishing a brain dump, ask: "Did anything come up that deserves its own wiki page?"
2. If yes — check whether a relevant page already exists. Update it, or propose a new one.
3. Show what you'd add. Get approval before writing.
4. A wiki page is worth creating when an idea is **reusable across sessions** — not every one-off thought. If in doubt, skip it.
5. Always update `wiki/index.md` when adding or updating wiki pages.
6. The goal: the wiki grows naturally. The owner talks; knowledge accumulates.

## Optional skills

`.claude/skills/` holds optional capabilities the vault works fine without. The owner enables them deliberately, usually by adding a key to `.env`.

Currently shipped:
- `generate-voice-memo` — turns the weekly briefing into an MP3 via the ElevenLabs API. Opt-in: requires `Eleven_Labs=` in `.env`. If the key is missing, the briefing skips the audio step silently. See `power-ups/voice-briefings.md`.

When the owner asks about voice briefings, audio versions, or "can I listen to this on a walk?", point them at `power-ups/voice-briefings.md` for the 3-minute setup. Don't push the skill — it's purely additive.

## Mistakes log protocol

`mistakes-made.md` is a **write-only log**. NOT read at session start.
- Durable lessons graduate into this CLAUDE.md as rules (this is how this file grows)
- The full log is read during briefings and when the owner asks
- The log still exists as a permanent record

When you make a mistake:
1. Append entry to `mistakes-made.md` (never overwrite).
2. Format: `## YYYY-MM-DD — Short title` / `**What happened:** ...` / `**What to do differently:** ...`.
3. Newest entries at the top.
4. **If the lesson is durable**, also add it as a rule in the relevant section above.

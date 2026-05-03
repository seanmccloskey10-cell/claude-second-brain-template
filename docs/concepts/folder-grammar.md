# Folder Grammar — Where Each Thing Lives

> **TL;DR:** Six folders, one rule each. `pillars/` for the trunks of what you're tracking. `raw/` for original sources you'll never edit. `wiki/` for synthesised knowledge. `inbox/` for quick capture you'll sort later. `decisions/` for choices you'll want to remember why you made. `docs/` for the user manual (reading material, not your data). Claude knows where each thing goes — you can just say it and Claude files it.

## The folders

### `pillars/` — the trunks

A pillar is a major area of your work or life that has its own context, ongoing decisions, and history. Most people start with one. Add more only when something genuinely doesn't fit the existing pillar.

Examples:
- A tutor's pillar might be "my teaching practice"
- A founder's pillar might be "the product"
- A researcher's pillar might be "my thesis"
- A writer's pillar might be "the novel-in-progress"
- A person tracking their reading habit might call it "what I'm reading"

**Rule:** the pillar file is the current state of what you're tracking, not a journal. Append updates with date stamps; don't rewrite the past.

### `raw/` — the immutable layer

Original sources. Articles, PDFs, podcast transcripts, screenshots, posts. **Never edited.** This is the audit trail. If a wiki page makes a claim, you should be able to trace it back to a source in `raw/`.

Each file gets a date in the filename and a frontmatter block. After Claude processes it, the frontmatter gets `processed: true` so the next `/brief` knows it's been turned into wiki.

**Rule:** read-only after capture. If you disagree with something a source says, capture your disagreement in the wiki — don't edit the source.

### `wiki/` — the synthesised layer

Your personal Wikipedia. Every page is a concept, idea, framework, or lesson — written in your own context, citing the raw sources it draws from. Claude builds this from `raw/` whenever you share an article ("I read this article" or `/ingest`).

The flow: `raw/` (sources) → `wiki/` (synthesis) → `wiki/index.md` (table of contents) → the weekly briefing reads everything → produces a single weekly summary with connections.

**Rule:** every wiki page cites at least one raw source. Every wiki page links to at least one other wiki page (a note without links is a bug).

### `inbox/` — the staging area

Fast capture. A thought you want to save now and sort later. A half-formed idea. Something Claude picked up from voice-to-text but isn't sure where it belongs.

**Rule:** the inbox should empty regularly. The weekly briefing includes "Unprocessed Items" — file inbox items into `pillars/`, `wiki/`, or `decisions/` (or delete them) once a week.

### `decisions/` — the memory of why

When you make a real decision (pricing, positioning, hiring, walking away from a project), Claude writes a decision file. Each one captures:

- What you decided
- Why (the context, the constraints, the alternatives you considered)
- When to revisit

**Rule:** decisions are append-only. If you change your mind later, write a new decision file that supersedes the old one — don't edit history.

### `docs/` — the manual

Setup guides, concept docs (like this one), the web-clipper instructions. **This is reading material for you, not data for Claude to synthesise.** Claude doesn't ingest `docs/` into the wiki.

**Rule:** if you find yourself wanting to add notes about your work inside `docs/`, you've put them in the wrong folder. They go in `pillars/`, `wiki/`, or `inbox/`.

## You don't have to file things yourself

When you tell Claude something, Claude figures out where it goes. *"I had a thought about my pricing"* → goes to the pillar (or wiki if it's a reusable principle). *"Save this article"* → goes to `raw/`. *"I just decided to drop a client"* → goes to `decisions/`. *"I'm not sure where this fits"* → goes to `inbox/`.

You can override Claude's filing decision anytime. The rule is: Claude shows you where it'd write before writing.

## Files you'll see at the root

- `README.md` — this is your vault home page. The "Your Vault Right Now" section gets customised during first-time setup.
- `CLAUDE.md` — instructions Claude reads automatically. You don't usually need to read or edit this.
- `log.md` — append-only activity log. The weekly briefing, ingests, and other rhythms write a one-line entry here when they fire.
- `mistakes-made.md` — when Claude gets something wrong, it logs the mistake here. Durable lessons get promoted into CLAUDE.md so Claude doesn't repeat them.

## Cross-references

- [Three layers of memory](three-layers-of-memory.md) — why this folder grammar matters
- [The four rhythms](the-four-rhythms.md) — which rhythm writes to which folder
- [Ikigai interview](ikigai-interview.md) — a future-mode reflective ritual that reads from across these folders

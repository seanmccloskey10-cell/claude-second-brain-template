---
title: What a Wiki Page Looks Like (Example)
type: wiki
status: active
created: 2026-04-30
updated: 2026-04-30
tags: [example, meta]
---

> 📘 **Example file.** This shows what a finished wiki page looks like. The `[[wikilinks]]` at the bottom point to files that don't exist yet — they're illustrative. Your real wiki pages will link to your real `raw/` and `pillars/` files. Feel free to delete this example once you've got the hang of it.

## What This Is

A wiki page captures one idea, framework, lesson, or concept — written in your own context, citing the raw sources it draws from.

The point of the wiki: when you ask Claude a question later, it pulls from these pages first. Wiki pages are the synthesised knowledge layer of your vault. Your `raw/` folder is the source material; your `wiki/` folder is what you (and Claude) actually think about it.

## How a wiki page is structured

A typical wiki page has these parts:

- **Frontmatter** at the top (the `---` block) — title, type, status, created/updated dates, tags
- **An optional TL;DR** quote block right at the top — a 1-3 sentence summary that makes the page scannable
- **Sections** — usually some combination of "What This Is", "Why It Matters", "How It Applies", "Open Questions", "Owner's Take", and "Sources"
- **Wikilinks** — internal links in `[[double brackets]]` pointing to other pages
- **Sources section** at the bottom — citations to the `raw/` files that inform this page

Not every page needs every section. Use what the idea calls for. **One concept per page** — split if a page tries to cover two.

## Why pages should link to other pages

A wiki page without links is a dead-end. Claude can't follow it, you can't navigate from it, and over time it gets orphaned. Every page should connect to at least one other page. Common targets:

- The relevant pillar (so the idea is anchored in the work it relates to)
- Sibling wiki pages (so connected ideas form a graph)
- The raw source(s) the page draws from (so claims are traceable)

## How a page evolves over time

Wiki pages are living documents. As you ingest more sources or have more conversations, Claude updates them — adding sections, flagging contradictions, citing new evidence. The page below is illustrative; a real wiki page after six months looks much richer.

## Owner's Take

> Owner's Take sections preserve your exact words, date-stamped. Never paraphrase, never overwrite — append. They're the part of the wiki that captures *your* thinking specifically, in your voice.

- 2026-04-30 — "This example page exists to show what's possible. The real value comes when this folder fills up with my actual thinking, not template copy."

## Open Questions

- What's the right granularity for a wiki page in my domain — concept-level, decision-level, project-level?
- When should I split a long page into two?
- How often is my wiki actually being read by Claude versus just sitting there?

## Sources

- _(this example page has no real source — your real wiki pages will cite the raw files they draw from, like `[[raw/2026-04-30-some-article]]`)_

## Related

- [[pillars/your-pillar]]
- [[wiki/index]]

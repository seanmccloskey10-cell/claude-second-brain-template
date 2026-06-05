# Power-Up: Web Clipper

> **TL;DR:** Install one Chrome extension, import three template files, and you can save any YouTube video, X post, or article into your vault with a single click — pre-formatted and ready for Claude to process. Setup takes 10 minutes. Add it once your daily rhythm is going and you want reading-time to feed your brain automatically.

## When to add it

Once the core loop feels natural and you find yourself reading things you wish your brain knew about. The Web Clipper is what closes the gap between *"I read something useful"* and *"my vault knows it."* No point adding it on day one — add it when capture-as-you-read sounds appealing.

## Why it matters

Without Web Clipper, the article pipeline is a manual job — copy text, make a file in `raw/`, paste, name it, add frontmatter. That's enough friction that you stop doing it.

With Web Clipper, capture becomes one click. You scroll X, find a smart take, click the extension icon. Done. The post is in `raw/` with the correct frontmatter, ready for Claude to process when you next sit down. **This is the difference between a vault that grows and one that doesn't.**

## What you'll build

| Template | Captures | Saves to |
|---|---|---|
| YouTube | Video transcripts (channel, date, duration) | `raw/podcasts/` |
| X / Twitter | Single posts with author and date | `raw/` |
| Article | Blog posts, news, newsletters | `raw/` |

All three save with the exact frontmatter your `/ingest` flow expects. Zero manual cleanup.

## Want Claude to walk you through it?

Just say *"help me set up the Web Clipper power-up"* and Claude will read [`docs/web-clipper/setup.md`](../docs/web-clipper/setup.md) and take you through it one step at a time. The full step-by-step (install Obsidian → install the extension → connect your vault → import the three templates → test) lives there. The short version is below.

## Setup (one-time, ~10 minutes)

1. **Install Obsidian itself** — [obsidian.md/download](https://obsidian.md/download) (free). Open it → **Open folder as vault** → pick your vault folder. The Web Clipper delivers files through Obsidian's URL handler, so Obsidian needs to be installed and running, even though you use the vault through VS Code + Claude day-to-day. *(Skip this and the clipper looks like it works in the browser but nothing lands in your vault.)*
2. **Install the extension** — [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf) from the Chrome Web Store (official, from the Obsidian team).
3. **Connect it to your vault** — Web Clipper icon → gear → **General → Vaults → Add vault** → enter your vault's folder name (matches what Obsidian shows top-left).
4. **Import the three templates** — they're in `docs/web-clipper/`. In Web Clipper Settings → **Templates** → **Import template** → select each of `youtube-template.json`, `x-post-template.json`, `article-template.json`.
5. **Test it** — open any article, click the clipper icon, **Save to Obsidian**. A new file should appear in `raw/`.

Full troubleshooting and per-source details are in [`docs/web-clipper/setup.md`](../docs/web-clipper/setup.md).

## The one tip people forget

**For YouTube, click "Show transcript" on the video first.** The clipper reads the transcript visible on the page — it doesn't call YouTube's API. No transcript panel open = no transcript captured. A YouTube video is a great first clip once you're set up.

## The full pipeline

```
SCROLL → CLICK CLIPPER → raw/ (with processed: false)
                              ↓
                     Sit down at computer
                              ↓
                     "process the new files in raw/"  (or /ingest)
                              ↓
                     wiki/ updated, raw marked processed
```

Web Clipper handles **capture only**. The captured files wait in `raw/` until you sit down and say *"process the new files in raw/"* (or type `/ingest`). Claude reads each one, runs a novelty check, updates your wiki where relevant, and marks the file processed. You stay in control of what enters your wiki.

## Cross-references

- [Power-ups menu](README.md) — the other upgrades
- [Full Web Clipper setup + troubleshooting](../docs/web-clipper/setup.md)
- [Folder grammar](../docs/concepts/folder-grammar.md) — where clipped sources land and why

# /ingest — Feed Your Second Brain

You are ingesting content into the owner's vault. They will give you one of:
- A pasted block of text (transcript, article, X post)
- A URL to fetch
- The phrase "process raw/" (or similar) — meaning ingest every file in `raw/` with `processed: false`

## Step 1: Identify what you've been given

Don't ask — figure it out.
- Wall of text with a YouTube title at the top → YouTube transcript
- URL to an article or blog → fetch with WebFetch
- URL to a YouTube video → ask the owner to paste the transcript (the "Show transcript" button on YouTube → copy)
- Short post with a single author → X post
- "Process raw/" → loop the steps below for every file in `raw/` (and `raw/podcasts/`) where frontmatter has `processed: false`

If the file was captured by the Web Clipper, it's already in `raw/` with the right frontmatter. Skip Step 3 (the file already exists) and go straight to Step 2 → Step 4.

Only ask the owner if you genuinely cannot tell.

Source types you'll see:
- `youtube` — video transcript
- `podcast` — audio transcript
- `article` — blog post, news article, newsletter
- `x-post` — single post from X / Twitter
- `other` — anything else

## Step 2: Novelty check (BEFORE saving or processing)

**This step prevents wasting the owner's time on stuff their vault already knows.**

Read the vault context FIRST:
1. Read `wiki/index.md`
2. Follow links to the 2-5 most relevant existing wiki pages
3. Read any relevant `pillars/` or `decisions/` files

Now compare the new content against what the vault already knows. Categorize every insight:

- **NEW** — the vault doesn't know this. Worth processing.
- **REINFORCED** — the vault already knows this, but the new source adds meaningful evidence or a different angle. Worth a short note.
- **REDUNDANT** — the vault already covers this fully. Skip.

**If everything is REDUNDANT:** Tell the owner immediately. "Your brain already knows all of this — covered in [file]. Skip?" Don't save, don't process. Saving their time IS the value.

**If mostly REDUNDANT with 1-2 NEW items:** Tell them. "Most of this is in your vault. The only new pieces are [X] and [Y]. Want me to save just those?"

**If substantially NEW:** Proceed.

## Step 3: Save to raw/ (skip if Web Clipper already saved it)

Only if the file isn't already in `raw/` from the Web Clipper.

Save to `raw/YYYY-MM-DD-short-descriptive-name.md`. For YouTube/podcast transcripts, save under `raw/podcasts/`.

Use this frontmatter:

```yaml
---
title: [Descriptive title]
type: raw
source_type: youtube | podcast | article | x-post | other
source_url: [URL if available, "pasted" if not]
source_author: [Author/creator name if known]
source_date: [Date of original publication if known, otherwise today]
ingested: [Today's date]
processed: false
trust: primary | practitioner | opinion
tags: [raw, topic1, topic2]
---
```

Trust levels:
- `primary` — official sources, documentation, research papers, company announcements
- `practitioner` — experienced builders sharing what worked (use this most often)
- `opinion` — takes, predictions, hot takes, unverified claims

Paste the full content below the frontmatter. **Do NOT summarize at this stage** — `raw/` is immutable source material.

## Step 4: Process into wiki

Extract insights — but ONLY the NEW and REINFORCED items from Step 2:
- What's the core idea?
- Why does it matter for the owner?
- What's actionable?
- Ignore filler, repetition, self-promotion, AND anything the vault already covers

Create or update wiki pages in `wiki/`:
- One concept per page
- Use `[[wikilinks]]` to connect to other vault pages
- Add source citation: `[Source: [[raw/YYYY-MM-DD-source-name]]]`
- Follow the vault's existing wiki style (look at other pages for the pattern)

**If there's nothing new enough to warrant a wiki page, don't create one.** Sometimes a one-line update to an existing page is the right move.

## Step 5: Connection scan

This is the most important step. Scan for connections — but only flag genuine ones:

**Reinforcements** — Does the new content support something already in the vault WITH new evidence?
> Add to the relevant page: `> REINFORCED BY: [new source] — [brief explanation]`

**Contradictions** — Does it disagree with something in the vault?
> Add to the relevant page: `> CONTRADICTION: [existing claim] vs [new claim] from [source]`

**Opportunities** — Does it create a cross-pillar opportunity worth acting on?
> Add to the relevant page: `> OPPORTUNITY: [description and which pillars it connects]`

Don't manufacture connections. If there isn't one, say so.

## Step 6: Update index and mark processed

- Update `wiki/index.md` if you added a new wiki page (skip for minor edits to existing pages)
- Change the raw file's frontmatter to `processed: true`
- Append to `log.md`: `## YYYY-MM-DD — ingest | source-name | [new wiki pages or "no wiki changes"]`

## Step 7: Report

Use this format. Keep it tight — the owner wants the takeaway, not a changelog.

**What it is:** [1-3 sentences explaining the content in plain English.]

**What your brain learned:**
- [Only NEW or meaningfully REINFORCED insights — bullet points]
- [If nothing new: "Your brain already knows this. Saved to raw/ for the record but no wiki changes needed."]

**Connections:**
- [Only genuine, non-obvious connections — bullet points]
- [Don't list connections to stuff the owner already knows about]

**Owner's Take?** [Only if there's a specific claim worth the owner weighing in on. Skip this section entirely if not needed.]

## Rules

- **Novelty check is mandatory.** Never skip Step 2. The whole point is to avoid noise.
- **Be honest about redundancy.** "Your brain already knows this" is a perfectly good outcome. It means the vault is working.
- **Never skip the connection scan.** Even redundant content can create a NEW connection.
- **Never summarize the raw file.** Raw is immutable. Summarization happens in wiki pages only.
- **Don't create wiki pages for the sake of it.** A one-line update to an existing page is often better than a new page.
- **One concept per wiki page** — when you do create one.
- **Use the vault's conventions.** Lowercase-with-dashes filenames, YAML frontmatter, wikilinks, no orphan pages.
- **Trust level matters.** A `practitioner` source saying "X works" is different from a `primary` source confirming X.
- **No credentials, PII, or sensitive client data in wiki pages.** Follow CLAUDE.md security rules.
- **Don't announce the process.** The owner shouldn't see "running Step 2 of /ingest." Just do the work and report the result.

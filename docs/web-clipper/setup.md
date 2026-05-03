# Web Clipper Setup — One-Click Capture Into Your Vault

> **TL;DR:** Install one Chrome extension, import three template files, and you can save any YouTube video, X post, or article into your vault with a single click. The files arrive pre-formatted and ready for your `/ingest` command. Setup takes 10 minutes.

## Why This Matters

Without Web Clipper, the article pipeline is a manual job — you copy text, create a file in `raw/`, paste, name it, add frontmatter. That's enough friction that you stop doing it.

With Web Clipper, capture becomes one click. You scroll X, find a smart take, click the extension icon. Done. The post is in `raw/` with the correct frontmatter, ready for Claude to process when you sit down at your computer.

**This is the difference between a vault that grows and one that doesn't.**

## What You'll Build

Three Web Clipper templates, each tuned for a different source type:

| Template | Captures | Saves to |
|---|---|---|
| YouTube | Video transcripts (with channel, date, duration) | `raw/podcasts/` |
| X / Twitter | Single posts with author and date | `raw/` |
| Article | Blog posts, news, newsletters | `raw/` |

All three save with the exact frontmatter your `/ingest` command expects. Zero manual cleanup.

## Setup (One-Time, ~10 Minutes)

### Step 0 — Install Obsidian itself (required)

The Web Clipper sends files into your vault folder via Obsidian's URL handler — so **Obsidian-the-app needs to be installed and pointed at your vault folder**, even though you can use the vault entirely through VS Code + Claude day-to-day.

1. Download Obsidian from [obsidian.md/download](https://obsidian.md/download) (free, Mac/Windows/Linux).
2. Open Obsidian → **Open folder as vault** → pick your vault folder (the one you cloned earlier).
3. That's it. You don't need to learn Obsidian or use it for anything else — it just runs in the background as a relay so the Web Clipper has a place to drop files.

If you skip this step, the Web Clipper will appear to work in the browser but nothing will land in your vault folder.

### Step 1 — Install the extension

Install [Obsidian Web Clipper](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf) from the Chrome Web Store. It's the official extension from the Obsidian team.

### Step 2 — Connect it to your vault

1. Click the Web Clipper icon in your browser toolbar
2. Click the gear icon (Settings)
3. Under **General → Vaults**, click **Add vault**
4. Enter the name of your Obsidian vault — this is the folder name (e.g. `my-brain`). It matches what Obsidian shows in its top-left corner.
5. Save

### Step 3 — Import the three templates

> 💡 **Tip — find the JSON files first.** Before you start importing, open `docs/web-clipper/` in your file explorer so you can grab the JSON files quickly when the import dialog asks for them.
>
> - In **VS Code**: right-click the `docs/web-clipper` folder in the left sidebar → **Reveal in File Explorer** (Windows) or **Reveal in Finder** (Mac).
> - **Or**: right-click the folder in VS Code → **Copy Path** → paste it into the import dialog's location bar when it opens.
>
> Keep that file explorer window open while you do the next steps.

The three template files are in `docs/web-clipper/`. For each one:

1. In Web Clipper Settings, click **Templates** in the left sidebar
2. Click the **⋯** menu (or **Import** button) → **Import template**
3. Browse to your `docs/web-clipper/` folder (the one you opened above) and select one of the three JSON files:
   - `youtube-template.json`
   - `x-post-template.json`
   - `article-template.json`
4. Repeat for the other two

When you're done, you should see three templates in your list:
- **Second Brain — YouTube**
- **Second Brain — X Post**
- **Second Brain — Article**

### Step 4 — Test it

Find any blog post or news article. Click the Web Clipper icon. The Article template should auto-select. Click **Save to Obsidian**.

Open your vault folder. You should see a new file in `raw/` with the article content and frontmatter at the top. If you do — you're done. If you don't, see Troubleshooting below.

## Daily Use

### Capturing a YouTube video

**Important:** Click "Show transcript" on the YouTube video first. The clipper reads the transcript that's visible on the page — it doesn't call YouTube's API.

Then click the Web Clipper icon. The YouTube template auto-selects. Click Save. The file lands in `raw/podcasts/` with the full transcript.

### Capturing an X post

Open any post (the URL must look like `x.com/username/status/123...`). Click the icon. The X template auto-selects. Save.

For threads: clip each post in the thread separately. There's no auto-thread feature.

### Capturing an article

For most blogs, news sites, and newsletters, the Article template auto-selects when you click the icon. If it doesn't (rare — happens on sites without standard schema markup), click the icon, then change the template dropdown manually to **Second Brain — Article**.

## Customizing the Trust Level

Every captured file gets a `trust:` field. The default is `practitioner`. Before clicking Save, you can change this in the popup:

- **`primary`** — official sources: docs, research papers, company announcements
- **`practitioner`** — experienced builders sharing what worked (use this most of the time)
- **`opinion`** — takes, predictions, hot takes, unverified claims

This matters later. When Claude processes your raw files, it weights primary sources heavier than opinions.

## Then What? — Processing the Captures

Web Clipper handles **capture only**. The captured files sit in `raw/` with `processed: false` in the frontmatter, waiting for you.

When you sit down at your computer and start Claude Code, just say:

> "Process the new files in raw/."

Or use the slash command:

```
/ingest
```

Claude reads each unprocessed file, runs a novelty check (is this actually new, or does the vault already know it?), updates wiki pages where relevant, and marks the raw file as processed.

That's the full pipeline:

```
SCROLL → CLICK CLIPPER → raw/ (with processed: false)
                              ↓
                     Sit down at computer
                              ↓
                     /ingest in Claude Code
                              ↓
                     wiki/ updated, raw marked processed
```

## Common Issues

### "The clipper saved the file but it went to the wrong folder"

Check Web Clipper Settings → Templates → tap the template → confirm the **Path** field. YouTube should be `raw/podcasts`, X and Article should be `raw`.

### "I clicked Save but nothing happened in my vault"

Two things to check:
1. Web Clipper Settings → General → confirm the vault name matches your Obsidian vault exactly
2. Open Obsidian — Web Clipper sometimes needs Obsidian running to deliver the file

### "The YouTube transcript is missing"

You forgot to click "Show transcript" on the YouTube video before clipping. The transcript panel has to be visible in your browser when you click the clipper icon.

### "The Article template didn't auto-trigger on a site I expected"

Some sites don't include standard schema markup. Click the clipper icon, then manually pick **Second Brain — Article** from the template dropdown.

### "I want to capture something that doesn't fit any of these templates"

That's fine — paste the content into Claude Code directly with `/ingest`. The slash command handles loose pastes too.

## Limitations (By Design)

- **No novelty check at capture time.** That happens when you process. You might capture redundant stuff — Claude tells you when it does, and you can skip it.
- **One clip per post for X threads.** Acceptable at normal volumes. If you find yourself clipping 10-tweet threads regularly, paste them into Claude Code instead.
- **No auto-processing.** The Web Clipper doesn't run Claude. You still sit down at your computer and run `/ingest`. This is intentional — you stay in control of what enters your wiki.

## What's Next

Once this is humming for a week or two, you'll start to feel the compounding. Articles you read on Tuesday inform decisions you make on Friday. The vault stops being a folder and starts being a thinking partner.

That's the goal.

---

**Files in this folder:**
- `youtube-template.json` — import for YouTube videos
- `x-post-template.json` — import for X / Twitter posts
- `article-template.json` — import for blog posts and articles

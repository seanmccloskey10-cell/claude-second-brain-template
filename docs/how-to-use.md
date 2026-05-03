# How to Use Your Second Brain

You talk to Claude. That's it. Claude reads your vault automatically and knows how to handle whatever you give it.

## Your Daily Loop

### 1. Start a session
Open your vault folder in VS Code. Start Claude Code. Claude reads your vault automatically and knows your context.

If you want, kick off the session by saying *"hi, I'm back"* (or typing `/hello`). Claude will give you a 6–8 line briefing on where you are.

If you set up the [global instruction file](global-instruction-file.md), this works from ANY folder — not just the vault.

### 2. Capture thoughts as they come
Throughout your day, when something strikes you — an idea, a frustration, a question — open Claude Code and just tell it:

"I had a thought about my pricing — I think I'm undercharging for one-on-one sessions."

Claude figures out where it goes, shows you what it would write, and saves it once you approve. Takes 30 seconds. Voice-transcribe if you can — it's faster and you'll say more.

### 3. Check in weekly
Once a week, Claude reads your entire vault and gives you a briefing: what's changed, what you've been thinking about, connections between ideas, and one thing to focus on this week.

**You don't have to remember to do this.** Claude keeps track. If it's been a week since your last briefing, Claude generates one automatically at the start of your next session. You can also trigger it yourself anytime — either say *"give me a briefing"* or type `/brief`.

This is where the magic happens. The more you've added during the week, the richer the briefing. After a few weeks, you'll start seeing patterns you didn't notice yourself.

---

## Feeding Your Brain: The Article Pipeline

Your vault gets smarter when you feed it. Here's how to turn your social media scrolling into actual knowledge:

### The fast path — Web Clipper (recommended)

Install the [Obsidian Web Clipper](web-clipper/setup.md) Chrome extension once and capture becomes one click:

1. Scroll X / a blog / YouTube. Find something good.
2. Click the Web Clipper icon. The right template auto-selects.
3. Click Save. The file lands in `raw/` with full frontmatter.
4. Later, in Claude Code: `/ingest` (or "process the new file in raw"). Claude reads it, novelty-checks it, and updates your wiki.

Setup takes 10 minutes once. After that, capture is friction-free. **See [docs/web-clipper/setup.md](web-clipper/setup.md).**

### The manual path — copy-paste

If you don't want the extension (or you're capturing something the clipper can't reach, like a PDF or a screenshot of a paywalled post):

1. Create a file in `raw/`:
   - Name it `YYYY-MM-DD-short-description.md` (e.g., `2026-04-14-client-retention-article.md`)
   - Paste the content
2. Tell Claude to process it. Something like: "I saved an article to raw/. Can you turn it into knowledge for my wiki?"
3. Claude reads it, pulls out what's relevant to YOU, and creates or updates wiki pages.
4. The raw file stays untouched. It's your receipt.

### What Claude does behind the scenes
When you share a thought, process an article, or have a conversation, Claude automatically checks whether anything discussed deserves a wiki page. If it does, Claude proposes one — you approve, and the knowledge is filed. You don't have to think about wiki pages at all. They build up as a side effect of talking to Claude.

### Why this matters
Most content consumption is passive — you read it, think "that was interesting," and forget it in a week. This pipeline turns reading into knowledge that compounds:

- Week 1: You save 2 articles. Claude creates 2 wiki pages.
- Month 1: You have 8-10 wiki pages. Claude's weekly briefing starts connecting them.
- Month 3: You ask "how should I price my new service?" and Claude pulls insights from articles you forgot you saved, combined with your own thinking from past conversations.

That's the compounding effect. Your past reading helps your future decisions.

### Pro tip
Be intentional about what you save. Not everything deserves a spot in your vault. Ask yourself: "Is this relevant to my work or my thinking?" If yes, save it. If it's just entertaining, keep scrolling.

---

## When You Need to Go Deep: The Brain Dump

When you have a lot on your mind — a new idea, a problem you're stuck on, a shift in how you're thinking about your work — just tell Claude:

"I want to talk through something. Can you interview me about my pricing strategy?"

Claude asks you questions, one at a time. You talk (voice-transcribe works best here). Claude listens, reflects back what it heard, pulls on interesting threads, and then shows you what it would capture before writing anything.

Think of it as a brain dump with structure. You talk, Claude organizes.

**When to use it:**
- First time setting up — tell Claude about what you want to track
- When your thinking has shifted and the vault feels outdated
- When you're stuck on a decision and want to think out loud
- When something big happened and you want to process it

---

## Making Decisions

When you make a decision worth remembering, just tell Claude:

"I decided to raise my rates from $40 to $50 starting next month."

Claude creates a file in `decisions/` with the context, your reasoning, and when you'd revisit it. Future-you will thank you — especially at 2am when you're second-guessing yourself.

---

## What Happens Over Time

**Week 1:** A few notes. Feels sparse. That's normal.

**Week 2-3:** The habit forms. You're capturing thoughts and saving articles. `/brief` starts having more to work with.

**Month 1:** 10-20 wiki pages. Claude's briefings get interesting — it starts connecting ideas you didn't connect yourself.

**Month 2-3:** The vault knows your work deeply. You ask questions and get answers informed by months of your own thinking plus every article you've saved.

**Month 6+:** The vault is genuinely an advisor. It knows your history, your patterns, your blind spots. It pushes back when you're about to repeat a mistake. It reminds you of insights from articles you've forgotten.

**This is what compounding looks like.** Every thought you capture, every article you save, every weekly briefing — it all stacks.

---

## What's Coming (future unlocks)

These aren't available today, but they're where this is headed:

- **More pillars.** You start with one. Eventually you add personal finance, health, a side project — and Claude starts making connections across all of them.
- **The Ikigai interview.** Once your vault has a few months of content, you can run a structured self-interview that uses your vault as evidence. See [docs/concepts/ikigai-interview.md](concepts/ikigai-interview.md).
- **Scheduled briefings.** In Claude Cowork, you can schedule weekly briefings to run every Monday morning. You wake up to a briefing without doing anything.
- **The producer layer.** Your vault doesn't just store knowledge — it produces things. Proposals, emails, strategies — all informed by your accumulated context.

For now, focus on the habit. Capture daily, review weekly. The rest comes naturally.

---

## Troubleshooting

**"Claude doesn't seem to know my context."**
Make sure you're opening the vault folder in VS Code before starting Claude Code. If you want context everywhere, set up the [global instruction file](global-instruction-file.md).

**"The briefing output is thin."**
That's normal early on. Keep capturing thoughts and saving articles. After a week or two of regular input, the briefings get much richer.

**"I saved an article but Claude didn't process it."**
You need to tell Claude to process it. Something like: "I put an article in raw/, can you turn it into wiki knowledge?" Claude will read it and extract what's relevant.

**"I'm not sure what to capture."**
If you thought it, it's worth capturing. Especially: frustrations, ideas, questions, things that surprised you, and things you keep repeating to different people.

**"This feels like a lot of work."**
It's 30 seconds to share a thought and 5 minutes for the weekly briefing on Friday. If that's all you do, the vault still compounds. Everything else is optional.

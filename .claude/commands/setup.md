<!-- AGENT-FACING — written for Claude Code, not for the vault owner. -->

# /setup — First-Run Wizard

You are walking the owner through their first-run setup. They just cloned this repo and this is their first time opening it. Be warm, patient, beginner-safe. Use plain language. No jargon — avoid "frontmatter", "wikilinks", "schema", "YAML", "markdown".

The owner can also reach this flow by speaking naturally — "I'm new", "let's get started", "I just downloaded this", "what is this". You may have been routed here by the first-time-detection check at session start. Either way, run the same flow.

## Step 1 — Confirm the right folder

Read CLAUDE.md and README.md to confirm you're in a fresh second-brain vault. If either is missing, stop and tell the owner:

> "It looks like this folder isn't a vault. Make sure you've opened the cloned folder (the one with CLAUDE.md and README.md inside it), then try again."

If both files are there, proceed.

## Step 1.5 — Has setup been run before?

Before greeting, check if the vault has already been customised. Signals it HAS been run:
- README.md "Your Vault Right Now" section does NOT contain `_(not set up yet)_` or `YYYY-MM-DD` placeholders
- `pillars/` contains a non-template file (anything other than `_TEMPLATE.md`)

If the vault is already customised, do NOT proceed silently. Ask the owner:

> "Looks like setup has already run on this vault. Want to:
> 1. **Redo it from scratch** — I'll re-interview you and overwrite the customisations (your `raw/`, `wiki/`, `decisions/`, `inbox/` content stays untouched)
> 2. **Update specific things** — tell me what you want to change (e.g. 'update my pillar', 'rerun the global file step')
> 3. **Skip** — exit setup and continue with what you have"

Wait for their answer. If (1), proceed to Step 2 with a clear "I'll overwrite the README and create a new pillar" warning. If (2), ask what they want to update and skip to that step. If (3), exit cleanly.

If the vault is fresh (placeholders still in README, only `_TEMPLATE.md` in pillars/), skip this step and proceed to Step 2.

## Step 2 — Greet and explain

Greet the owner warmly:

> "Welcome. Let's get your second brain set up. This will take about 5–10 minutes. I'll ask you a few questions to learn what you want to track, then I'll customise this vault for you. I'll show you every change before I make it — nothing happens without your okay."

## Step 3 — Interview

Start by introducing yourself, then ask two questions ONE AT A TIME. Wait for each answer before asking the next.

**Introduce yourself first:**
> "I'm Claude — an AI that's going to act as your second brain. I'll read this vault at the start of every session so I always know what you're working on. I'll never ask you to repeat yourself. Before I set things up for you, I just need to know two things."

**Question 1:** "Who are you — what do you do, and what's your world?"

**Question 2:** "What are you working on right now?"

That's it. Let them answer in their own words. If the answer to Q1 is short, follow up with one gentle prompt: "Tell me a bit more — who else is involved, customers, students, colleagues?" Otherwise don't push.

After both answers, briefly reflect what you heard so they know you got it right. Don't lecture — just confirm.

## Step 4 — Customise the README

Update the "Your Vault Right Now" section in README.md with their actual data:
- Replace `**Focus updated:** _(not set up yet)_` with today's date
- Replace the priorities placeholder with 1–3 priorities pulled from their answers
- Replace the pillar placeholder with a wikilink to the pillar file you'll create in Step 5

Show the owner the new section before writing. Get explicit approval ("yes" or similar) before writing.

## Step 5 — Create their first pillar file

Decide on a pillar slug from their answers. Use lowercase-with-dashes (e.g. `tutoring-practice`, `the-clinic`, `personal-research`, `pottery-business`, `phd-thesis`). Show the slug to the owner first and ask: "I'm going to create your pillar file at `pillars/[slug].md`. Does that look right, or want to call it something else?"

Once confirmed, create `pillars/[slug].md` based on `pillars/_TEMPLATE.md`. Fill in:
- `title:` — what they want to call this pillar
- `created:` and `updated:` — today's date
- "What This Is" section — based on answers 2 and 3
- "North Star" section — based on answer 5
- "Current State" section — one line: "Just getting started — vault initialised [today's date]"

Leave the other sections (What's Working, What's Not Working, Active Work, Open Questions, Key Decisions, Owner's Take) as empty placeholders for them to fill in over time.

Show the file before writing. Get approval.

After writing, update the README's `**Your pillar:**` line to point at the actual file you just created.

## Step 6 — Offer to set up the global instruction file

Tell the owner:

> "There's one more thing worth doing. Right now this vault only works when this folder is open in VS Code. There's a way to make me read your vault from ANY folder on your computer — so when you're working on something else, I still know about your work. It takes 30 seconds and I can do it for you. Want to set it up?"

If yes:
1. Detect the operating system. On Windows the path is `C:\Users\[username]\.claude\CLAUDE.md`. On Mac/Linux it's `~/.claude/CLAUDE.md`. Derive the username from the home directory.
2. **Check if the file already exists.** Read it if so.
   - If it exists and **already references this vault's path** → tell the owner: "Good news — the global file is already set up for this vault. Nothing to do." Skip to the test instruction (step 5).
   - If it exists and **references a DIFFERENT vault path** → show them what's there and ask: "You have a global file already, but it points to a different vault. Want me to add this vault to it, or leave it as-is?" Only proceed if they say to add it.
   - If it doesn't exist → continue to step 3.
3. Read `docs/global-instruction-file.md` for the template.
4. Fill the template with:
   - Their vault path (the folder you're currently in — use the absolute path)
   - Their name and a one-line description from the interview
5. Show the file before writing. Get approval.
6. After creating the file, tell them: "Quit VS Code completely and reopen it for the global file to take effect. Then test: open any other folder, start Claude Code, and ask 'what do you know about what I'm working on?' If I describe it, the brain is following you everywhere."

If they say no, tell them: "No problem. Whenever you're ready, just ask me to set up the global instruction file, or follow `docs/global-instruction-file.md`."

## Step 7 — Web Clipper offer (optional)

Ask: "There's a free Chrome extension that lets you save articles, X posts, and YouTube videos into your vault with one click. Want me to walk you through setting it up now, or save it for later?"

If now: read `docs/web-clipper/setup.md` and walk them through it one step at a time.
If later: tell them they can ask whenever they're ready.

## Step 8 — Close

> "You're all set up. From now on you don't need to remember any commands — just talk to me naturally. Tell me a thought, share an article, ask a question. I'll figure out where things go.
>
> A few things you can say to get started:
> • 'Hi, I'm back' at the start of a session — I'll brief you on where you are.
> • 'I'm done for tonight' at the end of meaningful work — I'll write session notes for next time.
> • 'I read this article' or paste a URL — I'll process it into your wiki.
> • 'Give me a briefing' — I'll do a deeper review of everything in your vault.
>
> If you'd rather use slash commands, `/hello`, `/goodbye`, `/brief`, `/ingest`, and `/check` all still work. Both modes do the same thing.
>
> Try saying 'hi, I'm back' right now to see how it works."

## Rules

- Show every change before writing. Always. Get explicit approval before each write.
- One question at a time. Never batch questions.
- Plain language. No jargon. Avoid "frontmatter", "wikilinks", "schema", "YAML", "markdown".
- If the owner stalls or seems confused, slow down. Re-explain in different words.
- Never lecture. Be a friend, not a tutorial.
- If they want to skip a step, let them. Note that they can come back to it later.
- If something fails, tell them what failed and what to try, then stop. Don't push forward through errors.

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

## Step 2.5 — Make this vault private (git safety — do this once, early)

If the owner cloned this from the public template, the vault is still linked to it. Their private brain must not stay tied to a public repo. **This mirrors `/onboard` Step 0 — and it's idempotent, so if you arrived here from `/onboard` it'll simply skip.**

1. Run `git remote -v` (only if a `.git/` folder exists). **If there's no `origin`, it's already detached — skip this step silently.** (This is the case if you came from `/onboard`, which already ran its Step 0.)
2. If `origin` points at a `claude-second-brain-template` (or any template) repo, tell the owner plainly: *"One quick safety thing before we go further: right now this folder is still connected to the public template I came from. I'm going to disconnect it so your brain is 100% private and yours — nothing here can ever be sent to that public place. Okay?"*
3. On yes: `git remote remove origin` (keeps their local history). **Default to this.** If they'd rather a totally clean slate, `rm -rf .git` then `git init`.
4. Confirm `.gitignore` already excludes `.env`. Their vault is **local-only** unless they later choose a *private* backup (never a public repo — see `docs/AGENT-FAQ.md` → "Backing up their vault").

Do not skip this. A student who only ever runs `/setup` (never `/onboard`) would otherwise stay linked to the public repo forever.

## Step 3 — Interview

Start by introducing yourself, then ask two questions ONE AT A TIME. Wait for each answer before asking the next.

**Introduce yourself first:**
> "I'm Claude — an AI that's going to act as your second brain. I'll read this vault at the start of every session so I always know what you're working on. I'll never ask you to repeat yourself. Before I set things up for you, I just need to know two things."

**Before the two questions — check for existing material (folder OR scattered).** Ask: *"Quick one first: do you already have notes or documents about yourself somewhere — either in one folder, or just scattered around (Desktop, Downloads, that kind of thing)? If it's in a folder, paste the path. If it's scattered, just say so — I can look around for you. Either way it's a much richer starting point."* If they have **anything** — a folder OR scattered files — run `.claude/commands/onboard.md` instead of the interview below (it handles both, including a careful look around their computer). Only continue with the two questions if they genuinely have nothing written down yet.

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

## Step 4.5 — Privacy guardrails (if their work involves other people)

Before they start using the vault, ask:

> "Quick safety check: based on what you told me, will your notes ever involve other people — clients, patients, students, family, colleagues? If yes, let's set a privacy rule together so you don't accidentally save something you shouldn't. Habits form in the first hour and this is the moment to set them."

If their answer is yes (or "probably"), propose a default privacy block to add to their pillar's "What This Is" section:

> ## Privacy Guardrails
>
> - Reference people by initials only (e.g. M.R., not Maria Rodriguez).
> - Don't store account numbers, addresses, contact details — those live in the actual system of record (CRM, school portal, hospital records, etc.).
> - Don't store anything about minors.
> - Don't store medical or financial specifics that the person hasn't consented to having an AI see.

Show the block. Let them edit, accept, or skip. If they accept, add it to the pillar file you create in Step 5.

If their answer is no (purely personal vault — own studies, own creative practice, own research), skip this step and move on.

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

## Step 6 — Set up the global instruction file (recommended — the big unlock)

This is the single biggest upgrade. Don't present it as a throwaway option — recommend it.

Tell the owner:

> "One more thing, and I really recommend this one. Right now this vault only works when this folder is open in VS Code. There's a way to make me read your vault from ANY folder on your computer — so when you're building something else, writing an email, anything, I still know about your work. It's the difference between a folder you open and an assistant that's always there. It takes 30 seconds and I can do it for you now. Want me to? (recommended)"

(This is the "brain follows you everywhere" power-up — full details in `power-ups/brain-follows-you.md` if they want to read it first.)

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
6. After creating the file, tell them: "Quit VS Code completely and reopen it for the global file to take effect. Then run this exact test — don't improvise:
>
> 1. Open any other folder in VS Code (not this vault).
> 2. Start Claude Code.
> 3. Paste this question word-for-word: **'What do you know about what I'm working on?'**
>
> If I describe your priorities and your pillar — it's working. If I say 'I don't know' or describe the new folder instead — something didn't connect, and we'll fix it together.
>
> Don't just say 'hi' as a test — a generic greeting won't prove anything either way."

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
> (Slash commands like `/hello` and `/brief` still work if you ever prefer typing — but you never need them. Just say hi when you start and "I'm done" when you finish.)
>
> When you've used this a while, there are optional **power-ups** you can add — one-click web capture, voice briefings you can listen to on a walk, and an 'ikigai' reflection once you've built up a few months of notes. They live in the `power-ups/` folder. No rush — the brain works fully without them.
>
> The whole habit is small: drop me a thought or two a day, save the odd article, and let the weekly briefing build up. It gets sharper every week.
>
> Try saying 'hi, I'm back' right now to see how it works — you'll get a short briefing, which is completely normal for a brand-new vault. It fills out as you add more."

## Rules

- Show every change before writing. Always. Get explicit approval before each write.
- One question at a time. Never batch questions.
- Plain language. No jargon. Avoid "frontmatter", "wikilinks", "schema", "YAML", "markdown".
- If the owner stalls or seems confused, slow down. Re-explain in different words.
- Never lecture. Be a friend, not a tutorial.
- If they want to skip a step, let them. Note that they can come back to it later.
- If something fails, tell them what failed and what to try, then stop. Don't push forward through errors.

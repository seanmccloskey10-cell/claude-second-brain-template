<!-- AGENT-FACING — written for Claude Code, not for the vault owner. -->

# /onboard — Build the Vault From the Owner's Own Folder

Run this when the owner already has a folder of their own material — notes, documents, exports, a "stuff about me" folder — and wants their second brain **bootstrapped from it**, instead of starting from a blank vault and a two-question interview.

This is the richer alternative to `/setup`. Use `/onboard` when there's existing material to import; use `/setup` when there isn't.

**Triggers (natural language):** "build my brain from this folder", "import my notes from [path]", "I have a folder about me", "populate the vault from my desktop", "here's a folder of my stuff" — or the owner's tutor handed them a prompt that routes here.

Be beginner-safe. Plain language with the owner — no jargon ("frontmatter", "wikilinks", "schema"). The owner's data is personal and local. Show every batch before writing. Never push through errors.

## Step 0 — Make this vault the owner's OWN (git safety — do this FIRST)

The owner almost certainly cloned this from a **public** template. Their personal brain must never stay tied to that public repo.

1. Run `git remote -v`. If `origin` points at a `claude-second-brain-template` (or any template) repo, the vault is still linked to it.
2. Tell the owner, plainly: *"Right now this folder is still linked to the public template I was copied from. I'm going to disconnect it so your second brain is 100% private and yours — nothing here can ever be sent to that public place. Okay?"*
3. On yes: `git remote remove origin` (keeps their local history). If they'd rather a totally clean slate, `rm -rf .git` then `git init`. **Default to `git remote remove origin`.**
4. Confirm `.gitignore` already excludes `.env`. Remind them their vault is **local-only** unless they later choose a *private* backup (see `docs/AGENT-FAQ.md` → "Backing up their vault"). Never a public repo.

## Step 1 — Find their material (three scenarios)

People arrive with their stuff in different shapes. Ask **one** question first to find out which:

> *"Quick question before I build anything. Is the stuff you want your brain built from: (a) sitting in one folder or project, (b) not really written down anywhere yet, or (c) scattered around your computer — some on the Desktop, some in Documents, a few downloads?"*

Then branch:

### (a) One folder or project — the main path
- Ask once: *"Great — paste the path, or drag the folder in."* If they already gave a path, use it.
- **List the folder first** — don't read everything blindly. Note file types, rough counts, anything huge or binary.
- Read the text-like files (.md, .txt, notes, exports, readable PDFs). For images, audio, video, big PDFs, or .docx you can't read cleanly — **ask** whether the content matters; don't force or silently skip.
- If the folder is large, summarise what you see and propose which parts to ingest first. Ingest in batches; don't try to swallow everything at once.
- This includes another VS Code project (e.g. a "my-business" or "about-me" folder full of notes) — treat it the same way: list, then read the text files.

### (b) Not much written down yet — switch to the interview
- They don't have material to import. Don't force `/onboard` — **run the `/setup` interview instead.** Read `.claude/commands/setup.md` and follow it from Step 2 (greet) onward: two questions, build their README + first pillar from their answers.
- Tell them plainly: *"No problem — you don't need a folder of notes to start. I'll ask you a couple of questions instead and we'll build from there. You can always import a folder later by saying 'build my brain from this folder'."*
- After the interview, come back and offer the global-file power-up (Step 5 below).

### (c) Scattered across the computer — broad search, with permission
- Their notes are spread across the Desktop, Documents, Downloads, etc. You'll do a **broad sweep** to find what's relevant — but only with their OK first.
- Ask: *"I can look across your usual spots — Desktop, Documents, Downloads — for notes and documents that look like they're about you or your work. Want me to do that? I'll show you a list of what I find before reading anything properly, and you tick what's actually relevant."*
- On yes, search those common locations (plus any folder they name) for **text-bearing files**: `.md`, `.txt`, `.docx`, readable `.pdf`, and obvious notes/exports. Skip system folders, app data, and anything binary/huge.
- **Present a categorised found-list** — group by location, one line each (name + where + rough size/type). Don't read full contents yet. Ask: *"Here's what I found. Tick the ones that are actually about you or your work — I'll ignore the rest."*
- Once they've picked, read **only** the chosen files (same care as path (a): summarise large ones, ask about binaries), then continue to the privacy pass below.

**Whichever branch you took (a or c), go straight to Step 2 — the privacy pass is mandatory before anything is written.** (Branch (b) builds from a live conversation, so apply the same privacy judgement as you go.)

## Step 2 — Privacy pass (MANDATORY — never skip)

Before ANYTHING is written into the vault, scan what you read for sensitive data:

- **Credentials / passwords / API keys / tokens** → never copy in. Note "stored in [their tool]" instead.
- **Other people's personal details** (full names, contact details, account numbers, addresses) → reference by initials; don't store contact/account details.
- **Anything about minors** → don't store.
- **Medical / financial specifics** they may not want an AI to retain → ask before storing.

Tell the owner plainly what you found and how you'll handle it. Offer to add a **Privacy Guardrails** block (the one in `setup.md` Step 4.5) to their main pillar. Get their steer before writing anything.

## Step 3 — Propose the structure (the map) BEFORE writing

From their material, infer the shape of their second brain and show it as a plan. This is the Karpathy "personal Wikipedia" pattern — the human curates, you turn raw material into linked pages.

- **Pillars** — the 1–4 big areas the material is about (their work, a project, a life area, a research practice). One file each.
- **Wiki pages** — the reusable knowledge / concepts / people / things worth their own page. One concept per page, linked together.
- **Decisions** — any clear past decisions worth recording with their context.
- **Inbox** — loose odds and ends with no home yet.
- **Raw** — the original source files, kept verbatim, as provenance for the wiki pages.

Show this as a short tree with one line each. Ask: *"Here's the shape I'd give your brain from this folder — does it look right? Anything to add, drop, or rename?"* Wait for approval.

## Step 4 — Build it (in small, shown batches)

Once the map is approved, build it, showing each batch before writing:

- Copy the originals into `raw/` (verbatim) with frontmatter (`type: raw`, `source_type: other`, `source: imported from [folder]`, `processed: false`) — these are the provenance.
- Create the pillar file(s) from `pillars/_TEMPLATE.md`, filled from their material (What This Is, North Star, Current State).
- Create wiki pages — **one concept per page**, in the owner's **own words** where they wrote them (preserve their voice; use "Owner's Take" for verbatim quotes — never paraphrase their voice into a summary). Link with `[[wikilinks]]`. Cite the source: `[Source: [[raw/...]]]`.
- Update `wiki/index.md`.
- Mark each raw file `processed: true` once its content is reflected in the wiki.
- Append to `log.md`.

Discipline: don't flatten their voice. One concept per page. Every page links to at least one other (a page with no links is a bug).

## Step 5 — Customise the README + offer the global file

- Update README's "Your Vault Right Now": today's date, 1–3 priorities, link to the main pillar (same as `setup.md` Step 4).
- **Strongly recommend** the "brain follows you everywhere" global instruction file (`setup.md` Step 6 / `power-ups/brain-follows-you.md`). It's the single biggest upgrade — it makes the vault work from *any* folder, not just this one. Frame it as recommended, not optional-afterthought: *"I really recommend one more thing — it makes me know your work from any folder on your computer, not just this one. Want me to set it up? (recommended)"* Still show the file before writing.

## Step 6 — Test, then point forward

- Suggest a test: *"Ask me something only your notes would know — 'what am I working on?', or 'what did I decide about X?' — so you can watch your brain answer from your own material."*
- Introduce the ongoing loop: talk to me naturally to capture thoughts; use the **Obsidian Web Clipper** to pull in new sources (`power-ups/web-clipper.md`). A YouTube video is a great first clip — remember to click **"Show transcript"** first.
- Point at the power-ups: *"When you've used this a while, there are optional power-ups you can add — voice briefings you can listen to on a walk, and an 'ikigai' reflection once you've built up a few months of notes. They're all in the `power-ups/` folder, no rush."* (See `power-ups/README.md`.)
- Close: *"From here on, just talk to me naturally. Say 'hi, I'm back' next time and I'll pick up where we left off."*

## If you get stuck

Read `docs/AGENT-FAQ.md` (required software, Mac vs Windows differences, common gotchas) **before** guessing or asking the owner. If still stuck after the FAQ, tell the owner exactly what's wrong in plain language and stop — don't guess or push through errors.

## Rules

- Step 0 (git detach) and Step 2 (privacy pass) are mandatory. Do them before any writing.
- Show every write before doing it. The owner's data is sensitive.
- Never copy credentials or secrets into the vault.
- Preserve the owner's exact words. Don't summarise away their voice.
- Plain language with the owner. No jargon.
- If a file is huge / binary / unreadable, ask — don't silently skip.

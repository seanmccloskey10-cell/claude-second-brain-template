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

## Step 1 — Find their material (discovery first)

**Most non-technical owners do NOT have everything in one tidy folder.** Their material is usually scattered — a doc on the Desktop, some PDFs in Downloads, notes in a couple of places. Treat **scattered as the normal case**, a single clean folder as the lucky exception, and an empty slate as the fallback. So lead with the offer to look around — it's the most common case and the most useful.

Open with all three on the table, sweep first:

> *"Before I build anything, let's find what you've already got — most people's notes are a bit scattered. I can take a quick look around your usual spots (Desktop, Documents, Downloads) and show you a list of what I find — you tick what's actually relevant and I only properly read those. Or, if it's all in one folder already, just point me to it. Or, if you haven't really written much about yourself down yet, that's fine too — I'll just ask you a few questions instead."*

Then follow whichever fits. (Resolve the real OS paths yourself — `~/Desktop` etc. on Mac, `C:\Users\<name>\Desktop` etc. on Windows; see `docs/AGENT-FAQ.md`.)

### (c) Scattered across the computer — the broad sweep (most common; do it carefully)

A **two-pass, consent-gated** sweep. **Never read file contents before the owner has seen the list and picked.**

1. **Consent + scope.** Confirm before looking: *"I'll look in your Desktop, Documents and Downloads (and anywhere else you name) for things that look like personal notes or documents about you or your work. I won't open anything yet — first I'll just show you what's there. Okay?"*
2. **Pass 1 — names only.** List **filename, location, type, rough size** for text-bearing files (`.md`, `.txt`, `.docx`, `.rtf`, readable `.pdf`, obvious notes/exports). **Do not read contents yet.** Skip system folders, app data, code repos, installers, and anything binary/huge. Bias toward "looks like notes / about-them"; when unsure, include it and let them decide.
3. **Found-list + tick.** Present it grouped by location, one line each. Say: *"Here's what I found. Tick the ones that are actually about you or your work — I'll ignore the rest. If something looks sensitive (bank, tax, medical, someone else's stuff) and you'd rather I never even read it, just leave it unticked."*
4. **Pass 2 — read only the ticked files.** Now open them, with the same care as a single folder (summarise large ones, ask about binaries you can't read). Then go to the privacy pass (Step 2).

Why names-first: in a sweep you're touching files the owner didn't hand you, so the privacy gate has to happen at **read** time, not just before writing. Showing names first lets them keep sensitive files out of your reading entirely.

### (a) One folder or project
- *"Great — paste the path, or drag the folder in."* If they already gave a path, use it.
- **List the folder first** — don't read everything blindly. Note file types, rough counts, anything huge or binary.
- Read the text-like files (.md, .txt, notes, exports, readable PDFs). For images, audio, video, big PDFs, or .docx you can't read cleanly — **ask** whether the content matters; don't force or silently skip.
- Large folder → summarise what you see, propose what to ingest first, ingest in batches.
- This includes another VS Code project (a "my-business" or "about-me" folder full of notes) — same treatment: list, then read the text files.
- **Then offer the sweep as a complement:** *"Want me to also glance at your Desktop and Downloads for anything else about you that wasn't in this folder?"* People often have a folder PLUS scattered extras. On yes, run the (c) sweep for the rest.

### (b) Not much written down yet — switch to the interview
- No material to import. Don't force `/onboard` — **run the `/setup` interview instead.** You've already done git detach in Step 0 above, so when `/setup` reaches its own git-safety step (2.5) it'll see no `origin` and skip cleanly. Read `.claude/commands/setup.md` and follow it from Step 2 (greet) onward: two questions, build their README + first pillar. (Setup's "do you have material?" check has effectively already been answered — confirm "we just checked, you don't have much yet" and move straight on; don't re-interrogate them.)
- Before accepting "nothing", offer one gentle sweep — people who *think* they have nothing often have a few relevant docs lying around: *"Want me to take a quick look around your Desktop and Downloads first, just in case? If there's nothing useful, we'll just do the questions."*
- If genuinely empty: *"No problem — you don't need a folder of notes to start. I'll ask you a couple of questions instead. You can always import or have me look around later."* After the interview, offer the global-file power-up (Step 5).

**For (a) and (c): go to Step 2 — the privacy pass is mandatory before anything is written.** (For swept files, the read is already gated by the names-first tick above; the privacy pass still runs on what you actually read.) **(b)** builds from a live conversation — apply the same privacy judgement as you go.

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
- Offer the Web Clipper now: *"Want me to set up the Web Clipper power-up so you can save articles and YouTube videos straight into your brain with one click? Takes about 10 minutes — or we can leave it for another day."* (If yes, follow `power-ups/web-clipper.md`.)
- Point at the rest of the power-ups: *"When you've used this a while, there are more — voice briefings you can listen to on a walk, and an 'ikigai' reflection once you've built up a few months of notes. They're all in the `power-ups/` folder, no rush."* (See `power-ups/README.md`.)
- The ongoing habit is small: *"From here it's easy — drop me a thought when you have one, paste me the odd article, and I'll keep your brain growing. The weekly briefing gets sharper every week."*
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

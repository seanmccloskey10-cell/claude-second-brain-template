<!-- AGENT-FACING. Read this when you hit an install / setup / OS / tooling problem during setup, /onboard, or Web Clipper setup — BEFORE guessing or asking the owner. The owner does not need to read this file. -->

# AGENT-FAQ — Troubleshooting & Context for the Agent

When something is unclear or breaks while you're helping set this up, **read the relevant section here before guessing or asking the owner.**

## What we're actually doing (mission context)

You're helping a usually non-technical person turn a folder of their own notes into a living **second brain** — an Obsidian vault that you (Claude) read at the start of every session so you have memory of their work and they never repeat themselves.

The pattern is Andrej **Karpathy's "LLM-friendly personal Wikipedia"**: the human curates and directs; you turn their raw material into linked wiki pages and keep them organised.

Typical flow: clone this template → **disconnect it from the public repo** (it becomes THEIR private vault) → ingest their personal folder (`/onboard`) → build pillars + wiki pages → they "Open folder as vault" in Obsidian to browse → ongoing capture via chat + the Web Clipper.

## Required software (and how to check)

| Tool | Why | Check | Notes |
|---|---|---|---|
| **Claude Code** | The whole system | `claude --version` | Must be authed via `claude login` (their plan) — **NOT** an API key. |
| **VS Code** | Where they run Claude Code | `code --version` | Expected, but they can use any terminal. |
| **Git** | Cloning the template | `git --version` | After cloning, **disconnect the remote** (see `/onboard` Step 0). |
| **Obsidian** | Browsing the vault + Web Clipper | (the app) | Free, from obsidian.md. They choose **"Open folder as vault"** → the cloned folder. **Required for the Web Clipper.** |
| **Python 3.11+** | ONLY the optional voice-memo skill | `python --version` (Win) / `python3 --version` (Mac) | Skip entirely unless they enable voice briefings. |

## The plan-vs-API-key trap (important)

Their Claude plan (Pro / Max) covers Claude Code via `claude login`. If you see an `ANTHROPIC_API_KEY` set, that's a **separate metered bill** on top of their plan — almost never what they want. Switch them to `claude login` and unset the key. Never set up an API key for this.

## Mac vs Windows — and "Mac mini" is just a Mac

- **Python command:** Mac → `python3`; Windows → `python` or `py`. A **Mac mini is a normal Mac** — treat it exactly like any other Mac (same commands, same dialogs). There is nothing special about it here.
- **Installers:** Windows → `winget install -e --id <id>`. Mac → official `.pkg` from the vendor, or Homebrew if already present.
- **Permission dialogs:** Windows → **UAC** ("allow this app to make changes?" → Yes) and **SmartScreen** ("More info" → "Run anyway" for signed installers from python.org / code.visualstudio.com). Mac → **Gatekeeper** (right-click the installer → Open) and the **password dialog with the lock icon**. **Never have the owner type a password into the terminal** — always the OS GUI dialog.
- **Paths:** Windows `C:\Users\<name>\...` (backslashes); Mac `~/...` or `/Users/<name>/...`.
- **Line endings (CRLF vs LF):** irrelevant for plain markdown notes — don't worry about it here.

## Common gotchas

- **Web Clipper does nothing / clipped files don't appear:** Obsidian must be (a) installed, (b) have this folder **open as a vault**, and (c) be **running** when they clip. The clipper delivers into the open Obsidian vault — if Obsidian isn't open, the clip never lands. This is the #1 confusion; check it first.
- **YouTube clip comes through empty:** they must click **"Show transcript"** on the video FIRST, then clip.
- **"command not found" right after installing something:** the terminal needs reopening to pick up the new PATH. Close it, reopen, retry.
- **`git push` fails / "permission denied":** expected if the vault is still linked to the public template — they can't write to it. This is exactly why `/onboard` Step 0 **disconnects the remote**; their brain should be private and unlinked.
- **Vault is large / slow to read:** don't read every file at once. List first, ingest in batches, ask which parts matter most.
- **Unreadable files (images, audio, large PDFs, .docx):** read what's plain text; for the rest, **ask** the owner whether the content matters before trying to force it.
- **Owner pasted a path with spaces or quotes:** wrap paths in quotes; on Windows prefer the literal `C:\Users\...` form.

## Power-ups (optional upgrades — `power-ups/` folder)

The vault works fully without any of these. If the owner asks to "set up a power-up", "make my brain follow me everywhere", "add voice briefings", "set up the web clipper", or "do the ikigai thing", read the matching file in `power-ups/` (menu in `power-ups/README.md`) and walk them through it one step at a time:

- `power-ups/brain-follows-you.md` — the global instruction file (`~/.claude/CLAUDE.md` / `C:\Users\<name>\.claude\CLAUDE.md`). **The biggest upgrade — recommend it early.** After creating it, the owner must fully quit and reopen VS Code.
- `power-ups/web-clipper.md` — one-click capture (needs Obsidian installed + running; YouTube needs "Show transcript" first).
- `power-ups/voice-briefings.md` — ElevenLabs MP3 of the weekly briefing (opt-in `.env` key; the only thing that needs Python).
- `power-ups/ikigai.md` — future-mode reflective interview; only meaningful once the vault has a few months of content.

## Backing up their vault (when they ask)

The vault is **local-only by default — that's good for privacy.** If they want a backup or cross-device sync, the safe options are: a **private** GitHub repo (never the public template), a synced folder (iCloud / OneDrive / Dropbox), or Obsidian Sync. **Never push their personal vault to a public repo.**

## Why /hello and /goodbye exist (context limits)

You can't hold a months-old vault in a single session's memory. `/goodbye` writes session notes; `/hello` reads them next time. That's how memory persists across sessions despite the context window. Only explain this to the owner if they ask why the rhythm exists.

## When you're still stuck

Work through the relevant section above first. If it turns out the template itself is genuinely broken (not the owner's setup), they can report it via the repo's GitHub issues. Either way: **tell the owner exactly what's wrong, in plain language, and stop — don't guess or push through errors.**

# Voice Briefings (Optional)

> **TL;DR:** Your weekly briefing can also produce an MP3 you can listen to on a walk, alongside the written version. It's powered by ElevenLabs and needs a free API key. Skip this if you'd rather just read the briefing — everything else works the same. Setup takes 3 minutes.

## What this is

When you generate a weekly briefing — whether by saying *"give me a briefing"*, typing `/brief`, or letting Claude fire it automatically after 7 days — the briefing writes a `## Voice memo script` section at the end. A tighter, conversational version meant to be read aloud. If you've enabled the optional voice memo skill, that section gets turned into an MP3 saved to `wiki/briefings/audio/`.

A weekly briefing is roughly 5–7 minutes of audio. Listen on a walk, in the car, doing dishes. The full text briefing still gets written either way.

## Why it's optional

The vault is designed to work without any API keys, on your existing Claude plan, with no extra bills. The voice memo is a bonus that opts you into a separate (free) third-party service.

If you'd rather not bother, skip this entire doc. Nothing else changes.

## Setup (3 minutes)

### 1. Get a free ElevenLabs key

1. Go to [elevenlabs.io](https://elevenlabs.io) and sign up. **No credit card needed for the free tier.**
2. After signing in: profile menu → **API Keys** → **Create API Key**.
3. Copy the key. You'll only see it once — paste it somewhere safe immediately.

### 2. Add the key to your vault's `.env`

```bash
# macOS / Linux:
cp .env.example .env

# Windows (Command Prompt):
copy .env.example .env

# Windows (PowerShell):
Copy-Item .env.example .env
```

Open `.env` in VS Code. Replace the placeholder line:

```
Eleven_Labs=your-elevenlabs-key-here
```

with your actual key:

```
Eleven_Labs=sk_yourActualKeyValue123
```

Save the file. **`.env` is gitignored** — your key never gets committed or pushed.

### 3. Test it

In Claude Code, ask for a briefing — either:

```
/brief
```

…or just say:

> *"Give me a briefing."*

After the briefing is written, Claude will run the voice-memo skill automatically. You should see output like:

```
[generate-voice-memo] briefing: 2026-04-26.md
[generate-voice-memo] chars:    4123 (free tier: 10,000/mo, 7-min cap: 5500)
[generate-voice-memo] output:   .../wiki/briefings/audio/2026-04-26.mp3
[generate-voice-memo] calling ElevenLabs...
[generate-voice-memo] OK: wrote 1247 KB
```

The MP3 lands in `wiki/briefings/audio/`. Open it in any audio player.

## What it costs

ElevenLabs free tier = **10,000 characters per month**.

A weekly briefing's voice memo script is ~3,000–5,500 characters, so the free tier covers **2–3 audio briefings per month**. If you want every week:

- **Starter** — $5/month, 30K chars (covers ~6–10 briefings)
- **Creator** — $22/month, 100K chars (covers a lot)

Skip the upgrade unless you actually find yourself listening every week.

## How to disable it later

Two options:

1. **Delete `.env`** (or empty the `Eleven_Labs=` line). The skill exits silently when the key is missing. Future briefings just write the text version.
2. **Keep the key but tell Claude** *"don't generate audio for the next briefing."* Claude will skip the skill that one time.

The text briefing always gets written. The audio is purely additive.

## Changing the voice

The default narrator is a British female with stable long-form delivery. If you want a different voice:

1. Browse [ElevenLabs voice library](https://elevenlabs.io/voices). Pick one.
2. Copy the voice ID from its URL (it's a string like `xQoJctkjLbN6MAa5Ibhk`).
3. Run with `--voice-id <id>`:

```bash
python .claude/skills/generate-voice-memo/generate.py wiki/briefings/2026-04-26.md --voice-id <new-id>
```

Or hardcode it as the default in `.claude/skills/generate-voice-memo/generate.py` (top of file: `DEFAULT_VOICE_ID`).

## Failure modes — what to do

- **"ERROR: .env not found"** — run `cp .env.example .env` (or the Windows equivalent) and add your key.
- **"ERROR: Eleven_Labs= is empty or still the placeholder"** — open `.env` and replace `your-elevenlabs-key-here` with your actual key.
- **"ERROR: Voice memo script section not found"** — the briefing is using an older version of the prompt. Re-pull the latest [`brief.md`](https://github.com/seanmccloskey10-cell/claude-second-brain-template/blob/main/.claude/commands/brief.md) into `.claude/commands/`.
- **HTTP 401 from ElevenLabs** — your key is invalid or has been revoked. Generate a fresh one.
- **HTTP 429** — you've hit the monthly free-tier limit. Wait until the next month resets, or upgrade.

## Cross-references

- [The four rhythms](the-four-rhythms.md) — the weekly briefing rhythm produces the voice memo script
- [Three layers of memory](three-layers-of-memory.md) — what the briefing is for
- The skill itself: [`.claude/skills/generate-voice-memo/SKILL.md`](../../.claude/skills/generate-voice-memo/SKILL.md)

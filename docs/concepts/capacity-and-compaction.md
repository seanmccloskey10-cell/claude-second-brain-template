# Capacity and Compaction — Why Claude Forgets Mid-Conversation

> **TL;DR:** Claude has a fixed-size "context window" — how much it can hold in active attention at once. When a conversation gets long, Claude (or the harness) compresses older turns to make room for new ones. That compression is lossy: details degrade, then disappear. The vault solves this by writing things to disk so Claude can re-read them fresh next session. `/hello` and `/goodbye` are the bookends that make this work.

## The capacity problem

Claude is reading and thinking inside a finite window. Every word you say, every file Claude reads, every reply Claude generates — all of it competes for the same fixed space.

Modern Claude models can hold roughly the equivalent of a 500-page book in active attention. That sounds like a lot. It is, until you spend two hours building a project together — then it isn't anymore.

When the window gets full, two things happen:

1. **The harness summarizes.** Claude Code automatically compresses older conversation turns into shorter summaries to make room for new ones.
2. **Details get lost.** The summary is good — but it isn't the original. Names, decisions, exact phrasings, which file you said to leave alone — all of these can degrade or disappear.

This is **compaction**. It happens silently. You don't get a warning. The first sign is usually Claude asking you something it should already know, or repeating advice it gave you 30 minutes ago.

## Why this matters for a second brain

If you tried to keep all your knowledge in one long Claude conversation, you'd lose it. Compaction would summarise away the details. Restart the session, and you've lost everything that wasn't compressed.

The vault solves this by **writing things to disk**. Files are not subject to compaction. They sit on your hard drive forever (or until you delete them). Claude reads them fresh at the start of each session — no compression, no degradation.

## How hello and goodbye make this work

The trick is using files as the durable memory layer and the conversation as the working memory layer.

- **The "hello" rhythm** runs at the start of a session — when you say *"hi, I'm back"* or type `/hello`. It reads the relevant files (README, CLAUDE.md, last session's notes, current state) and briefs you. The conversation now has fresh context, not yesterday's compressed summary.

- **The "goodbye" rhythm** runs at the end of a meaningful session — when you say *"I'm done"* or type `/goodbye`. It writes the session's important takeaways to `SESSION-NOTES.md`. The next *hello* will load those notes — even though the in-conversation memory will be gone.

Together, they bridge sessions. Files don't compress. Conversation does. Move what matters to files before the conversation ends.

## Practical implications

- **Long sessions degrade.** If a conversation stretches past a few hours of real work, expect Claude to start losing earlier details. When you feel that happening, say *"let's wrap up"* and start fresh with *"hi, I'm back"*.
- **Don't dump huge documents into the chat.** Save them to `raw/` and let the ingest rhythm process them into the wiki. The wiki page is small; the raw document is large. Claude reading the wiki page next session is much more efficient than re-reading the document.
- **Trust the file, not the chat.** If Claude in a long session contradicts something written in your wiki, the wiki is right. Tell Claude to re-read the file.
- **The weekly briefing does the heavy lifting once a week.** It pulls everything together so the next session can start with the synthesised briefing instead of re-discovering connections.

## Cross-references

- [Three layers of memory](three-layers-of-memory.md) — why disk beats chat memory
- [The four rhythms](the-four-rhythms.md) — what each rhythm actually writes
- [Folder grammar](folder-grammar.md) — where to put what so it survives sessions

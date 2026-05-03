# The Ikigai Interview (Future Concept)

> **TL;DR:** A structured self-interview rooted in the Japanese concept of *ikigai* (生き甲斐 — "reason for being"). It maps your work, skills, passions, and what the world pays you for onto a four-circle framework. **Best used once your vault has real content in it** — at least a few months of captured thoughts, decisions, and processed sources. The interview reads your vault as evidence, not as a blank-slate questionnaire.

## What this doc is

This is a description, not a working command. There's no `/ikigai` slash command. When you're ready, paste the prompt at the bottom of this page into Claude Code and it'll walk you through the interview using your vault as raw material.

Think of this as a **future-mode** for your vault: not the daily capture loop, not the weekly briefing, but a once-or-twice-a-year reflective exercise that asks the harder question — *what is your work actually pointing at?*

## Why ikigai

Ikigai is a Japanese idea, often translated as "reason for being" or "the thing that makes life worth living." It's been popularised in the West through a four-circle Venn diagram:

```
              [What you LOVE]
                    │
                    │
   [What the   ─────┼───── [What you're
   world NEEDS]     │       GOOD AT]
                    │
                    │
              [What you can
                BE PAID FOR]
```

The intersection of all four is your ikigai. The pairs have names of their own:

- Love + good at = **Passion**
- Love + world needs = **Mission**
- World needs + paid for = **Vocation**
- Good at + paid for = **Profession**

Most people have two or three circles overlapping. The interesting work is finding where the fourth fits.

> ⚠️ **Honest caveat:** the four-circle diagram is a Western popularisation, not the original Japanese concept. In Japan, *ikigai* is closer to "small daily things that give life meaning" than a career-strategy framework. Both readings have value. Treat the interview as a useful structuring tool, not a sacred map.

## Why "after you have vault data"

A blank-slate ikigai questionnaire forces you to *invent* answers in the moment. That's how you end up with aspirational fluff that doesn't match how you actually spend your time.

A vault-grounded ikigai interview is different. By the time you have:
- A few months of weekly briefings
- Several pillars (or one pillar with rich Owner's Take entries)
- Decisions you can look back on
- Articles you've ingested and the wiki pages they produced
- Recurring themes Claude has surfaced in briefings

…you have *evidence*. The interview reads your evidence and asks: *given how you actually spent your time, what does your ikigai look like? What are you avoiding? What surprises you?*

Rule of thumb: **wait until you have at least 4–6 weekly briefings in your vault** before running this. If your vault is fresh, run the regular setup wizard instead and come back here in a few months.

## What the interview does

When you're ready, the prompt at the bottom of this page does the following:

1. **Reads your vault.** Pillars, the most recent 8 weekly briefings, all decisions, the wiki index, and Owner's Take sections across the whole vault.
2. **Sketches a starting picture.** Based on what it sees, it makes a tentative read of where each of the four circles sits for you. This is *not* the answer — it's a draft you'll push back on.
3. **Walks you through one circle at a time, in this order:**
   - Good at — easiest to evidence from the vault
   - Paid for — also easy to evidence
   - Love — harder; needs reflection
   - World needs — hardest; you have to look up from your own work
4. **Asks one question at a time.** Reflective, vault-grounded. *"You've written about X four times in the last two months — does that count as something you love, or are you complaining about it?"*
5. **Builds the Venn diagram in writing.** Saves it to `decisions/YYYY-MM-DD-ikigai-snapshot.md` (yes, decisions/ — because it's a self-reflective decision about where you stand).
6. **Surfaces the gaps.** Where do you only have two circles? Three? What would it take to add the fourth? **This is the most useful output.**
7. **Suggests one experiment.** Not a five-year plan. One concrete thing to try in the next month that closes a gap.

## When to run it

- **Once you've used the vault for 3+ months.** Rough rule.
- **At natural inflection points** — finishing a project, considering a pivot, end of a year, after a hard decision.
- **NOT every week.** This isn't a weekly briefing. It's a once-or-twice-a-year exercise. Running it too often dilutes the depth.

## When NOT to run it

- Vault is fresh — there's no evidence to read yet. Run the regular setup wizard.
- You're in the middle of a hard decision and looking for the framework to validate what you'd already decided. The interview will see through that and push back; you may not want that right now.
- You only have one pillar and haven't been adding to it. Capture more first.

## The prompt to paste (when you're ready)

Copy everything between the lines into Claude Code, in your vault folder.

---

```
I want to do an ikigai interview, grounded in my vault. Please run the
following flow.

PRE-FLIGHT
1. Confirm you're in a vault folder. If CLAUDE.md and README.md don't both
   exist at the root, stop and tell me I'm in the wrong folder.
2. Read everything in this order:
   - README.md (current focus)
   - All files in pillars/
   - The 8 most recent files in wiki/briefings/ (or all of them if fewer)
   - All files in decisions/
   - wiki/index.md
   - Skim the wiki for any pages with an "Owner's Take" section and
     read those sections.
3. If the total content is thin (fewer than 4 weekly briefings, only
   _TEMPLATE.md in pillars/, no decisions), STOP and tell me:
   "Your vault doesn't have enough captured yet for this to be
   meaningful. Come back after you have a few months of regular use.
   In the meantime, I can run a normal session — what do you want to
   work on today?"

DRAFT THE FOUR CIRCLES
4. Based ONLY on what's in my vault (no general advice, no inventing),
   sketch a starting picture for each of the four circles:
   - WHAT I LOVE — what topics or activities recur with energy?
   - WHAT I'M GOOD AT — what does the evidence show I do well?
   - WHAT I CAN BE PAID FOR — what's actually generating money or
     could?
   - WHAT THE WORLD NEEDS — what real problems do my notes describe?
5. Show me your draft. Tell me which circles felt clear from the
   evidence and which ones you're guessing about.

INTERVIEW (one question at a time)
6. Walk me through each circle in this order: good-at, paid-for, love,
   world-needs. For each circle:
   - Ask one reflective, vault-grounded question. Cite the file you're
     drawing from. Example: "Your most recent briefing said X. Is that
     something you actually love, or are you complaining about it?"
   - Wait for my answer. Reflect what you heard.
   - Pull on one thread, ONE follow-up question max, then move on.
7. Don't lecture. Don't summarise the literature on ikigai. Use plain
   language.

BUILD THE WRITTEN DIAGRAM
8. Write a snapshot to decisions/YYYY-MM-DD-ikigai-snapshot.md with:
   - The four circles, populated with what we landed on
   - The four pairwise overlaps (passion, mission, vocation, profession)
   - The center: what you think my ikigai looks like right now, with
     citations from the vault
9. Show it to me before writing. Get explicit approval.

SURFACE THE GAPS
10. Where am I missing a circle? Where do only two or three overlap?
    Don't generate "you should do X" — name the gap honestly.
11. Suggest ONE small experiment to try in the next month that would
    close one gap. Concrete, low-cost, runnable in the next four weeks.

CLOSE
12. Tell me where you saved the snapshot and what to come back to in
    six months.

Throughout: never invent data. If the vault doesn't say it, you don't
know it. Push back if I tell you something that contradicts what's
written. The whole point is that the vault IS my evidence.

Begin with the pre-flight check.
```

---

## What the snapshot file looks like

After the interview, you'll have a new file in `decisions/`:

```markdown
---
title: Ikigai Snapshot — 2026-04-30
type: decision
status: snapshot
created: 2026-04-30
updated: 2026-04-30
tags: [ikigai, reflection, personal]
---

## What This Is

A snapshot of where my four ikigai circles stood on 2026-04-30, based
on what was in my vault at the time.

## What I Love
- ...

## What I'm Good At
- ...

## What I Can Be Paid For
- ...

## What the World Needs
- ...

## The Pairwise Overlaps

### Passion (love + good at)
...

### Mission (love + world needs)
...

### Vocation (world needs + paid for)
...

### Profession (good at + paid for)
...

## My Ikigai Right Now (best read of all four)
...

## Gaps I'm Honest About
...

## One Experiment for the Next Month
...

## Revisit When
- 6 months from now (~2026-10-30)
- After any major work change
- If a future briefing keeps surfacing the same gap

## Sources

- [[pillars/your-pillar]]
- [[wiki/briefings/...]]
- [[decisions/...]]
```

## Why this isn't built as a slash command

Three reasons:

1. **It only makes sense once you have data.** A working command would tempt people to run it on day one, get aspirational fluff, and lose trust in the vault.
2. **It's a reflective ritual, not a workflow.** Slash commands are for routine work. This is something you do once or twice a year with intention.
3. **The prompt should be visible.** Reading the prompt above tells you what the interview *is* before you run it. That's part of what makes it useful — you can adjust it for your situation before pasting.

When you're ready: paste the prompt above into Claude Code in your vault folder. The interview will take 30–60 minutes. Don't rush it.

## Cross-references

- [docs/concepts/three-layers-of-memory.md](three-layers-of-memory.md) — the vault layer this interview operates on
- [docs/concepts/folder-grammar.md](folder-grammar.md) — why the snapshot lives in `decisions/`

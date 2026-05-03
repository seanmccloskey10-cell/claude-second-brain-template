# Activity Log

Append-only chronological record of vault operations. Claude appends to this after ingesting sources, generating briefings, and logging decisions. This file is NOT read at session start — it's navigated on demand when you need to know what happened and when.

**Format:**
```
## [YYYY-MM-DD] operation | title
```

**Operations:**
- `ingest` — processed a raw source into wiki pages
- `briefing` — ran a weekly briefing with vault health check
- `decision` — logged a decision

---

*Your first entry appears after you process an article or run your first briefing.*

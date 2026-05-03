# HANDOFF-PROMPT.md — Have Your Agent Set This Up For You

If you'd rather not install things yourself, hand the whole setup off to your AI agent. Paste the prompt below into Claude Code on your machine. The agent will:

- Check what's already installed (Git, Python, VS Code, Claude Code)
- Install whatever's missing — using the OS's normal trust dialogs, never asking you to type your password into a black terminal window
- Clone this template (or copy it from a USB drive if you already have it)
- Walk you through the setup wizard (the same flow you'd get from saying *"hi, I'm new"* or typing `/setup`)
- Tell you when it's actually done — with concrete checks, not vague "it's working"

The prompt is **OS-aware**: there's a Mac version and a Windows version below. Pick the one that matches your machine.

**Two delivery scenarios:**
- **USB handoff** — someone gave you a USB drive with the vault already on it. Use the prompts in **Section 1** below.
- **Self-install from GitHub** — you're starting from scratch and want to clone it yourself. Use the prompts in **Section 2** below.

Customise the four placeholders before pasting:
- `<NAME>` — your name
- `<ROLE>` — one line about what you do (e.g. "founder of a speech therapy clinic", "tutor", "consultant in fintech", "PhD student in linguistics", "I'm exploring a new career")
- `<DOMAIN>` — what the vault is going to track (e.g. "my consulting practice", "my teaching", "the speech therapy clinic", "my thesis", "my reading habit")
- `<PREFERENCES>` — anything Claude should know up front (e.g. "I don't work weekends", "my clients are healthcare-only", "I'm based in the UK", "I prefer concise answers")

---

## Section 1 — USB handoff (vault already on a drive)

Someone has given you a USB drive with a `my-second-brain` folder on it. Use the prompt for your OS below. The agent will copy the folder to your computer, install anything missing, and walk you through setup.

### Mac — USB handoff

```
Hi — I'm <NAME>. I'm <ROLE>.

I'm on a Mac. I'm not technical. Someone has given me a USB drive with
a folder called "my-second-brain" on it. I need you to:

1. Copy that folder from the USB drive to ~/Projects/my-second-brain
   (create the Projects folder if it doesn't exist).
2. Make sure I have VS Code and Claude Code installed.
3. Open the vault and run the setup wizard.

I don't type commands and I don't know what "git" or "Python" mean.
You're going to handle all of that.

Please follow this flow:

1. Enter plan mode FIRST. Tell me:
   - Whether you can see the USB drive (list /Volumes/ to find it)
   - What the USB folder path is
   - What's already installed on my Mac (VS Code, Claude Code)
   - What you propose to do
   Don't start running commands until I say "go".

2. Pre-warn me about any Apple dialogs I'll see, in plain English.
   The common ones:
   - "The git command requires the command line developer tools — install?"
     → Click Install.
   - macOS asking for my password during an install
     → Use the Apple GUI dialog with the lock icon. NEVER type my password
     into Terminal.
   - "Allow this app to access files in your Documents folder?" → OK.

3. Copy the folder:
   cp -r /Volumes/<USB-NAME>/my-second-brain ~/Projects/my-second-brain

   (Detect the USB name from /Volumes/ — ask me if you can't find it.)

4. Install anything missing — IN ORDER, with my "go" between each:
   - Python 3.11+ (prefer the .pkg from python.org for the GUI password dialog)
   - VS Code (if missing — download from code.visualstudio.com)
   - Claude Code (if missing — install then run `claude login` so it uses
     my plan. I do NOT want an API key. I'm on a Claude plan.)

5. Open ~/Projects/my-second-brain in VS Code.

6. Read README.md and CLAUDE.md end-to-end. Then read the four short
   concept docs in docs/concepts/ so you understand the system.

7. Start setup: type `/setup` in Claude Code. Walk me through it one
   question at a time.

8. Stop when setup is finished. DO NOT volunteer to install the optional
   voice-memo skill — I'll ask separately if I want it.

What "done" looks like — tell me ONLY when you've verified ALL of these:
- The folder ~/Projects/my-second-brain/ exists and contains CLAUDE.md,
  README.md, .claude/commands/ (with at least setup.md, hello.md,
  goodbye.md, brief.md), pillars/, raw/, wiki/, inbox/, decisions/.
- VS Code opens the folder without errors.
- `claude` runs in the folder's terminal.
- Setup ran to completion (README "Your Vault Right Now" is filled in,
  NOT showing `_(not set up yet)_` placeholders).
- A pillar file with a real name exists in pillars/ (not just _TEMPLATE.md).

If any of those aren't right, don't say "it's working" — stop and tell me
exactly what's off.

A few things I'd like you to know up front:
<PREFERENCES>

If anything unexpected happens — network failure, a dialog you don't
understand, a USB drive you can't find — stop and ask me. Don't silently
skip anything.

Let's begin — please enter plan mode first.
```

---

### Windows — USB handoff

```
Hi — I'm <NAME>. I'm <ROLE>.

I'm on Windows. I'm not technical. Someone has given me a USB drive with
a folder called "my-second-brain" on it. I need you to:

1. Copy that folder from the USB drive to C:\Users\<me>\Projects\my-second-brain
   (create the Projects folder if it doesn't exist).
2. Make sure I have VS Code and Claude Code installed.
3. Open the vault and run the setup wizard.

I don't type commands and I don't know what "git" or "Python" mean.
You're going to handle all of that.

Please follow this flow:

1. Enter plan mode FIRST. Tell me:
   - Which drive letter the USB is on (run `wmic logicaldisk get caption,
     description,drivetype` to find it — type 2 is removable)
   - What's already installed (VS Code, Python, Claude Code)
   - What you propose to do
   Don't start running commands until I say "go".

2. Pre-warn me about Windows dialogs I'll see, in plain English:
   - UAC ("Do you want to allow this app to make changes?") — click Yes.
   - SmartScreen ("Windows protected your PC") — click "More info" then
     "Run anyway" for signed installers from python.org or code.visualstudio.com.
   I will NEVER need to type my password into a terminal. If a step asks
   for that, stop and tell me — that's wrong.

3. Copy the folder:
   xcopy /E /I /H /Y <USB-DRIVE>:\my-second-brain C:\Users\%USERNAME%\Projects\my-second-brain

   (Detect the USB drive letter from step 1 — ask me if you can't find it.)

4. Install anything missing — IN ORDER, with my "go" between each:
   - Python 3.11: `winget install -e --id Python.Python.3.11`
     (Make sure "Add Python to PATH" is ticked if using the .exe installer.)
   - VS Code: `winget install -e --id Microsoft.VisualStudioCode`
   - Claude Code (run `claude login` after install so it uses my plan.
     I do NOT want an API key. I'm on a Claude plan.)

5. Open C:\Users\<me>\Projects\my-second-brain in VS Code.

6. Read README.md and CLAUDE.md end-to-end. Then read the four short
   concept docs in docs/concepts/ so you understand the system.

7. Start setup: type `/setup` in Claude Code. Walk me through it one
   question at a time.

8. Stop when setup is finished. DO NOT volunteer to install the optional
   voice-memo skill — I'll ask separately if I want it.

What "done" looks like — tell me ONLY when you've verified ALL of these:
- The folder C:\Users\<me>\Projects\my-second-brain\ exists and contains
  CLAUDE.md, README.md, .claude\commands\ (with at least setup.md,
  hello.md, goodbye.md, brief.md), pillars\, raw\, wiki\, inbox\, decisions\.
- VS Code opens the folder without errors.
- `claude` runs in the folder's terminal.
- Setup ran to completion (README "Your Vault Right Now" is filled in,
  NOT showing `_(not set up yet)_` placeholders).
- A pillar file with a real name exists in pillars\ (not just _TEMPLATE.md).

If any of those aren't right, don't say "it's working" — stop and tell me
exactly what's off.

A few things I'd like you to know up front:
<PREFERENCES>

If anything unexpected happens — a dialog you don't understand, a drive
letter you can't find, an install error — stop and ask me. Don't silently
skip anything.

Let's begin — please enter plan mode first.
```

---

## Section 2 — Self-install from GitHub (no USB)

### Mac — GitHub clone

```
Hi — I'm <NAME>. I'm <ROLE>.

I'm on a Mac. I'm not technical. I don't type commands, I don't edit code,
and I don't know what "git" or "Python" or "Homebrew" mean. You're going
to handle all of that for me.

I want you to clone and set up a local "second brain" template for me:

    https://github.com/seanmccloskey10-cell/claude-second-brain-template

It's a Claude-Code-powered system that gives you (Claude) memory about
my work across sessions. I'll use it to track <DOMAIN>. It runs entirely
on my Mac — nothing is hosted, nothing leaves my machine except a
weekly call to ElevenLabs IF I decide to enable optional voice briefings
(I'll let you know separately).

Permissions — just a one-time ack from me per install. You'll need
some or all of these depending on what's already on my machine:
- Xcode command-line tools (triggers a one-time Apple install dialog,
  for git)
- Homebrew (one-time install via the GUI bootstrap)
- Python 3.11+ via the official .pkg installer from python.org (uses
  the standard Apple password dialog with the lock icon — never asks
  me to type my password into Terminal)
- VS Code (one-time install via Homebrew or download)
- Claude Code (via `npm install -g @anthropic-ai/claude-code` once
  Node is installed, OR the official installer)

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. Enter plan mode FIRST. Tell me what you found on my machine
   (what's installed, what's missing) and what you propose to do.
   Don't start running commands until I say "go".

2. Pre-warn me about Apple permission dialogs I'll see during setup,
   in plain English. Tell me what each one is and what to click. The
   common ones:
   - "The git command requires the command line developer tools — install?"
     → Click Install. Takes ~5 minutes.
   - "Python.pkg is from an unidentified developer — open?"
     → Right-click the .pkg → Open (if Gatekeeper blocks the double-click).
   - "Terminal would like to access files in your Documents folder"
     → OK / Allow.
   - macOS asking for my password during install
     → Use the Apple GUI password dialog (the one with the lock icon).
     NEVER type my password into Terminal.

3. Check what's installed. Run version commands. Report what you find.

4. Install anything missing — IN ORDER, with my "go" between each:
   - Xcode command-line tools (if git is missing)
   - Homebrew (if a CLI install needs it later)
   - Python 3.11+ (prefer the .pkg installer for the GUI password
     dialog — Homebrew is fine if Homebrew is already installed)
   - VS Code (if missing)
   - Claude Code (if missing — run `claude login` after install so it
     uses my plan, NOT an API key. I do NOT want to set up a separate
     API key. I'm on a Claude plan.)

5. Clone the repo into ~/Projects/my-second-brain (create the Projects
   folder if it doesn't exist).

6. Open the cloned folder in VS Code.

7. Read README.md and CLAUDE.md end-to-end. Then read the four short
   concept docs in docs/concepts/ so you understand the system you're
   helping me with.

8. Start setup in Claude Code by typing `/setup` (the canonical
   trigger). The wizard interviews me, customises the README,
   and creates my first pillar. Walk me through it one question
   at a time.

9. Stop when setup is finished. DO NOT volunteer to install the
   optional voice-memo skill — I'll ask separately if I want it.

What "done" looks like — tell me ONLY when you've verified ALL of these:
- The folder ~/Projects/my-second-brain/ exists and contains CLAUDE.md,
  README.md, .claude/commands/ (with at least setup.md, hello.md,
  goodbye.md, brief.md), pillars/, raw/, wiki/, inbox/, decisions/.
- VS Code opens the folder without errors.
- `claude` runs in the folder's terminal and shows the Claude Code prompt.
- Setup ran to completion (the README's "Your Vault Right Now" section
  is filled in, NOT showing `_(not set up yet)_` placeholders).
- A pillar file with a real name exists in pillars/ (not just _TEMPLATE.md).
- If I said yes to the global instruction file during setup, ~/.claude/CLAUDE.md
  exists and references my vault path.

If any of those aren't right, don't say "it's working" — stop and tell me
exactly what's off.

A few things I'd like you to know up front:
<PREFERENCES>

If you hit anything unexpected during setup — network failure, a
dependency install error, a permissions dialog you don't understand —
stop and ask me before continuing. Don't silently skip or work around
anything.

Report back at each major step. Keep me in the loop.

Let's begin — please enter plan mode and tell me what's on my machine.
```

---

### Windows — GitHub clone

```
Hi — I'm <NAME>. I'm <ROLE>.

I'm on Windows. I'm not technical. I don't type commands, I don't edit
code, and I don't know what "git" or "Python" or "winget" mean. You're
going to handle all of that for me.

I want you to clone and set up a local "second brain" template for me:

    https://github.com/seanmccloskey10-cell/claude-second-brain-template

It's a Claude-Code-powered system that gives you (Claude) memory about
my work across sessions. I'll use it to track <DOMAIN>. It runs entirely
on my PC — nothing is hosted, nothing leaves my machine except a
weekly call to ElevenLabs IF I decide to enable optional voice briefings
(I'll let you know separately).

Permissions — just a one-time ack from me per install. You'll need
some or all of these depending on what's already on my machine:
- Git for Windows (via winget — triggers a one-time UAC dialog)
- Python 3.11+ (via winget OR the official installer from python.org —
  if installer, MAKE SURE the "Add Python to PATH" checkbox is ticked
  on the first screen)
- VS Code (via winget or download)
- Claude Code (via npm or the official installer once Node is in place)

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. Enter plan mode FIRST. Tell me what you found on my machine
   (what's installed, what's missing) and what you propose to do.
   Don't start running commands until I say "go".

2. Pre-warn me about Windows dialogs I'll see during setup, in plain
   English. The common ones:
   - UAC ("Do you want to allow this app to make changes?") — click Yes.
     This is Windows asking for admin permission for an installer.
   - SmartScreen ("Windows protected your PC") — click "More info" then
     "Run anyway" if it's a signed installer from python.org or
     code.visualstudio.com.
   - "Allow Python through Windows Defender Firewall?" — click Allow.
   I will NEVER need to type my password into a terminal. If a step
   asks for that, stop and tell me — that's wrong.

3. Check what's installed. Run version commands. Report what you find.
   Note: on Windows you'll use `python` (or `py`) NOT `python3`.

4. Install anything missing — IN ORDER, with my "go" between each:
   - Git for Windows: `winget install -e --id Git.Git`
   - Python 3.11: `winget install -e --id Python.Python.3.11`
     (Or the official installer from python.org — make sure
     "Add Python to PATH" is ticked.)
   - VS Code: `winget install -e --id Microsoft.VisualStudioCode`
   - Claude Code (run `claude login` after install so it uses my
     plan, NOT an API key. I do NOT want to set up a separate API key.
     I'm on a Claude plan.)

5. Clone the repo into %USERPROFILE%\Projects\my-second-brain (create
   the Projects folder if it doesn't exist).

6. Open the cloned folder in VS Code.

7. Read README.md and CLAUDE.md end-to-end. Then read the four short
   concept docs in docs/concepts/ so you understand the system you're
   helping me with.

8. Start setup in Claude Code by typing `/setup` (the canonical
   trigger). The wizard interviews me, customises the README,
   and creates my first pillar. Walk me through it one question
   at a time.

9. Stop when setup is finished. DO NOT volunteer to install the
   optional voice-memo skill — I'll ask separately if I want it.

What "done" looks like — tell me ONLY when you've verified ALL of these:
- The folder C:\Users\<me>\Projects\my-second-brain\ exists and contains
  CLAUDE.md, README.md, .claude\commands\ (with at least setup.md,
  hello.md, goodbye.md, brief.md), pillars\, raw\, wiki\, inbox\,
  decisions\.
- VS Code opens the folder without errors.
- `claude` runs in the folder's terminal and shows the Claude Code prompt.
- Setup ran to completion (the README's "Your Vault Right Now" section
  is filled in, NOT showing `_(not set up yet)_` placeholders).
- A pillar file with a real name exists in pillars\ (not just _TEMPLATE.md).
- If I said yes to the global instruction file during setup,
  C:\Users\<me>\.claude\CLAUDE.md exists and references my vault path.

If any of those aren't right, don't say "it's working" — stop and tell me
exactly what's off.

A few things I'd like you to know up front:
<PREFERENCES>

If you hit anything unexpected during setup — network failure, a
dependency install error, a permissions dialog you don't understand —
stop and ask me before continuing. Don't silently skip or work around
anything.

Report back at each major step. Keep me in the loop.

Let's begin — please enter plan mode and tell me what's on my machine.
```

---

## The hard rules baked into both prompts

1. **Plan mode FIRST.** The agent reports what it found and what it proposes BEFORE running anything.
2. **Permissions ack'd up front, not surprise pop-ups mid-execution.**
3. **NO terminal password prompts.** All elevated auth goes through OS-native trust UX (Apple GUI password dialog with the lock icon on Mac; UAC dialog on Windows).
4. **NO silent auto-install.** Each install asks for "go" first.
5. **"What done looks like" with concrete checks.** The agent verifies specific files exist and `/setup` completed, before claiming success.
6. **Plan, not API key.** The student's Claude plan covers Claude Code. The agent never sets up a separate `ANTHROPIC_API_KEY` — that would be a second bill.
7. **Optional voice memo stays optional.** The agent doesn't surface the ElevenLabs setup unless the student asks for it.

## When this prompt fits

- The user is non-technical
- The user is on a different OS than the one you (the helper) tested on
- The user has Claude Code installed and authenticated via `claude login` (not an API key)

## When this prompt does NOT fit

- The user is technical and wants to follow [docs/install.md](docs/install.md) themselves
- The user doesn't have Claude Code installed yet — direct them to the [Claude Code install guide](https://docs.anthropic.com/en/docs/claude-code) first
- The user is using `ANTHROPIC_API_KEY` instead of `claude login` — flag this and switch them to a plan first (an API key is a metered second bill on top of their plan, almost always not what they want)

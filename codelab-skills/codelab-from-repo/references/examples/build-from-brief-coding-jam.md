---
id: vibecode-coding-jam-codelab
title: Build & Ship an AI App with Antigravity
summary: A beginner-friendly workshop that takes you from idea to working AI app in 75 minutes using Antigravity. No coding experience required — AI writes the code, you direct it.
authors: Qingyue (Annie) Wang
keywords: Antigravity,Gemini,VertexAi,VibeCoding,category:AiAndMachineLearning,docType:Codelab,language:Python,language:TypeScript,product:VertexAi,skill:Beginner
award_behavior: AWARD_BEHAVIOR_ENABLE
layout: paginated
duration: 75

---

# 🪐 Build & Ship an AI App with Antigravity

---

## Introduction
**Duration: 3 min**

### Welcome

Hi! Welcome to Coding Jam. In the next 75 minutes, you're going to build a real, working AI web app.

**You don't need to know how to code.** You don't need to know what "React" or "Python" means. We'll walk through every single step together.

### Here's the Big Idea

You won't write code. **AI will write the code.** Your job is to be the **boss** — you describe what you want, you review the plan, and you tell the AI what to change.

### The One Sentence to Remember

> **"Fix the doc, not the code."**

When something isn't right, don't ask AI to "fix the code." Update the **plan** first, then ask AI to rebuild from the new plan. The plan (we'll call it the "doc") is the source of truth.

You'll see this idea come up over and over. By the end, it'll feel natural.

### What You'll Build

An AI-powered web app based on **this week's project brief**. Runs in your browser. Uses Google's **Gemini AI**. Fully yours by the end of the session.

### The Journey

| # | Step | Time | Required? |
|---|------|------|-----------|
| 1 | Install Antigravity | 4 min | ✅ |
| — | Quick Tour: How Antigravity Works | 2 min | ✅ |
| 2 | Install Required Tools | 5 min | ✅ |
| 3A | Clone Your Project | 3 min | ✅ |
| 3B | Install Workshop Skills | 3 min | ✅ |
| 4 | The Spec Talk | 5 min | ✅ |
| 5 | Generate 3 Design Docs | 4 min | ✅ |
| 6 | Review & Iterate | 4 min | ✅ |
| 7 | Implement + Test | 10 min | ✅ |
| 8 | Google Cloud + API Key | 5 min | ✅ |
| 9 | Preview & Verify | 8 min | ✅ |
| — | 🎉 MVP Celebration | — | ✅ |
| 10 | 🎁 Pivot or Expand | 3 min | OPTIONAL |
| 11 | 🎁 Polish the UI | 2 min | OPTIONAL |
| 12 | Conclusion | 2 min | ✅ |

Let's go.

---

## Install Antigravity
**Duration: 4 min**

Antigravity is the AI assistant we'll use for everything. It's an app that goes on your computer.

### Step 1.1 — Download

👉 Go to [https://antigravity.google/download](https://antigravity.google/download) in your browser.

👉 Click the download button for your operating system (Mac, Windows, or Linux).

👉 Run the downloaded installer. **Default settings are fine** — click through them.

### Step 1.2 — Launch & Sign In

👉 Launch Antigravity from your Applications folder (Mac) or Start Menu (Windows).

👉 Click **"Sign In"** when prompted.

👉 Use your **Google account**.

> aside positive
> **Tip:** Use the same Google account you'll use for Google Cloud later (Section 8). Easier to keep them the same.

### Step 1.3 — Verify the Welcome Screen

You should see Antigravity's welcome screen with **three big buttons**:

- **Open Folder** — opens an existing folder as a workspace
- **Open Agent Manager** — goes to the agent dashboard (this is where most of our work will happen)
- **Clone Repository** — downloads a project from GitHub (we'll use this in Section 3A)

More docs at [https://antigravity.google/](https://antigravity.google/) if you ever want to dig deeper.

✅ **Checkpoint:** Antigravity is installed, you're signed in, you see the welcome screen with three buttons.

---

## Quick Tour: How Antigravity Works
**Duration: 2 min**

Before we start using Antigravity, let's get oriented. **Read this slowly** — it'll make every later section easier.

### The Mental Model: 3 Layers

When you ask Antigravity to do something, three things happen:

| Layer | What it is | Who does it |
|-------|------------|-------------|
| 1️⃣ | You type **plain English** in the chat | You |
| 2️⃣ | The **AI agent** figures out which commands to run | Antigravity |
| 3️⃣ | **You approve** each command via a pop-up | You (click Allow) |

**You never type commands like `curl` or `npm install` yourself.** You ask in English, the agent decides, you approve.

### The Agent Manager — Where You'll Spend Most of Your Time

Once you open Antigravity and pick a project, you land in the **Agent Manager view**. This is your "mission control" for chatting with the AI.

```
┌─────────────────────────────────────────────────────┐
│  Antigravity — Agent Manager                        │
├─────────────────────────────────────────────────────┤
│                                                     │
│   💬 Your Agents                                    │
│                                                     │
│   ┌───────────────────────────────────────────┐     │
│   │  Workspace: coding-jam-week-1             │     │
│   │  Status: Idle                             │     │
│   └───────────────────────────────────────────┘     │
│                                                     │
│   ┌───────────────────────────────────────────┐     │
│   │  Ask anything...                          │     │
│   │                                           │     │
│   │                                           │     │
│   └───────────────────────────────────────────┘     │
│                                                     │
│   [Model: Gemini 3 Flash ▼]            ⬆ Send       │
│                                                     │
└─────────────────────────────────────────────────────┘
```

The parts you'll interact with:

- **Chat input** — labeled **"Ask anything"**. This is where you paste prompts.
- **Model picker** — a dropdown at the bottom. Default is **Gemini 3 Flash** (fast). Switch to **Gemini 3.1 Pro** for harder tasks like generating design docs or writing code.
- **Send button** — the **⬆ arrow** (or just press Enter).
- **Workspace card** — shows which project the agent is working on.

Files that the agent creates will appear in a file list (usually a side panel or popup) — we'll point them out when relevant.

### What a Permission Pop-Up Looks Like

When the agent wants to run a shell command (install something, run a server, etc.), a small dialog appears:

```
┌──────────────────────────────────────────────┐
│  🔔 Allow this command?                      │
│                                              │
│  uv pip install google-genai                 │
│                                              │
│  [ Allow ]  [ Always allow ]  [ Deny ]       │
└──────────────────────────────────────────────┘
```

- **Allow** — runs this one command, asks again next time
- **Always allow** — runs this and any similar command in the future (use sparingly)
- **Deny** — agent stops and asks what to do instead

> aside positive
> **Default to Allow.** You'll click Allow many times today. That's normal. Don't change the security mode to "Turbo" (auto-allow everything) — it's a habit that bites later.

### Quick Reference Card

| What you want to do | How |
|---|---|
| Focus the chat | **Cmd+L** (Mac) / **Ctrl+L** (Win/Linux) |
| Send a prompt | Press **Enter**, or click the arrow ⬆ button |
| Switch model | Click the model picker at the bottom of the chat |
| Reference a file in your prompt | Type **@** then the filename (e.g., `@BRIEF.md`) |
| Close a workspace to return to welcome screen | **File menu → Close Workspace** |

✅ **Checkpoint:** You can describe the 3-layer flow (chat → agent → pop-up) and you know where the model picker is.

---

## Install Required Tools (via Antigravity)
**Duration: 5 min**

Antigravity needs two helper tools on your computer:

| Tool | What it is (plain English) |
|------|----------------------------|
| **uv** | Manages Python — the language behind your app's backend |
| **git** | Downloads project files from the internet (Antigravity uses this for cloning) |

You won't type install commands yourself. **You'll ask Antigravity in English; it does the rest.**

### Step 2.1 — Open a Temporary Workspace

Antigravity needs a folder open to have a chat. (No folder = no chat.)

👉 On the welcome screen, click **"Open Folder"**.

👉 Create or pick any empty folder. Suggested: a new folder called `coding-jam-setup` somewhere convenient (your Desktop is fine). We'll switch to the real workshop project in Section 3A.

👉 Click **Open** (or **Select Folder**).

The Agent Manager view opens with your new (empty) workspace selected.

### Step 2.2 — Ask Antigravity to Check & Install Tools

👉 Press **Cmd+L** (Mac) or **Ctrl+L** (Win/Linux) to focus the chat input.

👉 Confirm the model picker at the bottom shows **Gemini 3 Flash** (default — fine for this).

📝 **Simplest prompt — paste this into the chat:**

```
Install uv and git on my computer if they're not already there. 
Don't install Node.js. Ask permission before each install command.
```

📝 **More detailed version (if you want):**

```
Check whether uv and git are installed by running their --version commands.
For any tool that's missing, install it using the best method for my OS:
- Mac: prefer `brew install` (install Homebrew first if missing)
- Windows: prefer `winget install`
- Linux: prefer `apt install` or `dnf install`
Ask permission before each install command. 
Do NOT install Node.js — we'll install it later only if needed.
When done, give me a summary of what's installed.
```

👉 Press **Enter** to send.

### Step 2.3 — Watch the Agent Work, Click Allow on Pop-Ups

🤖 **What you'll see in the chat:**

The agent replies with something like:

```
I'll start by detecting your operating system, then check whether 
uv and git are already installed.

Running: uname -a
```

Then a permission pop-up appears.

🔔 **Pop-up #1 (likely):**

```
Allow this command? `uname -a`
[Allow] [Always allow] [Deny]
```

👉 Click **Allow**.

The agent now sees your OS. It continues:

```
Detected: macOS (or Windows / Linux)
Now checking if uv is installed...

Running: uv --version
```

🔔 **Pop-up #2 (likely):**

```
Allow this command? `uv --version`
[Allow] [Always allow] [Deny]
```

👉 Click **Allow**. If uv is already installed, the agent moves on. If not, it proposes installing:

🔔 **Pop-up #3 (if uv is missing):**

```
Allow this command? `brew install uv`     (Mac)
                  OR `winget install astral-sh.uv`     (Windows)
                  OR `curl -LsSf https://astral.sh/uv/install.sh | sh`    (Linux)

[Allow] [Always allow] [Deny]
```

👉 Click **Allow**. Wait 30-90 seconds for the install.

🔁 **Repeat for git.** The agent checks `git --version`, then installs if missing.

### Step 2.4 — Read the Summary

When the agent is done, you'll see something like:

```
✅ Setup complete:
- uv 0.4.18 ✅ (installed)
- git 2.42.0 ✅ (already had it)
- Node.js: skipped (will install later if needed)
```

### If Something Goes Wrong

> aside negative
> **"I can't install Homebrew" / "winget not found"** — the agent will say so.
> 
> Fallback: open these in your browser and run the installers manually with default settings. Then tell Antigravity: *"I installed [tool] manually, please verify with the version command."*
> 
> - **uv:** [docs.astral.sh/uv/getting-started/installation/](https://docs.astral.sh/uv/getting-started/installation/)
> - **git:** [git-scm.com/downloads](https://git-scm.com/downloads)

✅ **Checkpoint:** Agent confirms uv and git are both installed. Total time: ~3-5 min (or ~7 min if Homebrew has to install first on Mac).

---

## Clone Your Project
**Duration: 3 min**

This is the **first time you'll use Antigravity's "Clone Repository" button.** No chat needed for this part — it's pure UI.

### Step 3A.1 — Pick This Week's Project

Coding Jam is an **8-week program** with a different mini-project each week. **Your facilitator will tell you which week we're doing today.** Find that row and copy the URL.

| Week | Project | Repo URL |
|------|---------|----------|
| 1 | AI Hairstyle Try-On | `https://github.com/cuppibla/codingjam-glow-up` |
| 2 | AI Avatar Generator | `https://github.com/cuppibla/codingjam-avatar-studio` |
| 3 | My Special Year Calendar | `https://github.com/cuppibla/codingjam-year-in-poetry` |
| 4 | Fridge to Recipe | `https://github.com/cuppibla/codingjam-fridge-chef` |
| 5 | AI Mood Jar | `https://github.com/cuppibla/codingjam-moodjar` |
| 6 | One-Page Portfolio | `https://github.com/cuppibla/codingjam-my-corner` |
| 7 | Resume Tailor | `https://github.com/cuppibla/codingjam-bulletproof` |
| 8 | AI Character Chat | `https://github.com/cuppibla/codingjam-character-chat` |

> aside positive
> **Drop-in this week? No problem.** Pick today's row. The codelab works exactly the same for any week.

### Step 3A.2 — Return to the Welcome Screen

We need to get back to the launch screen to use the "Clone Repository" button.

👉 In Antigravity, click **File menu → Close Workspace**.

The welcome screen reappears with the three big buttons.

### Step 3A.3 — Click "Clone Repository"

👉 Click the **"Clone Repository"** button (the third option).

👉 A dialog appears with **one input field** labeled something like "Repository URL" or "Git URL".

👉 **Paste the URL** for today's week from the table above (e.g., `https://github.com/cuppibla/codingjam-glow-up`).

👉 Click **Continue** (or **Next**).

👉 A second dialog asks where to save the project locally. **Choose a folder** like `~/coding-jam-week-1/` (replace "1" with this week's number). Your home folder or Desktop is fine.

👉 Click **Clone** (or **Save**).

### Step 3A.4 — Wait for the Clone, Open the Workspace

Antigravity downloads the repo (~5-10 seconds) and asks if you want to open it as a workspace.

👉 Click **Open** (or **Yes**).

### Step 3A.5 — Tour the Project

Look at the file list. You should see:

| File / Folder | What It Is |
|---------------|------------|
| **BRIEF.md** | The product idea — what we're building, in plain English |
| **reference/** | A folder with a working example app. **AI will read this when writing your code**, so your app matches the patterns. |
| **.gitignore** | A list of files git should ignore (technical — ignore it) |

👉 **Click `BRIEF.md`** to open it.

👉 Read it. Take **1 full minute** to absorb the project idea.

✅ **Checkpoint:** You've cloned the project, opened it as a workspace, and read BRIEF.md.

---

## 3B. Install Workshop Skills
**Duration: 3 min**

A **"skill"** is a set of instructions stored on GitHub that you can hand to your AI. It's like giving your chef a specialized cookbook: *"here's the Italian cookbook, use this when I order pasta."*

We'll install **two skill packages** inside this workspace. They won't affect any other project on your computer.

### Step 3B.1 — Confirm Your File List (BEFORE state)

Before we install, your project shows:

```
codingjam-week-1/
├── .gitignore
├── BRIEF.md
└── reference/
    └── moodjar-example/
        ├── README.md
        ├── backend/
        └── frontend/
```

Take a quick look — we'll come back here AFTER to verify new folders appeared.

### Step 3B.2 — Ask Antigravity to Install the Skills

👉 Press **Cmd+L** (or **Ctrl+L**) to focus the chat.

📝 **Paste this prompt:**

```
Please install the workshop skills into this workspace's .agent/skills/ 
folder. Run these two git clones from the project root:

1. git clone https://github.com/cuppibla/skills-garden .agent/skills/skills-garden
2. git clone https://github.com/google-gemini/gemini-skills .agent/skills/gemini-skills

When Antigravity asks permission to run each command, I'll click Allow.

When done, list the skills that are now available in this workspace.
```

👉 Press **Enter**.

### Step 3B.3 — Click Allow on the Two Pop-Ups

🤖 **What you'll see:**

The agent says something like:

```
I'll create the .agent/skills/ folder and clone both repos into it.

Running: git clone https://github.com/cuppibla/skills-garden .agent/skills/skills-garden
```

🔔 **Pop-up #1:**

```
Allow this command? `git clone https://github.com/cuppibla/skills-garden ...`
[Allow] [Always allow for git clone] [Deny]
```

👉 Click **Allow** (or **Always allow for git clone** if you want to skip future git prompts).

Wait ~5 seconds for the clone.

🔔 **Pop-up #2 (the second git clone):**

```
Allow this command? `git clone https://github.com/google-gemini/gemini-skills ...`
[Allow] [Always allow for git clone] [Deny]
```

👉 Click **Allow** again. Wait ~5 seconds.

### Step 3B.4 — Verify Skills Installed (AFTER state)

🤖 **The agent should report:**

```
✅ Skills installed at .agent/skills/

Available skills:
- skills-garden/design-doc-skills/pm-design-doc
- skills-garden/design-doc-skills/ux-design-doc
- skills-garden/design-doc-skills/eng-design-doc
- skills-garden/eng-skills/test-driven-dev
- skills-garden/eng-skills/gemini-api
- skills-garden/ux-design-skills/cloud-pup
- skills-garden/ux-design-skills/y2k-dreamcore
- gemini-skills/skills/gemini-api-dev
- gemini-skills/skills/gemini-live-api-dev
- gemini-skills/skills/gemini-interactions-api
```

👉 **Check your file list.** You should now see a new `.agent/` folder. Click to expand it:

```
codingjam-week-1/
├── .agent/              ← NEW!
│   └── skills/
│       ├── skills-garden/
│       └── gemini-skills/
├── .gitignore
├── BRIEF.md
└── reference/
```

### What Each Skill Does (for reference, no action needed)

| Skill | What it does | When we use it |
|-------|--------------|----------------|
| `pm-design-doc` | Writes the Product Design doc | Section 5 |
| `ux-design-doc` | Writes the UX Design doc | Section 5 |
| `eng-design-doc` | Writes the Engineering Design doc (with Testing strategy section) | Section 5 |
| **`test-driven-dev`** ★ | Writes tests, runs them, auto-fixes failures (max 3 tries) | **Section 7 (built-in)** |
| `gemini-api-dev` | Official Google skill — how to use Gemini API correctly | Sections 7, 8 |
| `gemini-api` | A simpler backup if the official skill is unavailable | Fallback |
| `cloud-pup`, `y2k-dreamcore` | Visual style references | Optional polish |

> aside positive
> **About permission pop-ups:** Antigravity asks before running each shell command. This is a safety feature — *good*. For our 2 git clones, click Allow. Don't disable security ("Turbo mode") just for this workshop.

✅ **Checkpoint:** Your file list shows a new `.agent/skills/` folder with both `skills-garden/` and `gemini-skills/` inside.

---

## 4. The Spec Talk
**Duration: 5 min**

The **Spec Talk** is a 2-minute conversation where you tell AI what you want to build. **No code, no docs, nothing built yet.** We're just *talking it through*.

### The One Required Question

The most important thing AI needs to know:

> **"What goes IN, what comes OUT?"**

Examples:
- *"A photo IN. A cartoon version of it OUT."*
- *"A user's mood (text) IN. A short uplifting story OUT."*
- *"A list of fridge ingredients IN. A recipe OUT."*

Once AI knows this, it can build something. Everything else just makes it better.

### Two Paths — Pick One

**PATH A — Use the brief as-is** (recommended if you're new)

**PATH B — Refine the brief first** (if you want to add your own twist)

---

### Path A — Use the Brief As-Is

📝 **Simplest prompt:**

```
Read @BRIEF.md and treat it as our final product spec for this session.

DO NOT generate any plans, design documents, or code yet. Just confirm 
back to me:
- What is the input?
- What is the output?
- What is the magical moment?

Wait for my next instruction before doing anything else.
```

📝 **Slightly fancier version (asks AI to summarize):**

```
Read @BRIEF.md. In 3 short bullet points, summarize:
1. What the user inputs
2. What the user gets back
3. The one moment that should feel magical

DO NOT generate any plans, docs, or code yet. Just give me the 3 
bullets and wait for my next instruction.
```

🎯 **MODEL: Gemini 3 Flash (default)** — this is a simple summarization task.

🤖 **What you'll see:**

The agent reads `BRIEF.md` (you'll see it open briefly) and replies with a short summary. Example:

```
Got it. Here's our spec:

1. INPUT: A selfie + a hairstyle preset (1 of 4)
2. OUTPUT: A side-by-side comparison image (before + after)
3. MAGICAL MOMENT: "OMG that's me with bangs!"

Standing by for your next instruction — no docs or code yet.
```

✅ **No code, no docs, no plans yet. We're just confirming alignment.**

---

### Path B — Refine the Brief First

📝 **Paste this:**

```
Here's what's in @BRIEF.md. Before we lock the spec, ask me 3 short 
questions to refine it:
1. What's the one input I want the user to provide?
2. What's the magical moment for the user?
3. What are we deliberately NOT building (to keep scope tight)?

DO NOT generate any plans, docs, or code yet. Just ask me the questions 
and wait for my answers.
```

🎯 **MODEL: Gemini 3 Flash (default)** — simple Q&A.

🤖 **What the agent will ask** (example):

```
Got it. 3 quick questions:

1. The brief says "selfie + hairstyle preset." Should the user pick 
   from 4 presets, or type a custom prompt?

2. What feeling do you want when the user sees the result — 
   surprise, delight, comedy?

3. Should we skip social sharing, animation, and saving? Or include 
   one of those?
```

👉 **Answer in 1-2 sentences each.** If you don't know an answer, type "skip" and move on.

**Example answers:**

```
1. Stick with 4 presets — no typing.
2. Delight + a little comedy. Add a "vibe rating" line.
3. Skip all three. Just show the result.
```

🤖 **The agent then summarizes — and waits:**

```
Locked spec:
- INPUT: selfie + 1 of 4 hairstyle presets
- OUTPUT: side-by-side image + "vibe rating" caption
- NOT BUILDING: typed prompts, sharing, saving, animation

Standing by — no docs or code yet. Tell me when to start.
```

---

### Don't Generate Docs Yet

At the end of the Spec Talk, the agent should NOT have generated any files. If you see `product.md` or other new files appearing, you can tell the agent: *"Stop — delete any docs you just created. We're still in the Spec Talk phase."*

### Tips

> aside positive
> **Be specific on inputs and outputs.**
> Vague: *"It helps people work out."*
> Specific: *"User uploads a 10-second video of themselves doing a yoga pose. They get back a 1-paragraph review of their form."*

> aside negative
> **Don't try to design the UI yet.** The Spec Talk is about *what*, not *how it looks*. The UI doc comes later in Section 5.

✅ **Checkpoint:** You've had a short conversation with Antigravity about your product idea, and it understands the inputs and outputs. **No files have been generated yet.**

---

## 5. Generate 3 Design Docs
**Duration: 4 min**

Now AI writes **three plans, on paper**, before any code happens. We do all three in **one prompt** using the three design-doc skills in sequence.

### The 3 Docs

| File | What's In It | Skill Used |
|------|--------------|------------|
| **product.md** | Who the user is, what we're solving, what features | `pm-design-doc` |
| **ui.md** | What screens look like, colors, fonts, layout | `ux-design-doc` |
| **engineering.md** | Tech stack, file structure, **+ Testing strategy section** | `eng-design-doc` |

### Step 5.1 — Switch to Gemini 3.1 Pro (Recommended)

Design doc generation benefits from a smarter model.

👉 In the chat, find the **model picker dropdown at the bottom**.

👉 Click it, select **Gemini 3.1 Pro** (exact label depends on your version).

> aside positive
> **Why switch?** Pro is slower (~30s vs 10s per doc) but writes better-structured docs. For one-shot deep tasks like design docs, Pro is worth the wait. You can switch back to Flash later.

### Step 5.2 — Generate All Three Docs at Once

📝 **Paste this — one prompt does all three:**

```
Apply all three design-doc skills in this order:

1. pm-design-doc from .agent/skills/skills-garden/design-doc-skills/pm-design-doc/
   → Generates product.md

2. ux-design-doc from .agent/skills/skills-garden/design-doc-skills/ux-design-doc/
   → Generates ui.md (based on the product.md you just created)

3. eng-design-doc from .agent/skills/skills-garden/design-doc-skills/eng-design-doc/
   → Generates engineering.md (based on product.md, ui.md, and @BRIEF.md)
   → MUST include a "Testing strategy" section with real content
     (specific functions to unit-test, one integration test per major flow,
     and what's deliberately NOT being tested)

Use the patterns in @reference/ as guidance for the engineering doc 
(but vary if the brief justifies it).

Save all three files in the project root. After each one is saved, 
briefly confirm what you saved before moving to the next.

When all three are done, give me a final summary listing the section 
titles in each file.
```

👉 Press **Enter**.

### Step 5.3 — Watch the Agent Work (~90 sec)

🤖 **What you'll see:**

The agent works through all three sequentially, posting updates like:

```
Step 1/3: Applying pm-design-doc skill...
✓ product.md saved (sections: Vision, Target User, User Journey, Features)

Step 2/3: Applying ux-design-doc skill...
✓ ui.md saved (sections: Screens, Components, Color palette, Tone)

Step 3/3: Applying eng-design-doc skill...
✓ engineering.md saved (sections: Summary, Architecture, Data model, 
  API surface, Testing strategy, Rollout)

All three design docs complete. Section summary:
- product.md: 5 sections (~120 lines)
- ui.md: 4 sections (~80 lines)
- engineering.md: 14 sections (~250 lines) — includes Testing strategy ✓
```

Total time: ~90 seconds (sometimes up to 2 min for Pro).

### Step 5.4 — Verify the Files Saved

👉 Check your file list. You should now see (in addition to what was there before):

```
codingjam-week-1/
├── product.md          ← NEW
├── ui.md               ← NEW
├── engineering.md      ← NEW
├── BRIEF.md
├── reference/
└── .agent/
```

If any are missing, paste:

```
I don't see all three files. Please make sure product.md, ui.md, 
and engineering.md are saved as separate files in the project root.
```

### Step 5.5 — Verify the Testing Strategy Section

👉 Click `engineering.md` to open it.

👉 Scroll down. Look for a section heading **"## 10. Testing strategy"** (or similar).

It should have actual content:
- A list of "Unit tests" with specific function names
- An "Integration tests" entry
- A "Deliberately not tested" list

If it's missing or thin, paste:

```
The "Testing strategy" section in @engineering.md is missing or too thin.
Re-apply the eng-design-doc skill. The Testing strategy must list:
- Specific functions that need unit tests
- One integration test per major user flow
- What's deliberately not being tested (and why)
```

> aside positive
> **Why this matters:** These three docs are **portable**. Chat history disappears. Saved docs don't. If you continue this project next week in any AI tool, the docs travel with you.

✅ **Checkpoint:** Three files saved. `engineering.md` has a real Testing strategy section.

---

## 6. Review & Iterate
**Duration: 4 min**

You're the boss. AI wrote the plan. Now you read it and request changes.

### The Most Important Habit

When you want a change, **change the DOC — not the code.** The doc is the source of truth.

### Step 6.1 — Read All Three Docs

👉 Open each one (click in the file list), top to bottom:

1. **`product.md`** — Does this describe what I want?
2. **`ui.md`** — Are the screens and look right?
3. **`engineering.md`** — Does the Testing strategy make sense? (You don't need to understand the tech — just check there IS a plan.)

### Step 6.2 — Comment Directly on the Docs (Like Google Docs)

Antigravity lets you leave **inline comments** on any file — just like Google Docs. The agent reads your comments and applies the changes.

👉 Open `product.md`.

👉 **Highlight the line or paragraph** you want to change.

👉 A toolbar appears with options. Click the **💬 comment icon** (or right-click → **Add Comment**).

👉 **Type your change request.** Examples:

```
"Change the target user from 'adults 25-40' to 'teens 13-18'"
```

```
"Make the share button optional, not a required feature"
```

```
"Add an 'undo' button to the user journey"
```

👉 Repeat for `ui.md` and `engineering.md` — leave as many comments as you want.

👉 When done, paste this in the chat:

```
Read all my inline comments across @product.md, @ui.md, and 
@engineering.md. Apply the changes I asked for. Show me a summary 
of what changed in each doc.
```

🤖 **Expected:** Agent reads comments, updates the docs, summarizes:

```
Changes applied:

product.md:
- Target user changed from "adults 25-40" to "teens 13-18"
- Share button moved to "nice-to-have"

ui.md:
- Updated copy tone to feel more Gen-Z

engineering.md:
- No changes needed — auth/storage assumptions unchanged
```

> aside positive
> **Why inline comments beat chat prompts:** You see exactly which line you're talking about. No "remember to mention which paragraph I meant" confusion.

> aside negative
> **Don't see the comment feature?** Some Antigravity versions don't have it yet. Fallback prompt:
> ```
> Update product.md: change target user from adults 25-40 to teens 13-18. 
> Then update ui.md and engineering.md to match where relevant — including 
> the Testing strategy if needed.
> ```

### Step 6.3 — Iterate Until It's Right

You can review again, leave more comments, ask for more changes. **No code has been written yet** — iterating is cheap.

### Step 6.4 — Approve the Plan

When the three docs feel right — when you'd be proud to show them to a friend — say:

```
The plan looks good. Let's move forward to implementation.
```

### Why We Do This

> aside positive
> **Imagine building a house.** You wouldn't pour the concrete and then decide where the kitchen goes. You'd update the blueprint first, get it right, *then* pour concrete. The docs are the blueprint.

> aside negative
> **Don't ask AI to "just write the code, we'll fix things later."** "Later" means fixing concrete with a chisel. Updating a doc takes 30 seconds; fixing a half-built app takes 30 minutes.

✅ **Checkpoint:** You've reviewed all three docs and approved them.

---

## 7. Implement + Test
**Duration: 10 min**

The biggest section of the codelab. AI takes the three docs and builds the app — **code AND tests together, in one go.** When this section ends, you'll have a working codebase that passes its own tests.

### Why Code + Tests Together?

> aside positive
> **About the test-driven-dev skill:** This skill is named after Test-Driven Development historically, but what we're doing isn't strict TDD (where tests come first). We're letting AI generate code, then immediately generate tests, run them, and auto-fix any failures. Think of it as **"tests as a safety gate" baked into implementation** — they catch issues before you click anything.

Your `engineering.md` already specifies what tests should exist (the Testing strategy section). The implementation isn't complete until those tests pass. So we do both in one stage.

### Step 7.1 — Switch to Gemini 3.1 Pro

Code generation + test writing benefits a lot from Pro.

👉 In the chat, set the model picker to **Gemini 3.1 Pro**.

### Step 7.2 — Ask AI to Build the Code AND the Tests

📝 **Paste this:**

```
You're going to do two things in one shot.

PART 1 — IMPLEMENT THE APP CODE
- Build it according to @engineering.md (stack, file structure)
- Match the UI described in @ui.md
- Use the patterns in @reference/ as guidance for code style
- Backend: use Python with `uv` for dependency management
- If your chosen stack requires Node.js and it isn't installed on my 
  system, install it via Antigravity (use brew/winget/apt) — ask 
  permission first
- DO NOT start any dev servers — that's a later section

PART 2 — APPLY THE TEST-GATE SKILL
After the code is written, apply the test-driven-dev skill from
.agent/skills/skills-garden/eng-skills/test-driven-dev.md.

Use the "Testing strategy" section in @engineering.md as the test plan.

IMPORTANT: Mock the Gemini API calls in tests — use a stub that returns
fake response data. The real API key isn't set up yet, and tests should
be deterministic and free anyway (best practice).

The skill should:
1. Write the tests described in the Testing strategy
2. Run them (use pytest for Python, Vitest or Jest for JS)
3. If any fail, fix the CODE (not the tests) and re-run
4. Up to 3 retry attempts max
5. If still failing after 3 tries, STOP and tell me what's broken

When Antigravity asks permission to run commands (uv sync, uv pip 
install, pytest, etc.), click Allow.

Report results when both parts are done.
```

### Step 7.3 — Watch and Wait (~3-5 min total)

This is the longest section. Antigravity will:

1. Create folders (e.g., `backend/`, `frontend/`)
2. Write code files (`main.py`, `services/gemini_client.py`, etc.)
3. Set up `pyproject.toml`
4. Install dependencies (you'll see pop-ups)
5. Write test files (`tests/test_main.py`, etc.)
6. Run pytest (you'll see another pop-up)
7. If any test fails, fix the code and re-run
8. Summarize at the end

### Step 7.4 — Click Allow on Pop-Ups (Multiple)

Common pop-ups during this section:

🔔 **Pop-up:** `uv sync` or `uv pip install fastapi google-genai pytest`
→ Click **Allow**

🔔 **Pop-up:** `uv run pytest tests/`
→ Click **Allow**

🔔 **Pop-up (if Node needed):** `brew install node`
→ Click **Allow**

🔔 **Pop-up (if re-running after a fix):** `uv run pytest tests/` (again)
→ Click **Allow** — this is the auto-fix loop in action

🤖 **What you'll see in the chat throughout (example):**

```
PART 1 — Writing code...
Creating backend/ folder...
Writing backend/main.py (FastAPI app entry point)...
Writing backend/services/gemini_client.py...
Writing backend/pyproject.toml...
[Pop-up: Allow uv sync?]
Running uv sync to install dependencies...
Writing frontend/index.html...
Writing frontend/styles.css...
Writing frontend/app.js...

PART 1 complete. Code structure ready.

PART 2 — Applying test-driven-dev skill...
Writing tests/test_main.py with mocked Gemini client...
- test_parse_brief
- test_call_gemini_returns_image (with mock)
- test_health_endpoint

[Pop-up: Allow pytest?]
Running tests: pytest tests/
Result: 2 passed, 1 failed.

Failed: test_call_gemini_returns_image — got string instead of bytes
Diagnosing... gemini_client.py returns response.text but tests expect 
inline_data.data. Fixing backend/services/gemini_client.py...

[Pop-up: Allow pytest? (retry)]
Re-running tests: pytest tests/
Result: 3 passed, 0 failed.

✅ ALL DONE
- Code: backend/ + frontend/ scaffolded, dependencies installed
- Tests: 3/3 passing
- Auto-fix loop: 1 iteration used (1 bug found and fixed)
- Ready for API key setup
```

### Step 7.5 — Read the Final Report

When done, check for:

- ✅ A `backend/` folder exists with code
- ✅ A `frontend/` folder exists with code
- ✅ A `tests/` folder exists with test files
- ✅ The summary says "all tests passing" (not "failed after 3 retries")
- ✅ The agent did NOT start any servers

### What If All 3 Test-Retries Fail?

**Rare but possible. It usually means the engineering doc's Testing strategy is unrealistic for what got built.**

📝 **Paste this:**

```
The auto-fix loop hit the 3-try cap. Pull up @engineering.md and look 
at the Testing strategy section. Is the strategy realistic for what 
got built? Suggest updates to the doc so the tests align with reality. 
Don't change the code yet — update the doc, then re-apply the 
test-driven-dev skill.
```

Same lesson: **fix the doc, not the code.**

### What If Something Looks Off?

👉 If AI built something that doesn't match the docs, **go back to the doc** — don't ask AI to "fix the code" in isolation.

Example:

```
I see you built the chat as a popup, but @ui.md says it should be a 
full page. Either update ui.md if a popup is actually better, OR 
rebuild the chat as a full page to match the current ui.md.
```

Always: **the doc is the source of truth.**

> aside positive
> **Why we test before previewing:** Tests catch broken imports + logic bugs without needing a browser open. If we previewed first, we'd find those same bugs by clicking around (5 min per bug). Tests find them in seconds. **Tests save time, they don't add work.**

> aside negative
> **Don't skip tests "to save time."** Skipping tests = confusing bugs at minute 50 that an auto-test would have caught at minute 35.

✅ **Checkpoint:** Code exists, tests exist, tests pass. Ready to set up the API key.

---

## 8. Google Cloud + API Key Setup
**Duration: 5 min**

Your app needs a Gemini API key to make real AI calls. To get one, you need a Google Cloud project with billing linked (your facilitator will give you free credits — **no real charges**).

**Everything in this section happens in your browser. You won't open the Terminal.**

### Step 8.1 — Claim Your Workshop Credits (30 sec)

1. Your facilitator shared a **credit redemption link** — open it in your browser.
2. Sign in with the same Google account you're using for Antigravity.
3. Click **"Accept Credits"** (or similar).

✅ A billing account is created in your name with the workshop credits.

> aside negative
> **Don't have the credit link?** Ask your facilitator now. This step is required for the KPI tracking.

### Step 8.2 — Create a Google Cloud Project (1 min)

1. Open [https://console.cloud.google.com](https://console.cloud.google.com) in a new browser tab.
2. Sign in with the same Google account.
3. **Accept Terms of Service** if shown (first time only).
4. At the **top-left**, find the **project dropdown** (next to the "Google Cloud" logo) — it says *"Select a project"* or shows a previously selected project name.
5. Click the dropdown. A popup opens.
6. Click **"NEW PROJECT"** (top-right of the popup).
7. Type a project name like `coding-jam-week-1`. Leave "Organization" as is.
8. Click **CREATE**.
9. Wait ~15 seconds. A bell 🔔 notification appears top-right when ready.
10. Click the notification to switch to your new project (or open the dropdown again and select it).

**You should now see the Dashboard for your new project.**

### Step 8.3 — Copy Your Project ID (30 sec)

On the Dashboard, find the **"Project info"** card (usually top-left).

It shows three fields:
- **Project name** — what you typed (e.g., `coding-jam-week-1`)
- **Project number** — a long number (NOT this one)
- **Project ID** — looks like `coding-jam-week-1-485032` ← **copy this** (hover and click the 📋 icon)

✏️ **Paste the Project ID** into a sticky note or scratch text file — you'll need it twice more.

> aside negative
> **Don't see the Project info card?**
> 
> Try the direct URL: [console.cloud.google.com/home/dashboard](https://console.cloud.google.com/home/dashboard) (make sure your new project is selected in the top dropdown).
> 
> Still missing? Click **+ ADD A CARD** at the top of the Dashboard, search for "Project info", click **ADD**.

### Step 8.4 — Link Your Billing Account to the Project (1.5 min)

**This is the KPI step.**

1. In the Cloud Console, click the **☰ Navigation menu** (top-left, 3 horizontal lines, next to "Google Cloud").
2. In the side menu, find and click **"Billing"**.
3. On the Billing page, in the left sub-menu, click **"My Projects"**.
4. You'll see a list of your projects. **Find the row for the project you just created**.
5. At the right end of that row, click the **⋮ Actions menu** (three vertical dots).
6. Click **"Change billing"**.
7. A panel opens. You'll see a dropdown labeled **"Billing account"** — select the billing account that has your workshop credits (probably the only option, named "My Billing Account" or "Trial Billing Account").
8. Click **"SET ACCOUNT"**.

✅ Wait 5 seconds. The "Billing account" column for your project row should now show the billing account name. **KPI hit!**

> aside negative
> **"I don't see Change billing in the menu"** → Your billing account may still be processing. Wait 30 seconds, refresh, try again.
> 
> **"My project isn't in the list"** → Make sure you're on "My Projects" (not "All Projects"). If still missing, the project may still be being created — wait 1 min and refresh.

### Step 8.5 — Get Your Gemini API Key from AI Studio (1 min)

1. Open [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey) in a new browser tab.
2. Sign in with the same Google account.
3. Click **"Create API key"** (top-right).
4. A dialog opens with a project dropdown:
   - **If your project (from Step 8.3) is in the list:** select it.
   - **If NOT in the list:** click **"Import project"**, paste your Project ID into the search, select it, click **"IMPORT"**. Then go back to "Create API key" and select your now-imported project.
5. Click **"Create API key in existing project"**.
6. **Copy the API key** that appears. Starts with `AIza...`, ~40 characters.

✏️ **Paste it somewhere safe** — you'll give it to Antigravity next.

> aside negative
> **Treat the API key like a password.** Don't paste it in public chats, screenshots, or commit it to a public GitHub repo. We'll put it in a `.env` file (already in `.gitignore`).

### Step 8.6 — Tell Antigravity to Set Up `.env` (30 sec)

Back in Antigravity, press **Cmd+L** to focus the chat.

> ⚠️ **STOP. READ THIS BEFORE PASTING.**
>
> The prompt below contains **`<<<PASTE_YOUR_API_KEY_HERE>>>`** and **`<<<PASTE_YOUR_PROJECT_ID_HERE>>>`** placeholders.
>
> You **MUST** replace these with your real values from Steps 8.3 and 8.5, otherwise the `.env` file will contain literal `<<<PASTE_...>>>` text and your app **won't work**.
>
> Before clicking Send, scan the prompt and confirm you see:
> - `GEMINI_API_KEY=AIzaSy...` (starts with `AIzaSy`, ~40 characters)
> - `GOOGLE_CLOUD_PROJECT=coding-jam-week-...` (your real Project ID with random suffix)
>
> **If you still see `<<<PASTE_...>>>` anywhere in the prompt, DO NOT send yet — replace them first.**

📝 **Prompt to paste (replace the `<<<...>>>` markers first!):**

```
Apply the gemini-api-dev skill from .agent/skills/gemini-skills/skills/gemini-api-dev/.
(If that skill isn't found, fall back to .agent/skills/skills-garden/eng-skills/gemini-api.md)

Create a .env file in the backend folder with these settings:
- GEMINI_API_KEY=<<<PASTE_YOUR_API_KEY_HERE>>>
- GOOGLE_CLOUD_PROJECT=<<<PASTE_YOUR_PROJECT_ID_HERE>>>
- Any other env vars the app needs based on @engineering.md

Also verify:
- .env is in .gitignore so the key never gets committed
- The backend code reads GEMINI_API_KEY at startup
- The Gemini SDK is initialized correctly (use google-genai for Python)

When Antigravity asks permission to install Python packages, click Allow.
When done, show me the .env contents with the KEY redacted (just first 6 chars + ...).
```

🤖 **Expected:** Agent creates `.env`, installs `google-genai` (you click Allow), confirms with redacted key:

```
✅ .env created at backend/.env
GEMINI_API_KEY=AIzaSy... (40 chars, redacted)
GOOGLE_CLOUD_PROJECT=coding-jam-week-1-485032

.env is already in .gitignore ✓
Backend reads GEMINI_API_KEY via os.getenv() ✓
Gemini client initialized ✓
```

> aside negative
> **If the agent reports `GEMINI_API_KEY=<<<PASTE_YOUR_API_KEY_HERE>>>`** — you forgot to replace the placeholder! Paste this:
> ```
> The .env file has the literal placeholder text instead of my real key.
> Please update GEMINI_API_KEY to AIzaSy... (paste your real key) and 
> GOOGLE_CLOUD_PROJECT to (paste your real Project ID).
> ```

### ✅ Checkpoint — Section 8 Done

- ✅ Workshop credits redeemed
- ✅ Google Cloud project created (Project ID saved)
- ✅ Billing linked to your project (KPI hit!)
- ✅ Gemini API key from AI Studio
- ✅ `.env` file in `backend/` with the **real** key (not the placeholder!)
- ✅ `.env` in `.gitignore`

> aside positive
> **You just did the longest, clickiest section.** Now: time to actually see the app.

---

## 9. Preview & Verify
**Duration: 8 min**

Code is built. Tests pass. API key configured. **Now** open the app and click around.

### What Humans Catch (That Tests Miss)

| Tests Catch | Humans Catch |
|-------------|--------------|
| Wrong return values | Ugly colors |
| Broken function calls | Confusing copy |
| Missing imports | Buttons in weird places |
| Off-by-one errors | Animation feels janky |
| Logic bugs | The vibe is off |

### Step 9.1 — Ask Antigravity to Start the Dev Server

🎯 **MODEL: Default (Flash) is fine.**

📝 **Paste this:**

```
Please start the dev server(s) so I can preview the app in my browser.
Tell me the URL when it's ready. When Antigravity asks permission to 
run the server command, I'll click Allow.
```

🔔 **Pop-up:** `uv run uvicorn main:app --reload` (or similar)
→ Click **Allow**

### Step 9.2 — Open the Preview URL

🤖 **The agent reports:**

```
Backend running at: http://localhost:8000
Frontend served at: http://localhost:8000 (backend serves it)
```

URL is usually `http://localhost:8000` or `http://localhost:5173`.

👉 Click the URL in the chat, or copy-paste into a new browser tab.

### Step 9.3 — Click Around ✅ REQUIRED

Use it like a real user would:

- Click every button
- Type things in
- Hover over things
- Try the main flow from start to finish

**If everything looks and feels right, jump to Step 9.7 (write README).** Steps 9.4-9.6 are only needed if you find issues.

### Step 9.4 — Report What's Wrong 🎁 OPTIONAL — only if you find issues

Don't try to fix it yourself. Use this template:

📝 **Template:**

```
Observed: [what I see — paste a screenshot or describe it]
Expected: [what I wanted instead]

Please diagnose and propose a fix.
```

📝 **Real example:**

```
Observed: The "Submit" button is dark gray on a light gray background — 
hard to see.
Expected: It should be the bright purple from @ui.md.

Please diagnose and propose a fix.
```

🤖 **Expected agent response:**

```
The button is using the default browser style instead of the ui.md 
purple. Fix: add a CSS class with --primary-color: #7C3AED.

I'll update frontend/styles.css now. May I edit the file?
```

🔔 **Pop-up:** "Allow this file edit?" → Click **Allow**

### Step 9.5 — Verify the Fix Worked 🎁 OPTIONAL — follows 9.4

When Antigravity makes a change:

1. **Refresh your browser** (Cmd+R / Ctrl+R)
2. **Check that the fix actually worked** — don't assume
3. If it's still wrong, paste a follow-up: *"That didn't fix it — the button is still gray. Try a different approach."*

### Step 9.6 — The Regression Rule ⭐ OPTIONAL

Here's a habit that separates beginners from real builders:

> **When you find a bug a test missed, write a test that catches it FIRST. Then fix the code.**

📝 **Paste this when you find a real bug:**

```
I just found a bug: [describe it]. Before we fix the code:

1. Write a test that catches this specific bug — it should FAIL right now
2. Show me the failing test
3. THEN fix the code so the test passes
4. Re-run all tests to confirm nothing else broke
```

This makes your test suite **stronger every time you find a bug**. The same bug literally cannot come back.

### Troubleshooting Cheat Sheet (reference)

| Symptom | Prompt to Paste |
|---------|-----------------|
| Server won't start / Port already in use | *"Port [X] is in use. Change config to use port [X+1]."* |
| "Failed to fetch" in browser | *"The frontend shows 'Failed to fetch'. Check that the backend is running and the frontend points at the right URL."* |
| "Module not found" error | *"Got error: [paste error]. What package needs installing?"* |
| Auth failure / "Permission denied" | *"My GEMINI_API_KEY in .env might be wrong. Walk me through verifying it works."* |
| UI doesn't match `ui.md` | *"Compare the current UI against @ui.md. What's off and how do we align them?"* |
| Tests broken when re-run | *"Re-apply the test-driven-dev skill — fix the code if tests fail, max 3 retries."* |

### Step 9.7 — Write a README ✅ REQUIRED

Once your app works, lock it in:

📝 **Paste this:**

```
The app works! Please create a README.md in the project root that explains:
- What this app does (in plain English)
- How to install it on a new machine (uv sync, etc.)
- How to run the dev server(s)
- The 3 design docs (@product.md, @ui.md, @engineering.md) are the 
  source of truth — anyone can read them to understand the system

Save it as README.md.
```

🤖 **Expected:** `README.md` appears in the file list.

### Why the README Matters

> aside positive
> **You're building something that lasts.** With `engineering.md`, your tests, and a README — you can walk away today and come back in 3 weeks. Everything you need to keep building is saved on disk. **This is a real project, not just a demo.**

✅ **Checkpoint:** You clicked around the app, fixed any issues (if any), and saved a README.

---

## 🎉 You Shipped an MVP!

Your app works. Tests pass. You have a README. **This is the win.**

If your 75 minutes are up — **you're done!** Jump to the [Conclusion](#12-conclusion--you-shipped-).

If you have time left, the next two sections are **optional bonus rounds**:

- **Pivot or Expand** — add a feature or change direction
- **Polish the UI** — make it prettier

Both are great practice. **Neither is required to ship.** The MVP is the win.

---

## 10. 🎁 Pivot or Expand (OPTIONAL BONUS)
**Duration: 3 min**

*This section is optional. Skip to [Conclusion](#12-conclusion--you-shipped-) if your time is up.*

### Two Paths

**Expand:** Add a feature. The plan mostly stays — you append.

**Pivot:** Change direction. The plan changes a lot. Old code becomes obsolete.

### The Discipline (Same as Before)

1. Update `product.md` first
2. Update `ui.md` to match
3. Update `engineering.md` — **including the Testing strategy**
4. Re-run implementation with the test-gate skill applied
5. Verify everything still works

### Step 10.1 — For Expand

🎯 **MODEL: Gemini 3.1 Pro**

📝 **Paste this:**

```
I want to add this feature: [describe it].

1. Update @product.md, @ui.md, and @engineering.md (including Testing 
   strategy) to include this feature
2. Show me the changes for review before implementing
3. Once I approve, implement the feature AND apply the test-driven-dev 
   skill to write tests for it (mock external APIs)
4. Run tests, auto-fix up to 3 times, report
```

### Step 10.2 — For Pivot

🎯 **MODEL: Gemini 3.1 Pro**

📝 **Paste this:**

```
I want to pivot the app in a new direction: [describe it].

1. Regenerate @product.md, @ui.md, and @engineering.md (including 
   Testing strategy) for the new direction. Delete what's no longer 
   relevant.
2. Show me the new docs for review
3. Once I approve, rewrite the code AND apply test-driven-dev to write 
   fresh tests (mocked APIs)
4. Run tests, auto-fix up to 3 times, report
```

### Why This Works

> aside positive
> **Pivot from code = pain. Pivot from spec + tests = clean.** If you tried to pivot by editing code, you'd find pieces of the old direction sticking out everywhere. Old tests would test old behavior. It'd be a mess. When you pivot from the docs, AI starts fresh from a clean plan.

✅ **Checkpoint:** Either you skipped this section or you successfully pivoted/expanded using the doc-first discipline.

---

## 11. 🎁 Polish the UI (OPTIONAL BONUS)
**Duration: 2 min**

*This section is optional. Skip to [Conclusion](#12-conclusion--you-shipped-) if your time is up.*

### Just Iterate Freely

🎯 **MODEL: Default (Flash) is fine** — polish is small changes.

No skills required — just plain English. Examples:

📝 **Prompt examples:**

```
Make the primary button a brighter purple.
```

```
Increase the hero headline font size by 20%.
```

```
Add a subtle drop shadow to the cards.
```

🤖 **After each prompt:** refresh your browser to see the change. Iterate.

### Optional: Try a Visual Style

Two style references live in the skills you installed:

- **`cloud-pup`** — soft, friendly, pastel sky vibes
- **`y2k-dreamcore`** — chrome, holographic, millennium nostalgia

📝 **To try one:**

```
Apply the cloud-pup style from .agent/skills/skills-garden/ux-design-skills/cloud-pup.md 
to the current frontend.
```

(Or `y2k-dreamcore.md` if that's more your mood.)

**Completely optional.** Skip if you'd rather just tweak colors directly.

### Don't Try to Be "Done"

> aside negative
> **Polish has no finish line.** Set a 2-minute timer. When it dings, ship what you have. Don't get stuck here.

✅ **Checkpoint:** Your app looks more polished. You stopped before perfection.

---

## 12. Conclusion — You Shipped! 🎉
**Duration: 2 min**

You did it.

### What You Built

- ✅ An AI-powered web app
- ✅ Three design docs (`product.md`, `ui.md`, `engineering.md`)
- ✅ A real test suite that runs every time you change code
- ✅ A `README.md` so you can come back to this any time
- ✅ A connection to Google's Gemini AI
- ✅ A Google Cloud project with billing linked (KPI ✅)

You went from idea → working app in 75 minutes, **without writing a single line of code yourself.** That's wild.

### What You Learned

| Skill | Why It Matters |
|-------|----------------|
| **Spec → Code+Test → Verify** | Plan first. Build code and tests together. Click around last. Always in that order. |
| **Fix the doc, not the code** | When something's off, change the plan and rebuild. Don't patch. |
| **Tests as a safety gate** | Built into implementation — AI catches the dumb stuff before you have to. |
| **The regression rule** | Every human-found bug becomes a test. The bug can never come back. |
| **Doc-driven pivots** | When direction changes, change the doc — AI handles the rest. |
| **Antigravity 3-layer flow** | English in chat → agent picks command → you approve. |

### The One Sentence to Take Home

> **"Ask the next question. Fix the doc, not the code."**

This works for any project, any tool, any AI. Today's app was just practice.

### Coming Back Next Week?

- Pick a different row from the 8-week table in Section 3A
- Clone that week's repo via Antigravity's **"Clone Repository"** button
- The skills install fresh per workspace (workspace-scoped = no leftover state)
- You can reuse your same Google Cloud project (still there with billing linked)
- Everything else is the same workflow you just learned

### What's Next

- **Deploy to the internet:** Check out the [Build & Deploy with Cloud Run codelab](deploy-understand-ai-motion-lab.md) to put your app online
- **Build at home:** Your three docs are portable. Open them in any AI tool and keep building
- **Bring a friend:** Pair through this codelab with someone new. Teaching is the fastest way to learn

### Resources

- [Antigravity Documentation](https://antigravity.google/)
- [Antigravity Skills Docs](https://antigravity.google/docs/skills)
- [Antigravity Conversation View](https://antigravity.google/docs/conversation-view)
- [Official Gemini Skills (Google)](https://github.com/google-gemini/gemini-skills)
- [Coding Jam Starter (all 8 weeks)](https://github.com/cuppibla/coding-jam-starter)
- [Skills Garden (the skills we used)](https://github.com/cuppibla/skills-garden)
- [Gemini API Documentation](https://ai.google.dev/docs)
- [FastAPI Documentation](https://fastapi.tiangolo.com)

> aside positive
> **Welcome to the club.** You're a builder now. Go build more things.

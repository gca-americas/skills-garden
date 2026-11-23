# Codelab scaffolds

Two scaffolds, one per arc (see `SKILL.md` → "Pick the arc"). Copy the matching
one, replace every `<placeholder>`, and match the formatting in the bundled
examples under `references/examples/`. Keep the frontmatter YAML-fenced and the
`**Duration: N min**` lines bold.

> Reminder: `👉` = do in UI · `👉💻` = run in terminal · `[READ ONLY]` / `[OPTIONAL]`
> sections need no checkpoint · every hands-on step ends in an Expected-output block.

---

# ════════════════════════════════════════════════════════════
# SCAFFOLD A — "Deploy & understand" (DEFAULT, finished demo/starter repo)
# ════════════════════════════════════════════════════════════

```markdown
---
id: <kebab-case-id>
title: Build & Deploy <X> with <Y, Z>
summary: <one sentence, present tense, what they end up with>
authors: Qingyue (Annie) Wang
keywords: <Tech1>,<Tech2>,category:AiAndMachineLearning,category:Cloud,docType:Codelab,language:<Lang>,product:<Product>,product:VertexAi,skill:<Beginner|Intermediate|Advanced>
award_behavior: AWARD_BEHAVIOR_ENABLE
layout: paginated
duration: <total-minutes>
---

# <emoji> Build & Deploy <X> with <Y, Z>

---

## Introduction
**Duration: 3 min**

### What You'll Build

**<Project>** is <one-line pitch>. <How it works in 1–5 numbered bullets:>

1. **<Verb>** … using **<Tech>**
2. **<Verb>** … using **<Tech>**

By the end of this codelab, you'll have <the artifact> deployed to **<host>** and
understand the <system> that powers it.

### Architecture Overview
<img src="img/architecture.png" />

### Core Technologies

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **<Component>** | <Tech + pinned version> | <what it does> |
| **<Component>** | <Tech + pinned version> | <what it does> |

---

## 📦 Clone the Repository
**Duration: 2 min**

### 1. Open Cloud Shell Editor

👉 Open [Cloud Shell Editor](https://ide.cloud.google.com/) in your browser.

### 2. Clone the Code

👉💻 In the terminal, clone the repository:

\`\`\`bash
cd ~
git clone <repo-url>
cd <repo-dir>
\`\`\`

### 3. Explore the Project Structure

\`\`\`
<repo-dir>/
├── backend/        # <what it is>
├── frontend/       # <what it is>
└── <script>.sh     # <what it does>
\`\`\`

> aside positive
> **Key directories to know:**
> - `<path>` — <why it matters>

---

## 🛠️ <Cloud / Project Setup>
**Duration: 5 min**

### Part 1: <Claim credits / pick project>

👉 <UI action>.

### Part 2: <Create project / enable APIs>

👉💻 <command>:

\`\`\`bash
<command>
\`\`\`

> aside positive
> **What each API does:**
>
> | API | Purpose |
> |-----|---------|
> | `<api>` | **<Name>** — <what it does> |

---

## 🧠 [READ ONLY] Understanding the Architecture
**Duration: 5 min**

This section explains how <the system> works end-to-end. **No action needed** —
just read to understand it before deploying.

### The <Pipeline / Flow>
<img src="img/pipeline.png" />

### Stage 1: <Name>

<One line: what happens.>

> aside positive
> **What <Component> does / Why <choice>:**
> <plain explanation of the concept — the payoff of the whole codelab>

**How it works** (`<path/to/file>`):

\`\`\`<lang>
# Simplified from <path/to/file>
<minimal representative snippet>
\`\`\`

<!-- Repeat one ### Stage per concept. This is where concepts get explained. -->

---

## 🚀 Deploy the Backend
**Duration: 8 min**

### 1. Understand the <Dockerfile / config>

\`\`\`dockerfile
# <path>/Dockerfile
<key lines>
\`\`\`

> aside positive
> **Why <choice, e.g. ffmpeg / 2Gi memory>?** <reason>

### 2. Deploy to Cloud Run

👉💻 <command>:

\`\`\`bash
<deploy command>
\`\`\`

> aside positive
> **Key deployment flags explained:**
>
> | Flag | Purpose |
> |------|---------|
> | `<flag>` | <what it does> |

### 3. Verify the Backend

👉💻 Test the health endpoint:

\`\`\`bash
curl $BACKEND_URL/api/health
\`\`\`

**Expected output:**

\`\`\`json
{"status":"ok"}
\`\`\`

> aside positive
> 🎉 Your backend is live!

---

## 🎨 Deploy the Frontend
**Duration: 5 min**

<same pattern: understand → deploy → get URL → open it>

---

## 🎮 [OPTIONAL] Play With the Demo
**Duration: 5 min**

1. Open the **Frontend URL** in your browser
2. <interaction>
3. <what they'll see>

> aside negative
> **First-time generation** may take longer as models initialize.

---

## 🎉 Conclusion
**Duration: 2 min**

### What You've Built

✅ **<Capability>** — <one line>
✅ **<Capability>** — <one line>

### Key Concepts You Learned

1. **<Concept>** — <one-line recap>
2. **<Concept>** — <one-line recap>

### What's Next?

- <extension idea>
- Run locally in mock mode — <how>

### Resources

- [<Official doc>](<url>)
- Source repo: <url>
```

---

# ════════════════════════════════════════════════════════════
# SCAFFOLD B — "Build from a brief" (from-scratch / vibe-code session)
# ════════════════════════════════════════════════════════════

```markdown
---
id: <kebab-case-id>
title: Build & Ship <X> with <Tool>
summary: <one sentence; note duration & "no coding experience required" if true>
authors: Qingyue (Annie) Wang
keywords: <Tool>,Gemini,category:AiAndMachineLearning,docType:Codelab,language:Python,language:TypeScript,product:VertexAi,skill:Beginner
award_behavior: AWARD_BEHAVIOR_ENABLE
layout: paginated
duration: <total-minutes>
---

# <emoji> Build & Ship <X> with <Tool>

---

## Introduction
**Duration: 3 min**

### Welcome
<warm, plain-language welcome; state who it's for and that AI writes the code.>

### The One Sentence to Remember
> **"Fix the doc, not the code."**
<explain: update the plan/spec first, then rebuild from it.>

### What You'll Build
<the artifact, in one short paragraph.>

### The Journey

| # | Step | Time | Required? |
|---|------|------|-----------|
| 1 | <Step> | <N> min | ✅ |
| — | <Read-only tour> | <N> min | ✅ |
| <n> | <Optional bonus> | <N> min | 🎁 |

---

## <emoji> Install <Tool>
**Duration: <N> min**

👉 <download/install action>.
👉💻 <verify install>:

\`\`\`bash
<command>
\`\`\`
**Expected output:** <version string>

---

## <n>. The Spec Talk
**Duration: 5 min**

A short conversation where you tell AI what to build. **No code yet.**

### The One Required Question
> **"What goes IN, what comes OUT?"**

Examples:
- *"A photo IN. A cartoon version OUT."*

👉💻 Paste to your AI tool:

\`\`\`
Read @BRIEF.md and treat it as our product spec. DO NOT generate plans or code
yet. Confirm back: input? output? the magical moment? Then wait.
\`\`\`

---

## <n>. Generate Design Docs
**Duration: <N> min**

> aside positive
> **Why design docs first?** <explain: the doc is the source of truth; code is
> regenerated from it. This is "fix the doc, not the code" in practice.>

👉💻 <prompt to generate the design doc(s)>.

**Checkpoint:** you should now have `<doc1>.md`, `<doc2>.md` in your repo.

---

## <n>. Implement + Test
**Duration: <N> min**

👉💻 <prompt to implement from the docs>.

**Checkpoint — prove it works:** <command + expected visible result>.

> aside negative
> If it's wrong, **don't patch the code** — fix the doc and regenerate.

---

## <n>. <Cloud / API key setup> & Deploy
**Duration: <N> min**

<same cloud-setup + verify-checkpoint pattern as Scaffold A.>

---

## 🎉 Conclusion — You Shipped!
**Duration: 2 min**

### What You've Built
✅ <capability>

### Key Concepts You Learned
1. **<Concept, e.g. spec-driven development>** — <recap>

### What's Next?
- 🎁 <optional bonus / pivot idea>

### Resources
- [<doc>](<url>)
```

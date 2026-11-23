# House style for codelabs

These rules make a codelab *ours*. The gold standard is the bundled
`references/examples/deploy-understand-ai-motion-lab.md` — when in doubt, match it.
Apply all four principles plus the formatting conventions to every codelab.

## The four principles

### 1. Explain every concept clearly
This is the signature of our codelabs and the thing learners thank us for. Every
technology, API, IAM role, flag, and pipeline stage gets a plain-language
explanation. Three tools do the heavy lifting:

- A **`## 🧠 [READ ONLY] Understanding the Architecture`** section (or a
  "Deep Dive") that walks the system stage by stage. Per stage: one line of *what
  happens*, a `# Simplified from <file>` snippet, and an `aside positive`.
- **`aside positive` "Why / What" boxes** — `Why "Nano Banana"?`,
  `What Gemini Extracts:`, `What makes this special:`, `Why Cloud Run?`.
- **"What each X does" tables** — for APIs enabled, IAM roles granted, deploy
  flags, env vars.

A learner should finish knowing *why*, not just having pasted commands.

### 2. Show, then explain
Get the learner to a running, visible result first; explain the machinery after.
The arc is **deploy/run → understand → play**, not theory up front. (The
`[READ ONLY]` deep-dive sits *after* setup and *before/around* deploy — never as a
wall of text before the first win.)

- ❌ Open with 30 lines of architecture theory before anything runs.
- ✅ Clone → get cloud set up → read the architecture → deploy → see it live.

### 3. Evidence-driven — every hands-on step proves itself
A step is done when the learner can *observe* it worked. Each hands-on step ends
with a checkpoint: a `👉💻` command and the **exact expected output** block, a test
that passes, or a visible behavior change.

```
👉💻 Test the health endpoint:
\`\`\`bash
curl $BACKEND_URL/api/health
\`\`\`
**Expected output:**
\`\`\`json
{"status":"ok"}
\`\`\`
```

`[READ ONLY]` and `[OPTIONAL]` sections are exempt — tag them so it's clear no
checkpoint is expected.

### 4. Version-pinned, doc-anchored
- Pin every model id, SDK, and tool version — in the **Core Technologies** table
  and in Prerequisites (e.g. `gemini-3-flash-preview`, `veo-3.1-fast-generate-001`,
  `Python 3.11`).
- Every code snippet is traceable to a real file: head it with `# from <path>` or
  `# Simplified from <path>`.
- Never let a snippet stand in for current official docs — link the doc in
  **Resources** and note that APIs evolve.

## Formatting conventions (copy these exactly)

### Frontmatter — YAML-fenced, at the very top
```yaml
---
id: <kebab-case-codelab-id>
title: Build & Deploy <X> with <Y>
summary: <one-sentence what-they-build, present tense>
authors: Qingyue (Annie) Wang
keywords: <FreeTag1>,<FreeTag2>,category:AiAndMachineLearning,category:Cloud,docType:Codelab,language:Python,product:CloudRun,product:VertexAi,skill:Intermediate
award_behavior: AWARD_BEHAVIOR_ENABLE
layout: paginated
duration: 45
---
```
`keywords` taxonomy: free product/tech tags first (e.g. `Gemini,Veo,NanoBanana`),
then the structured tags:
- `category:` — `AiAndMachineLearning`, `Cloud`, …
- `docType:Codelab` — always present.
- `language:` — `Python`, `TypeScript`, `Go`, `Dart`, … (repeat for multiple).
- `product:` — `CloudRun`, `VertexAi`, … (repeat for multiple).
- `skill:` — `Beginner` | `Intermediate` | `Advanced`.

`duration` is total minutes (sum of the per-section durations).

### Title & sections
- `# 🎬 <Title>` — H1 with a topic-matching emoji; same wording as `title`.
- `---` horizontal rules between major sections.
- `## <emoji> <Section name>` for each phase. Recurring emoji: `📦` clone/setup,
  `🛠️`/`⚙️` configure, `☁️` cloud, `🏗️` architecture, `🤖` agents, `🧠` deep-dive,
  `🧪` pipeline, `📱` frontend, `🚀` deploy, `🎮` play, `🎉` conclusion.
- `**Duration: N min**` on the line directly under each `##` (bold, minutes —
  never `MM:SS`).
- Tag sections that aren't hands-on: `## 🧠 [READ ONLY] Understanding the
  Architecture`, `## 🎮 [OPTIONAL] Play With the Demo`.
- `### N. <Sub-step>` or `### Part N: <…>` for numbered steps within a section.

### Action markers
- `👉` — do this in the UI/browser/console ("👉 Open Cloud Shell Editor").
- `👉💻` — run this in the terminal ("👉💻 Deploy to Cloud Run:").
- Every actionable instruction starts with one. Non-action prose has neither.

### Asides
- `> aside positive` — tips, "why", "what X does", encouragement, "🎉 it's live!".
- `> aside negative` — pitfalls, cost/quota warnings, "first run is slow", gotchas.
- Tables nest fine inside asides (see the "What each API does" table).
- A codelab with **no `aside negative` anywhere** hasn't hit the real pitfalls yet.

### Tables
Use them generously for comparison/reference:
- **Core Technologies** (intro): `Component | Technology | Purpose`.
- **What each X does**: APIs, IAM roles, deploy flags, env vars.
- **The Journey** (build-from-brief arc): `# | Step | Time | Required?` overview.

### Images
- `<img src="img/architecture.png" />` for diagrams; `![cover](img/demo.gif)` for
  the final-result GIF. Store assets in an `img/` folder beside the codelab.

## Variations across the corpus (all valid)
These appear in Annie's published codelabs — reach for them when they fit:

- **Scenario / "The Challenge" hook.** Open with a concrete scenario *before*
  "What You'll Build" (e.g. a disaster-response story) to add stakes and context.
- **Split intro.** The opening can be one `## Introduction` *or* separate top-level
  sections: `## The Challenge` → `## What You'll Build` → `## Core Technologies`.
- **Workshop vs self-paced tags.** When a lab runs both live and self-serve, tag
  prereq/setup sections like `## Environment Prep (Skip if in Workshop)`.
- **Multi-part series.** For a Level 0–5 / multi-codelab series, cross-link the
  sibling parts and add a "Workshop Content" list of links in the conclusion.
- **Combined tags.** `[OPTIONAL] … (Read Only)` is fine when a section is both.
- **Layered deep-dive.** Structure the `[READ ONLY]` architecture section by layer
  (Tooling → Agent → Orchestration) when that's how the system decomposes.

## Voice
- Direct, second person ("you'll build"), short sentences.
- Bilingual is fine where natural (Annie writes 中英文 mixed), but keep all code,
  commands, and frontmatter in English.
- Encouraging at milestones ("🎉 Your backend is live!"), honest about slow/costly
  steps.

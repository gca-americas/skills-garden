# Reference codelabs — study these before drafting

These are Annie's real codelabs, bundled so the skill is self-contained. Read the
one matching your arc before writing, and make your output look and read like it.
(The `<img src="img/…">` references won't resolve here — these are for studying
*structure and wording*, not rendering.)

| File | Arc | Why it's here |
|------|-----|---------------|
| [`deploy-understand-ai-motion-lab.md`](deploy-understand-ai-motion-lab.md) | **Deploy & understand** (default) | The canonical gold standard — "Build & Deploy an AI Motion Lab with Gemini, Veo & Cloud Run." |
| [`build-from-brief-coding-jam.md`](build-from-brief-coding-jam.md) | **Build from a brief** | Vibe-code session — "Build & Ship an AI App with Antigravity." Note the **Spec Talk**, **"Fix the doc, not the code"**, and the **Journey** overview table. |

**Published render** (no local file — this is the live exported result, useful as
proof the format renders correctly):
<https://codelabs.developers.google.com/codelabs/survivor-network/instructions> —
"Build a Multimodal AI Agent with Graph RAG, ADK & Memory Bank." Shows the
variations in `../style-rules.md`: a scenario hook, split intro, "(Skip if in
Workshop)" tags, a layered `[READ ONLY]` deep-dive, and Levels 0–5 series links.

## What to copy from these

- **Frontmatter** — YAML-fenced (`---`): `id / title / summary / authors / keywords /
  award_behavior / layout / duration`. `keywords` taxonomy: free tags first, then
  `category:… , docType:Codelab , language:… , product:… , skill:Beginner|Intermediate|Advanced`.
- **Title** — emoji prefix matching the topic (`# 🎬 …`).
- **`**Duration: N min**`** under every `##` section (bold, minutes — never `MM:SS`).
- **Emoji section headers** + `[READ ONLY]` / `[OPTIONAL]` tags on non-hands-on sections.
- **Action markers** — `👉` = do in UI/browser · `👉💻` = run in terminal. Every
  action line starts with one.
- **Core Technologies table** in the intro — `Component | Technology | Purpose`.
- **The `[READ ONLY] Understanding the Architecture` section** — the heart of "every
  concept clearly explained." Per stage: a one-line "what happens", a
  `# Simplified from <file>` snippet, and an `aside positive` "Why X? / What X does:" box.
- **"What each X does" tables** for APIs, IAM roles, deploy flags, env vars.
- **Verify checkpoints** — a `👉💻` command immediately followed by an **Expected
  output** block.
- **Conclusion** — ✅ "What You've Built", a numbered "Key Concepts You Learned"
  recap, "What's Next?", and "Resources".

## Adding your own

Drop any `.md` codelab in this folder and add a row to the table above. To refresh
a bundled copy from a source file, re-run `cat -s <source>.md > <name>.md` (squeezes
the double blank lines). Keep at least one complete example per arc.

---
name: codelab-from-repo
description: >-
  Generate a publishable, Google Codelabs-format codelab from an existing repo or
  demo, in Annie's house style — emoji-tagged sections, 👉/👉💻 action markers, a
  [READ ONLY] architecture deep-dive that explains every concept, evidence-driven
  verify checkpoints, and version-pinned snippets. Use when someone wants to turn a
  repo or demo into a hands-on step-by-step codelab, onboard to how we author them,
  or convert example code into a guided learning path. Triggers on "make a codelab
  from this repo", "turn my repo/demo into a tutorial", "codelab for <project>",
  "hands-on guide from this codebase".
---

# Codelab From Repo

Turn an existing repository or demo into a **Google Codelabs-format codelab** —
a guided, step-by-step hands-on tutorial — written in Annie's house style. This
skill doesn't just emit output; it teaches *how we decide* what makes a good
codelab, and it holds the bar set by Annie's published codelabs.

## Read this first

Before drafting anything, read **`references/examples/`** — it bundles Annie's real
codelabs (one complete example per arc) with a `README.md` listing exactly what to
copy from them. Everything you generate should look and read like those files. The
conventions are captured in `references/style-rules.md`; the fill-in scaffolds are
in `references/codelab-template.md`.

## When to use this

- A teammate has a working repo/demo and needs a teaching artifact from it.
- Onboarding: learning how we structure codelabs by generating one.
- Converting `examples/` or a demo into a publishable codelab.

## House style — the non-negotiables

Read `references/style-rules.md` and apply all of it. The four principles:

1. **Explain every concept clearly.** This is what makes a codelab *ours*. Each
   technology, API, flag, and pipeline stage gets a plain explanation — through a
   `## 🧠 [READ ONLY] Understanding the Architecture` section, `aside positive`
   "Why X? / What X does:" boxes, and "what each X does" tables. A learner should
   finish understanding *why*, not just having copy-pasted.
2. **Show, then explain.** Get the learner to a running, visible result, then
   explain the machinery behind it. The arc is deploy/run → understand → play,
   not a wall of theory up front.
3. **Evidence-driven.** Every hands-on step ends with a verifiable checkpoint —
   a command (`👉💻`) followed by the **exact expected output** the learner should
   see. No step ships without a way to know it worked. Read-only and optional
   sections are exempt (tag them `[READ ONLY]` / `[OPTIONAL]`).
4. **Version-pinned, doc-anchored.** Pin SDK/model/tool versions (in the Core
   Technologies table and Prerequisites). Cite the real repo file each snippet
   comes from. Never present a snippet as a substitute for current official docs.

## Pick the arc

Annie's codelabs come in two shapes. Choose based on the source, and confirm with
the user if it's ambiguous:

- **Deploy & understand** *(default — for a finished demo/starter repo).*
  Clone → cloud setup → `[READ ONLY]` understand the architecture → deploy →
  `[OPTIONAL]` play → conclusion. Example:
  `references/examples/deploy-understand-ai-motion-lab.md`.
- **Build from a brief** *(for a from-scratch or vibe-code session).*
  Install tools → **Spec Talk** ("What goes IN, what comes OUT?") → generate
  design docs → implement & test → deploy. Mantra: **"Fix the doc, not the code."**
  Example: `references/examples/build-from-brief-coding-jam.md`.

Both use the same formatting conventions; they differ only in the step arc.
`references/codelab-template.md` has a scaffold for each.

## Workflow

Run these phases in order. Tell the user what you found at the end of Phase 1
before drafting.

### Phase 1 — Ingest the source
Build an accurate mental model. Read, do not guess:
- `README*`, `CONTRIBUTING*`, docs/ — stated purpose and quickstart.
- Manifests: `package.json`, `pyproject.toml`/`requirements*.txt`, `go.mod`,
  `pom.xml`, etc. → languages, deps, **exact versions to pin**.
- Entry points, `examples/`, `samples/`, `demo/`, deploy scripts (`init.sh`,
  `setup.sh`, `Dockerfile`, `cloudbuild.*`), and tests → the real usage surface
  and the natural happy path.
- Directory structure → module boundaries (you'll reproduce this as the
  "Explore the Project Structure" tree).
Produce a short brief: what it does, the dependency/version list, the deploy
surface (does it ship to Cloud Run? what cloud setup is needed?), and which **arc**
fits.

### Phase 2 — Design the learning arc
- Choose the arc (above). Map the sections to the chosen template.
- List the **concepts** the learner must understand, and decide where each is
  explained — most belong in the `[READ ONLY] Understanding the Architecture`
  section, each with its own `aside` or table.
- For every hands-on step, name the **verify checkpoint** (command + expected
  output) before writing prose.
- Confirm audience, prerequisites, total duration, and the `skill:` level. Ask the
  user only if the source doesn't make these obvious.

### Phase 3 — Draft the codelab
Copy the matching scaffold from `references/codelab-template.md` and fill it.
Hard requirements (see the examples in `references/examples/` for the live shape):
- **YAML-fenced frontmatter** at the very top: `id`, `title`, `summary`,
  `authors`, `keywords` (with the `category:/docType:Codelab/language:/product:/skill:`
  taxonomy), `award_behavior: AWARD_BEHAVIOR_ENABLE`, `layout: paginated`,
  `duration`.
- `# 🎬 Title` with a topic-matching emoji; `---` rules between sections.
- One `## <emoji> Section` per phase, each with `**Duration: N min**` underneath
  (bold, minutes — never `MM:SS`). Tag non-hands-on sections `[READ ONLY]` /
  `[OPTIONAL]`.
- A **Core Technologies** table (`Component | Technology | Purpose`) in the intro.
- Action lines start with `👉` (do in UI) or `👉💻` (run in terminal).
- Code blocks **traceable to real files** (`# from <path>` or `# Simplified from <path>`).
- Concepts explained via `aside positive` "Why/What" boxes and "what each X does"
  tables; pitfalls via `aside negative`.
- Conclusion with ✅ **What You've Built**, a numbered **Key Concepts You Learned**
  recap, **What's Next?**, and **Resources** (incl. the source repo link).

### Phase 4 — Verify against the checklist
Run `references/checklist.md` and fix every miss. In particular flag:
- any unpinned version, any snippet with no repo provenance,
- any hands-on step lacking an observable checkpoint,
- frontmatter/`keywords` taxonomy or `**Duration: N min**` syntax errors,
- a missing `[READ ONLY] Understanding the Architecture` (or equivalent
  concept-explanation) section.
Report remaining judgment calls to the user rather than silently guessing.

## Output

Write the codelab to `<repo-slug>-codelab.md` (or `CODELAB.md` inside the repo, as
Annie does). Images go in an `img/` folder next to it; reference them with
`<img src="img/architecture.png" />`. This is the **Devsite codelab** format
(`award_behavior`, `layout: paginated`) — don't tell the user to run the public
`claat export`. If they need a local preview, render the markdown to a static HTML
page the way the published codelabs are (a `preview.html`), not the public `claat` tool.

## Onboarding mode

If the user is new to authoring codelabs (or asks "how do we do this"), walk them
through `references/onboarding-guide.md` — explain *why* each house-style rule
exists as you apply it, using their repo as the worked example.

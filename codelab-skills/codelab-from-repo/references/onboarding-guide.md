# How we write codelabs — onboarding guide

Welcome. This explains *why* our codelabs look the way they do, so you can make
good judgment calls, not just fill a template. Read it once, then let the skill
drive. The single best thing you can do is read the bundled examples in
`references/examples/` — our real codelabs — and imitate the one matching your arc.

## What a codelab is (and isn't)
A codelab is a **guided, hands-on build with checkpoints** — the learner runs
things and *sees them work* at every step, and walks away *understanding* the
system. It is not a blog post, not API reference, and not a slide deck. If a reader
could finish it without running anything, or finishes without understanding *why*
it works, it isn't one of ours.

We publish in **Google Codelabs (Devsite) format**: YAML frontmatter with
`award_behavior` / `layout: paginated`, emoji-tagged sections, `👉`/`👉💻` action
markers. (This is *not* the old public-`claat` key:value format — don't reach for
`claat export` on our frontmatter.)

## The two arcs
Our codelabs come in two shapes. Pick by what you're starting from:

1. **Deploy & understand** *(default — a finished demo or starter repo).*
   Clone → cloud setup → `[READ ONLY]` understand the architecture → deploy →
   `[OPTIONAL]` play → conclusion. Example:
   `references/examples/deploy-understand-ai-motion-lab.md`.
2. **Build from a brief** *(a from-scratch or vibe-code session).*
   Install → **Spec Talk** ("What goes IN, what comes OUT?") → design docs →
   implement & test → deploy. Mantra: **"Fix the doc, not the code."** Example:
   `references/examples/build-from-brief-coding-jam.md`.

## The mindset (why our four rules exist)

1. **Explain every concept clearly** — This is what people remember us for. A
   codelab that only lists commands teaches copy-paste; ours teach understanding.
   The `[READ ONLY] Understanding the Architecture` section, the `aside positive`
   "Why/What" boxes, and the "what each X does" tables are where that happens. The
   **Key Concepts You Learned** recap at the end closes the loop.

2. **Show, then explain** — Newcomers quit when the codelab opens with a wall of
   theory or setup. Get them to a visible, running result, *then* explain the
   machinery. Understanding lands better once there's something working to attach
   it to.

3. **Evidence-driven** — A step without a checkpoint is a step the learner can't
   trust. Every hands-on step ends with: run this (`👉💻`) → see exactly this
   (Expected output). `[READ ONLY]`/`[OPTIONAL]` sections are the only exceptions,
   and we tag them so it's obvious.

4. **Version-pinned, doc-anchored** — Models and SDKs move fast. Pin versions in
   the Core Technologies table so the codelab reproduces, cite the real repo file
   each snippet came from, and link the live docs so no one ships a stale snippet.

## Your first codelab in 4 moves
1. **Point the skill at your repo/demo.** It reads README, manifests, deploy
   scripts, examples, tests, and gives you a brief + a proposed arc. Sanity-check
   the arc.
2. **List your concepts and where each is explained.** Most go in the
   `[READ ONLY] Understanding the Architecture` section, each with its own aside
   or table. If you can't explain a concept simply, you don't understand it yet.
3. **Name every checkpoint before writing prose.** If you can't state how a
   hands-on step proves itself, the step isn't designed yet.
4. **Run the checklist.** `references/checklist.md`. Fix every miss.

## Common mistakes (we've made them)
- Opening with architecture theory before anything runs → learner bounces. Show first.
- A `[READ ONLY]` section that's just a diagram with no "why" asides → looks
  thorough, teaches nothing. The asides *are* the teaching.
- Snippets that don't match the repo → learner gets errors → loses trust.
- No `aside negative` anywhere → you haven't hit the real pitfalls yet.
- Unpinned versions → "works on my machine," then doesn't.
- Plain `## Step 1` headers, `Duration: 00:02:00`, missing `👉` markers → it reads
  like someone else's codelab, not ours.

That's it. The skill handles the mechanics; you bring the judgment on the arc, the
honest checkpoints, and — above all — explaining every concept clearly.

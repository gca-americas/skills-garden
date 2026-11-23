# Codelab self-review checklist

Run this before declaring a codelab done. Every box must be checked or the miss
reported to the author. Compare against the examples in `references/examples/` when unsure.

## Frontmatter & metadata
- [ ] YAML-fenced frontmatter (`---`) at the very top
- [ ] `id` (kebab-case), `title`, `summary` (one sentence), `authors` present
- [ ] `keywords` includes `docType:Codelab`, a `skill:` level, and `category:` /
      `language:` / `product:` tags as applicable
- [ ] `award_behavior: AWARD_BEHAVIOR_ENABLE`, `layout: paginated`, `duration` present
- [ ] `duration` ≈ sum of the per-section `**Duration: N min**` lines

## Structure
- [ ] Single `# <emoji> Title` (H1) matching `title`
- [ ] `---` rules separate major sections
- [ ] Every `##` section has `**Duration: N min**` directly under it (bold, minutes — not `MM:SS`)
- [ ] `## Introduction` with **What You'll Build** + a **Core Technologies** table
- [ ] Architecture overview (image or ASCII) near the top
- [ ] Non-hands-on sections tagged `[READ ONLY]` / `[OPTIONAL]`
- [ ] Conclusion has ✅ **What You've Built**, **Key Concepts You Learned**,
      **What's Next?**, and **Resources** (with source repo link)

## Concept clarity (the signature)
- [ ] A `[READ ONLY] Understanding the Architecture` (or Deep Dive) section explains
      the system stage by stage
- [ ] Each concept/stage has an `aside positive` "Why X? / What X does:" box and/or
      a `# Simplified from <file>` snippet
- [ ] "What each X does" tables used for APIs / IAM roles / deploy flags / env vars
- [ ] A reader finishes understanding *why*, not just having pasted commands

## House style
- [ ] Emoji on the H1 and every `##` section header
- [ ] Action lines start with `👉` (UI) or `👉💻` (terminal)
- [ ] At least one `aside positive` (tip) and one `aside negative` (pitfall)
- [ ] Arc is **show, then explain** (running result before deep theory)

## Evidence & correctness
- [ ] **Every hands-on step** ends with a checkpoint: command + **Expected output** block
- [ ] All versions pinned (Core Technologies table + Prerequisites): lang, SDK, model, tools
- [ ] Every code snippet cites its real repo file (`# from <path>` / `# Simplified from <path>`)
- [ ] Commands and expected outputs match what the repo actually produces
- [ ] No snippet presented as a substitute for official docs (docs linked in Resources)
- [ ] No placeholder text (`<...>`) left unfilled

## Publish-readiness
- [ ] Image references resolve (`img/…` assets exist beside the file)
- [ ] Total duration sums to a believable session length
- [ ] Targets the Devsite format — do **not** instruct `claat export` for this frontmatter

# 🌱 Skills Garden

A small library of [Agent Skills](https://antigravity.google/docs/skills) used in the **Coding Jam** workshop and personal vibe-coding projects. Each skill is a folder containing a `SKILL.md` that teaches an AI agent (Antigravity, Claude Code, Gemini CLI, Cursor, etc.) how to do one thing well.

## What's in here

| Category | Skills | What they do |
|----------|--------|--------------|
| **`design-doc-skills/`** | `pm-design-doc`, `ux-design-doc`, `eng-design-doc` | Turn a raw product brief into three structured Markdown design docs — product, UX, engineering. The engineering doc includes a **Testing strategy** section that the TDD skill reads. |
| **`eng-skills/`** | `test-driven-dev`, `gemini-api` | Engineering disciplines. `test-driven-dev` is the **required** TDD methodology — write → run → fix → re-run, max 3 iterations. `gemini-api` is a fallback for the official [`gemini-api-dev`](https://github.com/google-gemini/gemini-skills) skill. |
| **`ux-design-skills/`** | `cloud-pup`, `y2k-dreamcore` | Two specific visual identities you can apply to a frontend. Optional — use when you want a strong style. |

## Install in Antigravity (workspace-scoped)

Workspace-scoped install only affects the current project — no global pollution. From an open Antigravity workspace, paste this in the agent chat:

```
Please clone https://github.com/cuppibla/skills-garden into .agent/skills/skills-garden.
When Antigravity asks permission to run git clone, click Allow.
List the skills now available in this workspace when done.
```

Antigravity proposes the `git clone`, you click Allow once, and the skills are installed inside `<workspace>/.agent/skills/skills-garden/`. When the project folder is deleted, the skills go with it.

## Install globally (across all your Antigravity projects)

If you want these skills available in every workspace:

```bash
git clone https://github.com/cuppibla/skills-garden ~/.gemini/antigravity/skills/skills-garden
```

## Use a single skill from this repo

Once installed, just tell the agent what to apply:

```
Apply the eng-design-doc skill to generate engineering.md for the current project.
```

```
Apply the test-driven-dev skill. Use the Testing strategy section in engineering.md
as the test plan.
```

## The one required skill

If you're running the Coding Jam workshop or building anything serious: **`eng-skills/test-driven-dev`** is required, not optional. It's the discipline that catches mistakes before humans have to. Everything else in this repo is a tool you reach for when useful.

## Related

- [Coding Jam Starter](https://github.com/cuppibla/coding-jam-starter) — the 8-week workshop briefs
- [Official Gemini skills (Google)](https://github.com/google-gemini/gemini-skills) — `gemini-api-dev`, `gemini-live-api-dev`, `gemini-interactions-api`

## License

MIT — use, fork, remix freely.

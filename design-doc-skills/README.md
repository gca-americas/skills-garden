# Design Doc Skills

Three independent Claude/Antigravity skills that turn a raw brief into a proper design doc — like having a sharp PM, UX designer, and staff engineer on your team. Use one, two, or all three. They don't depend on each other.

## The three skills

| Skill | Role | Output |
|---|---|---|
| `pm-design-doc` | Senior PM who ships | A sharp PRD with brutal scope cuts and one magical moment |
| `ux-design-doc` | Senior product designer | A UX doc anchored to one defining interaction and every screen state |
| `eng-design-doc` | Senior staff engineer | A software design doc with architecture, trade-offs, rejected alternatives, and risks |

## How they work

Each skill is **independent**. Give the same raw brief to any of them (or all three) and each will produce its own self-contained doc.

```
        raw brief / bullet pitch / one-liner
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ pm-design-   │ │ ux-design-   │ │ eng-design-  │
│ doc          │ │ doc          │ │ doc          │
└──────────────┘ └──────────────┘ └──────────────┘
        │              │              │
        ▼              ▼              ▼
     PRD.md          UX.md       DESIGN.md
```

Each output is a single Markdown file. Git-friendly, diff-friendly, portable.

## Design principles

All three skills share the same philosophy:

- **Cut more than you add.** Each doc has a "what we are NOT building" section that's as long as the "what we are building" section.
- **Be specific.** No "users might want to..." — name the user, the moment, the number, the trade-off.
- **One signature thing.** PM defines the soul, UX defines the defining interaction, Eng defines the most interesting trade-off.
- **Short.** PM doc 1.5–3 pages, UX doc 2–4 pages, Eng doc 3–6 pages. Anything longer hasn't been edited yet.
- **Push back.** Each skill includes a "things to push back on" section so the role pushes back on weak briefs instead of nodding along.
- **Independent, not chained.** Each skill reads only the raw brief. The Eng skill doesn't assume a PRD exists; it makes its own assumptions and flags them. Same for UX.

## Installing in Antigravity / Claude Code

Clone the repo into your agent's skills directory (or wherever your setup pulls skills from):

```bash
git clone https://github.com/<your-username>/design-doc-skills.git
```

Each subdirectory is a self-contained skill with a `SKILL.md`. Antigravity (and Claude Code, and Claude.ai with skill upload) will discover them automatically based on the YAML frontmatter's `description` field.

## Using them

Once installed, they trigger on natural phrases:

- "PRD this idea" / "make this a product doc" / "let's PM this" → `pm-design-doc`
- "spec the UX" / "what does this look like" / "design this" → `ux-design-doc`
- "tech-spec this" / "how do we build this" / "system design" → `eng-design-doc`

Or invoke them explicitly:

> "Run all three skills on this idea — I want a PRD, UX doc, and eng doc."

Each runs on the same input and produces its own doc.

## Project structure

```
design-doc-skills/
├── README.md
├── pm-design-doc/
│   └── SKILL.md
├── ux-design-doc/
│   └── SKILL.md
└── eng-design-doc/
    └── SKILL.md
```

Each skill is one file. No dependencies, no scripts, no assets — just opinionated prompts.

## License

MIT.

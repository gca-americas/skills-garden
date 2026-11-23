# Codelab Skills

Skills that turn a working repo or demo into a publishable, **Google Codelabs-format**
tutorial — in Annie's house style: emoji-tagged sections, `👉`/`👉💻` action markers, a
`[READ ONLY]` architecture deep-dive that explains *every* concept, evidence-driven
verify checkpoints, and version-pinned snippets.

## The skill

| Skill | Input | Output |
|---|---|---|
| `codelab-from-repo` | A finished demo/starter repo, or a from-scratch idea | A single `CODELAB.md` in Devsite codelab format, ready to publish |

## How to use it to generate a codelab

Once installed (see *Installing* below), trigger it with natural phrases:

- "make a codelab from this repo"
- "turn my demo into a hands-on tutorial"
- "codelab for `<project>`"
- "write a hands-on guide from this codebase"

The skill then runs four phases (full detail in [`codelab-from-repo/SKILL.md`](codelab-from-repo/SKILL.md)):

1. **Ingest** — reads README, manifests, deploy scripts, examples, tests → a repo
   brief with **pinned versions** and the natural happy path.
2. **Design the arc** — picks one of two shapes and names every verify checkpoint *first*:
   - **Deploy & understand** *(default)* — clone → cloud setup → `[READ ONLY]`
     architecture → deploy → `[OPTIONAL]` play → conclusion. For a finished demo/starter repo.
   - **Build from a brief** — install → **Spec Talk** → design docs → implement & test
     → deploy. For a from-scratch / vibe-code session.
3. **Draft** — fills the matching scaffold from `references/codelab-template.md`.
4. **Verify** — runs `references/checklist.md` and fixes every miss before handing back.

You get a `<repo-slug>-codelab.md` (or `CODELAB.md`) in Devsite format. To steer it
explicitly:

> "Make a **deploy-&-understand** codelab from this repo for **intermediate** developers."

## How to add an example codelab as a reference

The skill produces *our* style by **imitating real codelabs** bundled under
[`codelab-from-repo/references/examples/`](codelab-from-repo/references/examples/). It
reads the example matching the chosen arc as its gold standard. To bias generation
toward a particular structure or voice, add your own — three steps:

1. **Drop the codelab `.md`** into `codelab-from-repo/references/examples/`, named by
   arc so it's obvious which shape it teaches:
   - `deploy-understand-<name>.md`
   - `build-from-brief-<name>.md`

   If the source has lots of double blank lines, squeeze them on the way in:

   ```bash
   cat -s path/to/source.md \
     > codelab-from-repo/references/examples/deploy-understand-<name>.md
   ```

2. **Register it** — add a row (file · arc · why it's here) to
   [`references/examples/README.md`](codelab-from-repo/references/examples/README.md)
   so the skill knows it exists and what to copy from it.

3. **Keep at least one complete example per arc.** A good reference has complete YAML
   frontmatter, the full section arc, real concept-explanation asides, and verify
   checkpoints — a codelab you'd actually publish.

> Examples are studied for **structure and wording**, not rendered — so unresolved
> `img/...` links inside a bundled example are fine. The two shipped examples
> (`deploy-understand-ai-motion-lab.md`, `build-from-brief-coding-jam.md`) are the
> canonical ones; the live published render is linked from that folder's README.

## Installing in Antigravity / Claude Code

Install the whole `skills-garden` repo (see the [top-level README](../README.md) for
the workspace-scoped and global commands). Agents discover `codelab-from-repo`
automatically from its `SKILL.md` frontmatter. Then just ask for a codelab in natural
language, as above.

## Project structure

```
codelab-skills/
└── codelab-from-repo/
    ├── SKILL.md                  # when to use it + the four-phase workflow
    └── references/
        ├── style-rules.md        # the house-style convention catalog
        ├── codelab-template.md   # fill-in scaffolds (one per arc)
        ├── checklist.md          # self-review before publishing
        ├── onboarding-guide.md   # why the rules exist (for new authors)
        └── examples/             # ← bundled reference codelabs: imitate these
            ├── README.md         #    what to copy + how to add your own
            ├── deploy-understand-ai-motion-lab.md
            └── build-from-brief-coding-jam.md
```

## License

MIT.

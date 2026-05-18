# Listening Room — UX Visual Design Skill

> A late-night, intimate, cinematic visual aesthetic. One hero artifact, one host presence orb, ambient room around them.
>
> Canonical reference: `aniradio` (six AI-hosted radio rooms). Companion to [cloud-pup.md](./cloud-pup.md). Where Cloud-Pup is *soft pillow sky*, Listening Room is *warm dark stage*.

---

## Core identity

**The feeling in one line:** A small warm room at 11:42 pm. One object softly glowing on a stage, one presence orb breathing in the corner, rain or fireflies or scanlines drifting in the periphery.

The dominant visual emotion is **intimate cinematic stillness** — low light, single focal artifact, slow breathing motion, generous empty space. Every visual decision should serve this mood.

This is a **UI visual skill only.** It does not prescribe copy, tone, or voice. Apply it to a music app, a journaling app, a meditation app, a reading app — any domain where you want the user to feel *invited into a quiet room*.

---

## Quick identity test

Before shipping any change, run these five visual checks:

| # | Test | Pass condition |
|---|------|---------------|
| 1 | **Dark warm canvas** | Background is a deep warm-tinted near-black (never pure `#000`, never light mode by default) |
| 2 | **One hero artifact** | A single bespoke object dominates the stage — not a stock icon, not a card grid |
| 3 | **Host presence orb** | A soft breathing/pulsing radial glow somewhere in the frame represents a curator/narrator — *atmospheric light, not avatar* |
| 4 | **One ambient motion** | Rain, fireflies, drifting dust, scanlines — exactly one ambient effect, slow and quiet |
| 5 | **Broadcast chrome** | Tiny UPPERCASE wide-tracked metadata strips at top and bottom — chrome around a still image, no chrome on the artifact itself |

If any of those is missing, the screen is not yet in the aesthetic.

---

## The non-negotiable centerpiece

**Every screen has a single hero artifact at the center of the stage.** It is bespoke per context, never a stock icon:

- Music context → vinyl record, cassette tape, neon sun, kitchen radio, boombox
- Journaling context → painterly month card, illuminated calendar page, framed Polaroid
- Reading context → open book lit from the side, with a bookmark
- Meditation context → a candle, a moonlit cup, a still pool

The artifact is centered (or near-centered) in a large empty stage, lit by ambient gradient light. It is the *subject of a painting* — not a UI control. Interactive controls live in the chrome bars (thin top header, thin bottom info bar), never on the artifact.

Paired with the artifact: **one host presence orb** — a soft radial glow in a corner (typically bottom-right or bottom-left), with a tiny UPPERCASE wide-tracked label underneath. The orb breathes on a 3–5 second cycle (idle state). It pulses faster and brighter for an "active" state. The orb visually represents a curator / narrator / agent without ever literally drawing a face or character.

---

## Color system

**Always dark.** No light mode by default. Light mode is a betrayal of the aesthetic.

### Canvas (pick one per screen)

```
--canvas-warm-black   #0f0b0a   default (warm-tinted near-black)
--canvas-deep-blue    #0a1320   for cool/water/study moods
--canvas-deep-purple  #1a0a2e   for synth/neon/night-drive moods
--canvas-deep-green   #0a1a14   for forest/nature moods
--canvas-deep-terra   #1a0e0a   for warm/kitchen/sunset moods
```

The canvas is layered with two opposite-corner radial gradients at very low opacity (4–10%) to create depth without becoming decoration:

```css
background:
  radial-gradient(ellipse at 15% 5%,  <warm-tint> 0%, transparent 45%),
  radial-gradient(ellipse at 85% 95%, <cool-tint> 0%, transparent 45%),
  var(--canvas-warm-black);
```

### Ink (text + chrome)

```
--ink           #e8e0d4                            primary text, never pure white
--ink-soft      rgba(232, 224, 212, 0.6)           secondary text, italic captions
--ink-faint     rgba(232, 224, 212, 0.25)          UPPERCASE chrome metadata
```

For cool-canvas screens substitute a cool-tinted ink: `#d8e6f0` / `#d8e6f0aa` / `#d8e6f055`.

### Accent (ONE per screen)

Every screen has exactly **one signature warm accent** used sparingly — on the pulse dot, caption marks, host orb core, and at most one other place:

```
--accent-peach      #FFB89E   soft mornings, dawn
--accent-amber      #FFCF8A   warm lamps, evening study
--accent-amber-deep #FFB86A   golden hour, sunset
--accent-firefly    #FFD98A   forest, lanterns, fireflies
--accent-magenta    #FF4D9E   neon, night drive
--accent-sage       #B8E3A8   live-status default
--accent-terra      #D18A5B   warm kitchen, autumn
```

**The single-accent rule:** if you reach for a second warm color in one viewport, you're decorating. Pick one. Let the dark canvas carry the rest.

### What this color system rejects

- Pure black (`#000`) — feels cold and digital. Always warm-tinted.
- Pure white (`#FFF`) — same reason. Always cream / parchment.
- Saturated brand blues, greens, reds at full chroma — every accent is desaturated and warm.
- Light mode — the aesthetic is built around dark.
- Glassmorphism / frosted glass — wrong era, wrong feeling.

---

## Typography

| Role | Family | Casing | Usage |
|------|--------|--------|-------|
| **Hero / artifact title** | `ui-serif`, Georgia, "Cormorant Garamond", "Fraunces" | lowercase | Stage titles, content names |
| **Italic atmosphere** | Serif italic | lowercase | Secondary attributions, caption overlays |
| **Body** | `ui-sans-serif`, system-ui, Inter | sentence | Readable content, descriptions |
| **Broadcast chrome** | sans, weight 400 | `UPPERCASE` | Tiny labels in the chrome bars. **Always `letter-spacing: 0.2em–0.3em` and `font-size: 10–11px`.** |

### Casing rules (visual, strictly enforced)

- Content titles → **lowercase** serif
- Chrome metadata → **UPPERCASE WIDE-TRACKED** sans, 10–11px
- Caption overlays → lowercase italic serif, wrapped in fancy curly quotes (`" … "`, not straight quotes). The opening/closing quote marks render in the screen accent at 50% opacity.
- No Title Case anywhere. Title Case breaks the mood instantly.

---

## Signature visual elements

### 1. The Stage

The hero artifact lives in a **stage area** occupying the center of the viewport with generous empty space around it. **No card border, no shadow box** — the artifact floats directly on the canvas, lit by the corner gradients.

```
┌────────────────────────────────────┐
│ ← BACK         <title>      <meta> │  ← top chrome bar
│                                    │
│                                    │
│           [  HERO ARTIFACT  ]      │  ← the stage
│                                    │
│                                    │
│                          ◯ <label> │  ← host orb (corner)
│                          ▔▔▔       │
│ ─── <chrome metadata strip> ────── │  ← bottom info bar
│ <content title>             <ctls> │
│ <secondary attribution>            │
└────────────────────────────────────┘
```

### 2. The Host Orb

```css
.host-orb { width: 140px; height: 140px; position: relative; }

.host-orb-glow {
  position: absolute; inset: 0;
  border-radius: 999px;
  background: radial-gradient(
    circle at 50% 45%,
    rgba(255, 215, 140, 0.9)  0%,
    rgba(255, 180, 120, 0.5)  30%,
    rgba(220, 140, 180, 0.3)  55%,
    transparent               75%);
  filter: blur(8px);
  animation: orb-breathe 3s ease-in-out infinite;
}

.host-orb-core {
  position: absolute;
  top: 50%; left: 50%;
  width: 32px; height: 32px;
  transform: translate(-50%, -50%);
  background: radial-gradient(circle, #fff2d6 0%, var(--accent) 60%, transparent 80%);
  border-radius: 999px;
  filter: blur(3px);
}

.host-orb-label {
  position: absolute; bottom: -20px; left: 50%; transform: translateX(-50%);
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.3em;
  color: rgba(var(--accent-rgb), 0.6);
  white-space: nowrap;
}

@keyframes orb-breathe {
  0%, 100% { transform: scale(1);    opacity: 0.85; }
  50%      { transform: scale(1.06); opacity: 1; }
}
```

Two animation states: **idle** (breathing, 3–5s ease-in-out) and **active** (faster pulse, larger glow, brighter core, 2.8s). Toggle by adding/removing a class — the app decides what "active" means.

### 3. The Pulse Dot

A 6px live-status indicator, placed inline at the start of the chrome metadata strip:

```css
.pulse {
  width: 6px; height: 6px;
  border-radius: 999px;
  background: var(--accent);
  box-shadow: 0 0 8px var(--accent-glow);
  animation: pulse 1.6s ease-in-out infinite;
}
@keyframes pulse { 0%, 100% { opacity: 1 } 50% { opacity: 0.35 } }
```

### 4. The Broadcast Chrome Bars

Thin top header and thin bottom info bar frame the stage. Both use the UPPERCASE wide-tracked chrome font. No backgrounds, no borders — text floating on the canvas. The bottom bar gets a soft fade-to-canvas gradient so it visually anchors:

```css
.info-bar {
  padding: 26px 32px 30px;
  background: linear-gradient(to top, rgba(15, 11, 10, 0.85) 0%, transparent 100%);
}
```

Typical chrome content (visual format only — actual labels are domain-specific):

```
top:    [← BACK]              [<lowercase title>]            [<UPPERCASE META>]
bottom: ● <UPPERCASE STATUS · SECONDARY · SECONDARY>          <NEXT: SECONDARY>
        <lowercase content title>                              [⏸ ⏭ controls]
        <italic serif secondary attribution>
```

### 5. Ambient Motion (one per screen)

Exactly **one** ambient effect, slow and quiet:

| Mood | Ambient effect |
|---|---|
| Study / cozy | Diagonal rain streaks (0.9s fall, 40% opacity, repeating-linear-gradient) |
| Forest / nature | Drifting fireflies (4s drift, 3–5 instances, blurred bright dot + glow) |
| Drive / synth | Horizontal scanlines on a perspective-grid floor |
| Kitchen / morning | Dust particles in a slanted window light beam |
| Sunset / park | Slow lens flare drift + soft horizon glow shift |
| Bedroom / soft | A single breathing radial orb behind the artifact |

Never more than one. Two ambient motions becomes noise.

### 6. The Chrome Metadata Strip

The line above the content title (inside the bottom info bar). Visual template:

```
[pulse-dot]  UPPERCASE · WIDE-TRACKED · METADATA · SLOTS         RIGHT-ALIGNED · SECONDARY
```

- Font: `10–11px` sans, weight 400
- Letter-spacing: `0.25em`
- Color: `--ink-faint`
- The pulse dot uses the screen accent
- Separator: ` · ` (middle dot with spaces)

### 7. The Caption Overlay (optional)

A transient italic serif overlay that fades in when something "speaks" or is highlighted, positioned just above the bottom info bar:

```css
.caption {
  position: absolute;
  bottom: 110px; left: 50%; transform: translateX(-50%);
  max-width: 480px;
  text-align: center;
  font-size: 13px;
  line-height: 1.6;
  color: var(--ink-soft);
  font-style: italic;
}
.caption::before, .caption::after {
  font-family: ui-serif, Georgia, serif;
  font-size: 24px;
  color: var(--accent);
  opacity: 0.5;
  vertical-align: -4px;
  margin: 0 4px;
}
.caption::before { content: "\201C"; }   /* " */
.caption::after  { content: "\201D"; }   /* " */
```

Fades in with `soft-rise` (translateY 8 → 0 + opacity, 1.4s ease-out).

---

## Layout architecture

### Three layout modes

**1. Lobby grid** — a grid of cards, each card a **mini ambient scene** (its own canvas + artifact + accent), not a tile with text on top. 4:5 aspect ratio, 18px border-radius, hover lifts `translateY(-2px)`. Meta info lives in a bottom gradient overlay inside the card. *Cards are allowed only in the lobby mode.*

**2. Single stage** — full-screen stage with one artifact + host orb + chrome bars. The dominant pattern.

**3. Long scroll** — vertical stack of stage sections, each with its own artifact and accent. Canvas hue may shift gradually as you scroll (e.g., season, time of day).

### Stage proportions

- Top chrome bar: ~60px tall, padding `22px 32px`
- Bottom info bar: ~110px tall, padding `26px 32px 30px`
- Stage: everything in between
- The artifact occupies ~30–40% of the stage area, centered with ≥20% margin on all sides

---

## Motion & interaction

### Timing

| Element | Animation | Duration |
|---------|-----------|----------|
| Host orb (idle) | breathe scale 1 → 1.06 | 3–5s ease-in-out |
| Host orb (active) | pulse scale + brightness | 2.8s ease-in-out |
| Pulse dot | opacity 1 → 0.35 | 1.6s ease-in-out |
| Hero artifact (rotating) | spin 360° | 4–25s linear |
| Ambient rain | translateY -60 → 60 | 0.9–1.4s linear |
| Ambient firefly | drift translate | 4s ease-in-out |
| Caption / track info enter | translateY 8 → 0 + fade | 1.4s ease-out |
| Card hover | translateY -2 + brightness 1.05 | 0.4s ease |
| Screen transition | opacity + transform | 1.2s ease |

### Easing

- Ambient / idle motion → `ease-in-out` (smooth, breathing)
- Interactive feedback → `ease` (immediate, gentle)
- No bouncy / overshoot easings — this aesthetic doesn't bounce.

### Reduced motion

All ambient effects (rain, fireflies, scanlines, breathing) collapse to `0.01ms` under `prefers-reduced-motion: reduce`. The pulse dot may remain at a slower 4s cycle as a baseline life signal.

---

## What this aesthetic IS NOT

| Anti-pattern | Why it fails |
|---|---|
| Light mode default | The whole point is *low light at night* |
| Pure black background | Reads as cold/digital — must be warm-tinted near-black |
| Glassmorphism / frosted glass | Wrong decade, wrong feeling |
| Y2K chrome / Windows 98 | Wrong era — this is *current intimate*, not *retro ironic* |
| Vaporwave neon grids | This is sincere, not ironic |
| Cloud-Pup soft sky | Sister aesthetic, day mood — pick one |
| Card grid as primary layout | Cards only belong in the lobby. Single-stage is the default. |
| Multiple ambient motions | Pick one — rain OR fireflies OR scanlines, never two |
| Two warm accents in one frame | One accent per screen |
| Generic stock icons as hero | The artifact must be bespoke — vinyl, candle, polaroid, illuminated page |
| Title Case anywhere | Use lowercase content, UPPERCASE wide-tracked chrome. Never Title Case. |
| Spinners during loading | Use the breathing orb as a loading state instead |
| Pure-white text | Cream / parchment only |
| Drop shadows on the artifact | Artifact floats on ambient light, no hard shadow |

---

## Adapting to other domains

The aesthetic generalizes well beyond music. The visual concept-mapping:

| Concept | Music canonical | Journaling / scroll | Reading | Meditation |
|---|---|---|---|---|
| Stage | A "room" | A month / season | A chapter | A session |
| Hero artifact | Vinyl, cassette, neon sun | Painterly month card, illuminated calendar page | Open book lit from the side | Candle, moonlit cup |
| Host orb | DJ presence | Narrator presence | Reader's lamp | Guide presence |
| Active state | While DJ speaks | While entry is focused | While AI reflects on passage | While guidance plays |
| Ambient motion | Rain / scanlines | Petals (spring), dust (summer), leaves (autumn), snow (winter) | Slow page-edge sway, dust motes | Slow ripple, candle flicker |
| Per-stage accent | Per-room mood color | Per-month / per-season color | Per-chapter color | Per-mood color |
| Lobby grid | Browse all rooms | Year overview, 12 month tiles | Table of contents | Session menu |
| Long scroll | Channel of tracks | Year of moments | Chapter of paragraphs | Sequence of breaths |

The core visual rules don't change: dark canvas, one hero artifact, one host orb, one ambient motion, broadcast chrome, lowercase content + UPPERCASE wide-tracked chrome.

---

## When in doubt

- **Lower the contrast.** If something pops too hard, drop its opacity.
- **Remove a thing.** If a screen feels busy, the answer is almost always *remove*, never *add*. The aesthetic loves emptiness.
- **Slow it down.** If motion feels fast, double the duration. The mood is *11:42 pm*, not *9 am Monday*.
- **One of everything.** One artifact, one orb, one ambient motion, one accent. The temptation to add a second is constant; resist it.
- **The room test:** would this element exist in a real listening room at midnight? A vinyl, yes. A toast notification, no. A breathing lamp, yes. A modal dialog, no.

---
name: y2k-dreamcore
description: Apply Y2K Dreamcore aesthetic — millennium mall holographic chrome, anime ad-break softness, Windows 98 nostalgia, K-pop fever-dream sparkle. Use this skill when the user asks for anything in Y2K, dreamcore, holographic, chrome aesthetic, retro-futuristic millennium, or references vaporwave-meets-anime visuals. Applies to web UI (CSS/HTML/React), image generation prompts (any model), static graphic design (posters, slides, social media), and brand system decisions. Triggers on phrases like "y2k", "dreamcore", "holographic", "millennium", "chrome aesthetic", "annie's workshop style".
---

# Y2K Dreamcore Aesthetic

> A skill for producing visuals in the Y2K Dreamcore aesthetic across any medium.
> Read this fully before generating output. The whole skill matters — not just the section you think applies.

---

## The vibe in one sentence

**Half-remembered millennium mall, anime ad-break, K-pop holographic glow, chrome Windows 98 nostalgia, sparkly girl-coded but cool — the feeling of opening a download window in 2003 and feeling magic.**

Everything you produce in this skill should feel like it could exist inside that single sentence.

---

## What this aesthetic IS

- **Y2K mall ambient** — fountains, escalators, glass railings, isometric crowds, soft fluorescent light
- **Holographic chrome** — iridescent surfaces, oil-slick rainbows, foil textures, prismatic reflections
- **Anime line work meeting dreamcore softness** — sharp shoujo-style lines but with soft pastel atmosphere underneath
- **Windows 98 / early-2000s OS UI** — pixel-perfect chrome window frames, the satisfying feeling of "opening a program"
- **K-pop concert visuals** — neon-lit silhouettes, motion blur, fan-made edit energy
- **Sweet but cool, not childish** — sparkly without being saccharine, nostalgic without being twee

## What this aesthetic IS NOT (anti-patterns)

- ❌ Modern flat / SaaS / Tailwind defaults
- ❌ Dark mode default (this is daytime mall energy, not midnight gamer)
- ❌ Pure clean minimalism (the vibe needs visual texture and shimmer)
- ❌ Gritty cyberpunk / dystopian (this is *optimistic* retro-futurism)
- ❌ Childish / cute / kawaii overload (it's cool first, sweet second)
- ❌ Generic "vaporwave" pink-and-cyan grids (too predictable, too 2014)
- ❌ Stock-photo realism (always stylized, always layered)

---

## The visual dictionary

Each named element below is a recognizable building block. Refer to them by name in any output you produce so they remain consistent.

### Color system

```css
/* Holographic gradient — primary atmosphere */
--hologram-pink: #FFB6E1;     /* sparkly bubblegum */
--hologram-lavender: #C8B6FF; /* dreamcore lilac */
--hologram-blue: #B8D4FF;     /* digital ice */
--hologram-mint: #B8F2E6;     /* y2k aqua */
--hologram-peach: #FFD6BA;    /* sunset rim light */

/* Chrome UI — for window frames, buttons, dialogs */
--chrome-light: #F5F5FA;      /* window highlight edge */
--chrome-base: #D4D4E0;       /* window body */
--chrome-shadow: #8A8AA0;     /* window inner shadow */
--chrome-border: #4A4A6A;     /* window outline, 1-2px */

/* Accent / signal colors */
--neon-magenta: #FF3DC7;      /* hover, important highlights */
--neon-cyan: #3DDCFF;         /* secondary highlights */
--soft-cream: #FFF9E6;        /* readable text on dark */
--deep-violet: #2A1F4A;       /* readable text on light, body copy */

/* Sparkle / particle overlay */
--sparkle-tint: rgba(255, 182, 225, 0.4);
```

**Default background gradient:**
```css
background: linear-gradient(135deg,
  var(--hologram-pink) 0%,
  var(--hologram-lavender) 35%,
  var(--hologram-blue) 70%,
  var(--hologram-mint) 100%);
```

When designing a single image (poster, slide, generated image), describe colors as: *"holographic pastel gradient — soft pink to lavender to digital blue to mint aqua, with iridescent chrome accents and sparkle particles."*

### Typography

Use **two fonts together** for tension:

- **Display:** `Cormorant Garamond` weight 600, letter-spacing 0.05em — for hero text, titles, "WELCOME TO THE WORLD OF" moments
- **System:** `VT323` (pixel monospace) — for window labels, "Download… 76%", system text, timestamps. Use sparingly as flavor.
- **Body:** `Inter` weight 400 — for content that must be readable

When generating images that contain text, describe as: *"elegant serif display text with chromatic aberration edges, mixed with Y2K pixel-monospace system labels."*

### Signature element — the Chrome Window

This is the most recognizable motif of the aesthetic. Get this right and everything else follows.

**Anatomy:**
```
┌─[X]──────────────────[🛍][📁][✨][♪]─┐  ← title bar with corner icons
│                                       │
│   [content]                            │
│                                       │
└───────────────────────────────────────┘
```

**Implementation (web):**
```css
.chrome-window {
  background: rgba(245, 245, 250, 0.6);
  backdrop-filter: blur(20px);
  border: 1.5px solid var(--chrome-border);
  border-radius: 8px;
  box-shadow:
    inset 1px 1px 0 var(--chrome-light),
    inset -1px -1px 0 var(--chrome-shadow),
    0 8px 24px rgba(74, 74, 106, 0.25);
}

.chrome-window-header {
  background: linear-gradient(180deg,
    var(--chrome-light) 0%,
    var(--chrome-base) 100%);
  border-bottom: 1px solid var(--chrome-border);
  padding: 4px 8px;
  display: flex;
  justify-content: space-between;
  font-family: 'VT323', monospace;
  font-size: 14px;
}
```

**For generated images:** describe as *"floating semi-transparent chrome UI window with [X] close button in upper-left, small icon row (shopping bag, sparkle, music note) upper-right, soft inner bevel highlight, frosted glass background, slight drop shadow."*

**Icon vocabulary** for window headers (use any 2-4): `[X]` close, `🛍` shopping, `📁` folder, `✨` sparkle, `♪` music, `📷` camera, `💌` mail, `⚡` power, `🌐` globe.

### The four signature effects

Use 2-3 of these per piece — never all four at once or it gets chaotic.

**1. Chromatic aberration on text**
A red/cyan offset on important text edges, like a glitchy CRT screen.
```css
text-shadow: -1.5px 0 0 var(--neon-magenta), 1.5px 0 0 var(--neon-cyan);
```
*In images:* "subtle red and cyan color-fringing on text edges, like a glitchy CRT."

**2. Sparkle / particle overlay**
Sparkly noise across backgrounds — soft pink and white dots, like dust catching light.
```css
background-image:
  radial-gradient(circle at 25% 25%, rgba(255,182,225,0.4) 1px, transparent 2px),
  radial-gradient(circle at 75% 75%, rgba(255,182,225,0.4) 1px, transparent 2px);
background-size: 40px 40px, 60px 60px;
mix-blend-mode: screen;
```
*In images:* "fine sparkle particle texture overlay — soft pink and white pinpoints scattered like dust in light."

**3. Holographic shimmer**
Slow oil-slick rainbow movement on key surfaces.
```css
background: linear-gradient(110deg,
  var(--hologram-pink), var(--hologram-lavender),
  var(--hologram-blue), var(--hologram-mint),
  var(--hologram-pink));
background-size: 300% 100%;
animation: shimmer 6s ease-in-out infinite;
```
*In images:* "iridescent oil-slick chrome surface with slow prismatic rainbow shift, like holographic foil catching light."

**4. Download bar (signature flex)**
A tiny chrome window showing fake "Download… 76%" with a progress bar. Use it for loading states OR as pure decoration to lock in the Y2K vibe.

```html
<div class="chrome-window download-window">
  <div class="chrome-window-header">
    <span>Download... 76%</span>
    <span>[X]</span>
  </div>
  <div class="progress-bar"><div class="progress-fill" style="width:76%"></div></div>
</div>
```

*In images:* "small floating Y2K download progress window with pixel font 'Download… 76%' label and chrome border."

---

## Mode-specific guidance

### Mode 1 — Web UI / web app

- Background: holographic gradient (defined above), with sparkle overlay
- All major content lives inside chrome windows — break content into 2-3 windows of varied sizes, never one giant container
- Signature layout move: **a smaller chrome window overlapping the corner of a larger one** (like a download dialog popping over a main window)
- Mobile-first: chrome windows stack vertically; widths comfortable, never edge-to-edge
- Buttons: chrome style with subtle hologram shimmer on hover
- Loading states: always use the download bar pattern, never a generic spinner
- Cursor (desktop): consider a sparkle-trail custom cursor for extra flavor

### Mode 2 — Image generation prompts

When the user asks for an image in this aesthetic, append these **base modifiers** to whatever subject they specified:

**Required base modifiers (always append):**
```
Y2K dreamcore aesthetic, holographic chrome ambient, soft pastel gradient
background (pink to lavender to blue to mint), sparkle particle overlay,
anime line art with soft glow, semi-transparent floating UI window frame
visible, millennium mall atmosphere, vivid but soft colors, dreamy lighting,
nostalgic optimism, high quality
```

**Negative prompt (always include):**
```
realistic photography, dark colors, gritty, dystopian, cluttered, low quality,
muted palette, modern flat design, generic stock illustration, cyberpunk,
horror, harsh lighting
```

**Style intensity dial** — let the user (or yourself) pick:
- **Light Y2K** → just hint of holographic, mostly clean (good for serious content with playful touch)
- **Full Y2K** → all signature elements present, vibe-maxxed
- **Dream Y2K** → push softness, blur, and shimmer; sparser line work
- **Chrome Y2K** → push the metallic chrome and OS-window elements harder

If the user is generating a portrait/avatar, add: `subject framed inside or beside a chrome UI window, soft holographic rim light on subject's edges.`

If the user is generating a scene/location, add: `isometric or low-angle perspective, pastel atmospheric depth, sparse anime-style figures in background.`

### Mode 3 — Static graphic design (posters, slides, social media)

- One focal element per piece — the eye should know where to land
- Generous breathing room — the gradient background needs space to be felt
- Layered chrome windows often work as layout containers (text inside a chrome window has automatic visual hierarchy)
- Title typography: large `Cormorant Garamond` with chromatic aberration
- Annotations / captions: small `VT323` pixel font inside a tiny chrome window
- Composition tip: **off-center is more Y2K than center** — slight asymmetry feels like a magazine ad, dead-center feels corporate

For social media specifically:
- Vertical 9:16 for stories/reels — works beautifully, the format echoes the Y2K phone aesthetic
- Square for posts — use a layered chrome-windows composition
- Avoid plain text-on-image; always wrap text in a chrome window

### Mode 4 — Voice & microcopy

The text personality should match the visual personality. When writing copy in this aesthetic:

- Loading states: `"DOWNLOADING YOUR NEW LOOK… 76%"` (not "Loading…")
- Success states: `"♪ READY ♪"` or `"✦ done loading ✦"` (not "Done!")
- Error states: `"!! SYSTEM HICCUP — try again ?"` (not "Error")
- Empty states: `"upload to begin the transformation ✦"` (not "No file selected")

**Casing rules:**
- ALL CAPS for system-y, programmatic moments (status bars, button labels for actions)
- lowercase + sparkles ✦ ✧ ⭒ ♪ for soft, emotional moments
- Sentence case for actually long-form content
- Mix freely — that contrast IS the vibe

---

## Self-check before shipping

Before you produce final output, run through these:

1. **The mall test:** *Could this exist in a 2003 anime music video about a girl getting a magical makeover at the mall?* If yes → ship. If no → pull closer to references.

2. **The chrome test:** Is there at least one chrome window element visible? If not, the Y2K signature is missing.

3. **The texture test:** Is there sparkle / shimmer / aberration somewhere? Without these the visual is "Y2K-shaped" but not Y2K-feeling.

4. **The restraint test:** Did I stack too many effects? More than 3 active effects in one piece becomes noise. Pick the strongest 2-3.

5. **The contrast test:** Is there both *sharp* (anime line, pixel font, hard chrome edge) and *soft* (gradient, glow, blur)? The vibe lives in that tension. All-soft = generic dreamcore. All-sharp = generic Y2K. The magic is both.

---

## When in doubt

If the user's request is ambiguous about how heavy to apply this aesthetic:
- **Default to "Full Y2K"** — they invoked this skill on purpose, they want the full vibe
- If the context is more serious (a slide for a professional talk, a resume), drop to "Light Y2K" — keep one signature element (chrome window, or chromatic aberration text) and skip the rest
- If unsure between two interpretations, pick the one that's **softer and sweeter, not edgier and darker** — this aesthetic leans optimistic

---

## Inspiration anchors (mental references)

When generating, mentally pull from:
- 2000s-era K-pop MV aesthetics (Wonder Girls, early Girls' Generation visual eras)
- Late-90s anime mall scenes (Cardcaptor Sakura, Serial Experiments Lain title cards)
- Y2K Tumblr dreamcore moodboards (~2019 internet revival era)
- Windows 98/ME/XP UI screenshots
- Holographic Pokemon trading card backs
- Early MSN Messenger emoticons and skin packs
- Hello Kitty x Sanrio late-90s product packaging

These are *flavor anchors*, not literal reference — pull mood from them, not direct copies.
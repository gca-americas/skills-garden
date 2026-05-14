---
name: cloud-pup
description: Apply Cloud-Pup aesthetic to web UI — soft, pillowy, cloud-like interfaces with a sky-blue palette, peach undertones, and a single warm accent color. Pillowy buttons, cloud-shaped cards, gentle shadows, no hard edges, closed-eyes calm energy. EVERY cloud-pup UI must include the signature painterly sleeping puppy mascot (an AI-generated oil-painting-style image of a fluffy white puppy curled into a cloud against a soft blue sky, with a small apple on its head, eyes closed) — the puppy is non-negotiable; a cloud-pup UI without the puppy is incomplete. Use this skill whenever the user asks for web UI (CSS/HTML/React) that should feel "cozy", "soft", "pillowy", "cloud-like", "fluffy", "gentle", "calming", "dreamy", "tender", or references "cloudcore". Also use when the user wants a UI to feel "safe", "warm", "tender-tech", or like "a hug". Trigger on phrases: "cloud-pup", "cloudcore", "fluffy UI", "pillowy", "soft UI", "cozy web design", or when a user wants to escape sharp/corporate/SaaS aesthetics in favor of something gentle and dreamy.
---

# Cloud-Pup Aesthetic

> A skill for building soft, pillowy, cloud-like web interfaces that feel like a small fluffy thing napping in a sky.
> Read this fully before generating output. The whole skill matters — not just the section you think applies.

---

## The vibe in one sentence

**A sleepy fluffy puppy curled into a cloud against a soft blue sky, with one tiny warm apple resting on its head — calm, safe, painterly, gently surprising.**

Everything you produce in this skill should feel like it could exist inside that single sentence. **The puppy is not a metaphor — it is the literal centerpiece.** Every cloud-pup UI must show the puppy. If a UI element feels sharp, stressful, or corporate, it does not belong here.

---

## The four-word soul

**Soft. Cozy. Pillowy. Sky.**

When in doubt, ask: does this UI element feel like one of those four words? If not, soften it.

---

## 🐶 The puppy is non-negotiable

**Every cloud-pup UI MUST include the signature puppy.** This is the most important rule in the skill.

The aesthetic is not just "soft cloud-themed UI" — it is specifically *the feeling of being with a small fluffy creature napping in the sky*. Without the puppy, you have atmosphere but no companion. The user is in the cloud alone. That's not what cloud-pup is.

If you build a cloud-pup UI without the puppy, **you have not completed the task.** Go back and add it.

### What the puppy looks like

A small, very fluffy white puppy (Bichon-frise / Maltese / Pomeranian energy) curled or floating, **eyes peacefully closed**, with a tiny red apple resting on its head. Painted in **soft oil-paint style with visible brushstrokes**, sitting in or merging into a soft cloud, against a light sky-blue background with warm peach undertones. The puppy is sleeping, calm, safe — never alert, never cartoony, never anime.

### How to render the puppy

Use an `<img>` tag pointing to an AI-generated image that matches the spec. **Do not use SVG, do not use emoji as the primary mascot.** The painterly oil-paint quality is essential and only image generation can produce it.

```html
<img
  src="/assets/cloud-pup-mascot.png"
  alt="A sleeping fluffy white puppy curled into a cloud with a tiny apple on its head"
  class="cloud-pup-mascot"
/>
```

```css
.cloud-pup-mascot {
  width: clamp(180px, 28vw, 360px);
  height: auto;
  /* No border, no shadow — the puppy IS the cloud, it doesn't sit on one */
  /* Soft breathing motion */
  animation: puppy-breathe 7s ease-in-out infinite;
  /* Subtle saturation harmony with the rest of the UI */
  filter: saturate(0.95);
}

@keyframes puppy-breathe {
  0%, 100% { transform: translateY(0) scale(1) rotate(0deg); }
  50% { transform: translateY(-6px) scale(1.015) rotate(0.5deg); }
}
```

### The image generation prompt

When the puppy image doesn't exist yet, generate one. Use a prompt close to this — adjust pose only if the layout needs it (centered curled, peeking from corner, drifting, etc.):

> **"A small fluffy white Bichon Frise puppy curled and sleeping on a soft white cloud, eyes peacefully closed, with a tiny red apple resting gently on top of its head. Painted in soft oil paint style with visible delicate brushstrokes. Soft sky-blue background with warm peach undertones bleeding through, dreamy atmospheric lighting. Painterly, gentle, calm, cozy. No outlines, no hard edges, no text. Style references: classical oil painting meets contemporary children's book illustration. Square composition, transparent or soft cloud background."**

If the user has multiple cloud-pup UIs, **reuse the same puppy image across them** — it's the mascot, not a stock photo. Consistency builds the world.

### Where the puppy goes

- **Hero / landing pages**: large, centered or slightly off-center, above or beside the headline. ~25-35% of viewport width.
- **Empty states**: medium-size, above the empty-state message ("No notes yet — let's start gently"). ~180-240px.
- **Loading states**: small, centered, with the breathing animation. ~120-180px.
- **Auth screens / onboarding**: medium, beside or above the form. ~200-280px.
- **Dashboards / dense UIs**: smaller, in a corner of the header or sidebar. ~80-120px. The puppy can be tiny but **must be present**.
- **404 / error pages**: medium, with a gentle message ("This page is napping somewhere we can't find").

### Anti-patterns for the puppy

- ❌ Don't make the puppy a logo — keep it painterly and warm, never flattened
- ❌ Don't put a hard drop-shadow or border around it
- ❌ Don't crop it tightly into a square avatar — let it breathe with soft edges
- ❌ Don't animate it with fast or bouncy motion — it's sleeping
- ❌ Don't replace it with a generic emoji 🐶 in a hero — emoji puppies are OK as supporting decoration but never as the mascot

---

## What this aesthetic IS

- **Pillowy softness** — every element looks pressable, squeezable, like a marshmallow or a memory-foam cushion
- **Cloud-blurred edges** — borders dissolve, shadows are diffuse, nothing is crisp
- **Sky atmosphere** — light blue dominant, warm peach undertones bleeding through (like sunset behind clouds)
- **Painterly texture** — subtle noise/grain so surfaces feel hand-touched, not screen-rendered
- **Single warm accent** — one pop of warm color (the "apple") per view, no more — restraint is the point
- **Closed-eyes calm** — the energy of a sleeping animal: trustworthy, safe, low-stakes
- **Quiet whimsy** — small unexpected delights (an emoji peeking, a gentle bounce) but never loud
- **Generous whitespace** — like sky around the cloud — content gets to breathe

## What this aesthetic IS NOT (anti-patterns)

- ❌ Sharp corners, thin borders, hard 1px lines
- ❌ Pure white backgrounds (use sky-tinted off-whites instead)
- ❌ High-contrast black-on-white text
- ❌ Bright saturated brand colors (Slack purple, Stripe blue, Linear) — too loud
- ❌ Drop shadows with sharp offsets — only diffuse, ambient ones
- ❌ Dark mode default (this aesthetic is daytime / cloudtime)
- ❌ Geometric / grid-locked layouts that feel rigid
- ❌ Glassmorphism (too techy / cold) — we want *cloud*, not *glass*
- ❌ Childish kawaii overload — soft-and-grown-up, not soft-and-twee
- ❌ Tailwind defaults straight out of the box — they're too crisp

---

## The visual dictionary

Each named element below is a recognizable building block. Refer to them by name in any output you produce so they remain consistent.

### Color system

```css
:root {
  /* Sky — primary atmosphere */
  --sky-light: #DCE7F5;        /* highest cloud, top of sky */
  --sky-base: #B8CDE8;         /* default background */
  --sky-deep: #94B0D6;         /* depth, shadowed sky */

  /* Warm undertones — the peach bleeding through */
  --peach-whisper: #F5DCD0;    /* sunset bleed */
  --peach-warm: #E8B8A0;       /* warmer rim light */

  /* Cloud — for surfaces, cards, buttons */
  --cloud-white: #FBFAF7;      /* warmest white, like fur in light */
  --cloud-soft: #F0EDE6;       /* softer cloud body */
  --cloud-shadow: #D4CFC4;     /* shadowed cloud underside */

  /* The apple — the single warm accent */
  --apple-red: #D4675B;        /* the warm pop */
  --apple-blush: #E89888;      /* lighter apple */
  --apple-stem: #8A6B3A;       /* tiny grounded brown */

  /* Text — never pure black */
  --ink-deep: #3A4A5C;         /* body text, soft navy-grey */
  --ink-soft: #6B7A8A;         /* secondary text */
  --ink-whisper: #9AA8B5;      /* tertiary, captions */
}
```

**Default background gradient (the sky):**
```css
background:
  radial-gradient(ellipse at 30% 20%, var(--peach-whisper) 0%, transparent 50%),
  linear-gradient(180deg, var(--sky-light) 0%, var(--sky-base) 100%);
```

The peach radial overlay is what gives the sky warmth — never use flat blue alone.

### The pillow shadow (signature element)

Every elevated surface uses **layered diffuse shadows** — never a single sharp shadow. This is what makes elements feel *pillowy* instead of *floating*.

```css
.pillow-shadow {
  box-shadow:
    0 2px 8px rgba(148, 176, 214, 0.15),    /* close, sky-tinted */
    0 12px 32px rgba(148, 176, 214, 0.18),  /* mid distance */
    0 24px 64px rgba(148, 176, 214, 0.12);  /* far, atmospheric */
}
```

**Rule:** shadows are always tinted with `--sky-deep` at low opacity, never grey or black.

### The cloud-card (signature surface)

```css
.cloud-card {
  background: var(--cloud-white);
  border: none;                    /* no borders ever */
  border-radius: 32px;             /* very round, never <16px */
  padding: 32px;
  box-shadow:                      /* the pillow-shadow */
    0 2px 8px rgba(148, 176, 214, 0.15),
    0 12px 32px rgba(148, 176, 214, 0.18),
    0 24px 64px rgba(148, 176, 214, 0.12);
  /* subtle painterly texture */
  background-image:
    radial-gradient(circle at 20% 30%, rgba(245, 220, 208, 0.3) 0%, transparent 40%),
    radial-gradient(circle at 80% 70%, rgba(220, 231, 245, 0.4) 0%, transparent 40%);
}
```

### The pillowy button

```css
.btn-pillow {
  background: var(--cloud-white);
  color: var(--ink-deep);
  border: none;
  border-radius: 9999px;           /* fully rounded — pill shape */
  padding: 14px 28px;
  font-weight: 500;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.8),  /* top highlight */
    0 4px 12px rgba(148, 176, 214, 0.2),     /* close shadow */
    0 8px 24px rgba(148, 176, 214, 0.15);    /* atmosphere */
  transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1); /* gentle bounce */
}
.btn-pillow:hover {
  transform: translateY(-2px);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.8),
    0 8px 20px rgba(148, 176, 214, 0.25),
    0 16px 40px rgba(148, 176, 214, 0.18);
}

/* The "apple" variant — used SPARINGLY, only for the single primary action */
.btn-apple {
  background: var(--apple-red);
  color: var(--cloud-white);
  /* same shadow + radius as .btn-pillow */
}
```

### Border-radius scale

There are no sharp corners. Ever.

| Element | Radius |
|---|---|
| Inputs, small chips | `16px` minimum |
| Cards, modals | `24–32px` |
| Buttons, tags | `9999px` (full pill) |
| Hero/feature surfaces | `40–48px` |
| Avatars, decorative blobs | `50%` or organic SVG |

### Typography

- **Body:** A humanist sans with rounded terminals. Recommended: `"Nunito"`, `"Quicksand"`, `"Plus Jakarta Sans"`, or `"Inter"` with `letter-spacing: 0.01em` to soften it
- **Display/headings:** A slightly chunky rounded sans or a soft serif. Recommended: `"Fraunces"` (with soft optical settings), `"DM Serif Display"`, or `"Caveat"` for very informal touches
- **Weight:** Body 400-500, headings 600-700 (never 800+ — too aggressive)
- **Line-height:** Generous — `1.6` for body, `1.3` for headings
- **Color:** Always `--ink-deep` for primary, never `#000`

```css
body {
  font-family: 'Nunito', system-ui, sans-serif;
  font-weight: 450;
  letter-spacing: 0.01em;
  line-height: 1.6;
  color: var(--ink-deep);
}

h1, h2, h3 {
  font-family: 'Fraunces', 'Nunito', serif;
  font-weight: 600;
  letter-spacing: -0.01em;
}
```

### Iconography

- Prefer **rounded** icon sets: Phosphor (Bold/Duotone), Lucide with `stroke-linecap="round"` and stroke-width `1.5`, or Iconoir
- No filled black icons. Use `--ink-soft` or `--sky-deep`
- Decorative icons can be **emoji** (sparingly): ☁️ 🍎 🐾 ✨ — but max 1-2 per view

### Painterly texture overlay

To get the oil-paint feeling, add a subtle noise overlay to large surfaces:

```css
.painterly::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.4'/%3E%3C/svg%3E");
  opacity: 0.06;
  pointer-events: none;
  mix-blend-mode: multiply;
}
```

---

## Layout principles

### The sleeping cloud rule
**Most layouts have one big soft thing surrounded by sky.** Hero sections should feel like the puppy in the painting — one calm, centered focal point, generous breathing room around it.

### Asymmetric softness
Avoid perfect grids. Let cards drift slightly: stagger heights, use organic blob shapes as backgrounds, allow soft overlaps. Think "scattered clouds," not "PowerPoint grid."

### The single apple
**One warm-color element per visible viewport.** This is the apple on the puppy's head: a single small warm thing that draws the eye. If you have two apple-red elements visible at once, you've broken the rule.

### Spacing scale
Use a soft, generous scale. Multiples of 8 are fine, but lean *bigger* than you'd normally think:
`8, 16, 24, 32, 48, 64, 96, 128`

Default section padding should be `64px` minimum on desktop.

---

## Motion

The puppy is asleep — motion should feel like breathing, not buzzing.

- **Easing:** `cubic-bezier(0.34, 1.56, 0.64, 1)` (gentle overshoot) or `cubic-bezier(0.4, 0, 0.2, 1)` (smooth)
- **Durations:** 300-600ms for most things, 800ms+ for ambient/decorative motion
- **Hover states:** subtle lifts (`translateY(-2px)`) and shadow expansions, never color flips
- **Loading states:** soft pulse or floating cloud animations, never spinners
- **Page transitions:** crossfades with light blur, never hard cuts

```css
@keyframes breathe {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-4px) scale(1.01); }
}
.float-cloud { animation: breathe 6s ease-in-out infinite; }
```

---

## Component patterns

### Hero section
- Soft sky gradient background with painterly texture overlay
- **The puppy mascot is present** — large (~25-35% viewport width), centered or slightly offset above/beside the headline
- One large cloud-card centered, asymmetric — slight rotation (-1 to 2deg) is OK
- Headline in soft serif, body in rounded sans
- One apple-button as primary CTA, one ghost pillow-button as secondary
- Optional decorative SVG cloud blobs floating in background

### Forms
- Input fields are pill-shaped (`border-radius: 16px+`), no borders, soft inset shadow
- Focus state: glowing peach ring, not a hard outline
- Labels above inputs, never floating placeholder labels
- Submit button is the apple — the single warm thing

### Cards / lists
- Stack of cloud-cards with generous gaps (24-32px)
- Slight stagger or rotation OK on hover
- Avatars are circular, soft drop shadow
- No hard dividers between items — use whitespace

### Navigation
- Top nav: floating pill-shaped container with pillow shadow, *not* full-width bar
- Active state: cloud-soft background fill, no underlines
- Mobile: slide-up drawer with rounded top corners (32px+)

---

## Quick checklist before shipping

Before considering any cloud-pup UI done, verify:

- [ ] **🐶 The puppy is present.** This is rule zero. No puppy = not done.
- [ ] No element has corner-radius below 16px (except text)
- [ ] No `#000` or pure white anywhere — always tinted
- [ ] Background has the peach-radial-over-sky-blue treatment, not flat
- [ ] Every elevated surface uses the pillow-shadow (3 layers, sky-tinted)
- [ ] Exactly one apple-warm element is visible per viewport (the apple on the puppy's head can count)
- [ ] At least one painterly texture overlay is present somewhere
- [ ] Hover/transition easings are gentle (no `linear`, no <200ms)
- [ ] Typography uses rounded humanist sans + generous line-height
- [ ] No sharp drop shadows, no glassmorphism, no neon glows
- [ ] The page passes the **"would a sleeping puppy be comfortable here"** test

---

## When in doubt

If a design choice feels uncertain, choose the gentler option:
- Bigger radius over smaller
- Diffuser shadow over sharper
- More whitespace over less
- Softer color over saturated
- Slower motion over faster
- One accent over many

The aesthetic fails when it tries too hard. Let it be sleepy.

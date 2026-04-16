# DESIGN.md — Regens Unite · Impact Village Mumbai 2026
**Project:** Sponsor/partner landing page — Impact Village Mumbai 2026
**By:** Regens Unite
**Live URL:** https://impact-village.netlify.app
**Source file:** `sponsor-mumbai-2026.html` (single-file, no build toolchain)
**Preview:** sync with `cp sponsor-mumbai-2026.html index.html`, served by `npx serve` on port 5173

---

## 1. Creative North Star — "The Regenerative Canvas"

The interface is treated as a **living, editorial layout** — not a template. It prioritizes grounding textures, intentional asymmetry, and a "human-centric" organicism. Components feel like they are **resting on a surface** rather than being trapped in a grid.

Premium feel is achieved through:
- Mastery of whitespace, not density of elements
- Tonal depth through surface-layer shifts, not explicit borders
- High-contrast typographic scale (editorial rhythm, not web defaults)
- Overlapping elements and deliberate asymmetry when appropriate

---

## 2. Surface & Layer Philosophy

Think of the UI as **stacked sheets of heavy-weight fine paper**. Depth is achieved by nesting lighter surfaces on darker ones — never through legacy drop shadows.

| Layer | Role | Colour |
|---|---|---|
| Page base | Primary background | `var(--cream)` `#ede8dc` |
| Alternate sections | Subtle tonal shift | `var(--sage-light)` `#d8e0c4` |
| Raised cards / inputs | High-contrast lift | `var(--white)` `#ffffff` |
| Dark sections | Anchoring, high impact | `var(--dark-green)` `#1c4532` |

Sections alternate cream → sage to create visual rhythm without any explicit dividers. Wave SVG elements (`wave-dg-cream`) handle the dark-green → cream transitions.

### The No-Line Rule
1px solid borders for sectioning or containment are **prohibited**. Structural hierarchy must be defined exclusively through background colour shifts. The single exception: "ghost borders" on interactive inputs (`rgba(28,69,50,0.12)` at low opacity).

### Glass & Gradient
For floating UI elements (nav, modal overlay), use semi-transparent backgrounds with `backdrop-filter: blur()`:
- **Nav:** `rgba(255,255,255,0.94)` + `blur(16px)`
- **Modal overlay:** `rgba(18,46,30,0.45)` + `blur(10px)`

### Elevation & Depth
If a floating effect is required (modal card, tier cards):
- Shadow blur: `32px–80px`
- Shadow tint: always use a tinted version of `var(--dark-green)`, never pure grey
- Example: `box-shadow: 0 32px 80px rgba(0,0,0,0.25)` on modal card

---

## 3. Colour Palette

All colours are defined as CSS custom properties on `:root`, matched to regensunite.earth.

| Token | Hex | Usage |
|---|---|---|
| `--dark-green` | `#1c4532` | Primary headings, dark sections (concept, CTA, footer) |
| `--mid-green` | `#2d6a4f` | Body text, labels, secondary icons |
| `--teal` | `#2b7a5c` | Accent links, event names, tags |
| `--light-green` | `#4fa87a` | Keyword highlights in headings (`<span class="kw">`) |
| `--terracotta` | `#c4503a` | Primary CTA buttons, eyebrow text, active indicators |
| `--terra-light` | `#e8755d` | Hover state for all terracotta elements |
| `--cream` | `#ede8dc` | Primary background, modal card |
| `--cream-dark` | `#e3ddd1` | Subtle surface variant |
| `--sage-light` | `#d8e0c4` | Alternate section backgrounds (Format, Past Events) |
| `--sage-mid` | `#ccd6b0` | Deeper alternate surface |
| `--white` | `#ffffff` | Cards, stat bar, inputs |

> **Note on original spec:** The planning-phase palette used `#316345` (primary green) and `#f7fbea` (surface). The implemented palette shifted to deeper forest greens and a warmer cream to better match regensunite.earth. The philosophy — botanical greens + earth neutrals + terracotta CTA — carried over faithfully.

---

## 4. Typography

### Typefaces
Loaded from Google Fonts.

| Token | Family | Usage |
|---|---|---|
| `--barlow` | Barlow, sans-serif | All headings, labels, eyebrows, stats, nav, CTAs |
| `--mulish` | Mulish, sans-serif | Body text, descriptions, form inputs, testimonials |

> **Note on original spec:** The planning phase specified Work Sans. Barlow + Mulish were chosen during implementation for a stronger editorial contrast — Barlow's condensed weight at 900 creates the commanding display presence; Mulish provides the humanist warmth in body copy. The editorial rhythm intent of the original is fully preserved.

### Type Scale

| Element | Font | Weight | Size |
|---|---|---|---|
| Hero title | Barlow | 900 | `clamp(3.5rem, 7.5vw, 7.5rem)` — uppercase, ls `-0.01em` |
| Hero subtitle | Mulish | 700 | `1.05rem` |
| Hero eyebrow | Barlow | 800 | `0.75rem` — uppercase, ls `0.14em` |
| Section heading | Barlow | 800 | `2.75rem` → `clamp(1.75rem, 8vw, 2.25rem)` mobile |
| Section label | Barlow | 800 | `0.7rem` — uppercase, ls `0.14em` |
| Concept card title | Barlow | 900 | `clamp(2.5rem, 4.5vw, 5rem)` — uppercase, ls `-0.02em` |
| Concept card desc | Mulish | 400 | `clamp(0.9rem, 1.1vw, 1.05rem)` |
| Tier card name | Barlow | 900 | `2rem` — uppercase |
| Nav links | Mulish | 600 | `0.875rem` |
| Nav CTA | Barlow | 800 | `0.8125rem` — uppercase, ls `0.05em` |
| Stat numbers (hero) | Barlow | 900 | `2.25rem` |
| Body / descriptions | Mulish | 400 | `0.9rem–1.05rem`, line-height `1.65` |

### Rules
- Display text: tight line-height (`0.9–1.1`) for impact
- Body text: generous line-height (`1.6–1.75`) for readability and "breathing" feel
- Keyword highlights in section titles: `<span class="kw">` → renders in `var(--light-green)`
- Eyebrows / labels: always uppercase, always Barlow 800, always letter-spaced

---

## 5. Spacing

| Context | Value |
|---|---|
| Section padding (desktop) | `5rem 3rem` — `.section` |
| Section padding (mobile) | `3rem 1.25rem` |
| Section inner max-width | `1100px` — `.section-inner` |
| Hero inner max-width | `860px` — `.hero-inner` |
| CTA section (desktop) | `10rem 3rem` |
| CTA section (mobile) | `4.5rem 1.25rem` |
| Major thematic section separation | `5rem–6rem` vertical |
| Card border radius | `1.25rem` |
| Pill border radius | `50px` — buttons, nav, badges |

---

## 6. Section Backgrounds (top → bottom)

| Section | Background |
|---|---|
| Nav | `rgba(255,255,255,0.94)` frosted glass pill, fixed |
| Hero | `var(--cream)` + `hero-bg.svg` full-bleed |
| Concept slider | `var(--dark-green)` |
| Why Mumbai | `var(--cream)` |
| Format / Programme | `var(--sage-light)` |
| Sponsor Tiers | `var(--cream)` |
| Past Events | `var(--sage-light)` |
| Partners marquee | `var(--cream)` |
| Timeline | `var(--cream)` |
| Updates / FAQ | `var(--cream)` |
| Final CTA | `var(--dark-green)` |
| Footer | `var(--dark-green)` |

---

## 7. Components

### Buttons

| Variant | Class | Style |
|---|---|---|
| Primary dark fill | `.btn-pill-fill` | `var(--dark-green)` bg · white · Barlow 800 · 0.8rem · uppercase |
| Outline terracotta | `.btn-pill-outline` | Transparent bg · `var(--terracotta)` border + text · hover fills |
| Terracotta fill | `.btn-pill-terra` | `var(--terracotta)` bg · white · hover `var(--terra-light)` |
| Nav / modal CTA | `.nav-btn-donate` | `var(--terracotta)` bg · no border · Barlow 800 · 0.8125rem |

All buttons: `50px` border-radius, Barlow 800, uppercase, letter-spaced.

### Navigation
- Fixed pill centred at `top: 1rem`, `z-index: 200`
- Glassmorphism: `rgba(255,255,255,0.94)` + `backdrop-filter: blur(16px)`
- Scrolled state (JS `.scrolled` class): shadow deepens
- Logo: `2.25rem` circle mark + wordmark ("Impact Village" / "Mumbai · Devcon 2026")
- Links: The Concept · Past Events · Updates
- CTA: "Get Involved" → opens modal
- **Mobile (≤768px):** anchor links hidden, only logo + CTA

### Modal — "Get Involved"
- Overlay: `rgba(18,46,30,0.45)` + `blur(10px)`, full-screen
- Card: `var(--cream)` bg, `1.5rem` radius, max-width `400px`
- Entry animation: `translateY(24px) scale(0.96)` → `(0) scale(1)`, spring easing `cubic-bezier(0.34, 1.4, 0.64, 1)`
- Fields: Name (req), Email (req), Organisation (optional) — ghost-style inputs
- On submit: POSTs to **Netlify Forms** (`name="get-involved"`), then swaps to confirmation screen
- Confirmation: animated SVG checkmark (`stroke-dashoffset`) + "We got it, [first name]." · auto-closes `3.5s`
- Opens from: nav CTA · hero CTA · final CTA
- Submissions: `app.netlify.com/projects/impact-village/forms` → configure email notifications there

### Input Fields (ghost style)
- Background: `var(--cream-dark)` or light surface
- Border: `rgba(28,69,50,0.12)` — low opacity, never hard 1px solid
- Focus: border brightens toward `var(--dark-green)`

### FAQ Accordion
- Pure JS class toggle (`.open`)
- `max-height` transition `0 → 300px` with `overflow: hidden`
- `+` / `−` icon rotates on open

### Concept Slider
Sticky horizontal scroll section — the centrepiece of the page.

```
Section height:   calc(100vh × 5)   — 1 viewport per card
Card width:       78vw
Track padding:    0  calc((100vw - 78vw) / 2)  0  20vw
                  right pad centres last card · left pad offsets first card
```

- Sticky inner container `height: 100vh`
- Scroll progress: `progress = scrolled / (cards.length × window.innerHeight)`
- `maxX` computed from `cards[0].offsetWidth` (not `scrollWidth` — unreliable on flex with `overflow: visible`)
- **Text animation:** real-time `opacity` + shared `translateY` from viewport-centre distance. Stagger offsets: num `0`, title `0.09`, desc `0.20` — applied to opacity only (shared `translateY` keeps spacing constant)
- **Illustration:** same opacity fade + `translateX` drift. Mobile: `position: static`, `opacity: 1`
- Keyword highlights: `<span class="kw">` → `var(--light-green)`
- Dots + counter update per scroll tick

| Card | Copy | Highlight | Illustration |
|---|---|---|---|
| 01 | Your base for the week | "Your base" | `Slide1_illustration.png` |
| 02 | Fund a locally-owned innovation space | "locally-owned" | `Slide2_illustration.png` |
| 03 | A wallet in your wristband | "wristband" | `Slide3_illustration.png` |
| 04 | Bridging communities | "Bridging" | `Slide4_illustration.png` |

### Partners Marquee
- 2 rows, infinite CSS animation: row 1 left (`30s`), row 2 right (`34s`)
- Max-width: `780px`, centred
- Side fade overlays: `width: 100px` → `40px` mobile
- Logos: `72px` circles + label text, duplicated for seamless loop

---

## 8. Animations & Transitions

| Effect | Mechanism |
|---|---|
| Scroll reveal | `IntersectionObserver` → `.visible` class on `.reveal` elements |
| Nav scroll shadow | `scrollY > 20` → `.scrolled` class |
| Concept text | Real-time `opacity` + `translateY` from scroll distance |
| Concept illustrations | Real-time `opacity` + `translateX` from scroll distance |
| Modal entry | Spring `cubic-bezier(0.34, 1.4, 0.64, 1)` |
| Checkmark SVG | `stroke-dashoffset` animation `0.6s ease` |
| FAQ accordion | `max-height` `0 → 300px` |
| Marquee | `@keyframes marquee-left / marquee-right` |
| Progress dots | `width` + `background` `0.35s` |

---

## 9. Mobile (≤ 768px)

- `html, body { overflow-x: hidden }`
- Nav: anchor links hidden, logo + CTA only
- Section padding: `3rem 1.25rem`
- Section headings: `clamp(1.75rem, 8vw, 2.25rem)`
- All 2-col / 3-col grids → 1 column
- Concept slider: vertical stack; illustrations `position: static` + flow above text
- Featured tier card: `transform: none` (lift removed)
- Gallery: 3-col → 2-col
- CTA section: `4.5rem 1.25rem`
- Footer: column layout, `align-items: flex-start`

---

## 10. Do's and Don'ts

### Do
- **Use asymmetry** — offset text and image blocks intentionally; avoid perfectly equal margins
- **Embrace whitespace** — `5rem–6rem` between major sections is correct, not excessive
- **Layer surfaces** — allow elements to imply depth through tonal shifts, not borders or shadows
- **Use the editorial contrast** — small caps labels against massive display text creates narrative rhythm
- **Highlight key words** — use `<span class="kw">` in display headings to guide the eye
- **Keep CTAs terracotta** — it is the only warm signal in a cool botanical palette; use it sparingly

### Don't
- **Don't use 1px solid lines** for sectioning — instant template look
- **Don't use pure black** — use `var(--dark-green)` `#1c4532` for all "black" text
- **Don't use generic box shadows** — if a shadow doesn't look like ambient light on paper, remove it
- **Don't crowd sections** — if a block feels heavy, split or increase vertical spacing
- **Don't use blue** — there are no blues in this palette; all tonal range lives in the green-cream-terracotta space
- **Don't add borders to buttons** — only the outline variant has a border, and it is terracotta

---

## 11. Assets

```
assets/
  hero-bg.svg                  — botanical hero background (full-bleed)
  hero-illustration-1.webp     — hero illustration
  hero-illustration-2.svg      — hero illustration variant
  ru-logo-circle.png           — Regens Unite circular mark (nav, footer)
  ru-logo-dark.svg             — Regens Unite wordmark (dark)
  OG_image.jpg                 — Social share image (1200 × 630)
  Slide1_illustration.png      — Concept slider card 01
  Slide2_illustration.png      — Concept slider card 02
  Slide3_illustration.png      — Concept slider card 03
  Slide4_illustration.png      — Concept slider card 04
  photos/                      — Gallery: Brussels Impact Village event
```

---

## 12. Deployment

- **Host:** Netlify — project `impact-village`
- **Deploy:** `netlify deploy --dir . --prod` from project root
- **Always sync first:** `cp sponsor-mumbai-2026.html index.html`
- **Cache:** `index.html` → `no-cache` · `assets/*` → `1yr immutable` (see `netlify.toml`)
- **Forms:** Netlify Forms, `name="get-involved"` — submissions at `app.netlify.com/projects/impact-village/forms`

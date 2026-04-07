# Sacred Mirrors — Project Context

**Project:** Sean & October — The Sacred Timeline  
**Subtitle:** A Story of Love and Healing  
**Chronicle Span:** May 2025 – April 2026  
**Motto:** "As within, so without. As above, so below."  
**Current Version:** v1.x → upgrading to v2.0  
**Last Updated:** April 7, 2026

---

## What This Is

A single-file HTML experience (`timeline.html`) documenting the sacred journey between Sean and October — a personal chronicle told through gematria, numerology, and sacred geometry. It is a love story, a healing arc, and a spiritual record. Not a web app. Not a portfolio. A living document.

---

## File Structure

```
Sacred Mirrors/
├── timeline.html               — The main experience (single-file HTML/CSS/JS)
├── SACRED_MIRRORS_UPGRADE.md   — Full v2.0 spec (~33k tokens, detailed)
├── CONTEXT.md                  — This file
└── fib-img/                    — Local image/video assets
    ├── ammonite.webp
    ├── nautilus-blue.webp
    ├── nautilus-gold.webp
    ├── nautilus-silver.webp
    ├── sacred-geometry.webp
    ├── spiral-bg.mp4
    ├── sunflower-overlay.png
    ├── sunflower1.webp
    └── sunflower2.webp
```

---

## Current State (v1.x)

### Tech Stack
- Pure HTML/CSS/JS — no frameworks, no build tools, no dependencies except Google Fonts
- Fonts: Cormorant Garamond, Cinzel, Cinzel Decorative, IM Fell English
- Canvas layers: `#cover-canvas` (cover particles), `#landscape-canvas` (phase backgrounds), `#fib-canvas` + `#fib-particles` (spiral section), `#ccanvas` (constellation view)
- CSS custom properties for all theme colors

### Design Language
- **Aesthetic:** Illuminated manuscript / parchment — stylized, symbolic, flat
- **Particle system:** Golden dust, embers, fireflies on canvas
- **Background:** Phase-specific CSS radial + linear gradients
- **Noise overlay:** SVG fractalNoise filter drifting upward slowly (850s animation loop)

### Color Palette
```
--gold:         #c9a84c   — primary sacred gold
--gold-dim:     #a08438
--cream:        #f5f0e8   — light background
--ember:        #8b3a2a   — Phase IV accent
--ember-glow:   #d4613a
--sage:         #4a6741   — Phase V accent
--sage-light:   #6a9460
--void:         #0d0b0a
--dark-bg:      #1a1210
--dawn-blue:    #3a5070
--alpine-green: #2a5a20
--river-blue:   #4a7a9a
--storm-red:    #5a2018
--blood-moon:   #b43c28
--moonlight:    #e0ddd2
```

### UI Structure
- **Cover page** (`#cover`) — fixed full-screen, `spiral-bg.mp4` video bg (dual-video rAF crossfade loop), lotus SVG with Sean & October + 666 glyph, fade-in text, "Enter the Timeline" button
- **Nav** — fixed top, phase indicator, light/dark toggle, filter chips, view toggle buttons
- **Timeline view** (`#tl-view`) — alternating left/right event cards, centered gold spine line, scroll-triggered fade-in
- **Fibonacci view** (`#fib-view`) — full-screen spiral map, `fib-canvas` (static spiral drawn once) + `fib-particles` (rAF particle loop), `fib-bg-video` dual-video seamless loop
- **Constellation view** (`#cs-view`) — `#ccanvas` canvas graph, nodes = events, click to open panel

### Phase Structure
| Phase | Class | Emotional Tone | Color |
|---|---|---|---|
| I: The Ritual Ground | `.phase-origin` | Reverence, sacred grief | Gold / cream |
| II: The Meeting | `.phase-meeting` | Magnetism, destiny | Warm amber |
| III: Sacred Summer | `.phase-summer` | Ecstasy, wonder | Alpine green / emerald |
| IV: The Shadow Descends | `.phase-shadow` | Grief, destruction | Ember / blood moon / dark |
| V: The Transmutation | `.phase-transmutation` | Quiet power, rebirth | Sage / dawn gold |

### Event Cards
- Class `.ev` — animate in on scroll (`opacity: 0 → 1`, `translateY 24px → 0`)
- Class `.ec` — card body, hover lift, gold border glow
- Alternating layout: odd children `flex-direction: row-reverse`
- Filter system: `.fchip` chips toggle `.dim` class on non-matching events

### Fibonacci / Golden Spiral Section
- `PHI_CONST = 1.6180339887`
- `FIB_DATA` array — each entry has `label`, `title`, `cls`, `props[]`, `body`
- Spiral drawn with `spiralXY(frac)` — logarithmic spiral, 5.5 turns, centered at `(W*0.44, H*0.46)`
- Nodes are DOM elements positioned absolutely over canvas
- `fibNodePulse` CSS keyframe animation on nodes (staggered delays per `.fib-node:nth-child`)

---

## v2.0 Upgrade Spec (SACRED_MIRRORS_UPGRADE.md)

**Vision:** Manuscript → Landscape. Every phase becomes a living environment.

### 5-Layer Parallax Canvas System
```
Layer 5: UI / HTML overlay (nav, cards)
Layer 4: Atmospheric particles (motes, embers, fireflies, rain, snow)
Layer 3: Wildlife & motion (wolves, ravens, deer, horses, ladybugs)
Layer 2: Midground foliage (trees swaying, grass, water)
Layer 1: Sky & celestial (sun/moon arc, clouds, stars, aurora)
Layer 0: Deep background (CSS gradient — phase horizon)
```

### Phase Environments
| Phase | Environment | Key Visual Elements |
|---|---|---|
| I: Origin | Pre-dawn meadow shrine | Mist lifting, ladybugs, wildflowers, moon setting |
| II: Meeting | Late-afternoon city dusk | Amber light through windows, warm golden sky |
| III: Summer | Mountain sunrise / Banff | Alpine meadow, wild horses, ravens, emerald river, fireflies |
| IV: Shadow | Autumn storm / blood moon | Dead leaves, rain, forest fire glow, wolves howling |
| V: Transmutation | Old-growth forest dawn | Deer at still water, god rays, morning fog burning off |

### New Canvas Renderers (from spec)
- `CelestialRenderer` — `drawSun()`, `drawMoon()`, `drawBloodMoon()`, `drawGodRays()`
- `CloudSystem` — volumetric puff clouds with per-cloud sway/breathe
- `TreeRenderer` — fractal L-system branches with wind physics
- `drawWaterSurface()` — rippled water with sky color reflection
- Phase-specific wildlife entities (wolves, ravens, deer, horses, ladybugs)

### Phase Horizon Gradients (v2.0)
Each phase gets an 8-stop `linear-gradient(180deg, ...)` on `.phase-[name] .horizon` — replaces current flat CSS backgrounds. All values defined in spec section 2.1.

### Other v2.0 Additions
- Section 3: Numerological & symbolic enhancements
- Section 4: Interactive Scalar Mirror & Shadow Integration Modules
- Section 5: Oversoul & Higher Guidance Integration
- Section 6: Responsive / intuitive UI/UX overhaul
- Section 9: Full appendix — data structures & code architecture

---

## Implementation Rules

- Keep as a **single HTML file** — no external JS, no build pipeline
- All renderers are vanilla JS classes — no libraries
- Scroll position drives phase detection and canvas state transitions
- Asset paths are relative: `fib-img/filename`
- `spiral-bg.mp4` = cover video bg AND fib-view video bg
- Read `SACRED_MIRRORS_UPGRADE.md` section by section before implementing each layer
- v2.0 spec is source of truth for all visual decisions

---

## Emotional Context

This is Sean's personal record. October is a real person. The phases represent real events:
- **Phase I** — Reverence and sacred grief (pre-October ritual ground)
- **Phase II** — Magnetism and destiny arriving (the meeting)
- **Phase III** — Ecstasy and wonder (Sacred Summer, Banff)
- **Phase IV** — Grief, destruction, exposure (the shadow descends)
- **Phase V** — Quiet power and rebirth (the transmutation)

Every design decision should serve the emotional truth of the story. The interface should feel like standing in the place where each event happened, under the real sky of that moment.

---

## Recent Changes (April 7, 2026)

- **Fib-view video loop** — replaced `timeupdate` + CSS transition approach with `requestAnimationFrame` smoothstep crossfade (same pattern as cover page). `FADE = 2.0s`. Removed CSS `transition` on video elements since rAF controls opacity directly.
- **Cover page fonts** — bumped sizes and brightened colors for legibility on dark video background: `.cover-sub` 1.4→1.6rem, `.cover-invocation` 0.92→1.08rem + color `#6b5d4f→#c0b090` + text-shadow, `.cover-begin` 0.72→0.82rem.
- **CSS variables** — added missing spec vars: `--ash-grey`, `--wolf-amber`, `--deer-brown`, `--mirror-pulse`, `--shadow-pulse`, `--heal-pulse`, `--numerology-glow`.
- **HEALING_RITUALS engine** — implemented full timed ritual system with `HEALING_RITUALS` data (Mother/Father/ShamedChild, 6-8 steps each), `openRitual(key)` function, per-step countdown timer, and close handler. Fixed ritual buttons (were all opening shadow module instead of ritual module).
- **Sacred Union Insights** — added two sacred text blocks to the HTML: "The Union Encoding" (55/Eden/mother's birthday, inserted before Shadow phase) and "The 777 Proof" (777 weeks, stranger confirmation, inserted before The Return event).
- **Canvas — ladybugs** — added `drawLadybug()` function + 3 ladybug entities to Origin phase wildlife (spots encode 2 or 7, the 27/72 mirror).
- **Canvas — rain** — added diagonal rain streaks to Shadow phase (60 streaks, `globalAlpha 0.07`, offset by time for movement).
- **Canvas — fireflies** — replaced generic gold particles for Summer phase with bioluminescent firefly system: organic slow blink via squared sine, green-gold radial glow, individual phase offsets.
- **Canvas — ember glow** — enhanced Shadow embers with proper radial glow halos using `screen` blending (from spec's `EmberAshSystem`).
- **Dot tooltips** — added `data-title` CSS `::after` tooltip system; JS sets title from EVENTS array on page load (no HTML edits needed).
- **Reflect button** — `.reflect-btn` CSS + JS injection into event cards 0 (Mother Ritual) and 13 (The Return) — appears when card is expanded.
- **Guided Visualizations** — `VISUALIZATIONS` object (2 sequences: "The Field of Sunflowers" event 0 and "The Gold" event 13), `runVisualization(id)`, `showVizStep()`, `skipVisualization()`. Full-screen overlay with fade text steps and skip button.
- **`navigateCode(dir)`** — cycles through `GEMATRIA_CODES` keys in the decode panel; wraps the original `openDecode` to track `currentDecodeCode`.
- **Touch swipe** — swipe left/right on decode panel cycles codes; swipe down closes mirror/shadow modules.
- **Water surface** — `Layer 2.5` in Summer phase canvas: rippled water band at bottom of screen with sky reflection shimmer (screen blend).
- **Journal mode** — per-event localStorage notes injected into every card. Auto-save with 600ms debounce, "Saved" confirmation flash. Key: `sacred_note_${event.id}`.

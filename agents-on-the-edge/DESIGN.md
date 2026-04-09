# Agents on the Edge — Design System

> A custom Slidev deck for the **Subconscious × ACM Hackathon** (2026-04-09).
> Built to look _engineered_, not vibe-coded.

---

## 1. Design Intent

The original deck (see `/Users/ostepan/Downloads/Agents on the Edge.pdf`) is a
clean, 4:3-feeling keynote slideshow: bright-white slides, an orange header bar,
Arial Monospaced titles, and a few flat icons. That works. It is also, visibly,
a 30-minute slide job in Google Slides.

This rebuild keeps the **information architecture** verbatim (same 15 slides,
same facts, same QR codes, same links) but reframes the presentation as an
**editorial product demo** — closer to how Stripe Press, Vercel Ship, and Linear
ship a keynote. The deck should look like something the Subconscious team
itself would put on stage:

- **Precision, not decoration.** Every element is on a grid. Every motion has
  an easing curve and a purpose.
- **Monospace is a signature, not a gimmick.** Inherited from the source
  deck's title font — but upgraded to `JetBrains Mono` and used only for
  eyebrows, metadata, and code.
- **One color does the work.** Subconscious orange `#FF5C28` is the only
  accent. No rainbow, no gradients-for-the-sake-of-it. Glow and halation are
  derived from the same hue.
- **Dark by default.** The original deck is light; this one is dark. It reads
  better in a lecture hall, photographs well, and lets the orange brand mark
  _actually_ sing.
- **Assets are real.** Logos, product screenshots, and integration marks are
  lifted directly from `subconscious-monorepo/apps/web/public/` so the deck
  matches the shipping product pixel-for-pixel.

---

## 2. Canvas & Grid

| Token         | Value                                | Notes                              |
| ------------- | ------------------------------------ | ---------------------------------- |
| Canvas        | `1920 × 1080`                        | 16:9, retina-ready                 |
| Outer margin  | `96px` top / `112px` sides           | Safe area inside letterboxing      |
| Baseline grid | `8px`                                | All vertical rhythm snaps to 8px   |
| Column grid   | `12 col, 64px gutter`                | Used for multi-panel layouts       |
| Section tag   | Top-left, `88px` from edge           | Monospace eyebrow + index counter  |
| Footer rule   | `1px` hairline, `#1F1F1F`            | Runs full width above page number  |
| Page number   | Bottom-right, monospace, `0.55 opac` | `NN / 15` format, no decoration    |

Every slide shares the same header/footer chrome so navigation feels
deliberate and the eye has a stable anchor.

---

## 3. Color Tokens

Defined in `styles/tokens.css`:

```
--bg:           #07070A   /* near-black, slightly cool      */
--surface:     #0E0E12   /* cards, code blocks             */
--surface-2:   #14141A   /* raised panels                  */
--border:      #1F1F26   /* hairlines                      */
--border-hi:   #2A2A33   /* hover / focus                  */

--text:        #F5F5F7   /* primary type                   */
--text-muted:  #9A9AA6   /* captions, metadata             */
--text-faint:  #5A5A66   /* disabled, rule labels          */

--orange:      #FF5C28   /* brand primary                  */
--orange-hi:   #FF7A47   /* hover / motion highlights      */
--orange-lo:   #C94517   /* pressed / darker tier          */
--orange-glow: rgba(255, 92, 40, 0.45)

--cyan:        #7DD3FC   /* data, links (used rarely)      */
--green:       #34D399   /* success ticks                  */
```

### Usage rules

- **Background** is always `--bg`. Never pure black. Never white.
- **Orange fill** is reserved for: brand mark, active state, primary CTA,
  key numerals, and the animated trace of the logo orbit. It is _never_
  used as a full background bar (that's what separates this from the source
  deck).
- **Cyan and green** are accents for code output and success indicators only.
  They do not appear in headings.

---

## 4. Typography

Two families, three roles.

| Role            | Family                  | Weight | Size         | Tracking |
| --------------- | ----------------------- | ------ | ------------ | -------- |
| Display (H1)    | **Inter Tight**         | 800    | 112 / 96     | -0.035em |
| Section (H2)    | **Inter Tight**         | 700    | 64           | -0.025em |
| Body            | **Inter**               | 400/500| 28           | -0.005em |
| Eyebrow / Meta  | **JetBrains Mono**      | 500    | 13           | +0.18em  |
| Code            | **JetBrains Mono**      | 400    | 20           | 0        |
| Numerals (data) | **JetBrains Mono**      | 600    | varies       | 0        |

Fonts are loaded in `slides.md` frontmatter via Slidev's built-in
`fonts.provider: google` so there is no CDN reliance at build time.

### Rules

- H1 uses tight negative tracking and sits on a 1.02 line-height. Never
  wraps unless the slide demands it.
- All eyebrows are **UPPERCASE**, monospace, with a leading orange dot:
  `● 02 · SETUP`.
- Body copy never exceeds ~58 characters per line.
- Numerals inside schedules, code, timers, and API examples are always
  mono (`font-variant-numeric: tabular-nums`) so they don't jitter.

---

## 5. Iconography & Imagery

- **Logo**: `public/assets/brand/subconscious-logo.svg` (the 8-node orbit
  mark). Used as hero, footer watermark, and the source of the animated
  orbit component.
- **Wordmark**: `public/assets/brand/subconscious-full.svg`.
- **Product shots**: `public/assets/platform/*.png` — real screenshots of
  the dashboard, playground, and templates library, framed inside a
  browser-chrome Vue component (`<BrowserFrame>`).
- **Landing art**: `public/assets/landing/*.png` — the TIM / complex agent
  diagrams from subconscious.dev, used as ambient background art on
  section-break slides.
- **Integration marks**: `public/assets/integrations/*.svg` — Python,
  TypeScript, Claude, Exa, Parallel, Convex, E2B, etc. Used in the
  Set-Up and Docs slides as a ticker marquee.
- **Noise texture**: `public/assets/bg/noise.png` — applied at 4% opacity
  as a `::before` overlay on every slide to break up flat digital gradients.

All raster assets are served from `public/assets/` so Slidev's Vite build
picks them up without copy-transforms.

---

## 6. Motion System

Motion is the single biggest thing that separates this deck from the source.
Every transition has a named curve and a purpose.

| Token            | Value                           | Used for               |
| ---------------- | ------------------------------- | ---------------------- |
| `--ease-out`     | `cubic-bezier(0.22, 1, 0.36, 1)`| Standard enter         |
| `--ease-in-out`  | `cubic-bezier(0.65, 0, 0.35, 1)`| Shared layout          |
| `--ease-spring`  | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Badges, pill pops |
| `--dur-fast`     | `240ms`                         | Micro hover            |
| `--dur-base`     | `520ms`                         | Body element enter     |
| `--dur-slow`     | `900ms`                         | Hero / stage transitions |

### Animation patterns in use

1. **Orbit ring** — the hero logo animates its 8 outer nodes in a staggered
   sweep, then a subtle rotation loop (12s, linear). Pure CSS + `@keyframes`.
2. **Line trace** — the task-decomposition diagram (`Who We Are`) draws its
   edges with `stroke-dashoffset` on `v-click`.
3. **Token stream** — the Python SDK walkthrough types out code with a
   staggered character reveal (`TokenStream.vue`).
4. **Schedule tick** — the timeline (`How Today Works`) advances an orange
   dot along a vertical rule with each `v-click`.
5. **Integration marquee** — horizontally scrolling strip of integration
   logos on the Set-Up slide. Infinite, 40s linear loop.
6. **Judging cards** — lift + orange halation on hover, staggered entry on
   slide open.
7. **Slide-level shared axis** — Slidev's built-in `slide-left` transition,
   chosen because it reinforces linear progression through the schedule.

Motion respects `prefers-reduced-motion: reduce` — all infinite loops
collapse to a single static frame.

---

## 7. Component Inventory

Located in `components/`:

| File                  | Purpose                                         |
| --------------------- | ----------------------------------------------- |
| `OrbitLogo.vue`       | Animated 8-node Subconscious logo mark          |
| `Eyebrow.vue`         | Section tag + index (`● 02 · SETUP`)            |
| `SlideChrome.vue`     | Shared header/footer frame with page number    |
| `TaskTree.vue`        | The subtask decomposition graph                 |
| `ScheduleRail.vue`    | Vertical timeline with animated tick            |
| `BrowserFrame.vue`    | macOS-style chrome around product screenshots   |
| `TokenStream.vue`     | Typewriter-style code reveal                    |
| `IntegrationMarquee.vue` | Infinite scroller of Python/TS/Claude/etc.   |
| `JudgingCard.vue`     | Oversized criterion card with glow              |
| `AgentIdeaCard.vue`   | Compact card for the "Agent Ideas" grid         |
| `QRBlock.vue`         | Framed QR container with caption + URL          |
| `DotGrid.vue`         | Background dot grid for hero slides             |
| `StatPill.vue`        | Rounded metric chip (`HACK · 2h 15m · SOLO / 4`)|

Each component is <120 lines and is kept pure-Vue (no third-party deps).

---

## 8. Layouts

Slidev layouts live in `layouts/`:

- `cover.vue` — hero layout, dot grid bg, orbit logo, large display type
- `default.vue` — standard editorial layout with eyebrow + body
- `split.vue` — 7/5 column split for text + visual
- `centered.vue` — single-focus layout for QR-only slides
- `section.vue` — full-bleed chapter marker
- `end.vue` — closing build-ready call-to-action

---

## 9. Slide Map

| #  | Slide               | Layout      | Notable motion                      |
| -- | ------------------- | ----------- | ----------------------------------- |
| 01 | Agents on the Edge  | `cover`     | Orbit ring reveal + staggered title |
| 02 | Who We Are          | `split`     | Task-decomposition trace            |
| 03 | How Today Works     | `split`     | Schedule tick rail                  |
| 04 | Set-Up              | `default`   | Browser-frame product shots         |
| 05 | Set-Up Continued    | `default`   | Modal stack slide-in                |
| 06 | Python SDK          | `split`     | Token stream typewriter             |
| 07 | Docs Overview       | `split`     | Doc navigator highlight             |
| 08 | Example Agents      | `split`     | Capability checklist reveal         |
| 09 | Agent Ideas (grid)  | `default`   | 10-card staggered grid              |
| 10 | Judging Criteria    | `split`     | Two-card halation                   |
| 11 | Rubric              | `centered`  | QR reveal                           |
| 12 | Build!              | `section`   | CTA pulse                           |
| 13 | Group Submission    | `split`     | Numbered checklist reveal           |
| 14 | Demos               | `section`   | Time's-up heartbeat                 |
| 15 | Feedback            | `split`     | Form checklist + QR                 |

---

## 10. Asset Provenance

All imagery lives in `public/assets/` and was pulled from:

```
/Users/ostepan/Desktop/projects/subconscious/subconscious-monorepo/apps/web/public/
```

| Destination                        | Source                                          |
| ---------------------------------- | ------------------------------------------------ |
| `brand/subconscious-logo.svg`      | `public/logo.svg`                                |
| `brand/subconscious-full.svg`      | `public/icons/Subconscious_Logo.svg`             |
| `brand/subconscious-graphic.svg`   | `public/icons/Subconscious_Logo_Graphic.svg`     |
| `landing/tim.png` …                | `public/landing/*.png`                           |
| `platform/playground.png` …        | `public/platform/*.png`                          |
| `integrations/*.svg`               | `public/integrations/*.svg`                      |
| `bg/noise.png`                     | `public/bg/noise.png`                            |
| `universities/*.png`               | `public/universities/*.png`                      |

Nothing was regenerated. The deck ships the same visual language the
subconscious.dev site ships.

---

## 11. Build & Run

```
cd agents-on-the-edge
pnpm install
pnpm dev      # http://localhost:3030
pnpm build    # static export to dist/
pnpm export   # PDF export via playwright-chromium
```

Requires Node 20+.

---

## 12. Non-Goals

- No shadcn / no Tailwind runtime — the deck is pure Vue + scoped CSS to
  keep the bundle lean and the typography precise.
- No generative AI imagery. Every pixel either comes from the monorepo or
  is drawn in SVG by hand.
- No emoji. No clip art. No stock photography.
- No "slide transitions" beyond the single shared-axis slide-left.

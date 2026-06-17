# Uncle Inc. — Build Plan

## 1. PRODUCT
Uncle Inc. is an AI-assisted MVP development platform that walks early-stage startup founders through the full build-measure-learn loop in one workspace. A founder pastes a rough idea and the platform turns it into a problem spec, a clickable multi-screen prototype, a private user-testing link with session capture, and a deployed, analytics-instrumented MVP — then uses the captured behavior to propose the next iteration. The primary user is a non-technical or "code-curious" solo founder working pre-seed, short on time and runway, who currently stitches together Notion + Figma + Cursor/Replit + Typeform + GA + Vercel and still cannot close the loop between what shipped and what to ship next. The pain solved is the loop, not the code: research on early-stage founders consistently surfaces "what to build next" and "shipping fast enough to learn from real usage" as the two top blockers, and the compass motif makes the four-phase cycle the spine of the product.

## 2. WHO IT'S FOR
- **ICP**: solo or 2-person founding teams, pre-seed to seed, domain expert or ex-operator (not career dev), <10 hrs/week available for product work, current workflow is "Notion doc + Figma link + half-finished Replit + a GA property I never check."
- **Tone implications**: confident, technically literate, calm, no hustle-bro copy, no fake logos, no invented ARR claims. Show the workbench, not the lifestyle. Copy should sound like a senior engineer-friend, not a growth team.

## 3. LOOK & FEEL

### Visual system
- **Vibe**: dark analytical workbench. Linear meets a Bloomberg terminal meets a chartroom. Calm, focused, instrumented.
- **Palette** (Tailwind tokens):
  - `ink` `#0a0a0f` — page bg
  - `ink-2` `#111118` — card bg
  - `ink-3` `#1a1a24` — raised surfaces
  - `line` `#23232e` — 1px hairlines
  - `indigo` `#4f46e5` — primary
  - `cyan` `#06b6d4` — secondary
  - `teal` `#14b8a6` — highlight / success
  - `text` `#e6e6ef` — primary text (contrast 15.4:1 on ink)
  - `muted` `#8b8ba0` — secondary (7.4:1, AA passes)
  - `dim` `#5a5a70` — tertiary, used only on icons and hairlines
- **Typography**:
  - Headings: Space Grotesk 500/600/700, tracking `-0.02em` on h1, `-0.015em` on h2
  - Body: Space Grotesk 400, line-height 1.6
  - Mono: JetBrains Mono for eyebrows, version strings, coordinates, KPI numbers, code-style captions
  - Hero h1: `clamp(2.5rem, 6vw, 4.75rem)`; h2: `clamp(1.875rem, 3.5vw, 2.75rem)`
- **Layout**: 1200px max content, 24px gutter mobile / 48px desktop, section padding 96px desktop / 64px mobile, card radius 12px, button radius 10px, pill 999px, 1px hairlines, no drop shadows
- **Backgrounds**: 32px grid at 4% white masked with radial fade; 2% noise overlay; soft gradient mesh blobs (indigo→teal, 30% opacity, blurred 120px) behind hero
- **Iconography**: `lucide-react`, 1.5px stroke, 20px default, color `text` on `ink-3` squares
- **Imagery**: zero stock photos. Compass SVGs, ASCII-style build logs, terminal-flavored code snippets, dashboard mockups built in HTML/CSS
- **Motion**: compass needle 8s wobble, outer ring 60s rotation; section reveals 12px translateY + opacity, 600ms, stagger 80ms; card hover 200ms border→indigo; reduced-motion fully respected

### Compass motif (one SVG, three jobs)
1. **Logo mark** (24px, Nav): 8-point rose, N/S/E/W + intercardinal ticks, needle pointing NE
2. **Hero centerpiece** (320px): same compass + concentric range rings + thin lat/long web, outer ring rotates 360°/60s, needle wobbles
3. **Section dividers + Footer mark**: thin 1px line, small compass midpoint

Needle directions map to phases: **N = Refine, E = Build, S = Measure, W = Learn** — the hero shows all four as orbiting mono pills.

### Screens (= sections, single-page)

**Nav (sticky, top)**
- Left: Compass mark + "Uncle" wordmark (Space Grotesk 600, 1.125rem)
- Center: Product, Pricing, Manifesto, Changelog (anchor links + stubs)
- Right: "Sign in" muted link (non-functional stub, tooltip `// App launches with alpha`) + "Join waitlist" primary button → scrolls `#waitlist`
- Backdrop: transparent at top, `bg-ink/80 backdrop-blur-xl border-b border-line` after 40px scroll
- Mobile: hamburger toggles full-viewport sheet

**Hero**
- Mono eyebrow: `// v0.1 · private alpha`
- H1: "Build the MVP your idea deserves — not the one your weekend allows."
- Sub: "Uncle is an AI workbench for founders who need to ship, test, and learn before the runway runs out. One workspace. Four cardinal directions."
- CTA row: `[ Join the waitlist ]` (indigo) `[ See how it works ↓ ]` (ghost)
- Trust strip: NO testimonials. A live mono line fed by `GET /api/waitlist/count`: `// {n}+ founders on the list — no customers yet, just early believers.` Falls back to `// Join the list to make this real.` when n=0
- Right (desktop) / below (mobile): 320px compass centerpiece with 4 orbiting phase pills

**Features (2×3 grid desktop, 1 col mobile)**
1. **Idea Refinery** — paste a paragraph, get problem statement, target user, success metric, 3 anti-features to cut. Icon: `flask-conical`. Tag: `// 01 · REFINE`
2. **Prototype Generator** — describe a flow, get a clickable multi-screen prototype with real components, not a Figma frame. Icon: `boxes`. Tag: `// 02 · BUILD`
3. **Test Sessions** — share a link, record taps, hesitations, and missed affordances. Built-in consent + screen capture. Icon: `radar`. Tag: `// 03 · MEASURE`
4. **Instrumented Ship** — every button, screen, and drop-off wired to a real event stream. No GA setup, no GTM. Icon: `gauge`. Tag: `// 04 · SHIP`
5. **Iteration Suggestions** — AI reads session replays + funnels, proposes the next 3 changes ranked by expected lift. Icon: `refresh-cw`. Tag: `// 05 · LEARN`
6. **Decision Log** — every choice timestamped and reversible. A founder's git history for product decisions. Icon: `scroll-text`. Tag: `// 06 · REMEMBER`

Each card: 48px icon tile (indigo stroke on `ink-3`), h3 1.25rem, muted body, mono tag bottom-left. Hover: border lifts to indigo.

**Pricing (3 cards, middle highlighted)**
- **Solo** — `$0` — "Validate the idea" — 1 project, 50 test participants/mo, 14-day event retention
- **Startup** — `$29/mo` — "Ship and learn" — 5 projects, 500 participants, 90-day retention, iteration engine. **Most founders start here** (mono caption, indigo border)
- **Studio** — `$99/mo` — "Run a portfolio" — 25 projects, 5,000 participants, SSO, decision log export, priority queue
- Below: "All plans include the compass, the AI workbench, and unlimited collaborators during alpha. Pricing locks at launch for waitlist members."
- Each card has a `Join waitlist` button (no checkout — this is a teaser)

**FAQ (accordion, 5 items, single-open)**
1. *What stage should my idea be at?* — "Anywhere from a sentence to a half-built Replit. The earlier the better — Refinery is cheapest before you've written code you'll throw away."
2. *Do I need to know how to code?* — "No. Prototype Generator and Ship output production-grade Next.js you can read, but you don't have to. If you can write CSS you can extend it."
3. *How is this different from Cursor or Replit?* — "Cursor writes code with you. Replit hosts it. Uncle owns the loop between what you ship, what users do, and what you should ship next. Code is one of four cardinal directions, not the destination."
4. *When does it launch?* — "Private alpha opens to waitlist members in small batches. Public launch target Q1 2027 — this is a teaser, no fake ship dates, we'll update the line above as we get closer."
5. *Can I cancel or export my work?* — "Yes, both. Every project exports as a clean Next.js repo + a CSV of events + a PDF decision log. You leave with everything you brought."

**CTA waitlist**
- Section bg: subtle radial gradient indigo@20% → transparent
- H2: "Get on the list. We're opening alpha in small batches."
- Sub: "Two emails a month. Real product notes. No growth hacks, no spam."
- Form: email input + submit button, stacked mobile
- States: idle / submitting / success (form morphs to "You're in. Position #N" with teal check) / error

**Footer**
- 3 columns: Product (Features, Pricing, Changelog, Roadmap), Company (Manifesto, Contact, Privacy, Terms), Resources (Docs — soon, Status — soon, Brand kit)
- Bottom: compass mark + `© 2026 Uncle Inc.` (mono dim) + `Built with Next.js 14 · App Router`

## 4. USER FLOWS
**Primary flow: Land → Scan → Join waitlist**
1. Land on `/` with transparent nav
2. Read hero H1 + sub (~5s)
3. See live waitlist counter (`// 247+ founders on the list`)
4. Either scroll through Features → Pricing → FAQ, or hit `Join the waitlist` (smooth-scrolls to `#waitlist`)
5. Type email → submit → 600ms spinner → success card shows "You're in. Position #248." with teal check
6. Hit pricing card CTA → same flow with `source:
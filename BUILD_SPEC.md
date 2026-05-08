# liamdcollier.com — Build Specification

## Context

You are building a single-page personal website for Liam Collier at liamdcollier.com. This site is the personal credibility surface that pairs with infraxus.com (the firm's site). The two sites serve different purposes and must remain visually distinct while sharing a brand family.

Before you begin, fetch and read infraxus.com in full. It is the brand-family reference. The personal site must feel like it was built by the same hand that shaped infraxus.com — same restraint, same density, same refusal of marketing performance — but operating in a more personal register. Where infraxus.com is institutional, this site is human. The shift is in voice and a small number of humanising details, not in visual flourish.

## Audience and purpose

Bimodal audience. AU/NZ/US owner-operators of businesses doing US$1M-$30M revenue who received an email or were referred and are doing a 30-90 second verification check. AU recruiters running triage on contract finance applications. Occasional CFOs, US founders, and other referral traffic. All read fast. None tolerate multi-page navigation. The site's job is to clear verification at speed, then reward the small subset who scroll further with depth.

Conversion is not measured in volume. It is measured in the quality of replies. The site filters aggressively in favour of the right reader.

## The bar

This is a top-1% custom build in a specific category: the personal site of a senior operator who has chosen to maintain a personal presence with the same craft they bring to their work. The reference category is small. Examples in spirit: Patrick McKenzie's Kalzumeus, Jim Nielsen's site, Frank Chimero's site, Tom Blomfield's pre-acquisition personal site, the typographic register of Stripe Press, the spatial sensibility of well-designed central bank publications and serious technical documentation.

What unites these references: **the site looks made, not designed**. The craft is everywhere — in the type, the rhythm, the spacing — but invisible to a casual reader and immediately recognisable to a craft-aware reader. The site does not announce its production quality. It rewards close reading.

Anti-references — what this site explicitly does not look like: personal-brand sites for influencers or coaches, hero-photography-led founder sites, gradient-heavy SaaS landing pages, Webflow-template aesthetics, Awwwards-style motion-design portfolios. None of those.

The bar in concrete terms: a senior product designer at Stripe, Linear, or Vercel lands on this site and recognises that every typographic decision is deliberate, the spatial system is doing real work, and the architecture diagram is built rather than stock — *and also* registers that the voice is human, the page reads warmly, and the writer is recognisably a person. That dual registration — crafted and human — is what we are executing to.

## Tech stack and infrastructure

Static HTML, CSS, and minimal JavaScript. No framework. No build tooling beyond what's needed for the type stack. Deploy target: Vercel free tier. Total page weight target: under 200KB including fonts and the architecture diagram. Page must achieve a 100/100/100/100 Lighthouse score on Performance, Accessibility, Best Practices, and SEO. First Contentful Paint under 800ms on simulated 3G. No layout shift (CLS = 0). No render-blocking JavaScript.

Repository structure:

```
/
├── index.html
├── styles.css
├── fonts/
│   ├── Fraunces[opsz,SOFT,WONK,wght].woff2
│   ├── Inter.var.woff2
├── images/
│   ├── architecture-diagram.svg (placeholder for now)
│   ├── liam-portrait.jpg (optional, only if provided)
├── favicon.ico
├── favicon.svg
└── robots.txt
```

All assets self-hosted. No CDN dependencies. No external script tags. No analytics. No cookies. No tracking of any kind.

## Typography — non-negotiable

Use real, properly-licensed type. Self-host. The site lives or dies on type quality.

Font pairing: **Fraunces** (display) and **Inter** (body). Both are variable, both are free for any use, both are best-in-class in their categories.

Source the variable font files directly from their official sources:
- Fraunces: github.com/undercase-type/Fraunces (download the variable `.ttf` or `.woff2` from the Releases page)
- Inter: github.com/rsms/inter (download `Inter.var.woff2` from the latest release)

Do not load from Google Fonts CDN. Self-host. Subset to Latin Extended only. Use `font-display: swap` and preload both fonts in the document head.

Both fonts have full variable axis control. Use this — it's the entire reason these two were chosen over standard alternatives:

**Fraunces axes to use:**
- `wght` (weight) — set headings at 400 (regular), identity line at 380 for slightly lighter feel
- `opsz` (optical sizing) — set to match the actual rendered size at every size step (this is the variable that makes Fraunces look like a foundry font)
- `SOFT` — set to 50 for slightly softened terminals, more humanist feel
- `WONK` — set to 0 (off). Wonky alternates are too playful for this register.

**Inter axes to use:**
- `wght` — body at 400, system names and emphasis at 500
- `opsz` — set to match rendered size; Inter has subtle but real optical adjustments

Type rendering rules:
- `font-feature-settings: "kern" on, "liga" on, "calt" on, "onum" on` for body text (old-style figures in prose).
- `font-feature-settings: "tnum" on, "lnum" on` for tabular content (the Background block dates, system descriptions where numbers appear).
- `font-feature-settings: "smcp" on` for section headers (small caps).
- `text-rendering: optimizeLegibility`.
- Real apostrophes (`'`), real quotation marks (`" "`), em-dashes (`—`) only where structurally necessary — *the brief explicitly requests no em-dashes in body copy*. Use commas, periods, and parenthetical structures instead. Honour this.
- Hanging punctuation via `hanging-punctuation: first`.
- `text-wrap: pretty` on body paragraphs to avoid widows and orphans.

Body text: 18px base, 1.55 line-height, max-width 64ch.
Display text: scaled from 32px to 48px using clamp() for responsive sizing.
Modular scale: 1.250 (major third) for type sizing.

**Optical sizing implementation note:** Fraunces and Inter both expose `opsz` as a variable axis. The browser will pick this up automatically if you use `font-variation-settings` and let the CSS engine handle the size mapping, *but* the implementation is more reliable if you set `font-optical-sizing: auto` explicitly on body, headings, and any other typographic context. Do this on every type-bearing element. It's the difference between *technically using a variable font* and *actually using a variable font well*.

## Spatial system — non-negotiable

8px base unit. All spacing values are multiples of 8px (8, 16, 24, 32, 40, 48, 64, 96, 128). No arbitrary values.

Vertical rhythm: 8px baseline grid. All elements snap to the grid.

Page max-width: 720px for the main content column. Centred. Generous side margins on desktop (minimum 64px each side at 720px+ viewport widths). Mobile margins: 24px each side.

Sections separated by 96px on desktop, 64px on mobile. Within sections, paragraphs separated by 24px. Lists use 16px between items.

## Colour palette

Restrained. Five colours total.

- Background: `#FAF8F4` (warm off-white, paper-like)
- Body text: `#1A1A1A` (near-black, not pure black)
- Headings: `#0A0A0A` (slightly darker than body)
- Accent / links: `#1F4E5F` (deep teal, sampled from infraxus.com palette family — verify against the live site and adjust to match)
- Subtle / metadata: `#6B6B6B` (mid-grey for dates, captions, footer)

Hover states: links shift to `#0F2E3F` (darker teal) with a 1px underline appearing. Transition: 100ms ease-out.

Selection colour: text on selected text uses a faint warm yellow background (`#F5E6A8`) with `#1A1A1A` text.

## Page structure

The page has eight blocks in this exact order. Each block has a defined purpose and a defined length envelope.

### Block 1: Identity line

The first thing on the page. Positioned 96px from the top of the viewport on desktop, 64px on mobile.

Content:
> Liam Collier. Founder of Infraxus. I run a finance firm built around getting the numbers straight before the decisions get made.

Typography: this is the largest text on the page. Display face, regular weight, set at clamp(32px, 4vw, 48px). Line height 1.2. Three sentences, set on three lines if it fits naturally, otherwise allow flow. Use a manual `<br>` between sentences for typographic control.

No subheading. No tagline. No image alongside. The identity line stands alone.

### Block 2: Orienting paragraph

Single paragraph, ~60-90 words. Body text size. Sits 64px below the identity line.

Provisional copy (will be replaced in copy refinement pass — do not over-invest in this draft):

> Infraxus is a fixed-fee finance diagnostic for owner-operated businesses, US$1M to US$30M in revenue, in Australia, New Zealand, and the United States. I founded it in New York in 2025 and operate it from Melbourne and Medellín. Before Infraxus I worked in business advisory at BDO in Auckland, then as a finance business partner at a 130-person law firm in Melbourne. I built the technical infrastructure that runs the firm.

Body text. Standard paragraph spacing. The infraxus.com link is the only inline link in this block; styled as accent colour with subtle underline.

### Block 3: Questions this work tends to answer

Header: *Questions this work tends to answer*

Below the header, six questions in italic body text, each on its own line, 16px between them. Indent 32px from the left margin. No numbering, no bullet points.

The questions:

1. Why does my bank balance not match what the P&L says I'm making?
2. Can the business afford the next hire without breaking cashflow inside two quarters?
3. Which clients, projects, or service lines are actually profitable to serve, and which are quietly costing me money?
4. If revenue stays flat for the next twelve months, where does cash actually run out?
5. Is the financial information leadership is making decisions from accurate enough to be making decisions from?
6. What needs to happen in the next ninety days to put the business in a defensible position before the next downturn, lender review, or capital decision?

Set in italic to distinguish from declarative body text. The italic carries the *"these are questions, not statements"* signal typographically.

### Block 4: Built

Header: *Built*

Below the header, a single paragraph of orienting copy (~30-40 words):

> The infrastructure that runs Infraxus is built solo. Same architectural register as the offer: structured, documented, designed for the operator working alone. Selected systems below.

Then a list of three to five system descriptions. Each item is one line: a system name in body weight, followed by a one-sentence description in lighter grey. Items separated by 16px.

Use this content (provisional, refine in copy pass):

- **Infraxus Portal** (`app.infraxus.com`) — Multi-tenant finance intelligence product with AI commentary, forecast modelling, and authenticated client dashboards. Built April 2026.
- **Sales orchestration system** — Production B2B sales infrastructure replacing a Clay-based stack at one-tenth the cost. Sonnet qualifier, Apollo enrichment, HubSpot orchestration, twelve-inbox email cadence, autonomous LinkedIn outreach.
- **Sales intelligence reasoning layer** — Continuous analytical system above the sales infrastructure. Captures every interaction; runs Opus reasoning on a four-hour cadence; surfaces patterns and risks via Pushover and morning briefings.
- **Seek lead pipeline** — Autonomous AU job-listing scraper that converts hiring signals into qualified outbound leads. Runs unsupervised on a daily cadence.
- **Sales Command Center** — Authenticated operator dashboard at `app.infraxus.com/sales` consolidating funnel state, pipeline reality, channel health, and cohort intelligence into a two-tab surface.

System names in body text. URLs styled as accent links where they're live. Descriptions in `#6B6B6B`.

### Block 5: The architecture diagram

This is the visual centrepiece. Embed the SVG inline (`<svg>` tag, not `<img>` reference). Reasons: sharper at any zoom level, themable via CSS, no additional HTTP request.

The diagram will be supplied separately as `images/architecture-diagram.svg`. For the build, leave a placeholder div that matches the diagram's expected dimensions:

```html
<figure class="diagram">
  <!-- architecture-diagram.svg will be inlined here -->
  <figcaption>The Infraxus sales orchestration architecture, simplified.</figcaption>
</figure>
```

Style the figure with:
- 64px top and bottom margin
- Full-width within the content column
- `figcaption`: small caps, 14px, mid-grey, centred below the diagram with 16px top margin

The diagram itself will use the brand-family colour palette but is generated separately. The site build does not need to construct it.

### Block 6: Background

Header: *Background*

Below the header, a chronological timeline rendered as a structured list — not a visual timeline graphic. Each entry: location and date range on the left (italic, mid-grey, tabular figures), role/context on the right (body weight). Layout: definition-list pattern using CSS grid.

Entries:

- **Wellington, 2017–2020** — Bachelor of Commerce, Accounting and Finance, Victoria University of Wellington. Certificate of Excellence. A- GPA.
- **Auckland and Barcelona, 2020–2023** — Business Advisory at BDO. Promoted through four roles in under two years; trained two graduate consultants while completing the CA programme. Negotiated remote engagement structure to relocate to Barcelona for the final twelve months.
- **Melbourne, 2023–2024** — Finance Business Partner at a mid-tier law firm. Ran the finance brief in board meetings during repeated CFO absences; owned the three-way forecast for ATO and lender reporting; contributed to Remuneration Committee discussions including partner-level analysis.
- **New York, 2025** — Founded Infraxus. First version of the firm and its infrastructure built in Lower Manhattan over four months.
- **Melbourne / Medellín, 2026–present** — Operating Infraxus across both bases.

Format: definition list (`<dl>`) with custom styling. Two-column grid on desktop (location/date column 30%, content column 70%), stacked on mobile.

### Block 7: Detail

Header: *Detail*

Three small substance facts, each on its own line, in body text:

- Spanish (fluent). First lived in Medellín on exchange in 2018.
- Graduate Diploma in Chartered Accounting, CA ANZ, 2023.
- Australian work rights. Operating between Melbourne and Medellín.

This is the deliberately compressed credentials block. Three lines. No section, no paragraph, no expansion.

### Block 8: Footer

Bottom of page. Separated from Block 7 by 96px.

Three elements, all in mid-grey:

1. *liam@infraxus.com* (mailto link, accent colour)
2. A horizontal rule (1px, mid-grey, 30% opacity, full content-width)
3. Two lines of metadata:
   - *Last updated: [today's date in format "7 May 2026"]* — generate dynamically based on build date, hardcode as static text.
   - *Built solo. No tracking. No analytics. No cookies.*

This footer is the *signature* of the page. It communicates that the site is alive, maintained, and operates by the same principles the firm operates by.

## Microcopy details

- Section headers (Block 3, 4, 6, 7): set in display face, regular weight, 24px size, with 8px of letter-spacing increase, all small caps via OpenType feature (`font-feature-settings: "smcp" on`). 48px below the previous block, 32px above the block's content.
- Inline emphasis: italic, never bold. Bold reserved for system names in Block 4.
- Links: subtle underline (1px solid, offset 4px below baseline). Hover: colour darkens, underline thickens to 2px. Focus: 2px solid outline, accent colour, 4px offset.
- All numbers in tabular content use tabular figures (`font-feature-settings: "tnum" on`). All numbers in body prose use proportional old-style figures.

## Accessibility

WCAG AA minimum, target AAA where reasonable.
- Semantic HTML5: `<main>`, `<article>`, `<section>`, `<header>`, `<footer>`, proper heading hierarchy.
- All interactive elements keyboard-accessible.
- Focus indicators visible and high-contrast.
- Skip-to-content link at the top, visually hidden until focused.
- Alt text on the architecture diagram describing what it depicts in two sentences.
- `prefers-reduced-motion` respected for all transitions (set to instant when user prefers reduced motion).
- `prefers-color-scheme: dark` is *not* honoured. Site is light-mode only by deliberate choice; the warmth of the off-white paper colour is part of the brand register.
- `lang="en-AU"` on the html element.

## Mobile

The site is mobile-first in priority but desktop-tested for the craft layer. Most readers will be on mobile.

- Single-column layout always.
- Side margins: 24px.
- Type scales down: identity line at 32px, body at 17px.
- Background block: definition list collapses to stacked entries (location/date on its own line above the content, both visible without ambiguity).
- Architecture diagram: full-width, height auto-scaled. Must be readable on a 375px-wide viewport. If diagram complexity prevents this, provide a tap-to-zoom interaction (no JS needed; use `<details>` with the diagram inside, or a pure-CSS modal pattern).
- Tap targets minimum 44px square.
- No hover-dependent functionality.
- Test specifically on iPhone SE viewport (375x667) as the floor case.

## Build sequence — execute in this order

**Phase 1: Foundation.** Set up the repo, the static structure, the type stack (download Fraunces and Inter variable font files; subset and self-host). Establish the colour palette as CSS custom properties. Build the spatial system as CSS custom properties on `:root`.

**Phase 2: Page build.** Write index.html with all eight blocks in sequence using the provisional copy supplied above. Write styles.css implementing the typography, spatial system, and colour rules. Inline the architecture diagram placeholder.

**Phase 3: Microtypography pass.** Go through the entire site and verify: real apostrophes and quotes throughout, no em-dashes in body copy (replace with restructured sentences), proper figure types in their proper contexts, hanging punctuation working, optical sizing variable axis applied where the font supports it, kerning tuned on the identity line.

**Phase 4: Mobile pass.** Test at 375px, 414px, 768px, 1024px, 1440px viewport widths. Adjust spacing, type sizes, and the Background block grid behaviour. Verify the architecture diagram is readable or has a tap-to-zoom fallback.

**Phase 5: Accessibility and performance audit.** Run Lighthouse. Target 100/100/100/100. If any score is below 100, identify why and fix. Verify keyboard navigation works for all interactive elements. Verify screen reader output is sensible.

**Phase 6: Self-audit against the brief.** Re-read this build specification from the top. For each requirement listed, verify the build delivers it. Identify any gap. Where the implementation is below the bar described in *The bar* section, uplift it. Specifically check:

- Is every typographic decision deliberate, or are there places where defaults are leaking through?
- Is the spatial rhythm consistent, or are there breaks in the 8px grid?
- Does the page read as crafted-and-human, or has it slipped toward institutional cold?
- Would a senior product designer at Stripe, Linear, or Vercel landing on this page recognise the craft?

**Phase 7: Uplift pass.** Based on Phase 6 audit, make targeted improvements. Do not rebuild from scratch. Make precise, surgical changes that close the gap between current state and the bar.

**Phase 8: Final delivery.** Commit all files, push to the remote, deploy to Vercel, configure the liamdcollier.com domain DNS to point at the deployment, verify the live URL renders correctly.

## Constraints — read carefully

Do not interrupt the build to ask clarifying questions. The specification above is sufficient to complete the build. Where ambiguity exists, default to: more restraint, more whitespace, more typographic precision, less decoration.

Do not add elements not specified above. No hero photography. No motion graphics. No scroll-triggered animations. No testimonials. No social proof. No CTAs. No newsletter signup. No "work with me" buttons. No client logos. No footer navigation menu (the footer is just contact + metadata as specified).

Do not use any UI library, component library, or design system library. Build everything from scratch. This is a craft surface; importing components defeats the purpose.

Do not use Tailwind. Use vanilla CSS with custom properties.

Do not generate placeholder images. The architecture diagram is the only image. The portrait is optional and will be supplied if used.

Do not use lorem ipsum anywhere. The copy supplied above is the build copy; it will be refined in a separate pass post-launch.

When the build, audit, and uplift cycle is complete, finish without prompting for review or feedback. The next iteration will happen in a separate session.

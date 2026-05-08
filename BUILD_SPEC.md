# liamdcollier.com — Build Specification v3

## Status

This document supersedes any prior build specification for liamdcollier.com. The first build of this site produced a structurally and visually wrong result — a single column of running prose under bare headings, on a warm-off-white background with serif type, that reads as a Word document on a domain rather than as a designed personal site. This specification rebuilds the page from scratch.

## Background on the failure

The brief that produced the first build was written without the author having actually examined the rendered visuals of the reference sites. The author worked from text extraction of the references' HTML, which gave structural information but not visual information. That blind spot produced a brief that specified a visually thin treatment.

This v3 specification compensates for that blind spot by making *visual reference analysis* the first binding phase of the build. The colour palette, exact typographic treatment, and visual density specifications are deliberately left open in this document, because the author cannot specify them correctly without seeing the references. You — Claude Code — will determine those specifications by actually looking at the references using whatever tools you have available.

## Critical constraint

**You must not stop the build under any circumstances.** Phase 1 and Phase 9 are binding gates that produce real outputs, not optional steps. If a tool you would prefer is unavailable, find another way. If you reach a point where you have exhausted reasonable options, document what you tried and ship the strongest version you produced, with notes in the final delivery summary on what is still unresolved. The user is asleep and will review the live site in the morning. There is no one to review interim output. Push through.

## What stays from prior builds

**Infrastructure stays.** Repo, git remote, Vercel deploy, domain, Fraunces and Inter fonts in `/fonts`, `vercel.json`, `sitemap.xml`, `robots.txt`, favicon files. Do not touch.

**Page content stays.** The substance — the identity statement, the time-bucketed career arc, the systems list, the questions, the background entries, the credentials, the contact block — is specified in Phase 4 of this document.

**Tech stack stays.** Static HTML and CSS, no framework, self-hosted fonts, deploy to Vercel.

**Performance and accessibility targets stay.** Lighthouse 100/100/100/100 on production. WCAG AA minimum.

## What is being rebuilt

**Page architecture.** The page is rebuilt from scratch with structural variation across sections — discrete designed components, not running prose.

**Visual treatment.** Determined empirically by analysing reference sites in Phase 1. Not specified in this document. You will derive the visual treatment from the references, not from this document.

---

## Phase 1: Reference analysis (binding)

### Step 1.1 — Fetch the references' rendered presentation

For each of the following URLs:

1. Fetch the HTML.
2. Identify and fetch the linked stylesheet(s) referenced in the HTML (use WebFetch on the absolute URL of each stylesheet).
3. Read the CSS to extract: background colour(s), text colour(s), accent colour(s), font families used, font sizes, layout structure (grid / flexbox / single column), spacing system, any visual elements (borders, shadows, dividers), any unusual typographic moves.
4. If your tooling allows you to render the sites as screenshots (headless browser, Playwright, Puppeteer, any image-capture method), capture each site at 1440px and 375px viewports. If your tooling does not support this, proceed with HTML+CSS analysis only.

Reference URLs:

- `https://sive.rs` — Derek Sivers (primary structural reference)
- `https://interconnected.org` — Matt Webb (primary structural reference)
- `https://joshpigford.com` — Josh Pigford (primary structural reference)
- `https://www.kalzumeus.com` — Patrick McKenzie (primary structural reference)
- `https://infraxus.com` — Liam's firm site (visual register reference for brand family, but not structural reference)

### Step 1.2 — Synthesis of the visual register

After examining the references, write a short analysis (output to the conversation, not to a file) covering:

- **Background colour patterns.** What backgrounds do the four primary references use? Pure white, off-white, warm off-white, or something else? Do any deviate?
- **Text colour patterns.** Pure black, near-black, or something with character?
- **Accent / link colour patterns.** What hues are used? Are they similar across references or varied?
- **Type pairing patterns.** Do the references use serif body, sans-serif body, monospace, or mixed? What sizes?
- **Visual density patterns.** How busy do the pages feel? What ratio of text to other elements?
- **Structural-element patterns.** Do they use horizontal rules, borders, boxes, cards, columns, dividers, images, icons?
- **The cohesion question.** Looking at the four primary references and infraxus.com side by side, does the personal-site cluster have a distinct visual register from the firm-site? If so, what is it?

Then make a binding decision: **what colour palette, type treatment, and visual density will this build use, given what you actually saw?**

Justify the choice in 2-3 sentences. The choice may match prior specifications (warm off-white background, near-black text, deep teal accent). It may deviate. It may be substantially different. Make the call from evidence.

### Step 1.3 — Anti-pattern check

Specifically check whether any of the four primary references rely on:

- A single-column layout of running prose under section headings *without any other structural variation*.

If none of them do, that confirms what the v1 build got wrong. Note this in the analysis. Use it as a binding constraint: the rebuilt site must have structural variation across sections.

---

## Phase 2: Reset

Empty `index.html` and `styles.css`. Remove placeholder content from `images/architecture-diagram.svg` (keep the file, drop the contents). Confirm git is clean.

---

## Phase 3: Visual treatment design

Based on the Phase 1 analysis, define the design tokens for the build:

- Colour palette as CSS custom properties on `:root`
- Typography scale and feature settings
- Spatial scale (8px base, modular scale)
- Borders, dividers, and any other visual treatments

Document the choices in CSS comments at the top of `styles.css` so they are visible to a future maintainer.

---

## Phase 4: Page content specification

The page has nine sections in this order. Each is a discrete designed component with structural variation. The specification below covers the *content and intent* of each section, not the literal visual treatment, which you will design from Phase 1 evidence.

### Section 1: Header bar

Persistent header at the top. Two elements: wordmark *Liam Collier* on the left, navigation row on the right. Nav links: *Built · Background · Detail · Contact*. Each is an anchor link to its corresponding section with smooth scroll behaviour.

Header is not sticky. Sits at the top of the document.

On mobile, nav row collapses below the wordmark.

### Section 2: Identity block (centrepiece of upper page)

Contains, in this order:

- Name: *Liam Collier.*
- Role: *Founder of Infraxus, a finance firm for owner-operated businesses.* The word *Infraxus* is a link to `https://infraxus.com`.
- Time-bucketed career arc, five lines:
  - *(2017–2020): Studied accounting and finance in Wellington.*
  - *(2020–2023): Business advisory at BDO, Auckland and Barcelona.*
  - *(2023–2024): Finance business partner at a mid-tier law firm in Melbourne.*
  - *(2025): Founded Infraxus in New York.*
  - *(2026–): Operating between Melbourne and Medellín.*
- Headshot from `https://infraxus.com/images/headshot-liam.webp`. Download to `images/headshot-liam.webp` and reference locally.

Layout: text and headshot in some kind of arrangement that gives the headshot visual weight without dominating the page. The headshot should read as a *human anchor*, not a hero image. On mobile, headshot and text stack.

The career-arc lines should have typographic differentiation between the date range and the descriptive text. This is the Sivers pattern from `https://sive.rs`. Verify against the reference in Phase 1 and adapt.

### Section 3: Built (systems block)

The high-density signal section. Five systems, each as a structured row.

Each row contains:

1. **System name** — typographically prominent. If the system has a live URL, the name is the link.
2. **Status indicator** — a designed visual element (pill, tag, label, badge, your design choice based on Phase 1) that shows whether the system is *Live*, *Production*, or *Internal*.
3. **One-sentence description** — secondary visual weight.

The five systems:

- **Infraxus Portal** (`https://app.infraxus.com`) · *Live* — Multi-tenant finance intelligence product with AI commentary, forecast modelling, and authenticated client dashboards.
- **Sales orchestration system** · *Production* — B2B sales infrastructure replacing a Clay-based stack at one-tenth the cost. Sonnet qualifier, Apollo enrichment, HubSpot orchestration, twelve-inbox cadence, autonomous LinkedIn outreach.
- **Sales intelligence reasoning layer** · *Production* — Continuous analytical system above the sales infrastructure. Captures every interaction, runs Opus reasoning on a four-hour cadence, surfaces patterns and risks via Pushover and morning briefings.
- **Seek lead pipeline** · *Production* — Autonomous AU job-listing scraper that converts hiring signals into qualified outbound leads. Runs unsupervised on a daily cadence.
- **Sales Command Center** (`https://app.infraxus.com/sales`) · *Internal* — Authenticated operator dashboard consolidating funnel state, pipeline reality, channel health, and cohort intelligence.

Note: the dash separator above is for clarity in this specification. In the rendered HTML, replace dashes with the correct typographic separator for your visual treatment — a vertical bar, a centred dot, a colon, a thin rule, whatever is congruent with your design. **Do not use em-dashes anywhere in body copy.**

### Section 4: Architecture diagram

Visual centrepiece. The actual SVG will be supplied in a future session. For this build, render a placeholder that:

- Reads as a *deliberate empty state*, not a broken element
- Has the correct aspect ratio (16:9) and full content-column width
- Has a caption below: *The Infraxus sales orchestration architecture, simplified.*

The placeholder should look intentional. When the real SVG drops in later, the surrounding container styling stays the same.

### Section 5: Questions

Six questions in operator voice. Each on its own line:

1. *Why does my bank balance not match what the P&L says I'm making?*
2. *Can the business afford the next hire without breaking cashflow inside two quarters?*
3. *Which clients, projects, or service lines are actually profitable to serve, and which are quietly costing me money?*
4. *If revenue stays flat for the next twelve months, where does cash actually run out?*
5. *Is the financial information leadership is making decisions from accurate enough to be making decisions from?*
6. *What needs to happen in the next ninety days to put the business in a defensible position before the next downturn, lender review, or capital decision?*

Treatment: italic body text, indented from the content-column edge. Add a visual rhythm element at the start of each line if Phase 1 supports it. Designer's discretion based on what reads correctly.

### Section 6: Background

Definition-list pattern. Five entries. Each entry has a location-and-date column on the left and a description on the right.

- **Wellington · 2017–2020** — Bachelor of Commerce, Accounting and Finance, Victoria University of Wellington. Certificate of Excellence. A− GPA.
- **Auckland and Barcelona · 2020–2023** — Business Advisory at BDO. Promoted through four roles in under two years, trained two graduate consultants while completing the CA programme. Negotiated a remote engagement structure to relocate to Barcelona for the final twelve months.
- **Melbourne · 2023–2024** — Finance Business Partner at a mid-tier law firm. Ran the finance brief in board meetings during repeated CFO absences, owned the three-way forecast for ATO and lender reporting, contributed to Remuneration Committee discussions including partner-level analysis.
- **New York · 2025** — Founded Infraxus. First version of the firm and its infrastructure built in Lower Manhattan over four months.
- **Melbourne / Medellín · 2026–present** — Operating Infraxus across both bases.

Two-column grid on desktop, stacked on mobile. Same separator rule applies — choose one congruent with your visual register, no em-dashes.

### Section 7: Detail

Three single-line facts:

- *Spanish (fluent). First lived in Medellín on exchange in 2018.*
- *Graduate Diploma in Chartered Accounting, CA ANZ, 2023.*
- *Australian work rights. Operating between Melbourne and Medellín.*

### Section 8: Contact

- Email: `liam@infraxus.com` as a `mailto:` link.
- Elsewhere: small horizontal row of links — *Infraxus* (`https://infraxus.com`) and *LinkedIn* (`https://www.linkedin.com/in/liamdcollier`).

### Section 9: Footer

Two small text rows at the bottom of the page, separated from Section 8 by a generous gap and a horizontal rule:

- *Last updated: 7 May 2026*
- *Built solo. No tracking. No analytics. No cookies.*

---

## Phase 5: Section labels — design system

Every section (3 through 9) has a section label that establishes vertical rhythm and signals discrete components. Labels are small caps / spaced caps / similar treatment based on what Phase 1 analysis supports. Labels are accompanied by some kind of visual rule or divider that separates sections.

The label and rule treatment is *the connective tissue across the page*. It is the design element that prevents the page from reading as a single column of prose. **Get this treatment right or the build fails.**

---

## Phase 6: Build the page

HTML first. Semantic HTML5: `<header>`, `<main>`, `<section>` for each block, `<footer>`. Each section has an `id` matching the nav anchor (`built`, `background`, `detail`, `contact`). All interactive elements are keyboard-accessible. Skip-to-content link at the top, visually hidden until focused.

CSS second. Build from design tokens (CSS custom properties) defined in Phase 3. Then base typography. Then layout primitives. Then section-specific styling.

Microtypography pass at the end:

- Real apostrophes and quotation marks (`'`, `"`, `"`)
- No em-dashes in body copy
- `font-feature-settings`: kern, liga, calt, onum on body; tnum, lnum on tabular content; smcp on section labels
- `text-rendering: optimizeLegibility`
- `font-optical-sizing: auto` on every type-bearing element
- `text-wrap: pretty` on body paragraphs
- `hanging-punctuation: first` where supported

---

## Phase 7: Mobile pass

Test at 375px, 414px, 768px, 1024px, 1440px viewport widths. Specific behaviours:

- Header nav collapses to a second row below the wordmark
- Identity block: headshot moves above the text
- Background grid: definition list collapses to stacked entries
- All tap targets minimum 44px square
- All sections readable at 375px without horizontal scroll

---

## Phase 8: Lighthouse audit

Target 100/100/100/100. If any score is below 100, identify why and fix.

---

## Phase 9: Visual diff gate (binding)

This is the gate that compensates for the brief author's visual blind spots. **Do not skip it. Do not soften it. Do not stop on it — find a way through.**

### Step 9.1 — Capture the rebuilt site

If your tooling supports screenshot capture (headless browser, Playwright, Puppeteer): capture the rebuilt site at 1440px and 375px viewports.

If your tooling does not support screenshot capture: proceed to Step 9.2 using structured written analysis.

### Step 9.2 — Compare against references

For each of the four primary references (Sivers, Webb, Pigford, McKenzie):

If you have screenshots: place them side-by-side with the rebuilt site.

If you do not have screenshots: enumerate the discrete designed components present on each reference (using the HTML and CSS you fetched in Phase 1) and the discrete designed components present on the rebuilt site. Compare the lists.

For each comparison, ask:

1. Does the rebuilt site read as the same category of artifact as the reference, or as visually thinner?
2. Does the rebuilt site have comparable visual density per square inch?
3. Does the rebuilt site have structural variation across sections comparable to the reference?
4. Would a senior product designer at Stripe, Linear, or Vercel see the rebuilt site as belonging in the same set as the reference, or as a budget version?

### Step 9.3 — If the visual diff fails, uplift

If the rebuilt site reads as thinner, less designed, or less structurally varied than any of the four references:

- Identify the visual elements present on the references that are absent on the rebuilt site
- Add those elements within the constraints of this specification: no testimonials, no logo walls, no animations, no gradients, no marketing language
- Re-screenshot or re-enumerate
- Iterate until the rebuilt site sits credibly alongside the references, or until you have completed three uplift cycles

### Step 9.4 — If three uplift cycles are not enough

If after three uplift cycles the visual diff still fails, document what you tried in the final delivery summary, identify what specifically is causing the gap, ship the strongest version you produced, and continue to deploy. Do not stop the build. The user will review the live site in the morning and iterate from there.

---

## Phase 10: Deploy

Commit and push to main. Vercel auto-deploys. Verify the live URL renders correctly at liamdcollier.com.

---

## Phase 11: Final delivery

Output a summary with:

- Confirmation the live URL renders correctly
- Lighthouse scores
- The colour palette and design tokens you chose, with the justification from Phase 1.2
- The visual diff results from Phase 9 (including any uplift cycles and what you changed)
- Any unresolved gaps, with a clear note on what is still needed
- Any deviations from this specification, with reasons
- Location of the architecture diagram placeholder for replacement in a future session

---

## Constraints

Do not interrupt the build to ask clarifying questions. The user is asleep.

Where the specification covers content but not visual treatment, that is deliberate — the visual treatment is your call from Phase 1 evidence.

Where ambiguity exists, default to: more structural variation, more designed-component-feel, more visual density, less running prose.

Do not import infraxus.com's axis matrix patterns, fee dimension tables, or capability tables into the personal site. The visual register may transfer; the structural logic does not.

Do not use lorem ipsum. The copy supplied in this specification is the build copy. It will be refined in a separate pass post-launch.

Do not deploy a build that you have not tried hard to uplift. But also do not stop indefinitely. Three uplift cycles is the upper bound. Then ship and document.

Begin with Phase 1.

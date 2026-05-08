# liamdcollier.com — Architecture Diagram & Rigorous Audit Specification

## Purpose

The previous build of liamdcollier.com shipped with two unresolved gaps:

1. The architecture diagram is a styled empty state. The SVG file is intentionally empty. The visual centrepiece slot is unfilled.
2. The visual diff audit was self-graded as "PASS on cycle 1, no uplift required." This is the same failure mode as previous specs — the executor judging its own output. The result is materially better than the v1 Word-document build but has not been rigorously tested against the references.

This specification covers both. It generates the real architecture diagram from canonical source material and runs a properly rigorous audit-and-uplift cycle that gates on observable criteria rather than self-judgement.

## What stays from prior builds

Everything that is currently live at liamdcollier.com stays. This is not a rebuild. The page architecture, palette, typography, and section structure from the v3 build are correct and remain unchanged. This specification *adds* the diagram and *uplifts* the existing build where the audit identifies gaps.

## Phase 1: Read the source

Read `references/02_Sales_System_Reference.docx` in full. This document is the canonical reference for the Infraxus sales system architecture. It is sufficient to understand: the data sources, the processing layers, the orchestration components, the channels, the operator interfaces, and the relationships between them.

Output a brief structural summary (8-15 lines) of what the diagram needs to depict — components, layers, flows. This is your working brief for the SVG generation. Output it to the conversation.

## Phase 2: Generate the architecture diagram SVG

### Constraints

- **Format:** Inline-ready SVG. Self-contained, no external dependencies.
- **Dimensions:** 16:9 aspect ratio, designed for full content-column width (~720px wide on desktop, scaling down on mobile). Use `viewBox` for proper scaling. Do not hardcode pixel widths.
- **Colour palette:** Use the existing site palette tokens. Background should be transparent (the page background `#FBF6EC` shows through). Lines, boxes, and labels in `#1A1A1A` (body) and `#0A0A0A` (heading) for primary text. Accent components in `#1E50FF`. Status colours where meaningful: `#10B981` for live components, `#F59E0B` for production, `#71717A` for internal. Hairline rules in `#E8DEC9`.
- **Typography:** Inline `font-family` declarations referencing Inter (sans-serif fallback) for component labels. Do not embed fonts in the SVG.
- **Visual register:** The diagram is a **structural architecture diagram**, not a marketing infographic. Reference register: the system architecture diagrams in well-engineered technical documentation (Stripe Press, AWS architecture diagrams, Linear's engineering posts). Boxes, lines, labels. No gradients. No drop shadows. No 3D effects. No emoji. No icons that aren't structural.
- **Information density:** Match the depth of the source document. The diagram should reward close reading. A casual scan should communicate the overall shape (data sources → processing → orchestration → channels → reasoning layer → operator interface). A close reader should be able to identify specific named components (Sales Nav, Apollo, Sonnet qualifier, HubSpot, Telegram, Opus reasoning, etc.).

### Specific design moves

- **Layered structure.** The diagram should read top-to-bottom or left-to-right with clear functional layers. Source layer at the top/left. Processing layer in the middle. Output/orchestration at the bottom/right. Use whitespace and hairline dividers to separate layers visually, not boxes around groups.
- **Component naming.** Each component is a small rectangle with a tight border (1px, `#1A1A1A`), a name in body weight, and an optional one-line subtitle in muted weight (`#6B6B6B`).
- **Flow arrows.** Direction of data flow shown by thin arrows (1px or 1.5px, `#1A1A1A`, with simple triangular arrowheads). Arrows curve only when necessary; prefer orthogonal routing.
- **Status indicators.** If a component is live in production, mark it with a small dot in `#10B981`. If it's in a different state, use the appropriate status colour. Position dots in the top-right corner of the component rectangle. Sparingly — only on components where the state is meaningful.
- **No legend at first.** Try to make the diagram self-explanatory through component labelling. If a legend is genuinely necessary, add it as a small block in the bottom-right corner.
- **Title and caption.** The diagram has a small title at the top in eyebrow style (Inter, 11px, all caps, 0.18em letter-spacing, `#6B6B6B`): *INFRAXUS · SALES ORCHESTRATION ARCHITECTURE*. No caption inside the SVG — the caption already exists in the page (`<figcaption>`).

### Generation process

1. Sketch the component graph mentally from Phase 1's summary. Identify the layers and primary flows.
2. Generate the SVG as inline markup. Hand-write the SVG; do not use a generator that produces verbose machine output. Target under 8KB total file size. Comment the SVG with section headers (`<!-- SOURCE LAYER -->`, `<!-- PROCESSING -->`, etc.) so a future maintainer can edit it.
3. Save to `images/architecture-diagram.svg`.
4. Update `index.html` Section 4: replace the `<div class="diagram__placeholder">…</div>` with either an inline `<svg>…</svg>` (preferred, for sharpness and zero additional HTTP requests) or `<img src="/images/architecture-diagram.svg" alt="Architecture diagram of the Infraxus sales orchestration system. Data sources flow into a Sonnet qualifier, then into HubSpot orchestration which fans out to email and LinkedIn channels. A continuous Opus reasoning layer sits above all interactions and surfaces patterns to the operator.">`. The surrounding `<figure>` and `<figcaption>` stay as-is.
5. Adjust `styles.css` as needed for the inlined SVG: ensure it scales to full content-column width, maintains the 16:9 aspect ratio, and inherits the page's typographic colour and weight where SVG elements use `currentColor` or unstyled defaults.

### Quality bar for the diagram

The diagram must:
- Render at full content-column width on desktop without horizontal scroll
- Remain readable at 375px mobile viewport (component labels still legible — if not, increase font size in the SVG, do not change the diagram structure)
- Be visually congruent with the rest of the page (same palette, same typographic feel, same restraint)
- Communicate the architecture's structural shape in under five seconds of scan time
- Reward 30+ seconds of close reading with specific component-level information

If the first attempt does not meet any of these, regenerate. Up to three diagram-generation attempts before locking the result.

## Phase 3: Rigorous audit (replaces the failed self-graded audit)

This phase replaces the previous build's "PASS on cycle 1, no uplift required" failure. The audit is now gated on **observable, numerical, externally-verifiable criteria**, not on your judgement.

### Step 3.1: Capture screenshots

Use Puppeteer (already proven to work in the previous session) to capture:

1. The live liamdcollier.com at 1440px and 375px viewports. Two screenshots.
2. Each of the four primary references at 1440px and 375px. Eight screenshots.
3. infraxus.com at 1440px. One screenshot.

Save all to `/tmp/audit-screenshots/` with descriptive filenames.

### Step 3.2: Run the structural audit

For each of the four primary reference screenshots and the rebuilt site, do the following analysis. Output the results as a structured table.

**Component count.** Count the discrete designed components visible above the fold (top 900px on desktop). A "component" is any visually-distinct designed element: a header bar, a portrait, a status pill, a section label with rule, a definition list row, a card, a numbered list with custom markers, etc. Plain text paragraphs and bare headings do not count as components.

| Site | Above-fold components |
|------|----------------------|
| sive.rs | (count) |
| interconnected.org | (count) |
| joshpigford.com | (count) |
| kalzumeus.com | (count) |
| liamdcollier.com | (count) |

**The rebuilt site's component count must be within ±2 of the reference median.** If lower, the site is visually thinner than the references. If significantly higher, it may be over-busy.

**Section variation.** Count the number of distinct visual treatments across all sections of the page (not just above the fold). Two sections that look the same (e.g., two sections of running prose under bare headings) count as one treatment.

| Site | Distinct section treatments |
|------|---------------------------|
| sive.rs | (count) |
| interconnected.org | (count) |
| joshpigford.com | (count) |
| kalzumeus.com | (count) |
| liamdcollier.com | (count) |

**The rebuilt site's distinct treatment count must be ≥4.** Below 4 means insufficient structural variation.

**Visual density per square inch.** This is more qualitative but should be expressed as a 1-5 score where 1 is "very sparse, mostly whitespace and prose" and 5 is "highly dense, multiple structural elements per visible region." Reference comparison:

| Site | Density score (1-5) |
|------|--------------------|
| sive.rs | (score, with one-line justification) |
| interconnected.org | (score) |
| joshpigford.com | (score) |
| kalzumeus.com | (score) |
| liamdcollier.com | (score) |

**The rebuilt site's density score must be within ±1 of the reference average.**

**Brand-family bridge.** Verify that the rebuilt site shares the accent colour (`#1E50FF`) with infraxus.com. Verify that the typographic register is sufficiently distinct that the two sites do not read as duplicate templates. This is a yes/no verification with brief justification.

### Step 3.3: Mandatory uplift cycle (regardless of Step 3.2 result)

Even if Step 3.2 returns all-passing numbers, you must execute one full uplift cycle before considering the audit complete. This is the gate that prevents the cycle-1-pass failure mode.

In the uplift cycle:

1. Identify the **single weakest comparison** between the rebuilt site and the references. Even if all numerical criteria passed, there will be a weakest dimension. Name it.
2. Make a targeted improvement to address it. The improvement must be specific and observable — not a generic "make it better."
3. Deploy the change. Re-screenshot the rebuilt site at 1440px and 375px.
4. Re-run Step 3.2's measurements on the new screenshots.
5. Confirm the targeted dimension has measurably improved.

If the targeted dimension did not improve, the change was wrong. Revert and try a different uplift.

### Step 3.4: Second uplift cycle (also mandatory)

After Cycle 1 completes, identify the *next* weakest dimension and repeat the uplift process. Two uplift cycles are mandatory regardless of how the build looks. The point is to force at least two iterations of "look at it, find the weakest point, improve it" — which is the work that didn't happen on the previous build.

### Step 3.5: Continued uplift if criteria not met

If after Cycle 2, any of the numerical criteria from Step 3.2 still fail, continue uplift cycles until they pass. Maximum total cycles: 6.

If after 6 cycles the criteria still fail, document what specifically is causing the gap, ship the strongest version, and output a clear failure analysis explaining what is unresolved.

## Phase 4: Deploy

After the audit phase concludes (minimum 2 uplift cycles complete), commit and push to main. Vercel auto-deploys.

## Phase 5: Final delivery

Output a summary with:

- Confirmation the live URL renders correctly
- The diagram description summary from Phase 1
- The diagram generation result (success on which attempt, or failure analysis)
- Lighthouse scores on the new live deployment
- The full structural audit table from Step 3.2 (all five sites, all three measurements)
- A description of each uplift cycle: what was the weakest dimension, what change was made, did it improve
- Any unresolved gaps after the final cycle
- Any deviations from this specification, with reasons

## Constraints

The architecture diagram is the visual centrepiece of the page. It must be designed with the same care as the rest of the site, not as a quick fill of an empty placeholder. If the first SVG attempt feels rushed, regenerate.

The audit is binding. The minimum-two-uplift-cycle floor is non-negotiable. If you find yourself wanting to skip the second cycle because "it already passes," that is the exact failure mode this specification is preventing. Do the cycle.

Do not interrupt for review. Push through every phase. Output the final summary when complete.

Begin with Phase 1.
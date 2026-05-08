# liamdcollier.com — Career Operating-Mode Diagram Specification

## Status

This specification covers a single design uplift to the live liamdcollier.com site. The site is already deployed, the substance is correct, the typographic and structural design is correct. This brief covers *one specific element*: a custom SVG diagram for the Background section that visualises career operating-mode progression.

The diagram is intended to be the second engineered diagram on the page (after the architecture diagram in the Built section). Both diagrams should sit in the same visual register and reinforce each other as evidence that the operator behind the firm thinks structurally and designs systems deliberately.

## What this specification does NOT change

The page substance, identity statement, Built section, architecture diagram, Detail section, Contact section, footer, palette, typography, and overall structure stay exactly as they are. Do not modify any of these. The only changes this specification authorises are:

1. The Background section's visual treatment (adding the diagram)
2. The CSS specific to the Background section (to accommodate the diagram and adjust entry layout)
3. The HTML structure of the Background section (to insert the diagram and restructure the entry list as annotations beneath it)

Everything else on the page is locked.

## Conceptual brief

The diagram visualises the *operating mode* I have been in across my career, with locations and other contextual annotations attached. Operating mode means: was I a student, an employee, a remote contractor, an in-house operator, a founder. The vertical axis represents this progression. The horizontal axis is time, 2017 to 2026.

The shape that should emerge is a *step function* — a staircase showing progression from student to employee to remote contractor to in-house operator to founder, with locations and other annotations marked at each step.

The reason this matters: a career timeline that just lists locations and dates tells a reader *where* I have been. A diagram that shows operating mode tells a reader *how I have operated* and surfaces the deliberate progression in a way that text cannot. The visual hierarchy makes the *progression* (the staircase shape) the primary signal, with locations and dates as secondary annotations.

## Data — the eras and modes

Six career eras to visualise, in chronological order:

| Era | Years | Mode | Location | Counterparty | Currency | Notes |
|-----|-------|------|----------|--------------|----------|-------|
| 1 | 2017–2020 | Student | Wellington (WLG) | Victoria University of Wellington | NZD | BCom Accounting and Finance |
| 2 | 2020–2022 | Employee (full-time) | Auckland (AKL) | BDO | NZD | Business Advisory |
| 3 | 2022–2023 | Remote contractor | Barcelona (BCN) | BDO (remote) | NZD | Negotiated remote engagement |
| 4 | 2023–2024 | In-house operator | Melbourne (MEL) | Mid-tier law firm | AUD | Finance Business Partner |
| 5 | 2025 | Founder | New York (NYC) | Infraxus (founded) | USD | Lower Manhattan |
| 6 | 2026–present | Founder | Melbourne / Medellín (MEL/MDE) | Infraxus (split base) | AUD/USD | Operating across both bases |

Additionally, a *transition annotation* — Medellín exchange — sits as a marker on the timeline at 2018, even though it is not a career era. It is a one-line annotation only, indicating where Spanish-language acquisition began relative to the career arc.

## Vertical axis — operating modes

Five mode bands, ordered bottom to top:

1. **Student**
2. **Employee** (full-time, in-firm)
3. **Remote contractor** (selected client work, location-independent)
4. **In-house operator** (full-time, employer-side, in-firm)
5. **Founder**

The diagram shows progression *up* through these modes. Each era occupies its corresponding mode band horizontally for the duration of the era. The shape is therefore a step function ascending from bottom-left to top-right.

The mode labels appear as small left-aligned text outside the diagram's plot area, at the y-position of each band. They are part of the diagram's structural grid, not labels on individual eras.

## Horizontal axis — time

2017 to 2026, inclusive. Each year is a tick on the bottom axis.

Year labels are small, set in the same monospace or tabular figures register used for the architecture diagram annotations. They are subtle — secondary to the era blocks themselves.

## Visual treatment

### Overall register

Same register as the architecture diagram in the Built section. Do not deviate. This means: hairline strokes (1px or 1.5px max), no fills except the sparest possible use of palette accent for emphasis, no gradients, no shadows, no 3D effects, no decorative elements. Inline `font-family` declarations referencing Inter for component labels.

The diagram should read as *technical documentation*, not *infographic*. The reference register is the same one we used for the architecture diagram: structural diagrams from well-engineered technical documentation. Stripe Press. AWS architecture diagrams. Linear engineering posts. *Not* travel blog timelines, *not* career infographics, *not* corporate annual report charts.

### Era blocks

Each era is a horizontal block sitting at its corresponding mode height, spanning from its start year to its end year on the horizontal axis.

Block treatment:
- Outline only, 1px stroke, `#1A1A1A`. No fill.
- Height: small enough to read as a structural element, not as a chart bar. Suggested 24–32px.
- Each block has the era's primary annotation inside or directly above it: a short text string showing location code, currency code, and counterparty type. For example: `AKL · NZD · BDO`. Set in Inter, 11px, mid-grey, tabular figures where applicable.

### Step transitions

Where an era ends and the next begins at a higher mode, a thin vertical line connects the top of the lower era's block to the bottom of the next era's block — visualising the *step up*. 1px stroke, same colour as block outlines.

If two consecutive eras are at the same mode (which doesn't happen in this dataset but is worth specifying), the blocks butt up against each other on the same horizontal line, separated only by a small gap (4-8px).

### Mode band lines

Faint horizontal hairline rules at each mode level, running the full width of the diagram, behind the era blocks. Stroke: 0.5px, `#E8DEC9` (the same warm rule colour used elsewhere on the page). These are guidelines, not emphasis. They establish the mode bands visually without competing with the era blocks for attention.

### Year tick marks

At each year (2017 through 2026), a small tick mark on the bottom axis. Year label below each tick. Tabular figures, 10–11px, mid-grey.

### The Medellín 2018 annotation

A single small marker at the 2018 position on the bottom axis, *below* the year tick. Treatment: a small dot or short vertical hairline below the axis, with a one-line annotation text: `Medellín exchange · Spanish acquisition begins`. Set in italic, 10px, mid-grey. This is the only annotation that hangs below the main diagram body.

### Currency / location detail

Locations and currencies are encoded as short codes within each era block's annotation: `AKL · NZD · BDO`, `BCN · NZD · BDO (remote)`, `MEL · AUD · law firm`, `NYC · USD · founded`, `MEL/MDE · AUD/USD · split-base`. The codes are doing real work — they are not decoration — and they should be small enough that a casual scanner reads them as structural texture, while a careful reader can decode them as actual data points.

### Title and caption

A small eyebrow label *above* the diagram in the same treatment as the rest of the page section labels: `CAREER OPERATING MODE · 2017–2026`. Inter, 11px, all caps, 0.18em letter-spacing, mid-grey.

A figcaption *below* the diagram, in italic, mid-grey, centred: *Six eras across four countries and three currencies. Each step represents a deliberate progression in operating mode.*

### Dimensions

Aspect ratio: 16:5 or 16:6 (wider than the architecture diagram to fit the time axis). Full content-column width on desktop. On mobile, the diagram should remain readable at 375px viewport — if necessary, allow horizontal scroll *within the figure container only*, so the rest of the page does not horizontal-scroll.

Total file size target: under 8KB. Hand-write the SVG; do not use a generator that produces verbose output. Comment the SVG with section headers (`<!-- MODE BAND LINES -->`, `<!-- ERA BLOCKS -->`, `<!-- TRANSITIONS -->`, `<!-- ANNOTATIONS -->`, `<!-- AXIS -->`) so a future maintainer can edit it.

## HTML integration

The diagram is inlined directly into `index.html` (preferred for zero additional HTTP requests and CSS-style inheritance). Replace the current Background section's content as follows:

Current structure:
```html
<section id="background">
  <header>
    <span class="eyebrow">SECTION 04</span>
    <h2>Background</h2>
  </header>
  <dl class="background-list">
    <!-- entries -->
  </dl>
</section>
```

New structure:
```html
<section id="background">
  <header>
    <span class="eyebrow">SECTION 04</span>
    <h2>Background</h2>
  </header>
  <figure class="career-diagram">
    <div class="career-diagram__label">CAREER OPERATING MODE · 2017–2026</div>
    <!-- SVG inlined here -->
    <figcaption>Six eras across four countries and three currencies. Each step represents a deliberate progression in operating mode.</figcaption>
  </figure>
  <dl class="background-list">
    <!-- entries continue below the diagram, slightly compressed -->
  </dl>
</section>
```

The text entries in the `<dl>` continue as they currently are. Do not modify the entry text content. The diagram is *additive* — it sits above the entries and surfaces the geographic / mode dimension that the entries don't explicitly do. Readers who want detail still get the full text entries.

## CSS adjustments

Add new styles for `.career-diagram`, `.career-diagram__label`, `.career-diagram svg`, and `.career-diagram figcaption`. Use the existing design tokens (CSS custom properties on `:root`). Do not introduce new tokens; reuse the existing palette, type scale, and spatial scale.

Spacing:
- 64px between the section header and the diagram on desktop
- 32px between the diagram caption and the first text entry
- 48px on mobile for both gaps

The text entries below the diagram can be slightly compressed (less vertical space between entries) since the diagram is doing some of the structural work the spacing previously did. Reduce the inter-entry spacing by ~25% if it improves the section's overall rhythm.

## Iteration protocol — the critical part

This is the part that distinguishes a good diagram from a perfect one.

### Build cycle 1: structural skeleton

Build the SVG from scratch following the spec above. Capture a screenshot of the diagram both standalone and in-page context (Background section as it now looks). Output the screenshots and a short self-assessment: what's working, what's clearly weak, what needs the most attention in cycle 2.

### Cycles 2 through 5: mandatory iteration

For each of cycles 2, 3, 4, and 5:

1. Identify the single weakest dimension of the current diagram. Be specific. *Not* "could be better" — name the dimension. Examples: *the era block heights are inconsistent*, *the transition lines are too heavy*, *the year ticks compete with the annotations for attention*, *the Medellín annotation reads as disconnected*, *the mode band labels are cramped*.
2. Make a targeted edit to address it. The edit should be specific and observable — modify the SVG file in place, do not rebuild from scratch.
3. Re-screenshot. Place the new screenshot side-by-side with the previous cycle's screenshot. Confirm the targeted dimension has improved.
4. If the targeted edit didn't improve the dimension, revert it and try a different approach.

**Do not skip a cycle even if the current state looks good.** The minimum-five-cycle floor exists because a diagram that looks good in cycle 2 usually looks meaningfully better in cycle 5 after four targeted refinements.

### Cycles 6 through 10: contingent iteration

If after cycle 5 any of the following are true, continue iterating:

- The diagram does not pass the *register check*: would a senior product designer at Stripe, Linear, or Vercel see this as deliberately structural rather than as an infographic?
- The diagram does not pass the *information density check*: does a 30-second scan communicate the staircase progression, while a 2-minute close-read reward additional detail (location codes, currencies, the Medellín annotation)?
- The diagram does not pass the *register congruence check*: does it feel visually congruent with the architecture diagram in the Built section, or does it feel like a different design language?
- Any individual element reads as visually heavy, decorative, or out of place.

Iterate up to a maximum of 10 total cycles. If after 10 cycles any criteria still fail, ship the strongest version and document what is still unresolved in the final delivery summary.

### What "iterate" means specifically

Iterate means edit the existing SVG file and the existing CSS rules. Do not delete the SVG and write a new one. Do not start over. The whole point is *progressive refinement* — each cycle builds on the previous one. The audit trail of cycle-by-cycle screenshots should show *evolution* of a single diagram, not *replacement* of one diagram with another.

If at any point the diagram seems fundamentally wrong at a structural level (the staircase isn't reading, the mode bands aren't working, the time axis is failing), pause and output a clear analysis of what's structurally wrong and what alternative structure might work. Do not rebuild silently.

## Mobile adaptation

The diagram must be readable at 375px viewport. Strategies in order of preference:

1. The diagram scales down proportionally and remains legible. Era block annotations may need to shrink to 9–10px on mobile.
2. If at 375px the annotations become illegible, allow horizontal scroll *within the figure container only*. The diagram retains its desktop dimensions and the user swipes horizontally to scan the timeline. The rest of the page does not scroll.
3. As a last resort, simplify the mobile view: keep the staircase shape, drop the location-code annotations, and let the textual entries below the diagram carry the detail. Only do this if 1 and 2 both fail.

Test at 375px, 414px, 768px, and 1440px viewports.

## Performance and accessibility

Inline SVG, no additional HTTP requests. Total file weight increase target: under 6KB. The Lighthouse score must remain 100/100/100/100 on production.

Accessibility:
- The figure has a meaningful `aria-label` describing what the diagram shows: *Career operating-mode diagram showing six eras from 2017 to 2026, progressing from student to employee to remote contractor to in-house operator to founder, with locations across Wellington, Auckland, Barcelona, Melbourne, New York, and Medellín.*
- Each text annotation in the SVG is genuine SVG text (not converted to paths) so screen readers can read it.
- Colour contrast on all text annotations meets WCAG AA minimum.

## Deploy

After the iteration cycles complete:

1. Commit the changes (SVG inline in `index.html`, CSS in `styles.css`).
2. Push to main. Vercel auto-deploys.
3. Verify the live URL renders correctly at liamdcollier.com.
4. Re-screenshot the live deployed page at 1440px and 375px.

## Final delivery

Output a summary with:

- Confirmation the live URL renders correctly
- The final diagram screenshot at 1440px and 375px
- A description of each iteration cycle: what was the weakest dimension, what change was made, did it improve. Five entries minimum.
- The final SVG file size and Lighthouse scores
- Any unresolved issues after the final cycle, if any
- Any deviations from this specification, with reasons

## Constraints

The diagram must read as *deliberately structural* and *congruent with the architecture diagram*. If at any point in iteration it tips toward infographic, decorative, chart-like, or marketing-graphic register, revert and refactor.

Do not introduce new colours beyond the existing palette. Do not introduce new fonts. Do not introduce decorative elements. Do not use icons. Do not use illustrations.

Do not modify any other section of the page. Do not edit Built, Architecture, Identity, Detail, Contact, or footer.

Begin with cycle 1.
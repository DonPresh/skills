---
name: ux-audit
description: Runs a comprehensive UX audit of a design, screen, flow, or live product — usability/heuristic evaluation, WCAG 2.1 AA accessibility checks, and design-system/consistency checks in one prioritized report. Works from a Figma link, screenshot/image, or live URL. Use whenever the user asks to "audit," "review," or "evaluate" a design/page/flow, or says "UX audit," "heuristic evaluation," "usability review," "is this design good," "what's wrong with this screen," even naming just one angle. ALSO trigger automatically whenever the user attaches/drops an image of a UI screen or mockup with little or no other text (e.g. just an image + "thoughts?" or no caption) — treat a bare design screenshot as an implicit audit request, don't wait for the word "audit." Prefer this over a narrower single-angle review when the fuller picture would help.
---

# UX Audit

A UX audit looks at a design or product from three angles at once, because real problems rarely
respect the boundary between them: a low-contrast button is both an accessibility failure and a
usability failure; an inconsistent spacing pattern is both a design-system problem and a signal
that the hierarchy is muddled. Evaluating all three together, and cross-referencing them, produces
a more useful report than three separate reviews would.

The three angles:

1. **Usability** — Is the design clear, learnable, and efficient? Evaluate against recognized
   heuristics (Nielsen's 10, or equivalent): visibility of system status, match between system and
   the real world, user control and freedom, consistency and standards, error prevention,
   recognition over recall, flexibility and efficiency, aesthetic and minimalist design, error
   recovery, help and documentation. Also assess information hierarchy (is the most important
   thing the most visually prominent?), navigation clarity, and whether the flow matches the
   user's likely mental model and goal.

2. **Accessibility** — Evaluate against WCAG 2.1 Level AA. At minimum check: color contrast
   (4.5:1 for normal text, 3:1 for large text and UI components), text alternatives for images and
   icons, keyboard operability and visible focus states, touch target size (44x44pt / 24x24px
   minimum), heading structure and semantic hierarchy, form label association, and whether color
   alone is used to convey meaning (e.g. red/green status with no icon or text backup). See
   `references/accessibility-checklist.md` for the full checklist with WCAG success criteria
   references.

3. **Consistency** — Does the design use its own (or an implied) design system coherently? Check
   for: inconsistent spacing/sizing that isn't on a clear scale, multiple near-duplicate colors or
   type styles doing the same job, components that look similar but behave differently (or vice
   versa), inconsistent terminology or button/label phrasing, and misalignment to a visible grid.
   Where no formal design system is provided, infer the implicit one from repeated patterns in the
   design itself and flag departures from it.

## Dropping a screenshot is enough to start

If the user shares an image of a UI screen, app, or design mockup — even with no accompanying
text, or just something like "thoughts?" — that's the trigger. Don't wait for them to type "audit"
or ask a question first. Go ahead and run the full audit (Usability + Accessibility + Consistency)
against whatever the image shows, using the report structure below, and present it as your
response. If the image is ambiguous (e.g. it's not obviously a UI — a photo, a diagram, a random
screenshot with no interface in it), briefly confirm what they'd like before diving in rather than
auditing something that isn't a design.

## Before you start: get the input

The audit needs to actually see the thing being evaluated. Depending on what the user gives you:

- **Figma link** — read the file/frame with the Figma tools if available (get_design_context,
  get_screenshot). If Figma tools aren't available, ask the user to export a screenshot instead
  rather than guessing at the design from the link alone.
- **Screenshot(s) or image(s)** — read them directly. If the user shares a flow, ask for (or work
  from) each screen in sequence so you can also evaluate flow-level usability, not just individual
  screens.
- **Live URL** — use browser tools if available to load the page and inspect it (including
  computed styles, DOM structure for headings/labels, and interactive states like focus and
  hover). If no browser tool is available, ask the user for a screenshot instead.

Don't guess at content you can't see. If something is ambiguous or out of view (e.g. a modal that
might open on click, a state you can't reach), say so explicitly in the report rather than
inventing detail, and note it as something to verify rather than a confirmed finding.

If the user hasn't said what the product is for or who uses it, a quick one-line assumption is
fine ("assuming this is a B2B admin dashboard used by internal staff") — don't block the whole
audit on a clarifying question unless the design's purpose is genuinely unreadable from context.

## Report structure

Use this structure. Skip a section only if there is truly nothing to say in it (e.g. a
single-color icon audit may have nothing to say about navigation) — don't pad sections with filler
just to fill them out, and don't invent findings to make every category non-empty.

```markdown
# UX Audit: [name of design/page/flow]

## Summary
One short paragraph: overall impression, the 2-3 things that matter most, and the general
severity picture (e.g. "mostly polished, but one accessibility blocker and a recurring spacing
inconsistency").

## Findings

For each finding, use this format:

### [Severity] Short title of the issue
**Category:** Usability | Accessibility | Consistency
**Where:** specific location (screen name, element, coordinates, or URL/selector)
**Issue:** what's wrong, in plain terms
**Why it matters:** the concrete impact on a real user — not just "this violates heuristic X,"
but what a user actually experiences (gets lost, can't complete the task, excludes a screen-reader
user, etc.)
**Fix:** a specific, actionable recommendation — not "improve contrast" but "darken the button
text from #999 to at least #595959 to hit 4.5:1 against the white background"

## Prioritized recommendations
A short ranked list — High severity first — of what to fix first and why, for someone who only
has time to act on the top 3-5 items.
```

Severity levels:

- **High** — blocks task completion, excludes a class of users (e.g. keyboard-only or
  screen-reader users), or violates a WCAG AA success criterion outright.
- **Medium** — causes confusion, slows users down, or is a clear inconsistency, but doesn't block
  the task.
- **Low** — polish, minor inconsistency, or a nice-to-have improvement.

Order findings within the Findings section by severity (High, then Medium, then Low), and within
each severity roughly by how much of the design it affects.

## Calibration notes

- Ground every finding in something specific and visible — cite the actual color, spacing value,
  copy, or element rather than speaking generically. A reader should be able to go find the exact
  thing you're pointing at.
- Don't flag a pattern as an inconsistency if it's a deliberate, well-established convention (e.g.
  a destructive-action button being visually distinct on purpose is not an inconsistency).
- Accessibility findings should reference the relevant WCAG criterion where useful
  (e.g. "1.4.3 Contrast (Minimum)"), but explain the criterion in plain language too — not every
  reader knows WCAG numbering by heart.
- If you can't verify something without live interaction (e.g. actual keyboard tab order, actual
  screen-reader announcement text), say what you'd need to check it rather than asserting a result
  you didn't observe.
- Calibrate volume to the size of the input: a single button deserves a handful of findings, not
  twenty; a full multi-screen flow can reasonably surface a longer list.

See `references/accessibility-checklist.md` for the detailed WCAG 2.1 AA checklist to run through
during the accessibility pass.

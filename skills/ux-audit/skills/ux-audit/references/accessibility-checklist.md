# WCAG 2.1 AA Checklist for UX Audits

Work through this list during the accessibility pass of a UX audit. Not every criterion applies
to every design (e.g. video captioning doesn't apply to a static screenshot) — skip what's not
applicable rather than forcing a finding.

## Perceivable

- **1.1.1 Non-text Content** — Every meaningful image, icon, and graphic has (or should have) a
  text alternative. Decorative images should be marked as such (not read aloud).
- **1.3.1 Info and Relationships** — Structure conveyed visually (headings, lists, tables, form
  groupings) is also conveyed in markup/semantics, not just through spacing or color.
- **1.4.1 Use of Color** — Color is never the *only* way information is conveyed (e.g. error
  fields also get an icon/text, not just a red border; status also gets a label, not just a color
  dot).
- **1.4.3 Contrast (Minimum)** — Normal text: 4.5:1 against its background. Large text (18pt+, or
  14pt+ bold): 3:1. Check this for body copy, placeholder text, disabled states (disabled text is
  often exempt, but should still be checked), and text over images.
- **1.4.4 Resize Text** — Layout should hold up if text is scaled to 200%.
- **1.4.10 Reflow** — Content should work at narrow viewport widths without horizontal scrolling
  (for responsive/live-URL audits).
- **1.4.11 Non-text Contrast** — UI components (buttons, form field borders, focus indicators,
  icons that convey meaning) need 3:1 contrast against adjacent colors.

## Operable

- **2.1.1 Keyboard** — Every interactive element must be reachable and operable via keyboard alone
  (for live URLs: tab through the page and check).
- **2.4.3 Focus Order** — Tab order should follow a logical, visual reading order.
- **2.4.6 Headings and Labels** — Headings and form labels should be descriptive, not generic
  ("Section 2" vs "Shipping Address").
- **2.4.7 Focus Visible** — There must be a visible focus indicator on every interactive element
  when navigating by keyboard.
- **2.5.5 Target Size** — Touch targets should be at least 44x44px (WCAG AA references 24x24px as
  the minimum, with platform guidelines like iOS/Android often recommending 44x44pt); flag small
  or tightly-packed tap targets, especially on mobile.

## Understandable

- **3.1.1 Language of Page** — Page/document should declare its language (live URL audits only).
- **3.2.4 Consistent Identification** — Components with the same function should look and be
  labeled consistently across the product (e.g. don't call the same action "Delete" on one screen
  and "Remove" on another without reason).
- **3.3.1 Error Identification** — Errors are clearly identified in text, not just visually.
- **3.3.2 Labels or Instructions** — Form fields have visible labels or clear instructions, not
  just placeholder text that disappears on input (placeholder-as-label is a common and real
  usability + accessibility issue — flag it).

## Robust

- **4.1.2 Name, Role, Value** — For live URL audits, check that custom interactive components
  (custom dropdowns, toggles, modals) expose a proper role/state to assistive tech, not just
  visual styling. This usually requires inspecting the DOM/ARIA attributes, not just looking at
  the page.

## Quick triage for screenshots vs. live URLs

Screenshots/Figma files can only be evaluated for what's visible: contrast, target size, use of
color, label clarity, heading hierarchy inferred from visual style. Keyboard operability, focus
order, focus visibility, and ARIA/semantic markup require either a live URL with browser tooling
or an explicit note that these need separate verification. Say clearly which checks you could
actually perform versus which ones you're flagging as "needs live verification."

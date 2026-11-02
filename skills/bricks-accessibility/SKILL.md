---
description: Use when building, reviewing, or debugging accessibility of any user-facing Bricks site — landmarks, keyboard navigation, focus management, ARIA patterns (disclosure, dialog, combobox, popover, tabs, accordion, tooltip), prefers-reduced-motion, contrast, forms, media, WCAG 2.1/2.2 compliance, and screen reader testing. Covers Bricks-specific gotchas (auto-emitted `<header>`/`<footer>` landmarks, what Nav Nested/Offcanvas/Dropdown handle for you, what Custom Code elements require) and the universal a11y contracts every component must satisfy.
---

# Bricks Accessibility

Single source of truth for accessibility in Bricks sites. Consolidates the scattered a11y knowledge across `bricks-headers-footers`, `bricks-nestable-elements`, `bricks-interactions`, `bricks-seed-design-system`, `bricks-agent-repository`, `bricks-html-css-to-bricks`, and `bricks-playbook`, and fills the general-a11y gap (ARIA patterns, WCAG quick reference, testing checklist).

## When to use this skill

- Building any user-facing component (nav, form, modal, media, hero, footer)
- Reviewing an existing build for a11y bugs (Lighthouse, axe, client reports)
- Debugging a specific a11y issue reported by users, axe, WAVE, or screen reader testers
- Pairing with `bricks-quality-gate` before declaring any build done
- Any time the prompt mentions: accessibility, a11y, WCAG, ARIA, keyboard, focus, screen reader, contrast, alt text, reduced motion, skip link, landmark

## Bricks-specific gotchas

These are the quirks you only learn by shipping — consolidated here so you don't relearn them.

### Auto-emitted landmarks

Bricks wraps header templates in `<header>` and footer templates in `<footer>` automatically. Do **not** set `tag: "header"` on the root element of a header template — produces nested `<header><header>`, which is invalid HTML5, an accessibility regression, and triggers the "duplicate `<header>`" rule in axe / WAVE.

- Use `tag: "section"` or `tag: "div"` on the root of a header/footer template (no landmark conflict)
- Use `tag: "nav"` for the navigation row — `<nav>` is a different landmark and is valid inside `<header>`
- Reference: `bricks-headers-footers` skill lines 51–77, `bricks-seed-design-system` line 29
- Pages: do **not** embed a site-wide `<header>` or `<footer>` in a normal page body — Bricks owns those
- Pages: do **not** emit `<main>` manually — Bricks owns that landmark too (see `bricks-html-css-to-bricks` line 10)

### What Bricks handles for you

- **Nav Nested, Dropdown, Offcanvas:** `aria-expanded` and keyboard navigation are auto-managed
- Don't add duplicate logic — but verify per site (some custom themes break it)
- Reference: `bricks-nestable-elements` line 97
- **Interactions trigger `focus`:** fires on element focused via keyboard/tab (`bricks-interactions` line 42) — useful for focus-visible styling, hover-on-focus-open, etc.

### What Bricks does NOT handle

- **Custom Code elements** (HTML/CSS/JS): full responsibility on the author. No validation, no auto-aria.
- **Form fields:** labels, error association, fieldsets, help text, required state — all manual.
- **Image alt text:** set per element (Image, Gallery, Image Gallery). Bricks does not infer.
- **Landmark labels on `<nav>`:** add `aria-label` manually when you have multiple navs (primary, footer, breadcrumb).
- **Focus restoration** after overlay close: manual JS, OR use native `<dialog>` / `popover` (which do it for you).
- **Reduced motion:** CSS animations from global classes still run unless you wrap in `@media (prefers-reduced-motion: reduce)`.

### Element-level a11y decisions

- `<a>` with no `href` has no link semantics — use `<button>` for actions.
- `tag: "div"` is the safe default for layout containers. Only switch to `button`, `nav`, `main`, `article`, `section`, `aside` when semantically correct.
- Global classes are presentation-only — structural HTML must use semantic tags (`<button>` not `<div class="btn">`).
- Custom HTML output via Code element: write semantic HTML, not `<div class="everything">`.
- Repository routes that touch `role` / `aria-*` are limited (`bricks-agent-repository` line 49) — most aria needs are handled at element level via Bricks' built-in controls.
- Dynamic-data tags: ensure they don't strip semantic attributes (e.g., `{post_title}` rendered as an `<a>` text node, but the surrounding `<a href>` must be authored).

## Universal keyboard contract

Every interactive component must satisfy:

- **Tab / Shift+Tab** — moves focus to/from the component (native `<button>` / `<a href>` do this for free)
- **Enter / Space** — activates buttons and links
- **Escape** — closes overlays, returns focus to the trigger
- **No keyboard traps** — WCAG 2.1.2; user can always Tab away
- **Visible focus** — WCAG 2.4.7; use `:focus-visible` for styling, never remove outline without replacement
- **Logical reading order** — DOM order matches visual order (don't reorder with CSS `order` or grid arbitrarily)
- **Skip links** as the first focusable element on every page: `<a href="#main-content" class="skip-link">Skip to main content</a>`

## Focus management

- **Modal overlays:** use `<dialog>` + `showModal()` — browser handles focus trap, Escape, focus restoration, top-layer stacking, `::backdrop`. Don't hand-roll.
- **Light-dismiss overlays:** `popover="manual"` (Baseline 2025) + manual focus management. Better than `popover="auto"` for nav drawers (no light-dismiss surprise).
- **Everything outside the overlay:** `inert` attribute (Baseline 2023). Tree-based, no per-element loops.
- **Manual focus restore pattern:** store `document.activeElement` before open; on close, call `.focus()` on it.
- **`:focus-visible`** for styling — never `:focus` alone (creates annoying click focus rings).
- **`tabindex` values:** `-1` for programmatically focusable (without tab order), `0` for tab orderable, positive values break expected order — avoid.

## ARIA patterns for common UI

For each: when to use, minimal markup, keyboard contract, screen-reader expectation. All patterns are from W3C ARIA Authoring Practices Guide (APG).

### Disclosure (dropdown nav, collapsible panels)

- **When:** any "click to show more" UI
- **Pattern:** `<button aria-expanded="false" aria-controls="panel-id">Toggle</button>` + `<div id="panel-id" hidden>...</div>`
- **Keyboard:** Enter/Space toggles; Tab moves through; Escape closes + returns focus
- **Hidden panels:** `hidden` attribute or `display: none` — never `opacity: 0` or off-screen (items remain focusable)

### Site navigation (top-level nav, NOT menu)

- **Structure:** `<nav aria-label="Primary"><ul><li><a href="...">...</a></li></ul></nav>`
- **Dropdown items:** disclosure pattern (button + `aria-expanded` + `aria-controls`)
- **NEVER `role="menu"` / `role="menuitem"`** on web navigation — destroys link semantics; links vanish from screen reader link lists
- **`aria-current="page"`** on the active link
- **`<nav aria-label>`** distinguishes multiple navs (primary, footer, breadcrumb)

### Dialog (modal overlay)

- **Native:** `<dialog>` + `showModal()` — free top-layer, focus trap, Escape, focus restoration, `aria-modal="true"` implicit
- **Manual:** `<div role="dialog" aria-modal="true" aria-labelledby="title-id" aria-describedby="desc-id">` + manual focus management
- **Focus on open:** first focusable element, or the dialog itself if no focusable child
- **Focus on close:** restore to the element that opened the dialog
- **Backdrop click:** only dismisses if click target is the backdrop itself, not children

### Popover (non-modal overlay)

- **Native:** `popover="manual"` (Baseline 2025) — implicit anchor to invoker, light-dismiss optional
- **Use case:** mobile nav drawers, dropdowns, tooltips with rich content
- **Backdrop:** `<button popovertarget="my-popover" class="backdrop"></button>` pattern, or pseudo-element on the popover itself
- **Escape:** closes natively; restore focus to invoker manually
- **Layering:** native top-layer — no z-index wars

### Combobox (search / autocomplete)

- **Structure:** input keeps DOM focus; `aria-activedescendant` points to active `role="option"` in `role="listbox"`
- **Input attributes:** `role="combobox"`, `aria-expanded`, `aria-controls`, `aria-autocomplete="list|both"`
- **Result count:** `aria-live="polite"` region
- **Keyboard:** ArrowUp/Down moves active descendant; Enter selects; Escape closes + restores focus
- **IME-safe:** guard Enter with `event.isComposing` or `event.keyCode === 229` (CJK input)
- **Cmd+K shortcut:** bind globally, but guard against typing in text fields (`document.activeElement` check)

### Tabs

- **Structure:** `<div role="tablist">` containing `<button role="tab" aria-selected="true|false" aria-controls="panel-id" tabindex="0|-1">`
- **Panels:** `<div role="tabpanel" aria-labelledby="tab-id" tabindex="0">`
- **Roving tabindex:** one tab with `tabindex="0"` (selected), others `tabindex="-1"`; Arrow keys move focus
- **Activation:** automatic (focus moves + panel swaps) is fine for short lists; manual (focus moves, Enter/Space activates) for tabs that load content
- **Home/End:** jump to first/last tab (optional)

### Accordion

- **Headers:** `<button aria-expanded aria-controls>` (button, not heading + div)
- **Panels:** `<div role="region" aria-labelledby="header-id">`
- **Arrow keys:** optional enhancement for navigation between headers
- **Caveat:** avoid `aria-disabled` on accordion headers (use `disabled` only if actually disabled)

### Tooltip

- **Pattern:** `role="tooltip"` on the popup; accessible name from trigger via `aria-describedby`
- **Show on:** hover AND focus (never hover-only)
- **Hide on:** Escape, blur, mouse leave the trigger (with dismissible delay ≥500ms — WCAG 1.4.13)
- **Never** put interactive content inside a tooltip (links, buttons)

## `prefers-reduced-motion`

- **CSS:** `@media (prefers-reduced-motion: reduce) { *, ::before, ::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; scroll-behavior: auto !important; } }`
- **JS:** check `window.matchMedia('(prefers-reduced-motion: reduce)').matches` before starting any animation
- **Collapse to ~1ms, not `animation: none`** — `none` breaks dependents that listen for `animationend`
- **Scroll-driven animations** (`animation-timeline: scroll()`) — feature-detect with `CSS.supports()`; JS fallback. Not Baseline as of 2026.
- **View Transitions API** — wrap in `document.startViewTransition()` only after reduced-motion bail; CSS guard with `::view-transition-group(*) { animation: none !important; }` under reduced-motion
- **Client hint:** `Sec-CH-Prefers-Reduced-Motion` for server-side tuning

## Forms

- **Labels:** `<label for="input-id">` (preferred) or wrap the input. `placeholder` is **not** a label.
- **Required:** `required` attribute (preferred) or `aria-required="true"`
- **Error:** `aria-invalid="true"` + `aria-describedby="error-id"` pointing to error message element
- **Help text:** `aria-describedby="help-id"` pointing to help text element
- **Grouped controls** (radio, checkbox): `<fieldset><legend>...</legend>...</fieldset>`
- **Submit button text** describes the action ("Send message", not "Submit")
- **Live announce errors:** add the error message to an `aria-live="polite"` region
- **Focus management on error:** move focus to the first invalid field, not the form

## Images and media

- **Decorative:** `alt=""` (empty string, not missing). Use `role="presentation"` if `alt` is hard to set.
- **Informative:** descriptive `alt` (don't start with "Image of..." or "Photo of...")
- **Complex (chart, infographic):** short `alt` for summary + `aria-describedby` for longer description
- **Functional (image-as-link / image-as-button):** `alt` describes the destination or action, not the image
- **Video:** `<video controls><track kind="captions" src="..." srclang="en" label="English" default></video>`
- **Audio:** transcript link adjacent to player
- **Icon-only buttons:** `aria-label` (never rely on visible icon alone — WCAG 2.5.3 Label in Name)

## Color and contrast

- **WCAG AA:** 4.5:1 normal text, 3:1 large text (18pt+ regular or 14pt+ bold) and UI components
- **WCAG AAA:** 7:1 normal, 4.5:1 large
- **UI components / graphical objects:** 3:1 against adjacent colors (WCAG 1.4.11)
- **Focus indicators:** must contrast 3:1 with adjacent background (WCAG 2.4.11 / 2.4.13)
- **Tools:** Stark (Figma), axe DevTools (browser), Lighthouse, Polypane contrast checker
- **Never color alone:** pair with icon, text, or pattern (WCAG 1.4.1)
- **Brand colors often fail AA** — pair with sufficient neutrals; design tokens should expose both passing and brand-exact shades

## Live regions

- **`aria-live="polite"`** — announces when convenient (status messages, search result counts, form save confirmations)
- **`aria-live="assertive"`** — interrupts (errors, time-sensitive alerts)
- **`role="status"`** = polite + atomic, **`role="alert"`** = assertive + atomic (shorthand)
- **Set text content** (don't just show/hide via CSS — screen readers may not detect visibility changes)
- **Incremental updates:** prefer polite + small content over assertive + large content (less interruption)
- **Add region to DOM at page load,** even if empty — adding later may not be announced

## Quick WCAG 2.1 / 2.2 reference

The SCs that bite UI work most often. Link for full text: https://www.w3.org/WAI/WCAG22/quickref/

### Perceivable

| SC | Title | Common trigger |
|---|---|---|
| 1.1.1 | Non-text Content | Image / icon without alt |
| 1.3.1 | Info and Relationships | Skipping heading levels, no `<th>` for table headers, divs instead of lists |
| 1.3.2 | Meaningful Sequence | CSS reorder breaks DOM order |
| 1.4.1 | Use of Color | Error shown in red only |
| 1.4.3 | Contrast (Minimum) | Body text below 4.5:1 |
| 1.4.10 | Reflow | Horizontal scroll at 320px width |
| 1.4.11 | Non-text Contrast | UI components / focus rings below 3:1 |
| 1.4.12 | Text Spacing | Content clipping at 200% letter spacing |
| 1.4.13 | Content on Hover or Focus | Hover dropdown not dismissible / persistent |

### Operable

| SC | Title | Common trigger |
|---|---|---|
| 2.1.1 | Keyboard | Click-only event handlers |
| 2.1.2 | No Keyboard Trap | Modal without Escape |
| 2.1.4 | Character Key Shortcuts | Single-key shortcut active while typing |
| 2.4.1 | Bypass Blocks | No skip link |
| 2.4.3 | Focus Order | Modal focus jumps around |
| 2.4.4 | Link Purpose | "Click here" / "Read more" |
| 2.4.6 | Headings and Labels | Generic labels ("More") |
| 2.4.7 | Focus Visible | `outline: none` without replacement |
| 2.4.11 | Focus Not Obscured (2.2) | Sticky header covers focused element |
| 2.5.1 | Pointer Gestures | Multi-finger swipe without single-pointer alternative |
| 2.5.2 | Pointer Cancellation | Click fires on `mousedown` instead of `click` |
| 2.5.3 | Label in Name | Icon button `aria-label` doesn't include visible text |
| 2.5.7 | Dragging Movements | Drag-to-reorder without keyboard alternative |
| 2.5.8 | Target Size (Minimum) | Touch targets < 24×24 CSS px |

### Understandable

| SC | Title | Common trigger |
|---|---|---|
| 3.1.1 | Language of Page | Missing `<html lang>` |
| 3.2.1 | On Focus | Focus on input triggers unexpected action |
| 3.2.2 | On Input | `<select>` change navigates immediately |
| 3.3.1 | Error Identification | Error not announced or labeled |
| 3.3.2 | Labels or Instructions | Input with no label or help text |

### Robust

| SC | Title | Common trigger |
|---|---|---|
| 4.1.2 | Name, Role, Value | Custom control missing programmatic name |
| 4.1.3 | Status Messages | Form save not announced |

## Testing checklist

Before declaring any build accessible:

- [ ] Lighthouse a11y score ≥ 95 (100 ideal)
- [ ] axe DevTools (browser extension): zero violations at the level you're shipping (A or AA)
- [ ] Keyboard smoke test: Tab through every interactive element; verify Enter/Space/Escape behavior; verify focus return on overlay close
- [ ] Visible focus indicator on every interactive element (3:1 contrast, WCAG 2.4.11)
- [ ] Mobile (touch): all controls reachable with thumb (24×24 min, 44×44 recommended); no hover-only behavior
- [ ] Screen reader smoke test: VoiceOver (macOS/iOS) or NVDA (Windows) — navigate by landmarks, headings, links
- [ ] `prefers-reduced-motion: reduce` toggle (macOS: System Settings → Accessibility → Display): motion is suppressed
- [ ] 200% zoom and 320px viewport (WCAG 1.4.10 / 1.4.4): no horizontal scroll, no content clipping
- [ ] Color contrast: AA pass on all text and UI components
- [ ] Skip links: present, functional, first focusable element
- [ ] `<html lang="...">` correct on every page
- [ ] Page `<title>` unique and descriptive (per page)
- [ ] Forms: every input has a label, errors announce, submit is keyboard-accessible

## Bricks-specific testing tips

- Use `bricks-browser-verify` skill for visual verification, but **pair with axe DevTools** for a11y — visual checks miss semantic issues
- Custom Code elements are blind spots: rendered as-is, no validation
- Dynamic-data tags: ensure tags don't strip semantic attributes (`{post_title}` in an `<a>` keeps the href only if the surrounding `<a href>` is authored)
- Builder keyboard shortcuts (per `bricks-builder` line 165) are for the editor, not user-facing — don't confuse them with user keyboard contracts
- Use `bricks-plan-from-brief` to plan accessibility requirements into the brief, not bolt them on at the end
- Pair with `bricks-quality-gate` for build-time checks; manual a11y audit belongs in a separate review pass

## Common pitfalls (top 10)

1. **`role="menu"` on site nav** — destroys link semantics. Use disclosure pattern + real `<nav>` + `<ul>` of `<a>`.
2. **Hand-rolled focus trap** instead of `<dialog>` + `showModal()` — browser does it free, better than any library.
3. **Double `<header>` landmark** from Bricks template + manual `tag: "header"` — invalid HTML, axe violation.
4. **No skip link** — Tab takes 30+ keypresses to reach main content.
5. **Outline removed** with `outline: none` and no `:focus-visible` replacement.
6. **Hover-only menus** — fails on touch, fails keyboard (WCAG 1.4.13).
7. **Modal without Escape** or without focus return on close.
8. **Decorative images with descriptive alt** — adds noise to screen readers; use `alt=""`.
9. **Form input with only `placeholder`** as label — placeholder disappears on focus.
10. **Animations without `prefers-reduced-motion`** guard — vestibular disorder trigger.

## Related skills

- `bricks-headers-footers` — auto-wrap landmark rules
- `bricks-nestable-elements` — what Nav Nested / Offcanvas / Dropdown handle for you
- `bricks-interactions` — focus / hover / blur triggers
- `bricks-forms` — form element specifics
- `bricks-media-assets` — image alt text conventions
- `bricks-popups` — popover pattern in Bricks
- `bricks-performance` — performance overlap (CLS affects a11y via scroll disruption; focus indicators need contrast)
- `bricks-seed-design-system` — template / landmark setup
- `bricks-quality-gate` — pair with this for build-time verification

---
name: coreframework
description: "CoreFramework — the visual CSS management framework behind all Mantis & Crow Bricks sites. Covers the color system, typography and spacing scales, dark mode, grid classes, utility classes, breakpoints, the Bricks Integration addon and Figma sync. Load when configuring design tokens, setting up Bricks Theme Styles, or debugging CoreFramework output."
---

# CoreFramework Playbook

CoreFramework is a **free, visual CSS management tool** — a web app plus a free WordPress plugin (no licence key required) that owns the design system for all Mantis & Crow Bricks projects. It manages colours, typography, spacing, radii and breakpoints in one GUI and outputs CSS variables, utility classes and component styles.

**CoreFramework is the styles framework for every Bricks project.** Never hand-roll a CSS variable system when CoreFramework provides the whole stack. Tokens are edited in CoreFramework, never by hand in Bricks Theme Styles.

> Verify class and variable names against the live docs before writing CSS — they are generated, and the generator's naming is not always obvious. Every reference URL below returns markdown when you append `.md`.

## Core principles

- **One framework, all projects** — CoreFramework is the single source of truth for design tokens across all Bricks sites.
- **Variables over hardcoding** — `var(--primary)`, never `#2563eb`.
- **Dark mode is free** — light/dark pairs are set per colour and emitted automatically.
- **Responsive by default** — typography and spacing scale fluidly between a min and max screen width; no media queries needed.

---

## 1. Setup — web app vs WordPress plugin

CoreFramework exists as a **web app** (coreframework.com) and a **WordPress plugin** (free, on the WordPress.org repository). They hold the same project data; the plugin is what reads it on the front end.

**Onboarding options** (first launch, plugin version):

| Option | What it gives you |
|---|---|
| **Core Framework: Full experience** | Everything — colours, typography, spacing, **plus utility classes and variables**. Recommended when using a Core Framework UI kit. |
| **Variables Only: Minimalistic** | Variables only for the default setup (colours, typography, spacing, radii). Leanest output. |
| **Empty: Create your own** | Empty colour setup, but still imports default typography and spacing **with** utility classes and variables. |

**Onboarding preferences** (final step): **root font size** (`100%` or `62.5%`) and **dark mode** on/off. Enabling dark mode at onboarding sets up the light/dark colour options so you can pick a dark value for any colour that needs one.

**Plugin vs web app — when to use which:**

- The **web app** is where you design the system and export CSS; use it when a client has no WordPress yet, or to share a project read-only.
- The **plugin** is required on the site that renders the tokens.

---

## 2. Colour system

Colours are organised into **groups** — `brand`, `text`, `background`, `base` and any others you create. Each colour generates variables and can emit utility classes.

### Per-colour features

| Feature | Behaviour |
|---|---|
| **Utility class generation** | Per colour, toggle generation for **text**, **background** and **border** classes. |
| **Transparent variants** | `--primary--10` … `--primary--90` (10 %–90 % transparency). |
| **Shades** | 3–10 darker variants of a colour. |
| **Tints** | Lighter variants. |
| **Value types** | HEX, RGB, HSL and named values. |
| **Dark mode** | Per colour, enable a second value for dark mode. Colours without it render identically in both modes. |

### Default groups and variables

| Group | Purpose | Example variables |
|---|---|---|
| **Brand** | primary, secondary, accent, success, warning, danger, info | `--primary`, `--secondary`, `--accent` |
| **Text** | body and heading text | `--text-body`, `--text-title` |
| **Background** | page, section and card backgrounds | `--bg-body`, `--bg-section`, `--bg-card` |
| **Base** | neutral ramp | `--base-0` (white) → `--base-9` (near-black) |

### Workflow

1. Core Framework dashboard → **Colors** tab.
2. Define brand colours (primary, secondary, accent).
3. Define text colours (body, title).
4. Define background colours (body, section, card).
5. Enable **utility class generation** per colour — off by default, so a clean project emits variables only.
6. Enable **transparent variants** where you need tints of a brand colour.
7. Enable **dark mode** per colour that actually needs a different dark value.
8. Sync to Bricks.

**In Bricks with the Integration addon:** Core Framework colours appear in the native colour picker, with auto-suggest showing variable names and live hover preview.

### The shade-ramp trap — component classes are not free

Core Framework's own component classes (`.btn`, `.card`, `.input`, `.select`, `.badge`, `.link`, `.checkbox`, `.radio`, `.ghost`, `.slight`) and many utility classes depend on a **ramp** of derived tokens: `--primary-10`, `--primary-20`, `--primary-40`, `--primary-l-3`, `--primary-d-1`, `--secondary-20`, `--tertiary-d-1`, `--light-70`, `--dark-80`, and so on.

Those are **only emitted if the ramp is actually defined in the colour settings**. A project that defines flat tokens (`--primary`, `--secondary`, `--tertiary`) and no ramp will still ship the component CSS — and those rules will reference undefined variables. In CSS, `color: var(--undefined)` makes the **whole declaration invalid**, so the element silently loses its border, background tint, focus ring or hover state.

**The failure is silent and invisible until the class is used.** A site can look perfect for months because none of the broken utilities are applied to anything — then the first card or button drops its border.

**Rule:** before applying any Core Framework component or utility class to an element, confirm the referenced ramp tokens exist in the project's exported CSS. If they don't, define the ramp in Core Framework's colour settings (transparent variants / shades / tints) **first**, then regenerate. Do not patch the values into Bricks — a hand patch drifts on the next export.

---

## 3. Typography

Fluid type via a **base scale + ratio**, scaled between `--min-screen-width` and `--max-screen-width`.

### Variables

| Variable | Meaning |
|---|---|
| `--text-body` | body text **colour** |
| `--text-title` | heading text **colour** |
| `--text-xs` … `--text-6xl` | the font-size scale |
| `--font-body` | body font family |
| `--font-heading` | heading font family |

### The size scale

`--text-xs`, `--text-s`, `--text-m`, `--text-l`, `--text-xl`, `--text-2xl` … `--text-6xl`, where `--text-m` is the default body size.

**The scale is longer than it looks.** The generator emits as many steps as the ratio and base size produce — a real Core Framework project ships `--text-xs` through `--text-5xl`, and spacing through `--space-7xl`. Do not assume `2xl`/`6xl` are the ceiling. Read the project's exported CSS to see the actual steps.

**Assign heading tags to the scale deliberately** — `--text-m` for body, then step up per heading level. The scale is a ramp, not a mapping: CoreFramework's Oxygen blueprint maps `--text-4xl` → H2, `--text-3xl` → H3, `--text-2xl` → H4, `--text-xl` → H5/H6, `--text-5xl` → H1, `--text-6xl` → display/hero.

### Bricks Theme Styles

- Body colour `var(--text-body)` · Body size `var(--text-m)` · All headings colour `var(--text-title)`
- Remove explicit font sizes on headings — the scale handles it.

---

## 4. Spacing

Same technique as typography: a **base scale index** (which variable is the base — `--space-m` by default) plus a **ratio**, scaled fluidly across the viewport.

- **Ratios**: Minor Second, Major Third, Perfect Fourth, Golden Ratio and more. Switch to **manual mode** for exact control.
- **Manual mode** lets you rename variables and set explicit min/max sizes. The manual tab **cannot generate utility classes** — that feature is disabled there.

### Variables

`--space-3xs`, `--space-2xs`, `--space-xs`, `--space-s`, `--space-m`, `--space-l`, `--space-xl`, `--space-2xl` and beyond — the generator emits as many steps as the ratio produces, so a real project can run to `--space-7xl`. Check the exported CSS for the actual range.

### Bricks Theme Styles

Section padding: `var(--space-2xl)` top, `var(--space-m)` right, `var(--space-2xl)` bottom, `var(--space-m)` left. Container width: `var(--max-screen-width)`.

---

## 5. Dark mode

Each colour with **dark mode enabled** gets a second value. The front-end switch is set in **Preferences → Dark Theme**: **Automatic** (follows the user's system preference), **Light** (default) or **Dark**.

### The three theme classes

| Class | Where | Effect |
|---|---|---|
| `.cf-theme-dark` | **HTML root** (`<html>`) | Switches the whole site to the dark palette. Remove it to return to light. |
| `.theme-inverted` | any section or div | Inverts **that subtree only** — alternate palettes per section. |
| `.theme-always-light` / `.theme-always-dark` | a parent element | Locks that subtree to one palette regardless of the site mode (added in v1.6). |

If a child still changes when toggling, that element is probably using a hardcoded colour instead of a variable — fix the variable, not the class.

### Theme Styles — required for dark mode to work

Without these, dark mode breaks:

| Element | Setting | Value |
|---|---|---|
| **General** | Background colour | `var(--bg-body)` |
| **Body** | Colour | `var(--text-body)` |
| **Body** | Font size | `var(--text-m)` |
| **All Headings** | Colour | `var(--text-title)` |
| **Links** | Typography colour | `var(--primary)` |

---

## 6. Grid system

**Use the real class names.** The default preset generates a CSS grid with **8 columns** — `.column`, `.columns-2` … `.columns-8`. There is no `.grid-cols-*` family.

| Class | Purpose |
|---|---|
| `.column` | a single grid item |
| `.columns-2` … `.columns-8` | column count (`.columns-3` = 3 columns) |
| `.col-span-2` | span 2 columns |
| `.row-span-2` | span 2 rows (may need `height: 100%`) |
| `.gap-m` | gap size (from the spacing scale) |
| `.full-width` | break out of the container |

### Responsive suffixes

Breakpoint suffixes are appended to the class: `--on-s`, `--on-m`, `--on-l`, `--on-xl`.

```html
<div class="columns-3 gap-m full-width">
  <div class="column column--on-s columns-2--on-l">…</div>
</div>
```

`--on-s` = Small, `--on-m` = Medium, `--on-l` = Large, `--on-xl` = Extra Large. "All Breakpoints" is the default state.

> **Match the builder's breakpoints.** Core Framework's max-widths must line up with the builder's breakpoints or elements will render differently in the editor than on the front end.

---

## 7. Utility classes

Utility classes are **generated per section, opt-in** — they are not a fixed catalogue. In the Spacing section you choose which sets to emit; spacing generates **gap**, **margin** and **padding** sets, e.g. `.gap-m` resolves to `var(--space-m)`.

Each colour can generate **text**, **background** and **border** classes.

### Custom classes and variables

- **Selector group** — your own classes with your own properties and values. Adding a value surfaces your existing variables for reuse.
- **Variable group** — your own variables; always prefixed with `--`.

---

## 8. Breakpoints

Breakpoints are **yours to define**, not a fixed ladder. Add one with **Add new media query** and set min/max width; the editing window turns **green** when you are editing a breakpoint rather than "All Breakpoints".

When adding a breakpoint, set its max-width to match the builder's.

---

## 9. Bricks Integration addon

The addon bridges Core Framework and Bricks Builder, syncing classes, colours and variables into Bricks' native auto-suggest and colour picker.

### Features

- **Variable UI** — right-click any input to pick a variable visually
- **Variable auto-suggestion** — sorted by relevance in a custom dropdown
- **Class sync** — Core Framework classes appear in Bricks' native auto-suggest
- **Instant preview** — hover a class or variable to see it applied
- **Theme mode toggle** — switch dark/light from the Bricks top bar
- **Style visibility** — see every applied Core Framework style on an element

### Installation

Purchase at `https://coreframework.com/marketplace/bricks-builder-addon`, install and activate the plugin, then enter the licence key in **Core Framework → Addons**. The addon UI appears in any Bricks page.

### Bricks Theme Styles — import the blueprint

**Option 1 (recommended):** in Bricks, open the cog → **Theme Styles** → `+` → **import** → download the official JSON blueprint linked in the docs ("Save Link As" on the file link).

**Option 2 — manual:**

| Element | Setting | Value |
|---|---|---|
| **Conditions** | Apply to | Entire Website |
| **General** | Background Colour | `var(--bg-body)` |
| **Links** | Typography Colour | `var(--primary)` |
| **Body** | Colour | `var(--text-body)` |
| **Body** | Font Size | `var(--text-m)` |
| **All Headings** | Colour | `var(--text-title)` |
| **Section** | Padding T/R/B/L | `var(--space-2xl)` / `var(--space-m)` / `var(--space-2xl)` / `var(--space-m)` |
| **Container** | Width | `var(--max-screen-width)` |
| **Heading** | Default Tag | `h2` |
| **Image** | Caption | No caption |

---

## 10. Figma integration

Core Framework has a **Figma Integration addon** (early access — desktop Figma only, desktop-plugin file, licence key required; not yet on the Figma marketplace).

**Connecting:** Web app → share the project → toggle **Shareable** → copy the **Project ID** (the unique string only, not the whole URL) → paste into the Figma plugin. Plugin version → **Core Framework → Addons** → enter the Figma licence key → open the Figma menu → create an API key → paste it into the Figma plugin.

**Variables sync** from Core Framework into Figma as **local variables** on save.

> **Edit variables in Core Framework only.** Changes saved in Core Framework overwrite what is in Figma. The Figma Variables modal is read-only in practice — editing there gets clobbered on the next save.

---

## 11. Preferences

| Setting | Meaning |
|---|---|
| **Project Title** | Names the project. |
| **Default Theme** | Starting palette. |
| **Root Font Size** | `100%` or `62.5%` — the base for all REM maths. |
| **Min / Max Screen Width** | The range the fluid scales interpolate across. |
| **Enable PostCSS** | Optional CSS processing. |
| **Output REM Units** | Emit REM instead of PX. |
| **Smooth Linear Gradients** | Gradient rendering option. |
| **Class Prefix** | Prefix in front of **all** Core Framework classes, to avoid collisions with existing site classes. |
| **Dark Theme** | Automatic / Light / Dark. |

> Set the **class prefix before building the site** — retrofitting one means renaming every class.
>
> **A project prefix renames the variables too.** haztech, for example, runs with a prefix that turns `--primary` into `--hs-primary` and `--secondary` into `--hs-secondary`. **Never assume `--primary` exists** — check the project's exported CSS first. Unprefixed names like `--space-m`, `--text-body`, `--max-screen-width` are usually left alone, but confirm rather than assume.

---

## 12. Project management

- **Remote import / export** — generate a public URL from a project; others can preview read-only or clone it into their own project. Useful for sharing a design system across Mantis & Crow projects.
- **Manage project** — project-level settings and asset management.

---

## 13. Integration with the Mantis & Crow workflow

### New Bricks project

1. Create the Core Framework project (web app) — brand colours, typography, spacing.
2. Import the Bricks Theme Styles blueprint, or configure it manually from the table above.
3. Install the Bricks Integration addon and enter its licence key.
4. Sync tokens to the site.
5. Document the project's token decisions in its MemPalace wing (`design` / `architecture` room).

### Existing project

1. Open the Core Framework dashboard and review the current tokens.
2. Change tokens **in Core Framework**, never directly in Bricks Theme Styles.
3. Sync the change to Bricks.

### What to document per project

Colour palette (groups and their light/dark pairs), typography scale and font choices, spacing scale and base index, breakpoint definitions **and how they map to the builder's**, component patterns.

---

## 14. Common patterns

```css
/* Variables, never hardcoded values */
.section {
  padding: var(--space-2xl) var(--space-m);
  background-color: var(--bg-section);
}
.section-title { color: var(--text-title); font-size: var(--text-4xl); }
.section-body { color: var(--text-body); font-size: var(--text-m); }

.card {
  background: var(--bg-card);
  border: 1px solid var(--base-2);
  border-radius: var(--radius-m);
  padding: var(--space-l);
}

.btn-primary {
  background: var(--primary);
  color: var(--primary-text, #fff);
  padding: var(--space-s) var(--space-l);
  border-radius: var(--radius-s);
}
```

---

## 15. Troubleshooting

| Problem | Cause / fix |
|---|---|
| Dark mode not working | `var(--bg-body)`, `var(--text-body)`, `var(--text-title)` missing from Theme Styles; or the colour has no dark value enabled. |
| A colour is identical in both modes | Dark mode not enabled for that colour. |
| Section still flips when it shouldn't | Child elements use hardcoded colours — fix the variable. |
| Variables absent in Bricks | Integration addon inactive or the project is not synced. |
| Type/spacing not scaling | `--min-screen-width` / `--max-screen-width` not set in Preferences. |
| Utility classes missing | Class generation is **opt-in** — enable it for that group/section. |
| Class names don't exist | The grid uses `.columns-*` / `.column`, not `.grid-cols-*`. Check the generated CSS. |
| Manual-mode variables have no classes | The manual tab disables class generation by design. |
| Editor and front end disagree | Core Framework breakpoint max-widths don't match the builder's. |
| A CF component loses its border / hover / focus ring | The ramp token it references (e.g. `--primary-d-1`) is undefined — define the ramp in Core Framework, don't patch Bricks. |
| Figma variables revert | They were edited in Figma — edit in Core Framework instead. |

---

## 16. Quick reference

**Colours** `--primary` · `--secondary` · `--accent` · `--success` · `--warning` · `--danger` · `--info` · `--text-body` · `--text-title` · `--bg-body` · `--bg-section` · `--bg-card` · `--base-0`…`--base-9`

**Typography** `--text-xs`…`--text-6xl` · `--font-body` · `--font-heading`

**Spacing** `--space-3xs`…`--space-2xl`

**Layout** `--max-screen-width` · `--min-screen-width`

**Grid** `.column` · `.columns-2`…`.columns-8` · `.col-span-2` · `.row-span-2` · `.gap-m` · `.full-width` · suffixes `--on-s` `--on-m` `--on-l` `--on-xl`

**Theme** `.cf-theme-dark` · `.theme-inverted` · `.theme-always-light` · `.theme-always-dark`

---

## When to use this skill

Setting up a Bricks project · configuring Core Framework tokens · setting up or debugging Bricks Theme Styles · working with CSS variables in Bricks · implementing dark mode · responsive typography or spacing · grid and component patterns · Figma sync · documenting a project's design system.

## When NOT to use this skill

Non-Bricks WordPress projects · projects without CoreFramework installed · headless builds.

## Related skills

`bricks-playbook` (Bricks methodology) · `bricks-design-systems` (tokens and global classes) · `bricks-seed-design-system` (new foundations) · `seo-playbook` · `aeo-playbook`

---

*Verified against https://docs.coreframework.com on 2026-11-12. Class names are generated — confirm against the project's exported CSS before shipping.*

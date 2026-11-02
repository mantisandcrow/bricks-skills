---
name: CoreFramework Playbook
description: CoreFramework — the visual CSS management framework powering all Bricks Builder projects. Covers color system, typography, spacing, dark mode, grid system, components, utility classes, breakpoints, and the Bricks integration addon.
---

# CoreFramework Playbook

CoreFramework is a **free, visual CSS management tool** that powers the design system for all Mantis & Crow Bricks projects. It provides a centralized interface for managing colors, typography, spacing, components, and utility classes — outputting clean CSS variables and utility classes.

**Always use CoreFramework as the design system framework** for Bricks projects. Never build custom CSS variable systems from scratch when CoreFramework provides the full stack.

## Core Principles

- **One framework, all projects** — CoreFramework is the single source of truth for design tokens across all Bricks sites
- **Variables over hardcoding** — Use CSS variables (`var(--primary)`) not hex values
- **Dark mode is free** — CoreFramework generates dark/light themes automatically
- **Responsive by default** — Typography and spacing are fluid, not fixed

## Architecture

CoreFramework generates three output layers:
1. **CSS Variables** — Design tokens (colors, spacing, typography) as `var(--name)` custom properties
2. **Utility Classes** — Pre-built classes for rapid layout and styling
3. **Component Styles** — Reusable element patterns via the component editor

## Key Reference URLs

All docs are at `https://docs.coreframework.com`. Append `.md` to any page URL for machine-readable markdown.

- Overview: `https://docs.coreframework.com/introduction/overview-of-core-framework.md`
- Bricks Integration: `https://docs.coreframework.com/builder-integrations/bricks-builder.md`
- Color System: `https://docs.coreframework.com/navigating-the-ui/color-system.md`
- Typography: `https://docs.coreframework.com/navigating-the-ui/typography.md`
- Spacing: `https://docs.coreframework.com/navigating-the-ui/spacing.md`
- Dark Mode: `https://docs.coreframework.com/how-to-use/dark-mode.md`
- Grid System: `https://docs.coreframework.com/how-to-use/grid-system.md`
- Components: `https://docs.coreframework.com/navigating-the-ui/components.md`
- Utility Classes: `https://docs.coreframework.com/navigating-the-ui/utility-classes-and-vars.md`
- Breakpoints: `https://docs.coreframework.com/navigating-the-ui/breakpoints.md`
- Manage Project: `https://docs.coreframework.com/navigating-the-ui/manage-project.md`
- Remote Import: `https://docs.coreframework.com/navigating-the-ui/remote-import.md`
- Preferences: `https://docs.coreframework.com/navigating-the-ui/preferences.md`

---

## 1. Color System

CoreFramework's color system manages unlimited colors organized into groups. Each color generates CSS variables automatically.

### Default Color Groups

| Group | Purpose | Example Variables |
|---|---|---|
| **Brand** | Primary, secondary, accent, success, warning, danger, info | `--primary`, `--secondary`, `--accent` |
| **Text** | Body and heading text colors | `--text-body`, `--text-title` |
| **Background** | Page and section backgrounds | `--bg-body`, `--bg-section` |
| **Base** | Neutral/utility colors | `--base-0` through `--base-9` |

### Color Features

- **Utility Class Generation** — Toggle per color to generate text, background, and border classes
- **Transparent Variants** — Generate `--primary--10` through `--primary--90` (10%–90% transparency)
- **Shades** — Generate 3–10 darker variants of any color
- **Tints** — Generate lighter variants
- **Value Types** — Supports HEX, RGB, HSL, and named values

### Color Workflow

1. Open CoreFramework dashboard → Colors tab
2. Define brand colors (primary, secondary, accent)
3. Define text colors (body, title)
4. Define background colors (body, sections, cards)
5. Enable utility classes for each color group
6. Enable transparent variants where needed
7. Export / sync to Bricks

### Bricks Color Integration

When the Bricks Integration addon is active:
- All CoreFramework color variables appear in Bricks' native color picker
- Auto-suggest dropdowns show variable names as you type
- Real-time preview on hover before applying

---

## 2. Typography

CoreFramework provides responsive typography via fluid scaling — no media queries needed.

### Typography Variables

| Variable | Description |
|---|---|
| `--text-body` | Main body text color |
| `--text-title` | All heading colors |
| `--text-xs` through `--text-6xl` | Font size scale |
| `--font-body` | Body font family |
| `--font-heading` | Heading font family |

### Typography Scale

The scale is fluid between `--min-screen-width` and `--max-screen-width`:
- `--text-xs` — Small/caption text
- `--text-s` — Small body text
- `--text-m` — Default body (use in Bricks Theme Styles)
- `--text-l` — Large body
- `--text-xl` — H5/H6
- `--text-2xl` — H4
- `--text-3xl` — H3
- `--text-4xl` — H2
- `--text-5xl` — H1
- `--text-6xl` — Display/hero

### Bricks Theme Style Setup

In Bricks Theme Styles → Typography:
- **Body color**: `var(--text-body)`
- **Body font size**: `var(--text-m)`
- **All headings color**: `var(--text-title)`

---

## 3. Spacing

Spacing generates responsive padding/margin values as CSS variables.

### Spacing Variables

| Variable | Typical Use |
|---|---|
| `--space-3xs` through `--space-2xs` | Micro spacing (inline elements, icons) |
| `--space-xs` through `--space-s` | Small spacing (form fields, cards) |
| `--space-m` | Default medium spacing |
| `--space-l` through `--space-xl` | Large spacing (section padding) |
| `--space-2xl` | Extra large (hero sections) |

### Bricks Theme Style Setup

For Section elements in Theme Styles:
- **Padding**: `var(--space-2xl)` top, `var(--space-m)` right, `var(--space-2xl)` bottom, `var(--space-m)` left
- For Container width: `var(--max-screen-width)`

---

## 4. Dark Mode

CoreFramework generates both light and dark color schemes. Toggle is built into the Bricks Integration addon.

### How It Works

- Each color has a light and dark value
- CoreFramework outputs CSS variables with `[data-theme="dark"]` selectors
- Toggle between modes from the Bricks Integration top bar, or via user system preference (`prefers-color-scheme`)

### Bricks Theme Style Setup for Dark Mode

Critical: Set these in Theme Styles so dark mode works:
- **Site background**: `var(--bg-body)`
- **Body text color**: `var(--text-body)`
- **Heading text color**: `var(--text-title)`
- **Link color**: `var(--primary)`

Without these variables in Theme Styles, dark mode will break.

---

## 5. Grid System

CoreFramework provides a CSS Grid system with predefined breakpoint-aware classes.

### Grid Classes

| Class | Purpose |
|---|---|
| `.grid` | Enables CSS Grid on container |
| `.grid-cols-1` through `.grid-cols-12` | Column count (responsive) |
| `.col-span-1` through `.col-span-12` | Column span |
| `.grid-gap-xs` through `.grid-gap-2xl` | Gap size |

### Responsive Grid

Grid classes are responsive by default — use breakpoint prefixes:
- `.grid-cols-3` — 3 columns on all screens
- `.md:grid-cols-2` — 2 columns on medium screens
- `.lg:grid-cols-4` — 4 columns on large screens

---

## 6. Components

CoreFramework's component editor manages reusable element patterns.

### Component Workflow

1. Design element in CoreFramework component editor
2. Define HTML structure, classes, and variables
3. Export as reusable component
4. Apply in Bricks via auto-suggest or copy/paste

---

## 7. Utility Classes & Variables

CoreFramework auto-generates utility classes for common patterns:

### Utility Class Categories

- **Text**: `.text-primary`, `.text-body`, `.text-center`, `.text-uppercase`
- **Background**: `.bg-primary`, `.bg-section`, `.bg-body`
- **Border**: `.border-primary`, `.border-radius-s`, `.border-radius-m`
- **Spacing**: `.p-xs` through `.p-2xl`, `.m-xs` through `.m-2xl`
- **Layout**: `.flex`, `.grid`, `.container`, `.max-width`
- **Display**: `.hidden`, `.block`, `.flex`, `.grid`

### Custom Variables

In Preferences, set your own prefix:
- Default: `--primary`, `--text-body`
- Custom: `--my-prefix-primary`, `--my-prefix-text-body`

---

## 8. Breakpoints

CoreFramework provides responsive breakpoints with easy class/variable management.

### Default Breakpoints

| Breakpoint | Width |
|---|---|
| `xs` | 0–479px (mobile portrait) |
| `s` | 480–767px (mobile landscape) |
| `m` | 768–1023px (tablet portrait) |
| `l` | 1024–1279px (tablet landscape) |
| `xl` | 1280–1439px (desktop) |
| `2xl` | 1440px+ (large desktop) |

### Breakpoint Features

- Edit any class or variable per breakpoint
- Visual feedback in the UI
- Overrides cascade: `xs` → `s` → `m` → `l` → `xl` → `2xl`

---

## 9. Bricks Integration Addon

The Bricks Integration addon bridges CoreFramework and Bricks Builder.

### Features

- **Variable UI** — Right-click any input to browse CoreFramework variables visually
- **Auto-Suggest** — Custom dropdown showing all available classes and variables
- **Instant Preview** — Hover over classes/variables to see live preview on elements
- **Theme Toggle** — Switch dark/light mode from within Bricks
- **Style Visibility** — See all applied CoreFramework styles on any element

### Setup

1. Purchase and install the addon from `https://coreframework.com/marketplace/bricks-builder-addon`
2. Activate in WordPress plugins
3. Open any Bricks page — the addon UI appears automatically

### Bricks Theme Styles Setup (Manual)

Create a new Theme Style in Bricks Settings → Theme Styles:

| Element | Setting | Value |
|---|---|---|
| **Conditions** | Apply to | Entire Website |
| **General** | Background Color | `var(--bg-body)` |
| **Links** | Typography Color | `var(--primary)` |
| **Body** | Color | `var(--text-body)` |
| **Body** | Font Size | `var(--text-m)` |
| **All Headings** | Color | `var(--text-title)` |
| **Section** | Padding (T/R/B/L) | `var(--space-2xl)` / `var(--space-m)` / `var(--space-2xl)` / `var(--space-m)` |
| **Container** | Width | `var(--max-screen-width)` |
| **Heading** | Default Tag | `h2` |
| **Image** | Caption | No caption |

### Bricks Theme Styles Setup (JSON Import)

Import the official CoreFramework JSON blueprint via Theme Styles → Import. Right-click the file link in the docs and "Save Link As" to download.

---

## 10. Project Management

### Remote Import / Export

- Generate a public URL from CoreFramework to share projects
- Others can preview in read-only mode or clone to their own projects
- Useful for sharing design systems across Mantis & Crow projects

### Preferences

Key settings to configure:
- **Class/Variable Prefix** — Custom prefix for all generated classes
- **REM Units** — Toggle between REM and PX output
- **Min/Max Screen Width** — Define fluid scaling range
- **Root Font Size** — Base font size for REM calculations

---

## 11. Integration with Mantis & Crow Workflow

### When Starting a New Bricks Project

1. Set up CoreFramework project with brand colors, typography, spacing
2. Import or configure Bricks Theme Styles with CoreFramework variables
3. Install Bricks Integration addon
4. Sync design tokens between CoreFramework and Bricks
5. Document project-specific CoreFramework config in `mempalace.yaml` rooms

### When Modifying an Existing Project

1. Open CoreFramework dashboard to review current design tokens
2. Make changes in CoreFramework, not directly in Bricks Theme Styles
3. Sync changes to Bricks via the addon or re-import

### Design Token Documentation

When CoreFramework is configured for a project, document:
- Color palette (brand, text, background groups)
- Typography scale and font choices
- Spacing scale
- Breakpoint overrides
- Component patterns

File these in the project's mempalace wing under appropriate rooms (e.g., `design`, `architecture`).

---

## 12. Common Patterns

### Setting Up a New Section

```css
/* Use variables, never hardcode */
.section {
  padding: var(--space-2xl) var(--space-m);
  background-color: var(--bg-section);
}

.section-title {
  color: var(--text-title);
  font-size: var(--text-4xl);
}

.section-body {
  color: var(--text-body);
  font-size: var(--text-m);
}
```

### Card Component Pattern

```css
.card {
  background: var(--bg-card);
  border: 1px solid var(--base-2);
  border-radius: var(--radius-m);
  padding: var(--space-l);
}

.card-title {
  color: var(--text-title);
  font-size: var(--text-xl);
}

.card-body {
  color: var(--text-body);
  font-size: var(--text-m);
}
```

### Button Patterns

```css
.btn-primary {
  background: var(--primary);
  color: var(--primary-text, #fff);
  padding: var(--space-s) var(--space-l);
  border-radius: var(--radius-s);
}

.btn-secondary {
  background: transparent;
  color: var(--primary);
  border: 2px solid var(--primary);
}
```

---

## 13. Troubleshooting

| Problem | Solution |
|---|---|
| Dark mode not working | Ensure `var(--bg-body)`, `var(--text-body)`, `var(--text-title)` are set in Theme Styles |
| Variables not showing in Bricks | Verify Bricks Integration addon is active; re-sync from CoreFramework |
| Colors look wrong in dark mode | Check that dark mode values are defined in CoreFramework color settings |
| Typography not scaling | Verify `--min-screen-width` and `--max-screen-width` are set in Preferences |
| Utility classes missing | Enable class generation per color/spacing group in CoreFramework |

---

## 14. Quick Reference — Essential Variables

### Colors
- `--primary`, `--secondary`, `--accent`
- `--success`, `--warning`, `--danger`, `--info`
- `--text-body`, `--text-title`
- `--bg-body`, `--bg-section`, `--bg-card`

### Typography
- `--text-xs` through `--text-6xl`
- `--font-body`, `--font-heading`

### Spacing
- `--space-3xs` through `--space-2xl`

### Layout
- `--max-screen-width`
- `--min-screen-width`, `--max-screen-width` (for fluid scaling)

### Base Colors
- `--base-0` (white) through `--base-9` (near-black)

---

## When to Use This Skill

Use this skill when:
- Setting up a new Bricks project
- Configuring or modifying CoreFramework design tokens
- Setting up Bricks Theme Styles
- Working with CSS variables in Bricks
- Implementing dark mode
- Creating responsive typography or spacing
- Building component patterns
- Debugging CoreFramework/Bricks integration issues
- Documenting a project's design system

## When NOT to Use This Skill

- Non-Bricks WordPress projects (use standard CSS)
- Projects without CoreFramework installed
- Headless/decoupled builds (no Bricks)

---

## Related Skills

- `bricks-playbook` — Bricks Builder methodology and patterns
- `seo-playbook` — SEO optimization (pairs with CoreFramework for performance)
- `aeo-playbook` — AI search optimization

---

*Last updated: 2026-09-09*
*Source: https://docs.coreframework.com*

---
name: bricks-builder
description: Use when working with Bricks Builder on WordPress. Handles layout creation, element management, style modifications, template editing, and MCP server interactions for Bricks Builder sites.
---

# Bricks Builder Skill

Use this skill when the user is creating, modifying, or troubleshooting Bricks Builder layouts, elements, styles, or templates on a WordPress site.

## When To Use

- Creating new page layouts or sections in Bricks
- Modifying existing Bricks elements, styles, or settings
- Working with Bricks templates, conditions, or theme styles
- Managing dynamic data or query loops in Bricks
- Troubleshooting Bricks layout issues
- Deploying Bricks changes via MCP

## MCP Server Setup

The Bricks MCP server provides these tools:

| Tool | Purpose |
|------|---------|
| `get_site_info` | Read site details, run diagnostics (connection checks) |
| `get_builder_guide` | Get Bricks builder guide / state — when needed, not before every edit |
| `bricks` | Manage Bricks settings, schema, queries |
| `content` | Manage posts, pages, elements |

### Conditional Discovery (no per-operation rituals)

- **Connection status**: call `get_site_info` (or equivalent diagnostics) on the **first MCP call of a session**, or **after an MCP error**, to confirm the server is alive. Don't call it before every operation.
- **Builder guide**: fetch `get_builder_guide` on the **first operation in a session** or when starting an **unfamiliar operation**. If you already know the target structure, skip it and go straight to the element-level read.
- **Fast path**: for routine edits (known post, known element, one setting), go straight to reading the element with `get-page-elements`, make the write, read back, verify, report.
- **Stop after 2 failed attempts**: if the same discovery/read fails twice, stop repeating it and reassess (connection, permissions, ability name) instead of retrying identical calls.

## Bricks Element Hierarchy

```
Section
├── Container
│   ├── Block
│   ├── Div
│   ├── Image
│   ├── Text
│   ├── Icon
│   └── ...
├── Container
│   └── ...
└── ...
```

## Common Operations

### Create a New Section
1. Read the current page/section state first (skip discovery rituals if you already have the structure)
2. Use `content` tool to create a new page/section
3. Define the element hierarchy
4. Set styles and responsive properties
5. Verify the output by reading back persisted settings

### Modify Existing Element
1. Read current state with `content` tool
2. Identify the element to modify
3. Apply changes incrementally
4. Test at different breakpoints

### Work with Templates
1. List available templates
2. Read template structure
3. Modify or create new template
4. Apply conditions if needed

## Style Guidelines

- Use Bricks' global classes for consistency
- Prefer class-based styling over inline styles
- Follow mobile-first responsive design
- Use rem/em for font sizes, px for precise layout
- Leverage CSS Grid and Flexbox through Bricks controls

## CRITICAL: MCP Write Conventions

### Global Classes via MCP

**`_cssGlobalClasses` must use class IDs (6-char hex), NOT class names.**

Bricks stores global class references as IDs (e.g. `"37d989"`), not names (e.g. `"mc-meta-item"`). The MCP API accepts name-based writes without error but the builder/frontend cannot read them.

```
CORRECT:   {"_cssGlobalClasses": ["37d989"]}
WRONG:     {"_cssGlobalClasses": ["mc-meta-item"]}
```

Get IDs from:
- `bricks/batch-create-global-classes` response → `classNameToId` map
- `bricks/list-global-classes` response → each item has `id` field
- `bricks/get-design-context` response → `globalClasses[].id`

### Write Reliability

- **Prefer a target-sized, verified write** — change only what the task needs, then re-read the element with `get-page-elements` and confirm the persisted settings.
- **Group related bounded edits** — a handful of related changes (several settings on the same element, or the same class across a few elements) can be batched into one pass; keep unrelated or high-risk changes in separate writes. Choose the write shape by scope (single `update-element` vs `batch-update-elements`) and read back the persisted settings whichever you use.
- Don't rely on tool-reported success alone; persistence behavior is project/version-specific (no universal "single always works / batch always fails" rule). Read back what the site actually saved.
- **Order caution (conditional)**: some 2.4-beta builds have been reported to disturb `children` order on writes. For beta or otherwise unproven write behavior, inspect the actual `children` via `get-page-elements` after writing (not `get-page-structure`); fix forward if disturbed, and use revisions/rollback only when available.
- Only use abilities confirmed to exist in the connected server's tool list — do not suggest unverified abilities.

### Global Class Workflow (Repeatable Process)

1. **Create class** via `batch-create-global-classes` → capture `classNameToId` map
2. **Apply class** via SINGLE `update-element` using the 6-char hex ID from step 1
3. **Remove duplicate styles** — set element-level style keys to `null` to delete them
4. **Verify** — re-read element with `get-page-elements` to confirm class is applied
5. **Regenerate CSS** — user runs Bricks > Settings > Performance > Regenerate CSS

### MCP Tool Names

MCP abilities use `mcp-adapter-execute-ability` as the tool name with `ability_name` and `parameters`:

```json
{"name": "mcp-adapter-execute-ability", "arguments": {
  "ability_name": "bricks/update-element",
  "parameters": {"postId": 123, "elementId": "abc", "settings": {...}}
}}
```

## Dynamic Data

Bricks uses `{{dc:...}}` syntax for dynamic content:
- `{{dc:post_title}}` — Current post title
- `{{dc:author_name}}` — Post author
- `{{dc:site_name}}` — WordPress site name
- `{{dc:custom_field:field_name}}` — Custom field value

## Safety Rules

1. **Never delete** elements or templates without user confirmation
2. **Always draft** — work in draft mode before publishing
3. **Back up first** — before major changes, note the current state
4. **Batch related bounded edits** — group related changes into one pass when they're bounded (a single targeted `update-element` for one element; a batched write for a set of related settings). Select the write shape by scope. Keep independent or high-risk changes separate, and always verify by reading back what the site actually saved
5. **Ask if unsure** — when an operation could be destructive

## Troubleshooting

If a Bricks layout isn't rendering correctly:
1. Check element hierarchy (Sections > Containers > Elements)
2. Verify CSS classes are applied correctly
3. Check for conflicting styles
4. Test responsive breakpoints
5. Clear any caching (browser + WordPress cache)

## Lessons Learned

Real problems encountered during sessions are filed in MemPalace:
```sh
mempalace search "query" --wing agency-services --room lessons
```
Only filed from actual work — not theoretical issues.

## Bricks Academy Reference

For Bricks Builder interface and core concepts:
- **Builder Interface**: https://academy.bricksbuilder.io/chapters/the-builder/
- **Builder Settings**: https://academy.bricksbuilder.io/chapters/the-builder/#settings
- **Builder Keyboard Shortcuts**: https://academy.bricksbuilder.io/chapters/the-builder/#keyboard-shortcuts
- **Builder Canvas**: https://academy.bricksbuilder.io/chapters/the-builder/#canvas
- **Developer Reference**: https://developer.bricksbuilder.io/

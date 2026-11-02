# Content Modeling Guide

Use this reference when the main question is whether the WordPress project chose the right entity boundaries before it chose the right field types.

## First Questions to Answer

1. **What are the real business entities?**
   - posts/articles
   - locations
   - staff
   - case studies
   - events
   - products
   - reusable page sections
   - site-wide settings

2. **Which concepts need their own lifecycle?**
   Give something its own content type when it needs one or more of:
   - its own permalink or canonical URL
   - independent publishing workflow
   - reuse across multiple pages
   - independent ownership/editors
   - archive/filter/search views
   - API exposure as a first-class object

3. **Which concepts are just attributes?**
   Keep data as fields when it is truly attached to a single parent object and does not need standalone lifecycle behavior.

## CPT vs Taxonomy vs Field

### Use a CPT When
- The thing is a first-class object
- It may need archives or single pages
- It has many attributes of its own
- It may be related to multiple other objects
- Editors think of it as "a thing we create and manage"

**Examples:** Team members, Locations, Events, Recipes, Testimonials reused across many pages

### Use a Taxonomy When
- The goal is classification, grouping, filtering, or faceting
- Multiple content items can share the same value
- Consistency matters more than free-form input
- You need browsable archive pages or filter UI

**Examples:** Topic, Location region, Audience segment, Service category

### Use a Field When
- The value belongs to exactly one object
- It is not reused elsewhere
- It does not need its own archive or filter ecosystem
- The value is naturally scalar or tightly scoped

**Examples:** Hero eyebrow text, Event registration URL, Staff headshot, External CTA label

## Smells That the Model Is Wrong

### Too Much in One CPT
- One post type covers several unrelated concepts
- Templates branch heavily on a `type` or `layout` meta field
- Editors need long instructions to explain what belongs in a given entry

### Too Much in Fields
- Important categories are entered as free text
- Related items are stored as comma-separated strings
- Template logic spends lots of effort converting text into structure

### Too Much in Flexible Content
- Every page is a bespoke stack of many near-duplicate layouts
- The site has no design-system boundaries
- Content becomes impossible to query or reuse
- Migrations would require layout-by-layout cleanup

## ACF-Specific Modeling Advice

### Repeater Fields
**Good for:** Short structured lists tied to one parent record, rows that do not need independent lifecycle

**Bad for:** Entities that need URLs, search, ownership, or reuse; large datasets later mined through `LIKE` queries

### Flexible Content
**Good for:** Bounded page-building with well-designed layouts, editorial composition with clear rules

**Bad for:** Unlimited page-builder freedom without governance, modeling domain objects that should really be entities

### Relationship / Post Object Fields
**Good for:** Explicit relations between existing entities, curated related content blocks

**Watch for:** Inconsistent return formats, unbounded selection UIs, accidental N+1 field access in templates

### Options Pages
**Good for:** Truly global settings or shared site-wide content

**Bad for:** Data that varies by page, user, locale, or campaign but was centralized out of convenience

## Migration Thinking

When the model changes, ask:
- Can old content still render?
- Do field names remain stable?
- Is there a backfill plan?
- Does API output change?
- Can editors understand what changed?

If the answer is "we'll just rename the field and update templates," treat that as risky.

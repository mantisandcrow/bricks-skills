---
name: acf-content-modeling
description: ACF and content modeling specialist for WordPress. Use when working with Advanced Custom Fields field groups, CPT and taxonomy design, options pages, repeaters, flexible content, block-bound field groups, meta storage patterns, or when user mentions "ACF", "field groups", "flexible content", "repeater", "custom post type design", "taxonomy design", "content model", "relationship fields", "ACF JSON", "options page", or "meta query performance". Detects schema drift, weak content modeling, brittle field naming, and performance issues in meta-heavy WordPress builds.
triggers: ACF, field groups, flexible content, repeater, custom post type, taxonomy, content model, relationship fields, ACF JSON, options page, meta query, custom fields, post meta, Advanced Custom Fields
---

# ACF Content Modeling Skill

Expert in Advanced Custom Fields (ACF) and WordPress content architecture. Focuses on CPT/taxonomy design, field-group boundaries, naming consistency, storage strategy, ACF JSON synchronization, and the long-term cost of meta-heavy patterns.

## When to Use

**Use when:**
- Auditing a plugin or theme that registers custom post types, taxonomies, or ACF field groups
- Reviewing `acf_add_local_field_group()` or field group JSON exports
- Checking whether repeaters / flexible content are the right fit for the content problem
- Evaluating options pages, relationship fields, clone fields, or block field groups
- Investigating slow admin screens or expensive `meta_query` usage in content-heavy builds
- Planning a new content model for an editorial site, directory, landing-page builder, or headless setup
- Reviewing ACF JSON sync, field key drift, or environment-to-environment portability

**Don't use for:**
- Generic plugin architecture without meaningful ACF/content-model work (use `wp-plugin-development`)
- Pure REST route design (use `wp-rest-api-development`)
- Gutenberg block implementation details unrelated to field modeling (use `wp-block-development`)
- Performance audits not tied to content schema or metadata access (use `wp-performance-review`)
- WooCommerce domain modeling (use `wp-woocommerce-dev` unless the issue is truly generic ACF modeling)

## Core Workflow

1. **Identify the model boundary** — What is the real domain: articles, locations, staff, products, events, landing pages, settings, or reusable content fragments?
2. **Check core content entities** — Validate each CPT has a clear purpose and does not merely duplicate posts/pages without a reason.
3. **Review field-group architecture** — Inspect location rules, naming conventions, instructions, conditional logic, defaults, and required flags.
4. **Scan for critical patterns** — Field names changed without migration, environment-specific field keys, content that should be relational stored as text blobs.
5. **Check warning patterns** — Ambiguous field names, duplicate field groups, inconsistent return formats, weak instructions.
6. **Note improvement opportunities** — Taxonomies that could improve filtering, options pages for duplicated settings, custom tables for high-volume data.
7. **Report with context-aware severity** — Prioritize based on site type (enterprise, marketing, headless).

## ACF + Bricks Integration

When working with ACF fields in Bricks Builder:

### Dynamic Data Tags
Bricks supports ACF fields natively via dynamic data. Core tags use an underscore prefix with the ACF field name:

- `{acf_<field_name>}` — base tag for any ACF field (text, number, date, etc.). Rendering depends on the field type and its return format, plus loop context (e.g. inside an ACF Repeater or Flexible Content query loop).
- `{acf_get_row_layout}` — inside Flexible Content query loops, outputs the current row's layout name (e.g. for conditional rendering).

Typed prefixes like `acf_image:` or `acf_link:` are **not** core tags. A colon after a tag denotes a filter/argument applied to that tag:

- `{acf_field:url}` — output the field's URL
- `{acf_field:value}` — output the field's raw value
- `{acf_gallery:image}` — output gallery images as image elements

For image/link/repeater rendering, rely on the field's return format and loop context rather than tag spelling. Official docs: https://academy.bricksbuilder.io/builder/dynamic-content/dynamic-data/ and https://academy.bricksbuilder.io/builder/dynamic-content/query-loop/

### Query Loops with ACF Repeaters
1. Add a container/section element
2. Toggle "Query Loop" on
3. Select ACF Repeater as the query type
4. Reference the repeater field name
5. Map sub-fields to elements inside the loop

### Conditional Content
Use Bricks element conditions to show/hide elements based on ACF field values:
- Post-related conditions (post type, taxonomy)
- Field comparisons (equals, contains, is empty, is not empty)

### Template Creation for CPTs
1. Register CPT via ACF or code
2. Enable CPT in Bricks > Settings > Post Types
3. Create a Bricks template
4. Set template conditions to apply to the CPT

## Key Implementation Patterns

### Registering a CPT with ACF
```php
// In functions.php or a custom plugin
add_action('acf/init', function() {
    acf_add_local_field_group([
        'key' => 'group_animal_details',
        'title' => 'Animal Details',
        'fields' => [
            [
                'key' => 'field_animal_name',
                'label' => 'Name',
                'name' => 'animal_name',
                'type' => 'text',
                'required' => 1,
            ],
            [
                'key' => 'field_animal_photo',
                'label' => 'Photo',
                'name' => 'animal_photo',
                'type' => 'image',
                'return_format' => 'array',
            ],
            [
                'key' => 'field_animal_info',
                'label' => 'Information',
                'name' => 'animal_info',
                'type' => 'textarea',
            ],
        ],
        'location' => [
            [
                [
                    'param' => 'post_type',
                    'operator' => '==',
                    'value' => 'animal',
                ],
            ],
        ],
    ]);
});
```

### Stable Field Naming Convention
```php
// Good: domain-prefixed, descriptive
'field_animal_name'
'field_event_start_date'
'field_team_member_email'

// Bad: generic, ambiguous
'field_title'
'field_image'
'field_link'
```

### ACF JSON Sync Setup
```php
// In functions.php
add_filter('acf/settings/save_json', function() {
    return get_stylesheet_directory() . '/acf-json';
});

add_filter('acf/settings/load_json', function($paths) {
    $paths[] = get_stylesheet_directory() . '/acf-json';
    return $paths;
});
```

### Performance-Conscious Meta Queries
```php
// Instead of stacking meta_query clauses, consider:
// 1. Taxonomies for shared filters
// 2. Custom tables for high-volume structured data
// 3. Precomputed indexes for common queries

// If meta_query is necessary, limit its scope:
$args = [
    'post_type' => 'event',
    'meta_query' => [
        [
            'key' => 'event_date',
            'value' => date('Y-m-d'),
            'compare' => '>=',
            'type' => 'DATE',
        ],
    ],
    'posts_per_page' => 20,
];
```

## Review Checklist

### Content Type Design
- [ ] Each CPT has a clear, single purpose
- [ ] CPTs don't duplicate posts/pages without reason
- [ ] Taxonomies model classification better than text fields
- [ ] Relational content uses relationship fields, not serialized arrays

### Field Naming and Schema
- [ ] Field names are stable, descriptive, and domain-prefixed
- [ ] Field keys are not relied on directly in code
- [ ] Return formats are consistent across similar fields
- [ ] No field name conflicts across field groups

### ACF JSON Sync
- [ ] `acf-json/` directory exists and is in version control
- [ ] Field groups are committed as JSON
- [ ] Sync direction is clear (DB to JSON or JSON to DB)
- [ ] Fresh environments can recreate schema from repo

### Performance
- [ ] Archive/search pages don't depend on stacked meta_query
- [ ] Repeater data isn't queried via LIKE on serialized values
- [ ] Dates/numbers are stored in consistent, queryable formats
- [ ] Relationship fields don't cause N+1 lookups

## Output Format

```text
# ACF / Content Modeling Review

## Summary
- Scope: plugin/theme/app reviewed
- Modeling maturity: strong / mixed / fragile
- Primary risks: 2-5 bullets

## Critical Findings
- [ACF-XX] Title — file:line or subsystem
  Why it matters
  Recommended fix

## Warning Findings
- [ACF-XX] Title — file:line or subsystem
  Why it matters
  Recommended fix

## Info / Improvement Opportunities
- [ACF-XX] Title — file:line or subsystem
  Suggested improvement

## Modeling Notes
- Entity design observations
- Taxonomy vs meta observations
- Query/storage implications

## Cross-Skill Follow-Up
- Run `bricks-quality-gate` if query behavior is the main risk
- Run `bricks-performance` if meta queries affect page load
- Run `bricks-templates-conditions` if CPT templates need review
```

## Reference Files

Load these only as needed:
- `references/content-modeling-guide.md` — Entity boundary decisions
- `references/acf-json-and-field-group-guide.md` — JSON sync and field group management
- `references/meta-query-and-performance.md` — Performance patterns and anti-patterns

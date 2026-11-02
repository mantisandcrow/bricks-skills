# ACF JSON and Field Group Guide

Use this reference when reviewing how teams manage field definitions across environments.

## Core Rule

Treat field definitions as code, not as production-only admin state.

## Healthy Workflow

- Field groups are edited locally or in a safe dev environment
- Local JSON is enabled
- Generated JSON files are committed to git
- Changes move through normal review and deployment
- Database-only changes are temporary and later exported

## Red Flags

### CRITICAL
- Field groups only exist in the database
- Production is the source of truth
- Field keys are copied into code without stable field names backing them
- Multiple environments carry silent schema drift

### WARNING
- `acf-json` is committed inconsistently
- Some field groups are JSON-backed and others are not
- Contributors are unclear whether to sync from DB to JSON or JSON to DB
- Field-group edits happen in production without a documented promotion path

## What to Inspect

- Is an `acf-json/` folder present?
- Is it ignored accidentally in `.gitignore`?
- Do field-group JSON files change when expected?
- Are developers using `acf/settings/save_json` or custom paths?
- Do commits show meaningful field-group diffs over time?

## Review Questions

1. Can a fresh environment recreate the schema from the repo?
2. Are field names stable even if field keys regenerate?
3. Is there a plan for renamed/removed fields?
4. Are block field groups, options pages, and clone fields all covered by the same sync discipline?

## Good Practices

- Keep ACF JSON in version control
- Document custom JSON load/save paths
- Prefer stable field names with domain prefixes
- Export major field-group refactors in the same PR as template/code changes
- Review JSON diffs alongside PHP/JS/template changes

## Bad Practices

- "It works on staging because the fields already exist there"
- "We'll sync the JSON later"
- "We renamed the field in ACF and assumed nothing else depends on it"
- "We copied a field group and only changed labels, not names, keys, or intent"

## Field Group Organization Tips

- Split giant groups by editorial task or component area
- Use tabs, instructions, defaults, and conditional logic to reduce editor error
- Avoid duplicate field groups with minor differences unless clone fields or composition can simplify them
- Make location rules reflect content boundaries clearly

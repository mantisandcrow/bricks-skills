# Meta Query and Performance Guide

Use this reference when ACF-driven data shapes start affecting runtime cost.

## Core Idea

ACF makes metadata easy to create, but `postmeta` is not a free analytics database or relational engine.

## High-Risk Patterns

### 1. Archive or Search Pages Built on Stacked `meta_query` Clauses

Example smell:
- Filter by location
- Filter by price band
- Filter by event date
- Filter by audience
- Sort by another meta field

This often means the site is leaning on `postmeta` for primary discovery behavior.

### 2. Querying Repeater or Flexible-Content Internals

Smells:
- `LIKE` comparisons on serialized values
- Wildcard meta keys for repeater rows in business-critical queries
- Reporting screens derived from nested flexible-content data

### 3. Inconsistent Storage Formats

Smells:
- Dates stored as different formats across environments
- Numbers stored as formatted strings with commas/currency
- Booleans stored inconsistently

These problems make filtering and sorting unreliable.

## Prefer These Alternatives When Scale Matters

- **Taxonomies** for shared filters/facets
- **Dedicated lookup tables** for high-volume structured data
- **Derived/indexed fields** for common queries
- **Scheduled denormalization** for expensive aggregates
- **Object caching or transient caching** for expensive assembled views

## Review Heuristics

### CRITICAL
- Revenue-critical or navigation-critical pages depend on heavy meta queries at scale
- Flexible content or repeater data is queried as though it were relational tables
- Date/number comparison logic is semantically wrong because values are stored as strings

### WARNING
- Repeated `get_field()` calls inside loops without normalization
- Complex page builds recompute derived content from nested ACF structures every request
- Relationship fields trigger avoidable N+1 lookups
- A CPT exists mostly to enable querying, but the real query keys remain buried in meta

### INFO
- Small/medium sites may tolerate meta queries today, but the model may still be strategically weak
- Precomputing a few derived fields can avoid bigger rewrites later

## Quick Review Questions

1. Which pages depend on filtering or sorting by ACF values?
2. How many posts participate in those queries?
3. Are the query keys scalar and consistently formatted?
4. Would a taxonomy or lookup table fit better?
5. Can results be cached or denormalized safely?

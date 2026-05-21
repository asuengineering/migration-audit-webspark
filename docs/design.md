# Migration Audit Webspark Design

## Objective

The goal of this project is to define a Drupal-side exporter that produces a normalized migration audit report comparable in shape to the existing WordPress-side export.

The report is intended for migration reconciliation and UAT workflows.

## Operating model

The Drupal module is an exporter, not a comparison engine.

Workflow:

1. Generate a WordPress audit export.
2. Generate a Drupal audit export.
3. Provide both exports to a GPT-based comparison workflow.
4. Produce reconciliation findings and UAT guidance.

## Design principles

### Export-first architecture

The Drupal module should focus on deterministic export generation.

It should not attempt to perform semantic equivalency analysis.

### Structural equivalency support

The export should capture enough structural information to support later comparison.

The report should help answer:

> Does Drupal contain a structurally equivalent content construct suitable for migration UAT?

### Platform-aware reporting

Drupal and WordPress model content differently.

The exporter should therefore expose:

- content structures
- entity types and bundles
- Layout Builder awareness
- dependency awareness
- reusable component awareness
- taxonomy relationships
- media relationships

without attempting to serialize full rendered output.

## Report families

- content
- taxonomy
- taxonomy_relationships
- media
- menus
- users
- forms
- seo
- redirects
- warnings
- summaries

## Content family

The content report should capture:

- entity type
- bundle
- identifiers
- URLs
- publication status
- structural summaries
- Layout Builder usage
- block usage
- media references
- taxonomy references
- unresolved dependencies
- migration metadata
- warning states

The content report should avoid:

- full-text comparison
- revision analysis
- translation analysis
- semantic scoring
- automated approval decisions

## Taxonomy family

The taxonomy report should capture:

- vocabulary
- term label
- term slug
- canonical URL
- referenced content count
- whether an archive or listing surface exists in Drupal
- taxonomy-related warning states

The taxonomy report is intended to support migration reconciliation for taxonomy archive recreation.

A Drupal migration should intentionally recreate the archive or listing experience associated with important taxonomy structures from WordPress.

The report should therefore help identify:

- terms that exist without an equivalent listing surface
- archive/listing pages that still need implementation
- taxonomy structures that are present but incomplete

The taxonomy report should not attempt to serialize full View configurations or rendered archive markup.

## Taxonomy relationships family

The taxonomy relationships report should provide a normalized export of content-to-term relationships.

The report should remain intentionally lightweight at the top-level export structure while still supporting deeper contextual enrichment through optional `details_json` metadata.

The stable export structure should support:

- content identifiers
- content URLs
- vocabulary identifiers
- term identifiers
- relationship field names
- relationship existence validation

Additional Drupal-specific relationship context may optionally be captured in `details_json` payloads where useful for later GPT-based reconciliation.

Examples may include:

- relationship cardinality
- parent or hierarchical term context
- field storage metadata
- multi-value relationship structures
- relationship warnings
- rendered relationship visibility indicators

## Canonical content record

```yaml
content_record:
  export_context:
    platform:
    export_timestamp:
    environment:

  object:
    entity_type:
    bundle:
    entity_id:
    uuid:
    title:
    url:
    published:
    updated:
    author:

  structure:
    layout_builder_enabled:
    block_count:
    inline_block_count:
    reusable_block_count:
    embedded_component_count:
    media_reference_count:
    taxonomy_reference_count:

  dependencies:
    media_present:
    taxonomy_present:
    reusable_components_present:
    unresolved_dependencies:

  migration_metadata:
    source_identifier:
    migration_group:
    migration_notes:

  warnings:
    unsupported_components:
    missing_dependencies:
    unresolved_references:
```

## Canonical taxonomy record

```yaml
taxonomy_record:
  vocabulary:
    machine_name:
    label:

  term:
    term_id:
    uuid:
    label:
    slug:
    canonical_url:

  relationships:
    referenced_content_count:

  archive_surface:
    listing_surface_exists:
    listing_surface_type:
    listing_surface_identifier:

  warnings:
    missing_listing_surface:
    unresolved_references:
```

## Drupal collection targets

The exporter should gather information from:

- nodes
- taxonomy terms
- block content
- Layout Builder configuration
- media references
- taxonomy references
- path aliases
- entity reference fields
- Views metadata where applicable

## Future enhancements

Potential future enhancements may include:

- Paragraphs support
- Views dependency awareness
- reusable component fingerprinting
- field-level structural summaries
- cross-site migration identifiers

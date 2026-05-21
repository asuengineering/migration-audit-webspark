# Canonical Content Record

## Purpose

This document defines the expected export shape for the `content` report family.

The export is intended to capture enough structural information from Drupal to support later comparison against a WordPress-origin export.

The report should not attempt to determine semantic equivalency or editorial correctness.

## Content report objectives

The content report should support:

- migration reconciliation
- UAT review
- content inventory validation
- structural equivalency analysis
- dependency awareness

## Export philosophy

The export should provide:

- enough detail to understand the Drupal-side implementation
- enough structure to compare against WordPress exports
- enough metadata to identify missing or unsupported migration outcomes

The export should avoid:

- full-text comparison
- revision analysis
- translation analysis
- semantic scoring
- automated approval decisions

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

## Drupal collection guidance

The Drupal exporter should gather information from:

- nodes
- block content
- Layout Builder configuration
- media references
- taxonomy references
- path aliases
- entity reference fields

## Important implementation note

The content report should acknowledge when Layout Builder or block-driven structures are present, but should not attempt to export full rendered markup.

The purpose is structural visibility, not page recreation.

## Future enhancements

Potential future enhancements may include:

- Paragraphs support
- Views dependency awareness
- reusable component fingerprinting
- field-level structural summaries
- cross-site migration identifiers

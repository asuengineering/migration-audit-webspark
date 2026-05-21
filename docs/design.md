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

## Drupal collection targets

The exporter should gather information from:

- nodes
- block content
- Layout Builder configuration
- media references
- taxonomy references
- path aliases
- entity reference fields

## Future enhancements

Potential future enhancements may include:

- Paragraphs support
- Views dependency awareness
- reusable component fingerprinting
- field-level structural summaries
- cross-site migration identifiers

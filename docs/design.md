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

### Platform-aware reporting

Drupal and WordPress model content differently.

The exporter should expose content structures, entity types, dependency awareness, taxonomy relationships, and media relationships without attempting to serialize full rendered output.

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

The content report should capture entity types, bundles, identifiers, URLs, publication status, structural summaries, Layout Builder usage, block usage, media references, taxonomy references, unresolved dependencies, migration metadata, and warning states.

Each report family should include:

- a text description of the report purpose
- a canonical record definition
- guidance for optional details_json enrichment

## Taxonomy family

The taxonomy report should capture vocabulary, term labels, slugs, canonical URLs, referenced content counts, and whether archive or listing surfaces exist in Drupal.

## Taxonomy relationships family

The taxonomy relationships report should provide a normalized export of content-to-term relationships.

The stable structure should support content identifiers, content URLs, vocabulary identifiers, term identifiers, relationship field names, and relationship existence validation.

Additional Drupal-specific relationship context may optionally be captured in details_json payloads.

## Canonical content record

content_record:
  object:
    entity_type:
    bundle:
    entity_id:
    title:
    url:

## Canonical taxonomy record

taxonomy_record:
  vocabulary:
    machine_name:
    label:

  term:
    term_id:
    label:
    slug:
    canonical_url:

## Canonical taxonomy relationship record

taxonomy_relationship_record:
  content:
    entity_type:
    bundle:
    entity_id:
    title:
    url:

  taxonomy:
    vocabulary_machine_name:
    term_id:
    term_label:
    term_slug:

  relationship:
    field_name:
    relationship_exists:

  details_json:
    optional_enrichment: true

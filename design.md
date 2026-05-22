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
- menu relationships

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

### Node-centric content model decision

The Drupal `content` family should be node-centric.

Each content record should represent a Drupal node as the primary comparable migration object, similar in role to WordPress posts, pages, and post-like custom post types within the existing WordPress export process.

The exporter may enrich node records with structural metadata derived from related Drupal systems.

These related structures should not be promoted to standalone `content` records unless they belong to a separate dedicated report family.

The purpose of this decision is to preserve structural comparability with the WordPress export while avoiding overly granular exports of Drupal implementation details that are not useful for migration reconciliation workflows.

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
- the public URL for that listing surface when one exists
- taxonomy-related warning states

The taxonomy report is intended to support migration reconciliation for taxonomy archive recreation.

A Drupal migration should intentionally recreate the archive or listing experience associated with important taxonomy structures from WordPress.

The report should therefore help identify:

- terms that exist without an equivalent listing surface
- archive/listing pages that still need implementation
- taxonomy structures that are present but incomplete

The taxonomy report should not attempt to serialize full View configurations or rendered archive markup.

## Menu family

The menu report should capture menu structures, navigation relationships, and presentation behavior so WordPress menus can be intentionally recreated in Drupal.

The most important WordPress-side menu settings are metadata values that transform a menu link into a specialized presentation object such as:

- a CTA/button
- a heading
- a social media icon object

Those mappings may be WebSpark-specific.

Before the Drupal module can fully implement `presentation_role` and `render_variant`, the implementation should investigate how the Renovation theme stores and exposes those menu object structures.

The menu report should help identify:

- menus that exist in the source but are not yet recreated in Drupal
- menu items that point to missing or changed destinations
- items that should render with a different presentation behavior than plain navigation links
- structural differences that affect navigation fidelity

## Forms, SEO, and redirect families

These report families are intended as later enhancement phases after the initial core export families are implemented.

The anticipated source modules are:

- forms: Webform
- redirects: Redirect and Pathauto
- seo: related SEO-oriented modules and configuration

The exact module inventory should be validated against the WebSpark Drupal distribution composer configuration before implementation begins.

## Warning model

Warnings included in the export should be treated as audit-trail objects used for migration reconciliation and UAT workflows.

Examples may include:

- unresolved references
- unsupported components
- missing listing surfaces
- incomplete structural mappings

These warnings should not necessarily fail report generation.

Operational export issues should be handled separately from migration/UAT warnings.

The exporter should maintain a lightweight operational warning log describing recoverable extraction issues encountered during report generation.

Examples may include:

- inaccessible entities
- partial extraction failures
- malformed configuration
- timeout conditions

Operational warnings should provide traceability when exported data is incomplete, missing, or partially derived without necessarily terminating report generation.

## Future enhancements

Potential future enhancements may include:

- Paragraphs support
- Views dependency awareness
- reusable component fingerprinting
- field-level structural summaries
- cross-site migration identifiers
- forms, SEO, and redirect family implementation

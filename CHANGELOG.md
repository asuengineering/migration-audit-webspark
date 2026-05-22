# Changelog

## Version 0.1 — Plan-only phase

### Repository purpose established

- Defined the repository as the planning surface for a future Drupal module.
- Established compatibility goals with the WordPress-side audit exporter from migration-freeze-webspark.

### Operating model established

- Drupal exporter defined as a report-generation system only.
- GPT-based workflows defined as the comparison and reconciliation layer.
- Established normalized export philosophy rather than semantic comparison inside Drupal.

### Canonical report families planned

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

### Content report planning

- Planned structural equivalency reporting.
- Added Layout Builder awareness.
- Added dependency awareness.
- Added canonical content record definition.
- Clarified node-centric content export model.
- Clarified that Layout Builder and related structures should enrich node records rather than become standalone content records.

### Taxonomy report planning

- Planned taxonomy archive/listing auditing.
- Added archive-surface validation concepts.
- Added canonical taxonomy record definition.

### Taxonomy relationship report planning

- Planned normalized content-to-term relationship exports.
- Added details_json extensibility guidance.
- Added canonical taxonomy relationship record definition.

### Media report planning

- Planned canonical asset validation.
- Added derivative-media detection concepts.
- Added redirect/path-stability concerns.
- Added canonical media record definition.

### Menu report planning

- Planned navigation fidelity auditing.
- Added presentation-aware menu auditing.
- Added CTA/button and home-link behavior concepts.
- Added canonical menu record definition.

### Repository structure refinement

- Consolidated repository into canonical root-level documents.
- Removed redundant draft architecture documents.
- Adopted full-document replacement workflow for repository updates.

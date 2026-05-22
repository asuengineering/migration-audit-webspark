# Changelog

## Version 0.1 — Plan-only phase

### Repository purpose established

- Defined the repository as the planning surface for a future Drupal module.
- Established compatibility goals with the WordPress-side audit exporter from migration-freeze-webspark.

### Operating model established

- Drupal exporter defined as a report-generation system only.
- GPT-based workflows defined as the comparison and reconciliation layer.
- Established normalized export philosophy rather than semantic comparison inside Drupal.
- Clarified loose parity reporting expectations between Drupal and WordPress exports.
- Established that Drupal-native structures should be exported with stable identifiers, URLs, labels, and relationship metadata rather than strict field parity requirements.

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
- Added taxonomy listing surface URL support for visual comparison and redirect planning workflows.

### Taxonomy relationship report planning

- Planned normalized content-to-term relationship exports.
- Added details_json extensibility guidance.
- Added canonical taxonomy relationship record definition.

### Media report planning

- Planned canonical asset validation.
- Added derivative-media detection concepts.
- Added redirect/path-stability concerns.
- Added canonical media record definition.
- Clarified that original WordPress uploads should be distinguished from generated thumbnail or srcset derivatives.
- Added source/destination path expectations for redirect generation workflows.

### Menu report planning

- Planned navigation fidelity auditing.
- Added presentation-aware menu auditing.
- Added CTA/button and home-link behavior concepts.
- Added canonical menu record definition.
- Added Renovation theme investigation requirements for menu presentation-role mappings.

### Forms, SEO, and redirect planning

- Planned Webform integration for forms reporting.
- Planned Redirect and Pathauto integration for redirect reporting.
- Documented SEO reporting as a future enhancement surface.
- Established WebSpark composer configuration as the source of truth for module inventory validation.

### Warning model planning

- Clarified separation between migration/UAT warnings and operational export warnings.
- Established warnings as audit-trail objects rather than report-failure conditions.
- Added lightweight operational export logging expectations for incomplete or partially-derived report data.

### Operational export planning

- Clarified CSV-based export expectations.
- Added ZIP packaging expectations for export artifacts.
- Added authenticated admin export interface expectations.
- Allowed implementation flexibility for Drupal-native export generation workflows.

### Repository structure refinement

- Consolidated repository into canonical root-level documents.
- Removed redundant draft architecture documents.
- Adopted full-document replacement workflow for repository updates.

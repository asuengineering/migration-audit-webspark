# Migration Audit Webspark Architecture

## Objective

The purpose of this project is to establish a Drupal-side reporting surface that can be mechanically compared against a WordPress-origin audit export.

The reporting system is intended to support:

- migration reconciliation
- QA and UAT validation
- discrepancy detection
- migration readiness analysis
- platform-level reporting consistency

## Design Principles

### Report-first architecture

The report contract should be considered the source of truth.

Drupal implementation details should derive from the report specification rather than the other way around.

### Platform translation awareness

Drupal and WordPress do not model content identically.

The reporting layer must therefore:

- preserve source intent
- identify translation loss
- identify unsupported constructs
- identify ambiguous mappings

### Deterministic output

The module should produce repeatable structured output suitable for:

- CSV export
- JSON export
- machine comparison
- automated reconciliation workflows

## Proposed Layers

### Layer 1: Data Collection

Drupal entity discovery and normalization.

### Layer 2: Report Normalization

Transform Drupal entities into canonical report objects.

### Layer 3: Comparison Metadata

Generate warnings, missing references, unsupported mappings, and translation-risk indicators.

### Layer 4: Export and Presentation

Expose structured exports and UI summaries.

## Expected Drupal Areas

- content entities
- taxonomy entities
- media entities
- menu systems
- redirect systems
- forms
- SEO metadata
- revision/workflow state
- Layout Builder and Paragraphs

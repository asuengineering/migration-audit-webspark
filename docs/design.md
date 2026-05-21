# Migration Audit Webspark Design

## What we are building

We are building a Drupal-side audit exporter that produces a normalized report in the same general shape as the WordPress-side audit export used in migration work.

The Drupal module is not the comparison engine.

Its job is to collect structural, dependency, and inventory information from Drupal and emit that information in a deterministic, machine-readable form that can later be compared against a WordPress export by GPT or another reconciliation workflow.

## Operating model

1. WordPress produces an audit export.
2. Drupal produces an audit export.
3. A GPT-based comparison workflow evaluates the two exports.
4. The comparison workflow produces migration reconciliation findings and UAT guidance.

## Design intent

The Drupal exporter should answer questions such as:

- What content exists in Drupal?
- What Drupal entity type and bundle represent it?
- What structural components does it use?
- What dependencies does it have?
- What warnings should a reviewer see?

The exporter should not attempt to decide whether Drupal and WordPress are equivalent inside the module itself.

## Report shape

The export should be organized into the same broad families used by the migration audit process:

- content
- taxonomy
- taxonomy relationships
- media
- menus
- users
- forms
- SEO
- redirects
- warnings
- summaries

## Content family

The content family is the most important part of the export at this stage.

It should collect Drupal-side content in a normalized form that includes:

- entity type
- bundle
- identifiers
- URL or alias
- publication status
- author metadata
- update metadata
- Layout Builder presence
- block usage
- media references
- taxonomy references
- unresolved dependencies
- migration notes
- warning states

The content family should be detailed enough for comparison later, but it should not attempt to reproduce rendered pages or perform semantic matching.

## Structural scope

The exporter should include enough of Drupal’s content model to represent common Webspark page constructions, including:

- nodes
- block content
- Layout Builder configuration
- media references
- taxonomy references
- path aliases
- entity reference fields

## Deliberate exclusions

The exporter should not attempt to include:

- full-text equivalency scoring
- revision analysis
- translation analysis
- rendered markup capture
- automated migration approval decisions

## Success criteria

The project is successful if the Drupal export can be handed to a GPT-based comparison workflow and used to determine what exists, what is structurally comparable, and what still needs human review during migration UAT.

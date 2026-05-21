# Export-First Architecture

## Revised operating model

This project no longer assumes that Drupal itself will perform migration reconciliation or comparison logic.

Instead:

- Drupal produces a normalized audit export.
- WordPress produces a normalized audit export.
- GPT or another comparison workflow evaluates the relationship between the two.

This separation is intentional.

## Why this approach

Drupal and WordPress model content differently.

Attempting to fully reconcile those differences inside Drupal would create unnecessary complexity and tightly couple the module to one migration direction.

The preferred approach is therefore:

1. export structured inventory and structural metadata from each platform
2. normalize the report shape across platforms
3. perform interpretation and comparison outside the CMS

## Expected workflow

### Step 1

Generate a WordPress audit export.

### Step 2

Generate a Drupal audit export.

### Step 3

Provide both exports to a GPT-based comparison workflow.

### Step 4

Generate reconciliation findings and UAT guidance.

## Implications for module design

The Drupal module should focus on:

- deterministic exports
- structural consistency
- dependency awareness
- stable identifiers
- meaningful content summaries

The Drupal module should avoid:

- semantic comparison
- editorial judgment
- automated migration approval decisions
- full-text equivalency validation

## Report philosophy

The goal is not to answer:

> Are all words identical?

The goal is to answer:

> Does Drupal contain a structurally equivalent content construct suitable for migration UAT and reconciliation?

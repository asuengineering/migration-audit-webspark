# Migration Audit Webspark

This repository is the canonical specification for a Drupal-side audit export module used in migration reconciliation work.

## Source of truth

- `docs/design.md` — human-readable design spec
- `specs/report-spec.yml` — machine-readable contract

## Operating model

Drupal exports a normalized report. WordPress exports a normalized report. A GPT-based comparison workflow performs the reconciliation outside Drupal.

The module itself should not attempt to decide equivalency; it should capture enough structure for later comparison.

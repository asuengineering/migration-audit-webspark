# Migration Audit Webspark

This repository contains the plan for a Drupal module that will eventually produce an audit-trail report compatible with the report generated from [migration-freeze-webspark](https://github.com/asuengineering/migration-freeze-webspark).

## Current mode

Version 0.1 is being developed in plan-only mode with the design and specification surface for a future formal Drupal module.

## Source of truth

- `design.md` — human-readable design spec
- `report-spec.yml` — machine-readable contract
- `CHANGELOG.md` — running summary of the design path so far

## Operating model

To complete our UAT process with the necessary degree of accuracy, we will seek to conduct an AI assisted comparison of original and destination sites (WordPress --> Drupal). This module is intended to produce one half of the artifacts needed for that mechanical comparison, with the other half being generated in WordPress.

The module itself should not attempt to decide equivalency; it should capture enough structure for later comparison.

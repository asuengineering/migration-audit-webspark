# Migration Audit Webspark

This repository contains the plan for a Drupal module that will eventually produce an audit-trail report compatible with the report generated from [migration-freeze-webspark](https://github.com/asuengineering/migration-freeze-webspark).

## Current mode

Version 0.2 represents the completion of the initial specification and discovery phase.

The repository should now contain a sufficiently complete planning surface to begin iterative construction of an actual Drupal module implementation.

Further refinement and expansion of the specification are expected to continue alongside implementation.

## Source of truth

- `design.md` — human-readable design spec
- `report-spec.yml` — machine-readable contract
- `CHANGELOG.md` — running summary of the design path so far

## Operating model

To complete our UAT process with the necessary degree of accuracy, we will seek to conduct an AI assisted comparison of original and destination sites (WordPress --> Drupal). This module is intended to produce one half of the artifacts needed for that mechanical comparison, with the other half being generated in WordPress.

The module itself should not attempt to decide equivalency; it should capture enough structure for later comparison.

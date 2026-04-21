---
categories:
- aoc
description: Spectral linting rules defining API design standards and conventions for Architect of the Capitol.
layout: rules
name: Architect of the Capitol API Rules
provider_name: Architect of the Capitol
provider_slug: architect-of-the-capitol
rule_count: 13
rules:
- description: Building responses must include an id field
  given: $.components.schemas.Building.properties
  name: aoc-building-id-required
  severity: error
- description: Building responses must include a name field
  given: $.components.schemas.Building.properties
  name: aoc-building-name-required
  severity: error
- description: Artwork responses must include a title field
  given: $.components.schemas.Artwork.properties
  name: aoc-artwork-title-required
  severity: error
- description: Artwork responses must include an artist field
  given: $.components.schemas.Artwork.properties
  name: aoc-artwork-artist-required
  severity: error
- description: Preservation project status must be a valid enum value
  given: $.components.schemas.PreservationProject.properties.status
  name: aoc-preservation-status-enum
  severity: error
- description: List responses must include a total count
  given: $.components.schemas[*List].properties
  name: aoc-list-responses-have-total
  severity: warn
- description: List responses must include a limit field
  given: $.components.schemas[*List].properties
  name: aoc-list-responses-have-limit
  severity: warn
- description: All API operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: aoc-operations-have-tags
  severity: warn
- description: All API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: aoc-operations-have-summary
  severity: error
- description: All API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: aoc-operations-have-operation-id
  severity: error
- description: Path parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: aoc-path-parameters-described
  severity: warn
- description: API info must include contact information
  given: $.info
  name: aoc-info-contact-required
  severity: warn
- description: API must define at least one server
  given: $
  name: aoc-servers-defined
  severity: error
rules_file: rules/aoc-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/architect-of-the-capitol/refs/heads/main/rules/aoc-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 5
slug: aoc-spectral-rules
tags:
- Federal Government
- Capitol Hill
- Congress
- Historic Preservation
- Government Services
- Spectral
- Linting
- API Governance
---

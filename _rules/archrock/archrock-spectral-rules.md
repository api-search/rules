---
categories:
- archrock
description: Spectral linting rules defining API design standards and conventions for Archrock.
layout: rules
name: Archrock API Rules
provider_name: Archrock
provider_slug: archrock
rule_count: 12
rules:
- description: Quarterly financials must include year
  given: $.components.schemas.QuarterlyFinancials.properties
  name: archrock-quarterly-year-required
  severity: error
- description: Fleet statistics must include utilization rate
  given: $.components.schemas.FleetStatistics.properties
  name: archrock-fleet-utilization-rate
  severity: error
- description: Equipment status must be a valid enum value
  given: $.components.schemas.Equipment.properties.status
  name: archrock-equipment-status-enum
  severity: error
- description: SEC filing type must be a valid enum value
  given: $.components.schemas.SecFiling.properties.type
  name: archrock-sec-filing-type-enum
  severity: error
- description: List responses must include a total count
  given: $.components.schemas[*List].properties
  name: archrock-list-responses-have-total
  severity: warn
- description: List responses must include a limit field
  given: $.components.schemas[*List].properties
  name: archrock-list-responses-have-limit
  severity: warn
- description: All API operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: archrock-operations-have-tags
  severity: warn
- description: All API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: archrock-operations-have-summary
  severity: error
- description: All API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: archrock-operations-have-operation-id
  severity: error
- description: API must use API key security scheme
  given: $.components.securitySchemes
  name: archrock-api-key-security
  severity: warn
- description: API info must include contact information
  given: $.info
  name: archrock-info-contact-required
  severity: warn
- description: API must define at least one server
  given: $
  name: archrock-servers-defined
  severity: error
rules_file: rules/archrock-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/archrock/refs/heads/main/rules/archrock-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 5
slug: archrock-spectral-rules
tags:
- Natural Gas
- Compression Services
- Oil And Gas
- Energy
- Industrial
- 'NYSE: AROC'
- Spectral
- Linting
- API Governance
---

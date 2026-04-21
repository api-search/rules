---
categories:
- amadeus
description: Spectral linting rules defining API design standards and conventions for Amadeus.
layout: rules
name: Amadeus API Rules
provider_name: Amadeus
provider_slug: amadeus
rule_count: 15
rules:
- description: API info must have a title field.
  given: $.info
  name: amadeus-info-title-required
  severity: error
- description: API info must have a description.
  given: $.info
  name: amadeus-info-description-required
  severity: error
- description: API info must have a version.
  given: $.info
  name: amadeus-info-version-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-summary-required
  severity: error
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-description-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-tags-required
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: amadeus-operation-operationid-required
  severity: error
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: amadeus-parameter-description-required
  severity: warn
- description: All GET operations must have a 200 response.
  given: $.paths[*].get
  name: amadeus-response-200-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: amadeus-response-description-required
  severity: warn
- description: API should define bearer security scheme.
  given: $.components.securitySchemes
  name: amadeus-security-bearer-defined
  severity: warn
- description: Schemas should have descriptions.
  given: $.components.schemas[*]
  name: amadeus-schema-description
  severity: info
- description: API paths should use kebab-case.
  given: $.paths
  name: amadeus-paths-kebab-case
  severity: warn
- description: API info should include contact information.
  given: $.info
  name: amadeus-contact-required
  severity: info
- description: API must define at least one server.
  given: $
  name: amadeus-servers-required
  severity: error
rules_file: rules/amadeus-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/amadeus/refs/heads/main/rules/amadeus-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 5
slug: amadeus-spectral-rules
tags:
- Airlines
- Aviation
- Booking
- Destinations
- Flights
- Hospitality
- Hotels
- Market Insights
- Tourism
- Transfers
- Travel
- Spectral
- Linting
- API Governance
---

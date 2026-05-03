---
api_specs:
- filename: vendr-openapi.yml
  format: yaml
  label: Vendr OpenPrice API
  slug: vendr-openapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vendr/refs/heads/main/openapi/vendr-openapi.yml
categories:
- vendr
description: Spectral linting rules defining API design standards and conventions for Vendr.
layout: rules
name: Vendr API Rules
provider_name: Vendr
provider_slug: vendr
rule_count: 11
rules:
- description: All Vendr API paths must be prefixed with /v1/
  given: $.paths[*]~
  name: vendr-path-version-prefix
  severity: error
- description: All operations must require X-API-Key authentication
  given: $.paths[*][*]
  name: vendr-security-defined
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: vendr-path-kebab-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: vendr-operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: vendr-operation-id-camel-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: vendr-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: vendr-summary-title-case
  severity: warn
- description: Authenticated operations must include a 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: vendr-401-response-required
  severity: warn
- description: Operations must document rate limit (429) responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: vendr-429-response-required
  severity: warn
- description: API info must include contact information
  given: $.info
  name: vendr-info-contact
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: vendr-schema-description
  severity: hint
rules_file: rules/vendr-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vendr/refs/heads/main/rules/vendr-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 7
slug: vendr-rules
source_filename: vendr-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Vendr API uses /v1/ prefix on all paths\n  vendr-path-version-prefix:\n    description: All Vendr API paths must be prefixed with /v1/\n    message: \"Path '{{value}}' must start with /v1/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  # Vendr API key auth via X-API-Key header\n  vendr-security-defined:\n    description: All operations must require X-API-Key authentication\n    message: Operations must have security defined\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  # Vendr uses kebab-case path segments\n  vendr-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment '{{value}}' must use kebab-case (lowercase with hyphens)\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n   \
  \     match: \"^(/v1)(/[a-z0-9]+(-[a-z0-9]+)*(/{[a-zA-Z]+})?)*$\"\n\n  # All operations must have operationId\n  vendr-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId should be camelCase\n  vendr-operation-id-camel-case:\n    description: operationId should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations need summaries\n  vendr-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must be Title Case\n  vendr-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # Responses must include 401 for authenticated endpoints\n  vendr-401-response-required:\n    description: Authenticated operations must include a 401 response\n    message: Operation must define a 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Responses must include 429 rate limit response\n  vendr-429-response-required:\n    description: Operations must document rate limit (429) responses\n    message: Operation must define\
  \ a 429 Too Many Requests response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  # Info must have contact\n  vendr-info-contact:\n    description: API info must include contact information\n    message: API info must include contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # All schemas should have descriptions\n  vendr-schema-description:\n    description: Schema properties should have descriptions\n    message: Schema property should have a description\n    severity: hint\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vendr/refs/heads/main/rules/vendr-rules.yml
tags:
- Pricing
- Procurement
- SaaS
- Software Spend Management
- Negotiation
- Spectral
- Linting
- API Governance
---

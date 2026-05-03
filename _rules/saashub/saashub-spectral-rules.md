---
api_specs:
- filename: saashub-openapi.yml
  format: yaml
  label: SaaSHub API
  slug: saashub-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/saashub/refs/heads/main/openapi/saashub-openapi.yml
categories:
- saashub
description: Spectral linting rules defining API design standards and conventions for SaaSHub.
layout: rules
name: SaaSHub API Rules
provider_name: SaaSHub
provider_slug: saashub
rule_count: 7
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: saashub-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: saashub-tags-title-case
  severity: warn
- description: API key query parameter must be present on all operations
  given: $.paths[*][get]
  name: saashub-api-key-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: saashub-operation-ids-camel-case
  severity: warn
- description: Path parameters should include examples
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: saashub-path-params-have-examples
  severity: warn
- description: Successful responses must return application/json
  given: $.paths[*][*].responses[?(@property.match(/^2/))]
  name: saashub-responses-include-json
  severity: warn
- description: Responses should follow JSON:API structure with data field
  given: $.components.schemas[*]
  name: saashub-jsonapi-response-structure
  severity: warn
rules_file: rules/saashub-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/saashub/refs/heads/main/rules/saashub-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 6
slug: saashub-spectral-rules
source_filename: saashub-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  saashub-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  saashub-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  saashub-api-key-required:\n    description: API key query parameter must be present on all operations\n    message: \"All SaaSHub API operations require an api_key query parameter\"\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n\n  saashub-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  saashub-path-params-have-examples:\n    description: Path parameters should include examples\n    message: \"Path parameter should include an example value\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: schema.example\n      function: truthy\n\n  saashub-responses-include-json:\n    description: Successful responses must return application/json\n    message: \"2xx responses should include application/json content\"\n    severity: warn\n    given: \"$.paths[*][*].responses[?(@property.match(/^2/))]\"\n    then:\n      field: content\n      function: truthy\n\n  saashub-jsonapi-response-structure:\n\
  \    description: Responses should follow JSON:API structure with data field\n    message: \"Response schema should include a 'data' property per JSON:API spec\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/saashub/refs/heads/main/rules/saashub-spectral-rules.yml
tags:
- Alternatives
- SaaS
- Software Discovery
- Software Catalog
- Spectral
- Linting
- API Governance
---

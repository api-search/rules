---
api_specs:
- filename: toys-r-us-commerce-openapi.yml
  format: yaml
  label: Toys R Us Commerce API
  slug: logicbroker-commerce
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toys-r-us/refs/heads/main/openapi/toys-r-us-commerce-openapi.yml
categories:
- toys
description: Spectral linting rules defining API design standards and conventions for Toys R Us.
layout: rules
name: Toys R Us API Rules
provider_name: Toys R Us
provider_slug: toys-r-us
rule_count: 10
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: toys-r-us-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: toys-r-us-operation-ids-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][*]
  name: toys-r-us-operation-description-required
  severity: warn
- description: The API must use subscription-key authentication.
  given: $.components.securitySchemes.apiKeyAuth
  name: toys-r-us-api-key-security
  severity: warn
- description: All operations must be tagged for categorization.
  given: $.paths[*][*]
  name: toys-r-us-tags-required
  severity: warn
- description: GET collection endpoints should support page and pageSize parameters.
  given: $.paths[?(!@property.match(/{.*}/))][get].parameters
  name: toys-r-us-pagination-params
  severity: hint
- description: All operations must define a 200 or 201 success response.
  given: $.paths[*][*].responses
  name: toys-r-us-response-200-defined
  severity: error
- description: All operations should define a 401 unauthorized response.
  given: $.paths[*][*].responses
  name: toys-r-us-response-401-defined
  severity: warn
- description: Document import endpoints (*/import) must use POST method.
  given: $.paths[?(@property.match('/import$'))][*]
  name: toys-r-us-import-endpoints-use-post
  severity: error
- description: Error response schemas should reference the shared Error schema.
  given: $.paths[*][*].responses[401,400,404].content.application/json.schema
  name: toys-r-us-error-schema-consistent
  severity: warn
rules_file: rules/toys-r-us-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toys-r-us/refs/heads/main/rules/toys-r-us-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 6
slug: toys-r-us-rules
source_filename: toys-r-us-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  toys-r-us-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  toys-r-us-operation-ids-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: defined\n\n  toys-r-us-operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: defined\n\n  toys-r-us-api-key-security:\n    description: The API must use subscription-key authentication.\n    severity: warn\n    given: \"$.components.securitySchemes.apiKeyAuth\"\n    then:\n      function: defined\n\n  toys-r-us-tags-required:\n\
  \    description: All operations must be tagged for categorization.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  toys-r-us-pagination-params:\n    description: GET collection endpoints should support page and pageSize parameters.\n    severity: hint\n    given: \"$.paths[?(!@property.match(/{.*}/))][get].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n\n  toys-r-us-response-200-defined:\n    description: All operations must define a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  toys-r-us-response-401-defined:\n    description: All operations should define a 401 unauthorized response.\n    severity: warn\n    given: \"$.paths[*][*].responses\"\
  \n    then:\n      field: \"401\"\n      function: defined\n\n  toys-r-us-import-endpoints-use-post:\n    description: Document import endpoints (*/import) must use POST method.\n    severity: error\n    given: \"$.paths[?(@property.match('/import$'))][*]\"\n    then:\n      field: post\n      function: defined\n\n  toys-r-us-error-schema-consistent:\n    description: Error response schemas should reference the shared Error schema.\n    severity: warn\n    given: \"$.paths[*][*].responses[401,400,404].content.application/json.schema\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toys-r-us/refs/heads/main/rules/toys-r-us-rules.yml
tags:
- Commerce
- Dropship
- E-Commerce
- Retail
- Supply Chain
- Spectral
- Linting
- API Governance
---

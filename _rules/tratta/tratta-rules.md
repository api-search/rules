---
api_specs:
- filename: tratta-openapi.yml
  format: yaml
  label: Tratta API
  slug: tratta
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tratta/refs/heads/main/openapi/tratta-openapi.yml
categories:
- tratta
description: Spectral linting rules defining API design standards and conventions for Tratta.
layout: rules
name: Tratta API Rules
provider_name: Tratta
provider_slug: tratta
rule_count: 12
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tratta-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: tratta-operationid-required
  severity: error
- description: OperationIds should start with a verb (list, get, create, update, delete)
  given: $.paths[*][*].operationId
  name: tratta-operationid-verb-noun
  severity: warn
- description: All operations must have tags
  given: $.paths[*][*]
  name: tratta-tags-required
  severity: warn
- description: API must use bearer authentication
  given: $.components.securitySchemes[*]
  name: tratta-bearer-auth-required
  severity: error
- description: Server URL must include organization UUID variable
  given: $.servers[*].url
  name: tratta-org-uuid-in-server
  severity: warn
- description: POST operations should return 201 Created
  given: $.paths[*].post.responses
  name: tratta-response-201-for-post
  severity: warn
- description: GET operations must return 200 OK
  given: $.paths[*].get.responses
  name: tratta-response-200-for-get
  severity: error
- description: List endpoints should support limit and page parameters
  given: $.paths[*].get
  name: tratta-pagination-params
  severity: warn
- description: Responses should wrap data in a data property
  given: $.components.schemas[?(@property.match(/Response$/))].properties
  name: tratta-data-wrapper
  severity: warn
- description: POST and PUT request bodies should use application/json
  given: $.paths[*][post,put].requestBody.content
  name: tratta-request-body-json
  severity: error
- description: Query parameter names should use snake_case
  given: $.paths[*][*].parameters[*][?(@.in=='query')].name
  name: tratta-snake-case-parameters
  severity: warn
rules_file: rules/tratta-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tratta/refs/heads/main/rules/tratta-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 8
slug: tratta-rules
source_filename: tratta-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tratta-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  tratta-operationid-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  tratta-operationid-verb-noun:\n    description: OperationIds should start with a verb (list, get, create, update, delete)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get|create|update|delete|bulk|report|search)[A-Z].*$\"\n\n  tratta-tags-required:\n    description: All operations must have tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field:\
  \ tags\n      function: truthy\n\n  tratta-bearer-auth-required:\n    description: API must use bearer authentication\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n          - oauth2\n\n  tratta-org-uuid-in-server:\n    description: Server URL must include organization UUID variable\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{org-uuid\\\\}.*\"\n\n  tratta-response-201-for-post:\n    description: POST operations should return 201 Created\n    severity: warn\n    given: \"$.paths[*].post.responses\"\n    then:\n      field: \"201\"\n      function: truthy\n\n  tratta-response-200-for-get:\n    description: GET operations must return 200 OK\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\
  \n  tratta-pagination-params:\n    description: List endpoints should support limit and page parameters\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  tratta-data-wrapper:\n    description: Responses should wrap data in a data property\n    severity: warn\n    given: \"$.components.schemas[?(@property.match(/Response$/))].properties\"\n    then:\n      field: data\n      function: truthy\n\n  tratta-request-body-json:\n    description: POST and PUT request bodies should use application/json\n    severity: error\n    given: \"$.paths[*][post,put].requestBody.content\"\n    then:\n      field: \"application/json\"\n      function: truthy\n\n  tratta-snake-case-parameters:\n    description: Query parameter names should use snake_case\n    severity: warn\n    given: \"$.paths[*][*].parameters[*][?(@.in=='query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tratta/refs/heads/main/rules/tratta-rules.yml
tags:
- Billing
- Collections
- Payments
- Debt Collection
- Fintech
- Spectral
- Linting
- API Governance
---

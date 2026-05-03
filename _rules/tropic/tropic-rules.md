---
api_specs:
- filename: tropic-openapi.yml
  format: yaml
  label: Tropic API
  slug: rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tropic/refs/heads/main/openapi/tropic-openapi.yml
categories:
- tropic
description: Spectral linting rules defining API design standards and conventions for Tropic.
layout: rules
name: Tropic API Rules
provider_name: Tropic
provider_slug: tropic
rule_count: 10
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: tropic-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: tropic-operation-tags-required
  severity: error
- description: All paths must be versioned with /v1/ prefix
  given: $.paths[*]~
  name: tropic-path-versioned
  severity: warn
- description: All operations must have a 2xx success response
  given: $.paths[*][get,post,put,patch,delete]
  name: tropic-response-success-defined
  severity: error
- description: Resource IDs should be path parameters named {id}
  given: $.paths[*]~
  name: tropic-ids-as-path-params
  severity: hint
- description: GET collection endpoints should support page and per_page parameters
  given: $.paths[*][get].parameters[*].name
  name: tropic-pagination-params
  severity: warn
- description: POST and PUT operations must define a requestBody
  given: $.paths[*][post,put]
  name: tropic-request-body-required
  severity: error
- description: Only Bearer authentication should be used
  given: $.components.securitySchemes.*
  name: tropic-bearer-auth-only
  severity: error
- description: Error responses should include an error field
  given: $.paths[*][*].responses[4*,5*].content.application/json.schema.properties
  name: tropic-error-response-shape
  severity: warn
- description: Timestamp fields should use date-time format
  given: $.components.schemas[*].properties[created_at,updated_at,approved_at]
  name: tropic-timestamps-iso8601
  severity: hint
rules_file: rules/tropic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tropic/refs/heads/main/rules/tropic-rules.yml
severity_counts:
  error: 4
  hint: 2
  info: 0
  warn: 4
slug: tropic-rules
source_filename: tropic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tropic-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]* ?)+$\"\n\n  tropic-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  tropic-path-versioned:\n    description: All paths must be versioned with /v1/ prefix\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  tropic-response-success-defined:\n    description: All operations must have a 2xx success response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n\
  \          type: object\n          minProperties: 1\n\n  tropic-ids-as-path-params:\n    description: Resource IDs should be path parameters named {id}\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v1/[a-z-]+(/\\\\{id\\\\}(/[a-z-]+)?)?)+$\"\n\n  tropic-pagination-params:\n    description: GET collection endpoints should support page and per_page parameters\n    severity: warn\n    given: \"$.paths[*][get].parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - per_page\n          - q\n          - status\n          - supplier_id\n\n  tropic-request-body-required:\n    description: POST and PUT operations must define a requestBody\n    severity: error\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  tropic-bearer-auth-only:\n    description: Only Bearer authentication should be\
  \ used\n    severity: error\n    given: \"$.components.securitySchemes.*\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n\n  tropic-error-response-shape:\n    description: Error responses should include an error field\n    severity: warn\n    given: \"$.paths[*][*].responses[4*,5*].content.application/json.schema.properties\"\n    then:\n      field: error\n      function: truthy\n\n  tropic-timestamps-iso8601:\n    description: Timestamp fields should use date-time format\n    severity: hint\n    given: \"$.components.schemas[*].properties[created_at,updated_at,approved_at]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tropic/refs/heads/main/rules/tropic-rules.yml
tags:
- Benchmarking
- Contract Management
- Cost Optimization
- Procurement
- Renewals
- SaaS Management
- SaaS Procurement
- Spend Management
- Supplier Management
- Spectral
- Linting
- API Governance
---

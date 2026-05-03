---
api_specs:
- filename: trpc-openapi.yml
  format: yaml
  label: tRPC HTTP Protocol
  slug: http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trpc/refs/heads/main/openapi/trpc-openapi.yml
categories:
- trpc
description: Spectral linting rules defining API design standards and conventions for tRPC.
layout: rules
name: tRPC API Rules
provider_name: tRPC
provider_slug: trpc
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trpc-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: trpc-operation-tags-required
  severity: error
- description: Error responses must use the TRPCErrorResult schema
  given: $.paths[*][*].responses[4*,5*].content.application/json.schema
  name: trpc-trpc-error-schema
  severity: warn
- description: All operations should define a 200 success response
  given: $.paths[*][get,post]
  name: trpc-success-response-defined
  severity: error
- description: tRPC procedure paths should use dot notation for nested routers (e.g., router.procedure) or flat names for root procedures
  given: $.paths[*]~
  name: trpc-procedure-path-format
  severity: hint
- description: Batch endpoints must use POST method
  given: $.paths[/batch]
  name: trpc-batch-endpoint-post
  severity: error
- description: Query procedures should use GET method
  given: $.paths[*]~
  name: trpc-query-uses-get
  severity: hint
- description: GET operations should define an input query parameter
  given: $.paths[*][get]
  name: trpc-input-query-param
  severity: hint
rules_file: rules/trpc-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trpc/refs/heads/main/rules/trpc-rules.yml
severity_counts:
  error: 3
  hint: 3
  info: 0
  warn: 2
slug: trpc-rules
source_filename: trpc-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  trpc-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]* ?)+$\"\n\n  trpc-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  trpc-trpc-error-schema:\n    description: Error responses must use the TRPCErrorResult schema\n    severity: warn\n    given: \"$.paths[*][*].responses[4*,5*].content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  trpc-success-response-defined:\n    description: All operations should define a 200 success response\n    severity: error\n    given: \"$.paths[*][get,post]\"\n    then:\n  \
  \    field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  trpc-procedure-path-format:\n    description: >-\n      tRPC procedure paths should use dot notation for nested routers\n      (e.g., router.procedure) or flat names for root procedures\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-zA-Z0-9._-]+|/\\\\{procedure\\\\})$\"\n\n  trpc-batch-endpoint-post:\n    description: Batch endpoints must use POST method\n    severity: error\n    given: \"$.paths[/batch]\"\n    then:\n      field: post\n      function: truthy\n\n  trpc-query-uses-get:\n    description: Query procedures should use GET method\n    severity: hint\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/batch$\"\n\n  trpc-input-query-param:\n    description: GET operations should define an input\
  \ query parameter\n    severity: hint\n    given: \"$.paths[*][get]\"\n    then:\n      field: parameters\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trpc/refs/heads/main/rules/trpc-rules.yml
tags:
- API Composition
- API Framework
- BFF
- End-to-End Type Safety
- RPC
- TypeScript
- Spectral
- Linting
- API Governance
---

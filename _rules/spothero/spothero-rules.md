---
api_specs:
- filename: spothero-parking-openapi.yml
  format: yaml
  label: SpotHero Parking API
  slug: spothero-parking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spothero/refs/heads/main/openapi/spothero-parking-openapi.yml
categories:
- spothero
description: Spectral linting rules defining API design standards and conventions for SpotHero.
layout: rules
name: SpotHero API Rules
provider_name: SpotHero
provider_slug: spothero
rule_count: 14
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: spothero-operation-ids-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: spothero-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: spothero-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: spothero-tags-required
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*].get
  name: spothero-response-200-required
  severity: error
- description: POST operations that create resources should return 201
  given: $.paths[*].post
  name: spothero-response-201-post
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete]
  name: spothero-error-401-required
  severity: warn
- description: All operations must document 429 Too Many Requests response
  given: $.paths[*][get,post,put,patch,delete]
  name: spothero-error-429-required
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: spothero-path-kebab-case
  severity: warn
- description: API must use API key authentication
  given: $.components.securitySchemes.ApiKeyAuth
  name: spothero-api-key-auth
  severity: error
- description: Request bodies must specify application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: spothero-request-body-content-type
  severity: error
- description: Success responses must include a schema
  given: $.paths[*][get,post].responses[200,201].content.application/json
  name: spothero-response-schema-required
  severity: warn
- description: Parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: spothero-parameters-have-descriptions
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: spothero-schemas-have-descriptions
  severity: info
rules_file: rules/spothero-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spothero/refs/heads/main/rules/spothero-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 7
slug: spothero-rules
source_filename: spothero-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spothero-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spothero-operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  spothero-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\\s[A-Z][a-z]*)*$\"\n\n  spothero-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function:\
  \ truthy\n\n  spothero-response-200-required:\n    description: GET operations must have a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  spothero-response-201-post:\n    description: POST operations that create resources should return 201\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.201\n      function: truthy\n\n  spothero-error-401-required:\n    description: All operations must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  spothero-error-429-required:\n    description: All operations must document 429 Too Many Requests response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.429\n      function: truthy\n\n  spothero-path-kebab-case:\n    description: Path segments must\
  \ use kebab-case\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  spothero-api-key-auth:\n    description: API must use API key authentication\n    severity: error\n    given: \"$.components.securitySchemes.ApiKeyAuth\"\n    then:\n      function: truthy\n\n  spothero-request-body-content-type:\n    description: Request bodies must specify application/json content type\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      field: application/json\n      function: truthy\n\n  spothero-response-schema-required:\n    description: Success responses must include a schema\n    severity: warn\n    given: \"$.paths[*][get,post].responses[200,201].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  spothero-parameters-have-descriptions:\n    description: Parameters must have descriptions\n    severity: warn\n  \
  \  given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spothero-schemas-have-descriptions:\n    description: Schema properties should have descriptions\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spothero/refs/heads/main/rules/spothero-rules.yml
tags:
- Parking
- Mobility
- Transportation
- Navigation
- Reservations
- Spectral
- Linting
- API Governance
---

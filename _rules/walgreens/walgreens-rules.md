---
api_specs:
- filename: walgreens-store-locator-openapi.yml
  format: yaml
  label: Walgreens Store Locator API
  slug: walgreens-store-locator
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walgreens/refs/heads/main/openapi/walgreens-store-locator-openapi.yml
- filename: walgreens-prescription-refill-openapi.yml
  format: yaml
  label: Walgreens Prescription Refill API
  slug: walgreens-prescription-refill
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walgreens/refs/heads/main/openapi/walgreens-prescription-refill-openapi.yml
- filename: walgreens-vaccine-scheduling-openapi.yml
  format: yaml
  label: Walgreens Vaccine Scheduling API
  slug: walgreens-vaccine-scheduling
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walgreens/refs/heads/main/openapi/walgreens-vaccine-scheduling-openapi.yml
categories:
- walgreens
description: Spectral linting rules defining API design standards and conventions for Walgreens.
layout: rules
name: Walgreens API Rules
provider_name: Walgreens
provider_slug: walgreens
rule_count: 10
rules:
- description: All Walgreens API requests must include apiKey in the request body
  given: $.paths[*][post,patch,put].requestBody.content.application/json.schema.required
  name: walgreens-api-key-required
  severity: error
- description: All Walgreens API requests must include affId in the request body
  given: $.paths[*][post,patch,put].requestBody.content.application/json.schema.required
  name: walgreens-affiliate-id-required
  severity: error
- description: All Walgreens API servers must use services.walgreens.com for production
  given: $.servers[*].url
  name: walgreens-base-url-consistency
  severity: warn
- description: All Walgreens API operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: walgreens-operation-ids
  severity: error
- description: All Walgreens API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: walgreens-operation-summaries
  severity: warn
- description: POST and PATCH operations must specify application/json content type
  given: $.paths[*][post,patch].requestBody.content
  name: walgreens-request-content-type
  severity: warn
- description: API paths should include a version segment
  given: $.paths
  name: walgreens-versioned-paths
  severity: warn
- description: All Walgreens API server URLs must use HTTPS
  given: $.servers[*].url
  name: walgreens-https-only
  severity: error
- description: All Walgreens API operations should document error responses
  given: $.paths[*][post,patch,put,get].responses
  name: walgreens-error-responses
  severity: warn
- description: Successful responses should have a schema defined
  given: $.paths[*][get,post,put,patch].responses[200,201].content.application/json
  name: walgreens-response-schema
  severity: warn
rules_file: rules/walgreens-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/walgreens/refs/heads/main/rules/walgreens-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: walgreens-rules
source_filename: walgreens-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\nrules:\n  walgreens-api-key-required:\n    description: All Walgreens API requests must include apiKey in the request body\n    message: \"Walgreens API operations must require apiKey authentication parameter\"\n    severity: error\n    given: \"$.paths[*][post,patch,put].requestBody.content.application/json.schema.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: apiKey\n\n  walgreens-affiliate-id-required:\n    description: All Walgreens API requests must include affId in the request body\n    message: \"Walgreens API operations must require affId affiliate identifier parameter\"\n    severity: error\n    given: \"$.paths[*][post,patch,put].requestBody.content.application/json.schema.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: affId\n\
  \n  walgreens-base-url-consistency:\n    description: All Walgreens API servers must use services.walgreens.com for production\n    message: \"Production server URL should use services.walgreens.com domain\"\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://services(-qa)?\\\\.walgreens\\\\.com\"\n\n  walgreens-operation-ids:\n    description: All Walgreens API operations must have operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  walgreens-operation-summaries:\n    description: All Walgreens API operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  walgreens-request-content-type:\n    description:\
  \ POST and PATCH operations must specify application/json content type\n    message: \"POST/PATCH requests should specify application/json content type\"\n    severity: warn\n    given: \"$.paths[*][post,patch].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"application/json\"\n\n  walgreens-versioned-paths:\n    description: API paths should include a version segment\n    message: \"API path should include a version segment (e.g. /v1/, /v2/)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^/api/[a-z]+/(v[0-9]+|scheduling)/\":\n              type: object\n\n  walgreens-https-only:\n    description: All Walgreens API server URLs must use HTTPS\n    message: \"Server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  walgreens-error-responses:\n    description: All Walgreens API operations should document error responses\n    message: \"Operation should document 400 and 403 error responses\"\n    severity: warn\n    given: \"$.paths[*][post,patch,put,get].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"403\"]\n            - required: [\"500\"]\n\n  walgreens-response-schema:\n    description: Successful responses should have a schema defined\n    message: \"200/201 response should define a response schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses[200,201].content.application/json\"\n    then:\n      field: schema\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/walgreens/refs/heads/main/rules/walgreens-rules.yml
tags:
- Pharmacy
- Healthcare
- Retail
- Prescriptions
- Vaccines
- Spectral
- Linting
- API Governance
---

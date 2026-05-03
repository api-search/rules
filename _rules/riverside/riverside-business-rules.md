---
api_specs:
- filename: riverside-business-openapi.yml
  format: yaml
  label: Riverside Business API
  slug: riverside-business-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/riverside/refs/heads/main/openapi/riverside-business-openapi.yml
categories:
- riverside
description: Spectral linting rules defining API design standards and conventions for Riverside.
layout: rules
name: Riverside API Rules
provider_name: Riverside
provider_slug: riverside
rule_count: 11
rules:
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: riverside-operation-has-tag
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: riverside-operation-has-summary
  severity: error
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: riverside-operation-has-operation-id
  severity: error
- description: API should use Bearer/API key authentication
  given: $.components.securitySchemes[*]
  name: riverside-api-key-auth
  severity: warn
- description: Recording endpoints should use recording_id as path parameter
  given: $.paths['/api/v1/recordings/{recording_id}'][*].parameters[?(@.in === 'path')]
  name: riverside-recording-id-path-param
  severity: info
- description: GET operations should have a 200 response
  given: $.paths[*].get
  name: riverside-responses-have-200
  severity: error
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: riverside-delete-returns-204
  severity: warn
- description: Paginated list endpoints should use page parameter
  given: $.paths[*].get.parameters[?(@.name === 'page')]
  name: riverside-pagination-uses-page
  severity: info
- description: Schema components should have descriptions
  given: $.components.schemas[*]
  name: riverside-schema-has-description
  severity: info
- description: Operations should document rate limiting in description
  given: $.paths[*][get,post]
  name: riverside-rate-limit-documented
  severity: info
- description: API paths should include version prefix (v1, v2, v3)
  given: $.paths[*]~
  name: riverside-versioned-paths
  severity: warn
rules_file: rules/riverside-business-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/riverside/refs/heads/main/rules/riverside-business-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 4
  warn: 4
slug: riverside-business-rules
source_filename: riverside-business-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Riverside Business API Conventions\n\n  riverside-operation-has-tag:\n    description: All operations must have at least one tag\n    message: Operation {{path}} is missing a tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  riverside-operation-has-summary:\n    description: All operations must have a summary\n    message: Operation {{path}} is missing a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  riverside-operation-has-operation-id:\n    description: All operations must have an operationId\n    message: Operation {{path}} is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  riverside-api-key-auth:\n    description: API should use Bearer/API\
  \ key authentication\n    message: Security scheme should use http bearer or apiKey type\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              type: string\n              enum:\n                - http\n                - apiKey\n\n  riverside-recording-id-path-param:\n    description: Recording endpoints should use recording_id as path parameter\n    message: Recording path parameter should be named recording_id\n    severity: info\n    given: \"$.paths['/api/v1/recordings/{recording_id}'][*].parameters[?(@.in === 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^recording_id$\"\n\n  riverside-responses-have-200:\n    description: GET operations should have a 200 response\n    message: GET operation {{path}} should have a 200 response\n    severity: error\n   \
  \ given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  riverside-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: DELETE operation {{path}} should return 204\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: truthy\n\n  riverside-pagination-uses-page:\n    description: Paginated list endpoints should use page parameter\n    message: List endpoint {{path}} should support pagination with page parameter\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.name === 'page')]\"\n    then:\n      field: schema.type\n      function: pattern\n      functionOptions:\n        match: \"^integer$\"\n\n  riverside-schema-has-description:\n    description: Schema components should have descriptions\n    message: Schema {{path}} is missing a description\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n\
  \      function: truthy\n\n  riverside-rate-limit-documented:\n    description: Operations should document rate limiting in description\n    message: Operation {{path}} should describe rate limits\n    severity: info\n    given: \"$.paths[*][get,post]\"\n    then:\n      field: description\n      function: truthy\n\n  riverside-versioned-paths:\n    description: API paths should include version prefix (v1, v2, v3)\n    message: Path {{path}} should include a version prefix\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/riverside/refs/heads/main/rules/riverside-business-rules.yml
tags:
- Podcast
- Video Recording
- Media
- Content Creation
- Audio
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: walk-score-openapi.yml
  format: yaml
  label: Walk Score API
  slug: walk-score-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walk-score/refs/heads/main/openapi/walk-score-openapi.yml
- filename: walk-score-transit-openapi.yml
  format: yaml
  label: Walk Score Transit API
  slug: walk-score-transit-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/walk-score/refs/heads/main/openapi/walk-score-transit-openapi.yml
categories:
- walk
description: Spectral linting rules defining API design standards and conventions for Walk Score.
layout: rules
name: Walk Score API Rules
provider_name: Walk Score
provider_slug: walk-score
rule_count: 7
rules:
- description: All Walk Score API requests must include the wsapikey parameter
  given: $.paths[*][get].parameters[*]
  name: walk-score-api-key-required
  severity: error
- description: All Walk Score API server URLs must use HTTPS
  given: $.servers[*].url
  name: walk-score-https-only
  severity: error
- description: All Walk Score API operations must have operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: walk-score-operation-ids
  severity: error
- description: All Walk Score API operations must have a summary in Title Case
  given: $.paths[*][get,post,put,patch,delete]
  name: walk-score-operation-summaries
  severity: warn
- description: Walk Score location endpoints should document lat and lon parameters
  given: $.paths[*][get].parameters
  name: walk-score-lat-lon-params
  severity: warn
- description: Walk Score API endpoints should support JSON response format
  given: $.paths[*][get].responses[200].content
  name: walk-score-json-format-support
  severity: warn
- description: Walk Score API responses should include error status codes
  given: $.paths[*][get].responses
  name: walk-score-status-codes
  severity: warn
rules_file: rules/walk-score-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/walk-score/refs/heads/main/rules/walk-score-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: walk-score-rules
source_filename: walk-score-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\nrules:\n  walk-score-api-key-required:\n    description: All Walk Score API requests must include the wsapikey parameter\n    message: \"Walk Score API operations must require wsapikey authentication parameter\"\n    severity: error\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          if:\n            properties:\n              name:\n                const: wsapikey\n          then:\n            properties:\n              required:\n                const: true\n\n  walk-score-https-only:\n    description: All Walk Score API server URLs must use HTTPS\n    message: \"Server URL must use HTTPS\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  walk-score-operation-ids:\n    description: All Walk Score API operations must have operationId\n\
  \    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  walk-score-operation-summaries:\n    description: All Walk Score API operations must have a summary in Title Case\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  walk-score-lat-lon-params:\n    description: Walk Score location endpoints should document lat and lon parameters\n    message: \"Location-based endpoints should include lat and lon parameters\"\n    severity: warn\n    given: \"$.paths[*][get].parameters\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name:\n                pattern: \"^(lat|lon)$\"\n\n  walk-score-json-format-support:\n\
  \    description: Walk Score API endpoints should support JSON response format\n    message: \"API should support JSON response format\"\n    severity: warn\n    given: \"$.paths[*][get].responses[200].content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"application/json\"\n\n  walk-score-status-codes:\n    description: Walk Score API responses should include error status codes\n    message: \"Walk Score operations should document 400 error responses\"\n    severity: warn\n    given: \"$.paths[*][get].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"400\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/walk-score/refs/heads/main/rules/walk-score-rules.yml
tags:
- Walkability
- Transit
- Bikeability
- Location
- Real Estate
- Urban Planning
- Transportation
- Spectral
- Linting
- API Governance
---

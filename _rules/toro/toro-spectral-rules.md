---
api_specs:
- filename: toro-horizon360-openapi.yml
  format: yaml
  label: Toro Horizon360
  slug: horizon360
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toro/refs/heads/main/openapi/toro-horizon360-openapi.yml
- filename: toro-intellidash-openapi.yml
  format: yaml
  label: Toro IntelliDash
  slug: intellidash
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/toro/refs/heads/main/openapi/toro-intellidash-openapi.yml
categories:
- toro
description: Spectral linting rules defining API design standards and conventions for Toro.
layout: rules
name: Toro API Rules
provider_name: Toro
provider_slug: toro
rule_count: 10
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: toro-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: toro-operation-summary-title-case
  severity: warn
- description: API paths must use kebab-case for path segments
  given: $.paths[*]~
  name: toro-paths-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: toro-must-have-tags
  severity: error
- description: All responses must have a description
  given: $.paths[*][*].responses[*]
  name: toro-responses-must-have-description
  severity: error
- description: All operations must define a success response (200 or 201)
  given: $.paths[*][get,post,put,patch,delete].responses
  name: toro-must-have-200-or-201
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: toro-parameters-must-have-description
  severity: warn
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: toro-request-body-content-type
  severity: warn
- description: Error responses (4xx, 5xx) should reference a schema
  given: $.paths[*][*].responses[4xx,5xx]
  name: toro-error-response-schema
  severity: warn
- description: List operations should support pagination parameters
  given: $.paths[*][get][?(@.operationId =~ /^list/)]
  name: toro-list-operations-must-support-pagination
  severity: warn
rules_file: rules/toro-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/toro/refs/heads/main/rules/toro-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: toro-spectral-rules
source_filename: toro-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  toro-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  toro-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  toro-paths-kebab-case:\n    description: API paths must use kebab-case for path segments\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-]+|/\\\\{[a-zA-Z0-9]+\\\\})*$\"\n\n  toro-must-have-tags:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\
  \n  toro-responses-must-have-description:\n    description: All responses must have a description\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  toro-must-have-200-or-201:\n    description: All operations must define a success response (200 or 201)\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  toro-parameters-must-have-description:\n    description: All parameters must have descriptions\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  toro-request-body-content-type:\n    description: Request bodies should use application/json content type\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n\
  \    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [\"application/json\"]\n\n  toro-error-response-schema:\n    description: Error responses (4xx, 5xx) should reference a schema\n    severity: warn\n    given: \"$.paths[*][*].responses[4xx,5xx]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            content:\n              type: object\n\n  toro-list-operations-must-support-pagination:\n    description: List operations should support pagination parameters\n    severity: warn\n    given: \"$.paths[*][get][?(@.operationId =~ /^list/)]\"\n    then:\n      field: parameters\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/toro/refs/heads/main/rules/toro-spectral-rules.yml
tags:
- Landscaping
- Irrigation
- Golf
- Equipment
- Smart Connected Products
- Fleet Management
- Turf Management
- Spectral
- Linting
- API Governance
---

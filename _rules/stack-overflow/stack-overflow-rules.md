---
api_specs:
- filename: stack-overflow-openapi.yml
  format: yaml
  label: Stack Overflow API
  slug: stack-overflow-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stack-overflow/refs/heads/main/openapi/stack-overflow-openapi.yml
- filename: stack-overflow-for-teams-openapi.yml
  format: yaml
  label: Stack Overflow for Teams API v3
  slug: stack-overflow-for-teams-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stack-overflow/refs/heads/main/openapi/stack-overflow-for-teams-openapi.yml
categories:
- stack
description: Spectral linting rules defining API design standards and conventions for Stack Overflow.
layout: rules
name: Stack Overflow API Rules
provider_name: Stack Overflow
provider_slug: stack-overflow
rule_count: 9
rules:
- description: All Stack Overflow API operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: stack-overflow-operation-summaries-title-case
  severity: warn
- description: Stack Overflow API operationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: stack-overflow-operationid-camel-case
  severity: warn
- description: All Stack Overflow API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: stack-overflow-operations-must-have-operationid
  severity: error
- description: List operations should support page and pagesize parameters
  given: $.paths[*].get.parameters[*]
  name: stack-overflow-pagination-supported
  severity: warn
- description: Stack Overflow list responses must use the wrapper format with items
  given: $.components.schemas[*]
  name: stack-overflow-wrapper-response-schema
  severity: warn
- description: Stack Overflow for Teams API must use bearer token authentication
  given: $.components.securitySchemes
  name: stack-overflow-teams-bearer-auth
  severity: error
- description: Stack Overflow for Teams paths must include team parameter
  given: $.paths[*]~
  name: stack-overflow-teams-path-includes-team
  severity: warn
- description: Error responses must reference ErrorResponse schema
  given: $.paths[*][get,post,put,patch,delete].responses[4*].content.application/json.schema
  name: stack-overflow-response-error-schemas
  severity: warn
- description: POST and PUT operations must have request bodies
  given: $.paths[*][post,put]
  name: stack-overflow-post-requires-body
  severity: error
rules_file: rules/stack-overflow-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stack-overflow/refs/heads/main/rules/stack-overflow-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 6
slug: stack-overflow-rules
source_filename: stack-overflow-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stack-overflow-operation-summaries-title-case:\n    description: All Stack Overflow API operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  stack-overflow-operationid-camel-case:\n    description: Stack Overflow API operationIds must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stack-overflow-operations-must-have-operationid:\n    description: All Stack Overflow API operations must have an operationId\n    message: \"Operation is missing operationId\"\n    severity:\
  \ error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  stack-overflow-pagination-supported:\n    description: List operations should support page and pagesize parameters\n    message: \"List operations should support pagination via page and pagesize\"\n    severity: warn\n    given: \"$.paths[*].get.parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-overflow-wrapper-response-schema:\n    description: Stack Overflow list responses must use the wrapper format with items\n    message: \"Response schema should include items array for list responses\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-overflow-teams-bearer-auth:\n    description: Stack Overflow for Teams API must use bearer token authentication\n    message: \"\
  Teams API must define bearerAuth security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-overflow-teams-path-includes-team:\n    description: Stack Overflow for Teams paths must include team parameter\n    message: \"Teams API paths should include the {team} path parameter\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/teams/\\\\{team\\\\}\"\n\n  stack-overflow-response-error-schemas:\n    description: Error responses must reference ErrorResponse schema\n    message: \"4xx responses should use ErrorResponse schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[4*].content.application/json.schema\"\n    then:\n      function: truthy\n\n  stack-overflow-post-requires-body:\n    description: POST and PUT operations must have request bodies\n\
  \    message: \"POST/PUT operations must define a requestBody\"\n    severity: error\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stack-overflow/refs/heads/main/rules/stack-overflow-rules.yml
tags:
- Answers
- Code
- Developer Community
- Developer Tools
- Knowledge Base
- Programming
- Q&A
- Questions
- Stack Overflow
- Spectral
- Linting
- API Governance
---

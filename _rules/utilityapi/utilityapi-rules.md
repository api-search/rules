---
api_specs:
- filename: utilityapi-openapi.yml
  format: yaml
  label: UtilityAPI
  slug: utilityapi
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/utilityapi/refs/heads/main/openapi/utilityapi-openapi.yml
categories:
- utilityapi
description: Spectral linting rules defining API design standards and conventions for UtilityAPI.
layout: rules
name: UtilityAPI API Rules
provider_name: UtilityAPI
provider_slug: utilityapi
rule_count: 8
rules:
- description: All operations must use bearerAuth security
  given: $.paths[*][*]
  name: utilityapi-bearer-auth-required
  severity: error
- description: Path parameters for resource IDs should be named 'uid'
  given: $.paths[*][*].parameters[*]
  name: utilityapi-uid-path-parameters
  severity: warn
- description: List endpoints should support 'next' cursor pagination
  given: $.paths[*].get
  name: utilityapi-pagination-next-cursor
  severity: warn
- description: List responses should use plural noun envelope
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: utilityapi-list-response-envelope
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: utilityapi-operations-must-have-summaries
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: utilityapi-operations-must-have-tags
  severity: warn
- description: Operations should define 401 error responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: utilityapi-error-response-defined
  severity: warn
- description: Operation IDs should use camelCase
  given: $.paths[*][*].operationId
  name: utilityapi-operation-ids-camel-case
  severity: warn
rules_file: rules/utilityapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/utilityapi/refs/heads/main/rules/utilityapi-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: utilityapi-rules
source_filename: utilityapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  utilityapi-bearer-auth-required:\n    description: All operations must use bearerAuth security\n    message: Operation must use bearerAuth security scheme\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  utilityapi-uid-path-parameters:\n    description: Path parameters for resource IDs should be named 'uid'\n    message: Resource identifier path parameters should be named 'uid'\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      function: pattern\n      field: name\n      functionOptions:\n        match: \"^(uid|username|name|provider|architecture|version)$\"\n\n  utilityapi-pagination-next-cursor:\n    description: List endpoints should support 'next' cursor pagination\n    message: List\
  \ operations should include 'next' cursor parameter\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: truthy\n      field: parameters\n\n  utilityapi-list-response-envelope:\n    description: List responses should use plural noun envelope\n    message: List responses should wrap items in a plural noun envelope\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      function: truthy\n      field: properties\n\n  utilityapi-operations-must-have-summaries:\n    description: All operations must have a summary\n    message: Operations must have a summary field\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: truthy\n      field: summary\n\n  utilityapi-operations-must-have-tags:\n    description: All operations must have at least one tag\n    message: Operations should be tagged for organization\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\
  \n    then:\n      function: truthy\n      field: tags\n\n  utilityapi-error-response-defined:\n    description: Operations should define 401 error responses\n    message: Operations should document 401 Unauthorized responses\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: truthy\n      field: '401'\n\n  utilityapi-operation-ids-camel-case:\n    description: Operation IDs should use camelCase\n    message: OperationId should use camelCase naming\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/utilityapi/refs/heads/main/rules/utilityapi-rules.yml
tags:
- Energy
- Utilities
- Green Button
- Billing Data
- Meter Data
- Clean Energy
- Spectral
- Linting
- API Governance
---

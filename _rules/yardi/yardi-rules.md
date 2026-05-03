---
api_specs:
- filename: yardi-voyager-api-openapi.yml
  format: yaml
  label: Yardi Voyager API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/yardi/refs/heads/main/openapi/yardi-voyager-api-openapi.yml
categories:
- yardi
description: Spectral linting rules defining API design standards and conventions for Yardi.
layout: rules
name: Yardi API Rules
provider_name: Yardi
provider_slug: yardi
rule_count: 10
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: yardi-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase
  given: $.paths[*][*].operationId
  name: yardi-operation-id-camel-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: yardi-must-have-operation-id
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: yardi-must-have-tags
  severity: warn
- description: POST operations for imports must have a request body
  given: $.paths[*][post]
  name: yardi-post-must-have-request-body
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: yardi-must-have-description
  severity: warn
- description: All operations must have a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: yardi-responses-must-have-200
  severity: error
- description: Authenticated operations must document 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: yardi-responses-must-have-401
  severity: warn
- description: API must have contact information
  given: $.info
  name: yardi-must-have-contact
  severity: warn
- description: API must have terms of service
  given: $.info
  name: yardi-must-have-terms-of-service
  severity: warn
rules_file: rules/yardi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/yardi/refs/heads/main/rules/yardi-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 8
slug: yardi-rules
source_filename: yardi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  yardi-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  yardi-operation-id-camel-case:\n    description: All operationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    given: \"$.paths[*][*].operationId\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  yardi-must-have-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n\n  yardi-must-have-tags:\n    description: All operations\
  \ must have at least one tag\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: tags\n      function: truthy\n\n  yardi-post-must-have-request-body:\n    description: POST operations for imports must have a request body\n    message: \"POST operation importing data must have a request body\"\n    given: \"$.paths[*][post]\"\n    severity: warn\n    then:\n      field: requestBody\n      function: truthy\n\n  yardi-must-have-description:\n    description: All operations must have a description\n    message: \"Operation is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    severity: warn\n    then:\n      field: description\n      function: truthy\n\n  yardi-responses-must-have-200:\n    description: All operations must have a 200 response\n    message: \"Operation is missing a 200 success response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n\
  \    severity: error\n    then:\n      field: \"200\"\n      function: truthy\n\n  yardi-responses-must-have-401:\n    description: Authenticated operations must document 401 response\n    message: \"Operation is missing a 401 unauthorized response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    severity: warn\n    then:\n      field: \"401\"\n      function: truthy\n\n  yardi-must-have-contact:\n    description: API must have contact information\n    message: \"API info is missing contact details\"\n    given: \"$.info\"\n    severity: warn\n    then:\n      field: contact\n      function: truthy\n\n  yardi-must-have-terms-of-service:\n    description: API must have terms of service\n    message: \"API info is missing termsOfService\"\n    given: \"$.info\"\n    severity: warn\n    then:\n      field: termsOfService\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/yardi/refs/heads/main/rules/yardi-rules.yml
tags:
- Accounting
- Commercial Real Estate
- Coworking
- Investment Management
- Multifamily
- Property Management
- Real Estate
- Residential
- Self Storage
- Senior Living
- Spectral
- Linting
- API Governance
---

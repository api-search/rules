---
api_specs:
- filename: stack-exchange-openapi.yml
  format: yaml
  label: Stack Exchange API
  slug: stack-exchange-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stack-exchange/refs/heads/main/openapi/stack-exchange-openapi.yml
categories:
- stack
description: Spectral linting rules defining API design standards and conventions for Stack Exchange.
layout: rules
name: Stack Exchange API Rules
provider_name: Stack Exchange
provider_slug: stack-exchange
rule_count: 9
rules:
- description: All Stack Exchange API operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: stack-exchange-operation-summaries-title-case
  severity: warn
- description: Stack Exchange API endpoints must require the site query parameter
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: stack-exchange-site-parameter-required
  severity: warn
- description: Stack Exchange API operationIds must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: stack-exchange-operationid-camel-case
  severity: warn
- description: All Stack Exchange API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: stack-exchange-operations-must-have-operationid
  severity: error
- description: Stack Exchange API path parameters for IDs use semicolon-delimited format
  given: $.paths[*]~
  name: stack-exchange-semicolon-ids-in-path
  severity: info
- description: Stack Exchange API responses should use the wrapper envelope format
  given: $.paths[*][get,post,put,patch,delete].responses.200.content.application/json.schema
  name: stack-exchange-wrapper-response
  severity: info
- description: Stack Exchange list operations should support page and pagesize parameters
  given: $.paths[*].get.parameters[*]
  name: stack-exchange-pagination-parameters
  severity: warn
- description: Stack Exchange API must define OAuth 2.0 security scheme
  given: $.components.securitySchemes
  name: stack-exchange-oauth2-defined
  severity: error
- description: All tags referenced in operations must be defined at document level
  given: $.paths[*][get,post,put,patch,delete].tags
  name: stack-exchange-tags-defined
  severity: warn
rules_file: rules/stack-exchange-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stack-exchange/refs/heads/main/rules/stack-exchange-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: stack-exchange-rules
source_filename: stack-exchange-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stack-exchange-operation-summaries-title-case:\n    description: All Stack Exchange API operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  stack-exchange-site-parameter-required:\n    description: Stack Exchange API endpoints must require the site query parameter\n    message: \"Operation must include the 'site' query parameter\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-exchange-operationid-camel-case:\n    description: Stack Exchange API operationIds must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\
  \n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stack-exchange-operations-must-have-operationid:\n    description: All Stack Exchange API operations must have an operationId\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  stack-exchange-semicolon-ids-in-path:\n    description: Stack Exchange API path parameters for IDs use semicolon-delimited format\n    message: \"Path {ids} parameters accept semicolon-delimited lists of IDs\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z][a-z-/{}]*$\"\n\n  stack-exchange-wrapper-response:\n    description: Stack Exchange API responses should use the wrapper envelope format\n    message:\
  \ \"Response should use Stack Exchange wrapper format with items and has_more\"\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-exchange-pagination-parameters:\n    description: Stack Exchange list operations should support page and pagesize parameters\n    message: \"List operations should support page and pagesize parameters\"\n    severity: warn\n    given: \"$.paths[*].get.parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  stack-exchange-oauth2-defined:\n    description: Stack Exchange API must define OAuth 2.0 security scheme\n    message: \"Stack Exchange API spec must define oauth2 security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: oauth2\n      function: truthy\n\n  stack-exchange-tags-defined:\n\
  \    description: All tags referenced in operations must be defined at document level\n    message: \"Tags must be defined in the global tags list\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].tags\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stack-exchange/refs/heads/main/rules/stack-exchange-rules.yml
tags:
- Answers
- Code
- Community
- Developer Tools
- Knowledge Base
- Q&A
- Questions
- Stack Exchange
- Spectral
- Linting
- API Governance
---

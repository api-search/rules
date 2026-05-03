---
api_specs:
- filename: mapmyfitness-openapi.yml
  format: yaml
  label: MapMyFitness API
  slug: mapmyfitness-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/under-armour/refs/heads/main/openapi/mapmyfitness-openapi.yml
categories:
- ua
description: Spectral linting rules defining API design standards and conventions for Under Armour.
layout: rules
name: Under Armour API Rules
provider_name: Under Armour
provider_slug: under-armour
rule_count: 10
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: ua-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: ua-operation-summary-title-case
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: ua-tags-required
  severity: warn
- description: Paths should use trailing slash per Under Armour API convention
  given: $.paths[*]~
  name: ua-path-trailing-slash
  severity: info
- description: Operations must define at least one 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: ua-responses-must-include-success
  severity: error
- description: API must define OAuth2 security scheme
  given: $.components.securitySchemes
  name: ua-oauth2-security-defined
  severity: error
- description: Paths must include API version prefix
  given: $.paths[*]~
  name: ua-version-prefix-in-path
  severity: warn
- description: Path parameters must include a description
  given: $.paths[*][*].parameters[?(@.in == "path")]
  name: ua-path-parameters-described
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete.responses
  name: ua-delete-returns-204
  severity: warn
- description: POST create operations should return 201 Created
  given: $.paths[*].post.responses
  name: ua-post-returns-201
  severity: warn
rules_file: rules/under-armour-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/under-armour/refs/heads/main/rules/under-armour-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 6
slug: under-armour-rules
source_filename: under-armour-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ua-operation-ids-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: operationId\n      function: truthy\n\n  ua-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$'\n\n  ua-tags-required:\n    description: Operations must have at least one tag\n    message: Operation must include at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  ua-path-trailing-slash:\n    description: Paths should use trailing\
  \ slash per Under Armour API convention\n    message: Under Armour API paths use trailing slashes\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '.*\\/$'\n\n  ua-responses-must-include-success:\n    description: Operations must define at least one 2xx success response\n    message: Operation must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  ua-oauth2-security-defined:\n    description: API must define OAuth2 security scheme\n    message: Under Armour APIs require OAuth 2.0 security\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  ua-version-prefix-in-path:\n    description: Paths must include API version prefix\n    message: Path must include a version prefix like\
  \ /v7.1/\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: '^\\/v[0-9]+\\.[0-9]+\\/'\n\n  ua-path-parameters-described:\n    description: Path parameters must include a description\n    message: Path parameter must have a description\n    severity: warn\n    given: $.paths[*][*].parameters[?(@.in == \"path\")]\n    then:\n      field: description\n      function: truthy\n\n  ua-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: DELETE operation should include a 204 response\n    severity: warn\n    given: $.paths[*].delete.responses\n    then:\n      field: '204'\n      function: truthy\n\n  ua-post-returns-201:\n    description: POST create operations should return 201 Created\n    message: POST create operation should include a 201 response\n    severity: warn\n    given: $.paths[*].post.responses\n    then:\n      field: '201'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/under-armour/refs/heads/main/rules/under-armour-rules.yml
tags:
- Fitness
- Health
- Wearables
- Connected Fitness
- Sports
- Fortune 1000
- Spectral
- Linting
- API Governance
---

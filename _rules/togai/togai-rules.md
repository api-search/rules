---
api_specs:
- filename: togai-openapi.yml
  format: yaml
  label: Togai API
  slug: togai-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/togai/refs/heads/main/openapi/togai-openapi.yml
categories:
- togai
description: Spectral linting rules defining API design standards and conventions for Togai.
layout: rules
name: Togai API Rules
provider_name: Togai
provider_slug: togai
rule_count: 9
rules:
- description: All Togai API operations must use Bearer authentication
  given: $.components.securitySchemes
  name: togai-auth-bearer
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: togai-operation-id-camelcase
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: togai-operation-id-required
  severity: error
- description: All operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: togai-tags-required
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: togai-summary-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: togai-path-kebab-case
  severity: warn
- description: Pagination parameters should use nextToken or pageNo
  given: $.paths[*][get].parameters[?(@.name == 'pageToken' || @.name == 'nextToken')]
  name: togai-pagination-params
  severity: info
- description: Operations must define error responses
  given: $.paths[*][get,post,put,patch,delete].responses
  name: togai-error-responses
  severity: warn
- description: Request bodies should use application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: togai-request-body-json
  severity: warn
rules_file: rules/togai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/togai/refs/heads/main/rules/togai-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: togai-rules
source_filename: togai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Togai uses Bearer token authentication throughout\n  togai-auth-bearer:\n    description: All Togai API operations must use Bearer authentication\n    message: Security must be defined using bearerAuth\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  # OperationIds must use camelCase\n  togai-operation-id-camelcase:\n    description: OperationIds must use camelCase\n    message: \"{{property}} operationId should be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # All operations must have operationId\n  togai-operation-id-required:\n    description: All operations must have an operationId\n    message: Operation is missing an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n    \
  \  function: defined\n\n  # All operations must have tags\n  togai-tags-required:\n    description: All operations must be tagged\n    message: Operation is missing tags\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  # Summaries must use Title Case\n  togai-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"{{value}} summary should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ()-]*$\"\n\n  # All path segments should use kebab-case\n  togai-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment {{value}} should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}/]*)+$\"\
  \n\n  # Pagination parameters should use consistent names\n  togai-pagination-params:\n    description: Pagination parameters should use nextToken or pageNo\n    message: Pagination parameters should follow Togai conventions\n    severity: info\n    given: \"$.paths[*][get].parameters[?(@.name == 'pageToken' || @.name == 'nextToken')]\"\n    then:\n      function: defined\n\n  # 4xx responses should be defined\n  togai-error-responses:\n    description: Operations must define error responses\n    message: Operations should define 400 or 401 error responses\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n\n  # Request bodies should use application/json\n  togai-request-body-json:\n    description: Request bodies should use application/json\n    message: Request\
  \ body content type should be application/json\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/togai/refs/heads/main/rules/togai-rules.yml
tags:
- Billing
- Metering
- Usage-Based Pricing
- Revenue Management
- SaaS
- Fintech
- Spectral
- Linting
- API Governance
---

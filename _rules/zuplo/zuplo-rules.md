---
api_specs:
- filename: zuplo-openapi.yml
  format: yaml
  label: Zuplo Developer API
  slug: zuplo
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zuplo/refs/heads/main/openapi/zuplo-openapi.yml
categories:
- zuplo
description: Spectral linting rules defining API design standards and conventions for Zuplo.
layout: rules
name: Zuplo API Rules
provider_name: Zuplo
provider_slug: zuplo
rule_count: 9
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: zuplo-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: zuplo-operation-id-required
  severity: error
- description: Account-scoped paths must use {accountName} parameter
  given: $.paths['/v1/accounts/{accountName}/*']
  name: zuplo-account-name-path-param
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: zuplo-kebab-case-paths
  severity: warn
- description: All operations must define a 200 or 201 response
  given: $.paths[*][get,post,put,patch]
  name: zuplo-response-200-defined
  severity: error
- description: API uses Bearer token authentication
  given: $.components.securitySchemes.ApiKeyAuth
  name: zuplo-bearer-auth-scheme
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][*].tags
  name: zuplo-tags-required
  severity: warn
- description: DELETE operations should not have a request body
  given: $.paths[*].delete.requestBody
  name: zuplo-delete-no-body
  severity: warn
- description: PATCH operations should have a request body
  given: $.paths[*].patch
  name: zuplo-patch-has-request-body
  severity: warn
rules_file: rules/zuplo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/zuplo/refs/heads/main/rules/zuplo-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: zuplo-rules
source_filename: zuplo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  zuplo-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"'{{value}}' should be in Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  zuplo-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  zuplo-account-name-path-param:\n    description: Account-scoped paths must use {accountName} parameter\n    message: Account-scoped paths should use {accountName} as the path parameter\n    severity: warn\n    given: \"$.paths['/v1/accounts/{accountName}/*']\"\n    then:\n      function: truthy\n\n  zuplo-kebab-case-paths:\n    description: Path segments must use kebab-case\n    message: \"Path segment '{{value}}' should use kebab-case\"\
  \n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  zuplo-response-200-defined:\n    description: All operations must define a 200 or 201 response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  zuplo-bearer-auth-scheme:\n    description: API uses Bearer token authentication\n    severity: info\n    given: \"$.components.securitySchemes.ApiKeyAuth\"\n    then:\n      function: truthy\n\n  zuplo-tags-required:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  zuplo-delete-no-body:\n    description: DELETE operations\
  \ should not have a request body\n    severity: warn\n    given: \"$.paths[*].delete.requestBody\"\n    then:\n      function: undefined\n\n  zuplo-patch-has-request-body:\n    description: PATCH operations should have a request body\n    severity: warn\n    given: \"$.paths[*].patch\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zuplo/refs/heads/main/rules/zuplo-rules.yml
tags:
- AI Gateway
- API Management
- Gateways
- Platform
- Spectral
- Linting
- API Governance
---

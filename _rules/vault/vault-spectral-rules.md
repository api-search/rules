---
api_specs:
- filename: vault-kv-openapi.yml
  format: yaml
  label: HashiCorp Vault KV Secrets Engine API
  slug: vault-kv
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vault/refs/heads/main/openapi/vault-kv-openapi.yml
- filename: vault-sys-openapi.yml
  format: yaml
  label: HashiCorp Vault System Backend API
  slug: vault-sys
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vault/refs/heads/main/openapi/vault-sys-openapi.yml
categories:
- delete
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tags
- vault
description: Spectral linting rules defining API design standards and conventions for HashiCorp Vault.
layout: rules
name: HashiCorp Vault API Rules
provider_name: HashiCorp Vault
provider_slug: vault
rule_count: 28
rules:
- description: API title must be present.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "HashiCorp Vault".
  given: $.info.title
  name: info-title-starts-with-hashicorp-vault
  severity: warn
- description: API info description must be present.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: API specification must use OpenAPI 3.x.
  given: $
  name: openapi-version-3x
  severity: error
- description: Servers array must be defined.
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-required
  severity: error
- description: All Vault API paths begin at the server level v1 — paths should be relative.
  given: $.paths
  name: paths-v1-prefix
  severity: info
- description: Paths must not end with a trailing slash.
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-operationId-required
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "HashiCorp Vault".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-hashicorp-vault
  severity: warn
- description: All operations should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined.
  given: $
  name: tags-global-defined
  severity: warn
- description: All parameters should have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define at least one success (2xx or 204) response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Vault operations should define 403 Permission Denied response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-403-required
  severity: warn
- description: All responses must have a description.
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Schema definitions should have descriptions.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: schema-properties-have-descriptions
  severity: info
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Vault uses X-Vault-Token header, not Authorization Bearer.
  given: $.components.securitySchemes[?(@.type == 'apiKey')]
  name: vault-token-header-not-bearer
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 204 No Content.
  given: $.paths[*].delete.responses
  name: delete-returns-204
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-description
  severity: warn
- description: Operations should have x-microcks-operation for mock compatibility.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-has-microcks-extension
  severity: info
rules_file: rules/vault-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vault/refs/heads/main/rules/vault-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 5
  warn: 12
slug: vault-spectral-rules
source_filename: vault-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-starts-with-hashicorp-vault:\n    description: API title should start with \"HashiCorp Vault\".\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^HashiCorp Vault\"\n\n  info-description-required:\n    description: API info description must be present.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3x:\n    description: API specification must use OpenAPI 3.x.\n    severity: error\n    given: \"$\"\n    then:\n      field:\
  \ openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-required:\n    description: Servers array must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https-required:\n    description: Server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS\n  paths-v1-prefix:\n    description: All Vault API paths begin at the server level v1 — paths should be relative.\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/v1\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # OPERATIONS\n  operation-operationId-required:\n\
  \    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationId-camelCase:\n    description: operationId should use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,options,head]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-starts-with-hashicorp-vault:\n    description: Operation summaries should start with \"HashiCorp Vault\".\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^HashiCorp Vault\"\n\n  operation-description-required:\n    description: All operations should have a description.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-tags-required:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-global-defined:\n    description: Global tags array should be defined.\n    severity: warn\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters should have a description.\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Operations must define at least one success (2xx or\
  \ 204) response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n            - required: ['204']\n\n  response-403-required:\n    description: Vault operations should define 403 Permission Denied response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: '403'\n      function: truthy\n\n  response-description-required:\n    description: All responses must have a description.\n    severity: error\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-description-required:\n    description: Schema definitions should have descriptions.\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-have-descriptions:\n\
  \    description: Schema properties should have descriptions.\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  vault-token-header-not-bearer:\n    description: Vault uses X-Vault-Token header, not Authorization Bearer.\n    severity: info\n    given: \"$.components.securitySchemes[?(@.type == 'apiKey')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^X-Vault-Token$\"\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-returns-204:\n    description:\
  \ DELETE operations should return 204 No Content.\n    severity: info\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: '204'\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-description:\n    description: Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n\n  operation-has-microcks-extension:\n    description: Operations should have x-microcks-operation for mock compatibility.\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vault/refs/heads/main/rules/vault-spectral-rules.yml
tags:
- DevOps
- Encryption
- Open Source
- PKI
- Secrets Management
- Security
- Spectral
- Linting
- API Governance
---

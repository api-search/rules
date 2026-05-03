---
api_specs:
- filename: veeva-vault-openapi.yml
  format: yaml
  label: Veeva Vault Platform API
  slug: veeva-vault-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veeva/refs/heads/main/openapi/veeva-vault-openapi.yml
- filename: veeva-vault-openapi.yml
  format: yaml
  label: Veeva Vault Query Language (VQL) API
  slug: veeva-vault-query-language
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veeva/refs/heads/main/openapi/veeva-vault-openapi.yml
categories:
- delete
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- requestbody
- response
- schema
- security
- servers
- tag
- tags
- vault
description: Spectral linting rules defining API design standards and conventions for veeva.
layout: rules
name: veeva API Rules
provider_name: veeva
provider_slug: veeva
rule_count: 34
rules:
- description: Info title must be defined.
  given: $.info
  name: info-title-required
  severity: error
- description: Info title must start with "Veeva".
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: Info description must be defined and non-empty.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be defined.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information must be defined.
  given: $.info
  name: info-contact-required
  severity: warn
- description: Must use OpenAPI 3.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Each server must have a description.
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Path segments must use kebab-case (lowercase with hyphens, not underscores or camelCase).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Veeva" (company name prefix).
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: operationId must use camelCase.
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-operationid-camelcase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined.
  given: $
  name: tags-defined
  severity: warn
- description: Each tag must have a description.
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: All parameters must have a description.
  given: $..parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema with a type.
  given: $..parameters[*].schema
  name: parameter-schema-type
  severity: warn
- description: Request bodies should have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: requestbody-description-required
  severity: info
- description: Every operation must have at least one success (2xx) response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have a description.
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: error
- description: Authenticated operations should define a 401 response.
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-401-defined
  severity: warn
- description: Top-level component schemas must have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema property names should use snake_case (Vault convention with __v/__c suffixes).
  given: $.components.schemas[*].properties[*]~
  name: schema-properties-snake-case
  severity: info
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security must be defined.
  given: $
  name: security-global-defined
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body.
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Vault operations should use VaultSession security scheme.
  given: $.paths[*][get,post,put,delete,patch]
  name: vault-session-auth
  severity: info
- description: Vault API responses should include responseStatus in schemas.
  given: $.components.schemas[*].properties
  name: vault-response-status
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/veeva-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/veeva/refs/heads/main/rules/veeva-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 4
  warn: 19
slug: veeva-spectral-rules
source_filename: veeva-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: Info title must be defined.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  info-title-prefix:\n    description: Info title must start with \"Veeva\".\n    severity: warn\n    given: \"$.info.title\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Veeva\"\n\n  info-description-required:\n    description: Info description must be defined and non-empty.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API version must be defined.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information must be defined.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI\
  \ VERSION\n  openapi-version-3:\n    description: Must use OpenAPI 3.x.\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: Server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-description:\n    description: Each server must have a description.\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens, not underscores or camelCase).\n    severity: warn\n    given:\
  \ \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_-]+)+$\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash.\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-title-case:\n    description: Operation summaries must start with \"Veeva\" (company name prefix).\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Veeva \"\n\n  operation-description-required:\n    description: Every operation must have a description.\n    severity: warn\n    given: \"\
  $.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  operation-operationid-camelcase:\n    description: operationId must use camelCase.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-defined:\n    description: Global tags array should be defined.\n    severity: warn\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\
  \n  tag-description-required:\n    description: Each tag must have a description.\n    severity: warn\n    given: \"$.tags[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: \"$..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-type:\n    description: All parameters must have a schema with a type.\n    severity: warn\n    given: \"$..parameters[*].schema\"\n    then:\n      field: type\n      function: truthy\n\n  # REQUEST BODIES\n  requestbody-description-required:\n    description: Request bodies should have a description.\n    severity: info\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must have at least one success (2xx) response.\n\
  \    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  response-description-required:\n    description: All responses must have a description.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  response-401-defined:\n    description: Authenticated operations should define a 401 response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"401\"]\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description: Top-level component schemas must have a description.\n\
  \    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  schema-properties-snake-case:\n    description: Schema property names should use snake_case (Vault convention with __v/__c suffixes).\n    severity: info\n    given: \"$.components.schemas[*].properties[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*(__v|__c)?$\"\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined in components.\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  security-global-defined:\n    description: Global security must be defined.\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: \"\
  $.paths[*].get\"\n    then:\n      field: requestBody\n      function: falsy\n\n  delete-no-request-body:\n    description: DELETE operations should not have a request body.\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # VAULT-SPECIFIC RULES\n  vault-session-auth:\n    description: Vault operations should use VaultSession security scheme.\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"security\"]\n            - {}\n\n  vault-response-status:\n    description: Vault API responses should include responseStatus in schemas.\n    severity: info\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description:\
  \ Descriptions must not be empty strings.\n    severity: warn\n    given: \"$..description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/veeva/refs/heads/main/rules/veeva-spectral-rules.yml
tags:
- Spectral
- Linting
- API Governance
---

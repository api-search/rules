---
api_specs:
- filename: wildapricot-admin-api-openapi.yml
  format: yaml
  label: WildApricot Admin API
  slug: wildapricot-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/wildapricot/refs/heads/main/openapi/wildapricot-admin-api-openapi.yml
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- post
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for WildApricot.
layout: rules
name: WildApricot API Rules
provider_name: WildApricot
provider_slug: wildapricot
rule_count: 26
rules:
- description: API info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: API info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: API info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: API info should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: All WildApricot specs must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: WildApricot paths should use /accounts/{accountId}/ prefix
  given: $.paths[*]~
  name: paths-account-prefix
  severity: info
- description: Paths must not end with a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operation-id-required
  severity: error
- description: Operation summaries should start with "WildApricot"
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-wildapricot-prefix
  severity: info
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: Global tags array must be defined
  given: $
  name: tags-global-defined
  severity: warn
- description: Path parameters named accountId should use path-level definition
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'accountId')]
  name: parameter-account-id-path
  severity: info
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Request bodies must define content
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-content-required
  severity: error
- description: Every operation must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Security schemes must be defined for OAuth2
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: Operations should define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-security-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: POST operations should return 200 or 201
  given: $.paths[*].post
  name: post-returns-2xx
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/wildapricot-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/wildapricot/refs/heads/main/rules/wildapricot-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 4
  warn: 11
slug: wildapricot-spectral-rules
source_filename: wildapricot-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n\n  # INFO / METADATA\n  info-title-required:\n    description: API info must have a title\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: API info must have a description\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-version-required:\n    description: API info must have a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: API info should have contact information\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: All WildApricot specs must use OpenAPI 3.x\n    severity: error\n    given: $\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n \
  \ # SERVERS\n  servers-defined:\n    description: Servers array must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: Server URLs must use HTTPS\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-account-prefix:\n    description: WildApricot paths should use /accounts/{accountId}/ prefix\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(accounts|rpc)/\"\n\n  paths-no-trailing-slash:\n    description: Paths must not end with a trailing slash\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: All operations must have a summary\n    severity: error\n \
  \   given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: summary\n      function: truthy\n\n  operation-description-required:\n    description: All operations should have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: description\n      function: truthy\n\n  operation-operation-id-required:\n    description: All operations must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-summary-wildapricot-prefix:\n    description: Operation summaries should start with \"WildApricot\"\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete,head,options].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^WildApricot \"\n\n  operation-tags-required:\n    description: All operations must have at least one tag\n    severity:\
  \ warn\n    given: $.paths[*][get,post,put,patch,delete,head,options]\n    then:\n      field: tags\n      function: truthy\n\n  # TAGS\n  tags-global-defined:\n    description: Global tags array must be defined\n    severity: warn\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-account-id-path:\n    description: Path parameters named accountId should use path-level definition\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'accountId')]\n    then:\n      field: in\n      function: pattern\n      functionOptions:\n        match: \"^path$\"\n\n  parameter-description-required:\n    description: All parameters must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  # REQUEST BODIES\n  request-body-content-required:\n    description: Request bodies must define content\n    severity:\
  \ error\n    given: $.paths[*][post,put,patch].requestBody\n    then:\n      field: content\n      function: truthy\n\n  # RESPONSES\n  response-success-required:\n    description: Every operation must define at least one 2xx response\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: responses\n      function: truthy\n\n  response-description-required:\n    description: All responses must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS\n  schema-description-required:\n    description: Top-level schemas should have descriptions\n    severity: info\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  security-schemes-defined:\n    description: Security schemes must be defined for OAuth2\n    severity: warn\n    given: $.components\n    then:\n      field:\
  \ securitySchemes\n      function: truthy\n\n  operation-security-defined:\n    description: Operations should define security requirements\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: security\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  post-returns-2xx:\n    description: POST operations should return 200 or 201\n    severity: warn\n    given: $.paths[*].post\n    then:\n      field: responses\n      function: truthy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions must not be empty strings\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/wildapricot/refs/heads/main/rules/wildapricot-spectral-rules.yml
tags:
- Membership Management
- Associations
- Nonprofit
- Events
- Payments
- Spectral
- Linting
- API Governance
---

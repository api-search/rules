---
api_specs:
- filename: tinybird-openapi.yml
  format: yaml
  label: Tinybird API
  slug: tinybird
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tinybird/refs/heads/main/openapi/tinybird-openapi.yml
categories:
- tinybird
description: Spectral linting rules defining API design standards and conventions for Tinybird.
layout: rules
name: Tinybird API Rules
provider_name: Tinybird
provider_slug: tinybird
rule_count: 12
rules:
- description: All operations must have operationId values
  given: $.paths[*][get,post,put,delete,patch]
  name: tinybird-operation-ids-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: tinybird-operation-summaries-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: tinybird-operation-tags-required
  severity: warn
- description: All paths must begin with /v0/ to indicate API versioning
  given: $.paths
  name: tinybird-versioned-paths
  severity: error
- description: Paths should not have trailing slashes (except root collection paths)
  given: $.paths
  name: tinybird-no-trailing-slash
  severity: hint
- description: APIs must define bearer token security scheme
  given: $.components.securitySchemes.bearerAuth
  name: tinybird-bearer-auth-required
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: tinybird-response-200-defined
  severity: error
- description: Operations should define 401 unauthorized responses
  given: $.paths[*][post,put,delete,patch]
  name: tinybird-error-responses-defined
  severity: warn
- description: Schema objects should have descriptions
  given: $.components.schemas[*]
  name: tinybird-schemas-have-descriptions
  severity: hint
- description: Operation IDs must use camelCase (Tinybird convention)
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: tinybird-kebab-case-operation-ids
  severity: warn
- description: API info must include contact information
  given: $.info
  name: tinybird-info-contact-defined
  severity: warn
- description: API must define server URLs
  given: $
  name: tinybird-servers-defined
  severity: error
rules_file: rules/tinybird-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tinybird/refs/heads/main/rules/tinybird-rules.yml
severity_counts:
  error: 6
  hint: 2
  info: 0
  warn: 4
slug: tinybird-rules
source_filename: tinybird-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  tinybird-operation-ids-required:\n    description: All operations must have operationId values\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: defined\n\n  tinybird-operation-summaries-required:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: defined\n\n  tinybird-operation-tags-required:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag for grouping\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: defined\n\n  tinybird-versioned-paths:\n    description: All paths must begin with /v0/ to indicate API versioning\n    message:\
  \ Path {{value}} must begin with /v0/\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v0/\"\n\n  tinybird-no-trailing-slash:\n    description: Paths should not have trailing slashes (except root collection paths)\n    message: Path should not end with a trailing slash unless it is a collection path\n    severity: hint\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".[^/]/$\"\n\n  tinybird-bearer-auth-required:\n    description: APIs must define bearer token security scheme\n    message: Security scheme must include bearerAuth of type bearer\n    severity: error\n    given: $.components.securitySchemes.bearerAuth\n    then:\n      function: defined\n\n  tinybird-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: GET operation must have a 200 response defined\n    severity: error\n    given: $.paths[*].get\n    then:\n\
  \      field: responses.200\n      function: defined\n\n  tinybird-error-responses-defined:\n    description: Operations should define 401 unauthorized responses\n    message: Operation should include 401 response for unauthorized access\n    severity: warn\n    given: $.paths[*][post,put,delete,patch]\n    then:\n      field: responses.401\n      function: defined\n\n  tinybird-schemas-have-descriptions:\n    description: Schema objects should have descriptions\n    message: Schema property should include a description\n    severity: hint\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: defined\n\n  tinybird-kebab-case-operation-ids:\n    description: Operation IDs must use camelCase (Tinybird convention)\n    message: OperationId {{value}} must use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tinybird-info-contact-defined:\n\
  \    description: API info must include contact information\n    message: API info.contact must be defined\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: defined\n\n  tinybird-servers-defined:\n    description: API must define server URLs\n    message: At least one server must be defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tinybird/refs/heads/main/rules/tinybird-rules.yml
tags:
- Analytics
- Data
- Real-Time
- SQL
- Streaming
- Spectral
- Linting
- API Governance
---

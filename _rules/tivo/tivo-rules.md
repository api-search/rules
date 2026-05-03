---
api_specs:
- filename: tivo-video-metadata-openapi.yml
  format: yaml
  label: TiVo Video Metadata API
  slug: tivo-video-metadata
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tivo/refs/heads/main/openapi/tivo-video-metadata-openapi.yml
categories:
- tivo
description: Spectral linting rules defining API design standards and conventions for Tivo.
layout: rules
name: Tivo API Rules
provider_name: Tivo
provider_slug: tivo
rule_count: 13
rules:
- description: All operations must have operationId values
  given: $.paths[*][get,post,put,delete,patch]
  name: tivo-operation-ids-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: tivo-operation-summaries-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: tivo-operation-tags-required
  severity: warn
- description: All paths must begin with /v3/ for the Video Metadata API
  given: $.paths
  name: tivo-versioned-paths
  severity: error
- description: API must define bearer token authentication
  given: $.components.securitySchemes.bearerAuth
  name: tivo-bearer-auth-required
  severity: error
- description: All GET operations must define a 200 success response
  given: $.paths[*].get
  name: tivo-response-200-defined
  severity: error
- description: All operations must handle unauthorized responses
  given: $.paths[*][get,post]
  name: tivo-response-401-defined
  severity: warn
- description: Resource lookup operations must handle not found responses
  given: $.paths[*~contains('{')][get]
  name: tivo-response-404-defined
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: tivo-kebab-case-paths
  severity: warn
- description: Response schemas must use application/json content type
  given: $.paths[*][*].responses[*].content
  name: tivo-content-type-json
  severity: warn
- description: All schema objects should have descriptions
  given: $.components.schemas[*]
  name: tivo-schemas-have-descriptions
  severity: hint
- description: API must define at least one server URL
  given: $
  name: tivo-servers-defined
  severity: error
- description: API version should follow semantic versioning
  given: $.info.version
  name: tivo-info-version-semver
  severity: hint
rules_file: rules/tivo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tivo/refs/heads/main/rules/tivo-rules.yml
severity_counts:
  error: 6
  hint: 2
  info: 0
  warn: 5
slug: tivo-rules
source_filename: tivo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  tivo-operation-ids-required:\n    description: All operations must have operationId values\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: defined\n\n  tivo-operation-summaries-required:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: summary\n      function: defined\n\n  tivo-operation-tags-required:\n    description: All operations must have at least one tag\n    message: Operation must have at least one tag for grouping\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: tags\n      function: defined\n\n  tivo-versioned-paths:\n    description: All paths must begin with /v3/ for the Video Metadata API\n    message: Path {{value}}\
  \ must begin with /v3/\n    severity: error\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v3/\"\n\n  tivo-bearer-auth-required:\n    description: API must define bearer token authentication\n    message: Security scheme bearerAuth must be defined\n    severity: error\n    given: $.components.securitySchemes.bearerAuth\n    then:\n      function: defined\n\n  tivo-response-200-defined:\n    description: All GET operations must define a 200 success response\n    message: GET operation must have a 200 response defined\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: responses.200\n      function: defined\n\n  tivo-response-401-defined:\n    description: All operations must handle unauthorized responses\n    message: Operation must define a 401 unauthorized response\n    severity: warn\n    given: $.paths[*][get,post]\n    then:\n      field: responses.401\n      function: defined\n\n  tivo-response-404-defined:\n\
  \    description: Resource lookup operations must handle not found responses\n    message: Operations with path parameters must define 404 not found response\n    severity: warn\n    given: $.paths[*~contains('{')][get]\n    then:\n      field: responses.404\n      function: defined\n\n  tivo-kebab-case-paths:\n    description: Path segments must use kebab-case\n    message: Path segment must use kebab-case lowercase with hyphens\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9]+/[a-z][a-z0-9-]*(/\\\\{[a-zA-Z]+\\\\})?(/[a-z][a-z0-9-]*)?)*$\"\n\n  tivo-content-type-json:\n    description: Response schemas must use application/json content type\n    message: Response content type must be application/json\n    severity: warn\n    given: $.paths[*][*].responses[*].content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            application/json:\n\
  \              type: object\n\n  tivo-schemas-have-descriptions:\n    description: All schema objects should have descriptions\n    message: Schema must include a description\n    severity: hint\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: defined\n\n  tivo-servers-defined:\n    description: API must define at least one server URL\n    message: API must have servers defined\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: defined\n\n  tivo-info-version-semver:\n    description: API version should follow semantic versioning\n    message: info.version should use a versioned format like v3\n    severity: hint\n    given: $.info.version\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tivo/refs/heads/main/rules/tivo-rules.yml
tags:
- Entertainment
- Metadata
- Television
- Movies
- Music
- Streaming
- Spectral
- Linting
- API Governance
---

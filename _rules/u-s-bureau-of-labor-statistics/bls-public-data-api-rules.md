---
api_specs:
- filename: bls-public-data-api-openapi.yaml
  format: yaml
  label: BLS Public Data API
  slug: bls-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/u-s-bureau-of-labor-statistics/refs/heads/main/openapi/bls-public-data-api-openapi.yaml
categories:
- bls
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for U.S. Bureau of Labor Statistics.
layout: rules
name: U.S. Bureau of Labor Statistics API Rules
provider_name: U.S. Bureau of Labor Statistics
provider_slug: u-s-bureau-of-labor-statistics
rule_count: 33
rules:
- description: API title must be present and include "BLS" or "Bureau of Labor Statistics".
  given: $.info.title
  name: info-title-required
  severity: error
- description: API info must have a description with at least 50 characters.
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified.
  given: $.info
  name: info-version-required
  severity: error
- description: Contact information should be provided.
  given: $.info
  name: info-contact-required
  severity: warn
- description: All BLS API specs must use OpenAPI 3.0.x.
  given: $
  name: openapi-version-3
  severity: warn
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Server URL should point to api.bls.gov.
  given: $.servers[*].url
  name: servers-bls-domain
  severity: warn
- description: Path segments must use kebab-case (lowercase letters, numbers, hyphens, or {params}).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths should not have trailing slashes (except the multiple series POST endpoint).
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: info
- description: All paths should be accessed via a versioned server URL (v1 or v2).
  given: $.servers[*].url
  name: paths-versioned
  severity: info
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "U.S. Bureau of Labor Statistics".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationIds should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Global tags array should be defined.
  given: $
  name: tags-defined
  severity: info
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Query and path parameter names should use snake_case.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query' || @.in == 'path')].name
  name: parameter-snake-case
  severity: info
- description: POST request bodies should use application/json content type.
  given: $.paths[*].post.requestBody.content
  name: request-body-json
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 400 Bad Request response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-400-defined
  severity: warn
- description: All response definitions must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: warn
- description: All top-level component schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema property names should use snake_case.
  given: $.components.schemas[*].properties[*]~
  name: schema-property-snake-case
  severity: info
- description: Security schemes should be defined in components.
  given: $.components.securitySchemes
  name: security-scheme-defined
  severity: warn
- description: Security schemes should have a description.
  given: $.components.securitySchemes[*]
  name: security-scheme-description
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Descriptions should not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: BLS API responses include a 'status' field; schemas should document it.
  given: $.components.schemas.SeriesResponse.properties
  name: bls-status-field-documented
  severity: info
- description: registrationkey parameter should not be marked as required (public endpoints work without it).
  given: $.paths[*][get,post].parameters[?(@.name == 'registrationkey')].required
  name: bls-registration-key-optional
  severity: warn
rules_file: rules/bls-public-data-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/u-s-bureau-of-labor-statistics/refs/heads/main/rules/bls-public-data-api-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 7
  warn: 17
slug: bls-public-data-api-rules
source_filename: bls-public-data-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  # INFO / METADATA\n  info-title-required:\n    description: API title must be present and include \"BLS\" or \"Bureau of Labor Statistics\".\n    severity: error\n    given: $.info.title\n    then:\n      function: truthy\n\n  info-description-required:\n    description: API info must have a description with at least 50 characters.\n    severity: warn\n    given: $.info\n    then:\n      field: description\n      function: minLength\n      functionOptions:\n        min: 50\n\n  info-version-required:\n    description: API version must be specified.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  info-contact-required:\n    description: Contact information should be provided.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  # OPENAPI VERSION\n  openapi-version-3:\n    description: All BLS API specs must use OpenAPI 3.0.x.\n    severity: warn\n    given: $\n   \
  \ then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  # SERVERS\n  servers-defined:\n    description: At least one server must be defined.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  servers-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  servers-bls-domain:\n    description: Server URL should point to api.bls.gov.\n    severity: warn\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"api\\\\.bls\\\\.gov\"\n\n  # PATHS — NAMING CONVENTIONS\n  paths-kebab-case:\n    description: Path segments must use kebab-case (lowercase letters, numbers, hyphens, or {params}).\n    severity: warn\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^(/[a-z0-9{}-]*)+$\"\n\n  paths-no-trailing-slash:\n    description: Paths should not have trailing slashes (except the multiple series POST endpoint).\n    severity: info\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".+/$\"\n\n  paths-versioned:\n    description: All paths should be accessed via a versioned server URL (v1 or v2).\n    severity: info\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[12]$\"\n\n  # OPERATIONS\n  operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  operation-summary-prefix:\n    description: Operation summaries should start with \"U.S. Bureau of Labor Statistics\".\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        match: \"^U\\\\.S\\\\. Bureau of Labor Statistics\"\n\n  operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: description\n      function: truthy\n\n  operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-id-camel-case:\n    description: OperationIds should use camelCase.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  operation-tags-required:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n  \
  \    function: truthy\n\n  # TAGS\n  tags-defined:\n    description: Global tags array should be defined.\n    severity: info\n    given: $\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  parameter-description-required:\n    description: All parameters must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  parameter-schema-required:\n    description: All parameters must have a schema.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: schema\n      function: truthy\n\n  parameter-snake-case:\n    description: Query and path parameter names should use snake_case.\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].parameters[?(@.in == 'query' || @.in == 'path')].name\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n\
  \  # REQUEST BODIES\n  request-body-json:\n    description: POST request bodies should use application/json content type.\n    severity: warn\n    given: $.paths[*].post.requestBody.content\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - application/json\n\n  # RESPONSES\n  response-success-required:\n    description: All operations must define a 200 response.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"200\"\n\n  response-400-defined:\n    description: Operations should define a 400 Bad Request response.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"400\"\n\n\
  \  response-description-required:\n    description: All response definitions must have a description.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  # SCHEMAS — PROPERTY NAMING\n  schema-description-required:\n    description: All top-level component schemas should have a description.\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  schema-property-snake-case:\n    description: Schema property names should use snake_case.\n    severity: info\n    given: $.components.schemas[*].properties[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  # SECURITY\n  security-scheme-defined:\n    description: Security schemes should be defined in components.\n    severity: warn\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  security-scheme-description:\n\
  \    description: Security schemes should have a description.\n    severity: info\n    given: $.components.securitySchemes[*]\n    then:\n      field: description\n      function: truthy\n\n  # HTTP METHOD CONVENTIONS\n  get-no-request-body:\n    description: GET operations must not have a request body.\n    severity: error\n    given: $.paths[*].get\n    then:\n      field: requestBody\n      function: falsy\n\n  # GENERAL QUALITY\n  no-empty-descriptions:\n    description: Descriptions should not be empty strings.\n    severity: warn\n    given: $..description\n    then:\n      function: pattern\n      functionOptions:\n        match: \".{1,}\"\n\n  bls-status-field-documented:\n    description: BLS API responses include a 'status' field; schemas should document it.\n    severity: info\n    given: $.components.schemas.SeriesResponse.properties\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - status\n\
  \n  bls-registration-key-optional:\n    description: registrationkey parameter should not be marked as required (public endpoints work without it).\n    severity: warn\n    given: $.paths[*][get,post].parameters[?(@.name == 'registrationkey')].required\n    then:\n      function: falsy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/u-s-bureau-of-labor-statistics/refs/heads/main/rules/bls-public-data-api-rules.yml
tags:
- Federal Government
- Labor
- Statistics
- Employment
- Economic Data
- Spectral
- Linting
- API Governance
---

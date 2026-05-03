---
api_specs:
- filename: staples-advantage-eprocurement-api-openapi.yml
  format: yaml
  label: Staples Advantage eProcurement API
  slug: staples-advantage-eprocurement-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/staples/refs/heads/main/openapi/staples-advantage-eprocurement-api-openapi.yml
categories:
- staples
description: Spectral linting rules defining API design standards and conventions for Staples.
layout: rules
name: Staples API Rules
provider_name: Staples
provider_slug: staples
rule_count: 21
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][*].operationId
  name: staples-operation-ids-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: staples-operation-summary-title-case
  severity: warn
- description: All API paths must be versioned with /v1/ prefix
  given: $.paths
  name: staples-api-versioned-paths
  severity: error
- description: All operations must use Bearer token authentication
  given: $.paths[*][*]
  name: staples-bearer-auth-required
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: staples-get-operations-200
  severity: error
- description: POST create operations must return 201 Created
  given: $.paths[*].post
  name: staples-post-create-201
  severity: error
- description: All operations must define a 401 Unauthorized response
  given: $.paths[*][*]
  name: staples-unauthorized-response
  severity: error
- description: Operations with path parameters should define 404
  given: $.paths[*][*]
  name: staples-not-found-response
  severity: warn
- description: All operations must define a 429 Too Many Requests response
  given: $.paths[*][*]
  name: staples-rate-limit-response
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*].tags
  name: staples-operation-tags-required
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: staples-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: staples-path-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths
  name: staples-no-trailing-slash
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: staples-path-parameters-required
  severity: error
- description: Query parameters must have descriptions
  given: $.paths[*][*].parameters[?(@.in=='query')]
  name: staples-query-parameters-described
  severity: warn
- description: POST operations must define a request body
  given: $.paths[*].post
  name: staples-post-request-body
  severity: error
- description: Schema components should have descriptions where possible
  given: $.components.schemas[*]
  name: staples-schemas-have-descriptions
  severity: info
- description: API must have contact information
  given: $.info
  name: staples-info-contact
  severity: warn
- description: API must reference terms of service
  given: $.info
  name: staples-info-terms
  severity: info
- description: API must have a description
  given: $.info
  name: staples-info-description
  severity: error
- description: API must define at least one server
  given: $
  name: staples-servers-defined
  severity: error
rules_file: rules/staples-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/staples/refs/heads/main/rules/staples-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 2
  warn: 10
slug: staples-rules
source_filename: staples-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation naming and structure\n  staples-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., searchProducts, createOrder)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  staples-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n\n  staples-api-versioned-paths:\n    description: All API paths must be versioned with /v1/ prefix\n    message: \"Path '{{property}}' must start with /v1/\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  # Authentication requirements\n  staples-bearer-auth-required:\n    description: All operations must use Bearer token authentication\n    message: \"Operation must reference bearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  # Response codes\n  staples-get-operations-200:\n    description: GET operations must define a 200 response\n    message: \"GET operation must have a 200 response defined\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: \"responses.200\"\n      function: truthy\n\n  staples-post-create-201:\n    description: POST create operations must return 201 Created\n    message: \"POST operation creating resources must return 201 Created\"\n    severity: error\n  \
  \  given: \"$.paths[*].post\"\n    then:\n      field: \"responses.201\"\n      function: truthy\n\n  staples-unauthorized-response:\n    description: All operations must define a 401 Unauthorized response\n    message: \"Operation must define a 401 Unauthorized response\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.401\"\n      function: truthy\n\n  staples-not-found-response:\n    description: Operations with path parameters should define 404\n    message: \"Operation with path parameters should define a 404 Not Found response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.404\"\n      function: truthy\n\n  staples-rate-limit-response:\n    description: All operations must define a 429 Too Many Requests response\n    message: \"Operation must define a 429 Too Many Requests response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.429\"\n      function: truthy\n\
  \n  # Tags\n  staples-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  staples-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Path conventions\n  staples-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path must use kebab-case (lowercase, hyphens, path params)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9{}-]*$\"\n\n  staples-no-trailing-slash:\n    description: Paths must not have a trailing slash\n    message:\
  \ \"Path '{{property}}' must not end with a trailing slash\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # Parameter requirements\n  staples-path-parameters-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter must have required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: required\n      function: truthy\n\n  staples-query-parameters-described:\n    description: Query parameters must have descriptions\n    message: \"Query parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='query')]\"\n    then:\n      field: description\n      function: truthy\n\n  # Request body for POST/PUT\n  staples-post-request-body:\n    description: POST operations must define a request body\n    message: \"POST operation must include a requestBody definition\"\
  \n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Schema requirements\n  staples-schemas-have-descriptions:\n    description: Schema components should have descriptions where possible\n    message: \"Schema should include descriptive information\"\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: type\n      function: truthy\n\n  # Info\n  staples-info-contact:\n    description: API must have contact information\n    message: \"API info must include contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  staples-info-terms:\n    description: API must reference terms of service\n    message: \"API info should include termsOfService\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: termsOfService\n      function: truthy\n\n  staples-info-description:\n    description: API must have a description\n\
  \    message: \"API info must include a description\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  staples-servers-defined:\n    description: API must define at least one server\n    message: \"API must define servers with base URL\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/staples/refs/heads/main/rules/staples-rules.yml
tags:
- Office Supplies
- Retail
- Procurement
- B2B
- eProcurement
- Spectral
- Linting
- API Governance
---

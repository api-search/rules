---
api_specs:
- filename: starbucks-starbucks-api-openapi.yml
  format: yaml
  label: Starbucks API
  slug: starbucks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/starbucks/refs/heads/main/openapi/starbucks-starbucks-api-openapi.yml
categories:
- starbucks
description: Spectral linting rules defining API design standards and conventions for Starbucks.
layout: rules
name: Starbucks API Rules
provider_name: Starbucks
provider_slug: starbucks
rule_count: 18
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][*].operationId
  name: starbucks-operation-ids-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: starbucks-operation-summary-title-case
  severity: warn
- description: All API paths must be versioned with /v1/ prefix
  given: $.paths
  name: starbucks-api-versioned-paths
  severity: warn
- description: All operations must use Bearer token authentication
  given: $.paths[*][*]
  name: starbucks-bearer-auth-required
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: starbucks-get-operations-200
  severity: error
- description: POST create operations should return 201 Created
  given: $.paths[*].post
  name: starbucks-post-operations-201
  severity: warn
- description: All operations must define a 401 Unauthorized response
  given: $.paths[*][*]
  name: starbucks-unauthorized-response
  severity: error
- description: All operations must define a 429 Too Many Requests response
  given: $.paths[*][*]
  name: starbucks-rate-limit-response
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*].tags
  name: starbucks-operation-tags-required
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: starbucks-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: starbucks-path-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths
  name: starbucks-no-trailing-slash
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: starbucks-path-parameters-required
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*].name
  name: starbucks-parameter-descriptions
  severity: warn
- description: 200 responses should define a schema
  given: $.paths[*].get.responses.200.content.application/json
  name: starbucks-response-schema-defined
  severity: warn
- description: API must have contact information
  given: $.info
  name: starbucks-info-contact
  severity: warn
- description: API must have a description
  given: $.info
  name: starbucks-info-description
  severity: error
- description: API must define at least one server
  given: $
  name: starbucks-servers-defined
  severity: error
rules_file: rules/starbucks-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/starbucks/refs/heads/main/rules/starbucks-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 12
slug: starbucks-rules
source_filename: starbucks-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation naming and structure\n  starbucks-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., listMenuCategories, getStore)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  starbucks-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  starbucks-api-versioned-paths:\n    description: All API paths must be versioned with /v1/ prefix\n    message: \"Path '{{property}}' must start with /v1/ or /status for health checks\"\n    severity: warn\n    given: \"$.paths\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/(v[0-9]+/|status)\"\n\n  # Authentication requirements\n  starbucks-bearer-auth-required:\n    description: All operations must use Bearer token authentication\n    message: \"Operation must reference bearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  # Response codes\n  starbucks-get-operations-200:\n    description: GET operations must define a 200 response\n    message: \"GET operation must have a 200 response defined\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: \"responses.200\"\n      function: truthy\n\n  starbucks-post-operations-201:\n    description: POST create operations should return 201 Created\n    message: \"POST operation creating resources\
  \ should return 201\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: \"responses.201\"\n      function: truthy\n\n  starbucks-unauthorized-response:\n    description: All operations must define a 401 Unauthorized response\n    message: \"Operation must define a 401 Unauthorized response\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.401\"\n      function: truthy\n\n  starbucks-rate-limit-response:\n    description: All operations must define a 429 Too Many Requests response\n    message: \"Operation must define a 429 Too Many Requests response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.429\"\n      function: truthy\n\n  # Tags\n  starbucks-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag for categorization\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n   \
  \   function: length\n      functionOptions:\n        min: 1\n\n  starbucks-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  # Path conventions\n  starbucks-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment must use kebab-case (lowercase with hyphens)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9{}-]*$\"\n\n  starbucks-no-trailing-slash:\n    description: Paths must not have a trailing slash\n    message: \"Path '{{property}}' must not end with a trailing slash\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  # Parameter requirements\n \
  \ starbucks-path-parameters-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter '{{value}}' must have required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: required\n      function: truthy\n\n  starbucks-parameter-descriptions:\n    description: All parameters must have descriptions\n    message: \"Parameter '{{value}}' must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*].name\"\n    then:\n      function: truthy\n\n  # Schema requirements\n  starbucks-response-schema-defined:\n    description: 200 responses should define a schema\n    message: \"200 response should include a schema definition\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json\"\n    then:\n      field: schema\n      function: truthy\n\n  # Info\n  starbucks-info-contact:\n    description: API must have contact information\n    message:\
  \ \"API info must include contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  starbucks-info-description:\n    description: API must have a description\n    message: \"API info must include a description\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  starbucks-servers-defined:\n    description: API must define at least one server\n    message: \"API must define servers for base URL\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/starbucks/refs/heads/main/rules/starbucks-rules.yml
tags:
- Coffee
- Food Service
- Loyalty
- Ordering
- Retail
- Spectral
- Linting
- API Governance
---

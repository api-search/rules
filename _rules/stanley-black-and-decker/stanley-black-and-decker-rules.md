---
api_specs:
- filename: stanley-black-and-decker-tool-connect-api-openapi.yml
  format: yaml
  label: DEWALT Tool Connect API
  slug: dewalt-tool-connect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stanley-black-and-decker/refs/heads/main/openapi/stanley-black-and-decker-tool-connect-api-openapi.yml
categories:
- sbd
description: Spectral linting rules defining API design standards and conventions for Stanley Black & Decker.
layout: rules
name: Stanley Black & Decker API Rules
provider_name: Stanley Black & Decker
provider_slug: stanley-black-and-decker
rule_count: 20
rules:
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][*].operationId
  name: sbd-operation-ids-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: sbd-operation-summary-title-case
  severity: warn
- description: All API paths must be versioned with /v1/ prefix
  given: $.paths
  name: sbd-api-versioned-paths
  severity: error
- description: All operations must use Bearer token authentication
  given: $.paths[*][*]
  name: sbd-bearer-auth-required
  severity: error
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: sbd-get-operations-200
  severity: error
- description: POST operations that create resources must return 201
  given: $.paths[*].post
  name: sbd-post-create-201
  severity: warn
- description: All operations must define a 401 Unauthorized response
  given: $.paths[*][*]
  name: sbd-unauthorized-response
  severity: error
- description: Operations with path parameters should define a 404 response
  given: $.paths[*][*][?(@.parameters[*].in=='path')]
  name: sbd-not-found-response
  severity: warn
- description: All operations must define a 429 Too Many Requests response
  given: $.paths[*][*]
  name: sbd-rate-limit-response
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*].tags
  name: sbd-operation-tags-required
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: sbd-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: sbd-path-kebab-case
  severity: warn
- description: Collection resource paths should use plural nouns
  given: $.paths
  name: sbd-path-plural-nouns
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: sbd-path-parameters-required
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: sbd-parameter-descriptions
  severity: warn
- description: Schema objects should define properties
  given: $.components.schemas[*]
  name: sbd-schemas-have-properties
  severity: warn
- description: API must have contact information
  given: $.info
  name: sbd-info-contact
  severity: warn
- description: API must have a description
  given: $.info
  name: sbd-info-description
  severity: error
- description: API must define at least one server
  given: $
  name: sbd-servers-defined
  severity: error
- description: API should reference external documentation
  given: $
  name: sbd-external-docs
  severity: info
rules_file: rules/stanley-black-and-decker-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stanley-black-and-decker/refs/heads/main/rules/stanley-black-and-decker-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 1
  warn: 12
slug: stanley-black-and-decker-rules
source_filename: stanley-black-and-decker-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Operation naming and structure\n  sbd-operation-ids-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    message: \"Operation ID '{{value}}' must use camelCase (e.g., listTools, getBattery)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  sbd-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &+]*$\"\n\n  sbd-api-versioned-paths:\n    description: All API paths must be versioned with /v1/ prefix\n    message: \"Path '{{property}}' must start with /v1/\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^/v[0-9]+\"\n\n  # Authentication requirements\n  sbd-bearer-auth-required:\n    description: All operations must use Bearer token authentication\n    message: \"Operation must reference bearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  # Response codes\n  sbd-get-operations-200:\n    description: GET operations must define a 200 response\n    message: \"GET operation must have a 200 response defined\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: \"responses.200\"\n      function: truthy\n\n  sbd-post-create-201:\n    description: POST operations that create resources must return 201\n    message: \"POST operation creating resources should return 201 Created\"\n    severity: warn\n    given: \"$.paths[*].post\"\n\
  \    then:\n      field: \"responses.201\"\n      function: truthy\n\n  sbd-unauthorized-response:\n    description: All operations must define a 401 Unauthorized response\n    message: \"Operation must define a 401 Unauthorized response\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.401\"\n      function: truthy\n\n  sbd-not-found-response:\n    description: Operations with path parameters should define a 404 response\n    message: \"Operation with path parameters should define a 404 Not Found response\"\n    severity: warn\n    given: \"$.paths[*][*][?(@.parameters[*].in=='path')]\"\n    then:\n      field: \"responses.404\"\n      function: truthy\n\n  sbd-rate-limit-response:\n    description: All operations must define a 429 Too Many Requests response\n    message: \"Operation must define a 429 Too Many Requests response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"responses.429\"\n      function: truthy\n\
  \n  # Tags\n  sbd-operation-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag for categorization\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  sbd-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9+ ]*$\"\n\n  # Path conventions\n  sbd-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path must use kebab-case (lowercase, hyphens, path params)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[/a-z0-9{}-]*$\"\n\n  sbd-path-plural-nouns:\n    description: Collection resource paths should use plural\
  \ nouns\n    message: \"Collection paths should use plural nouns (tools, batteries, assets, jobsites)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+/[a-z].*\"\n\n  # Parameter requirements\n  sbd-path-parameters-required:\n    description: Path parameters must be marked as required\n    message: \"Path parameter must have required: true\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: required\n      function: truthy\n\n  sbd-parameter-descriptions:\n    description: All parameters must have descriptions\n    message: \"Parameter must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Schema requirements\n  sbd-schemas-have-properties:\n    description: Schema objects should define properties\n    message: \"Schema component should define properties\"\
  \n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: properties\n      function: truthy\n\n  # Info\n  sbd-info-contact:\n    description: API must have contact information\n    message: \"API info must include contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  sbd-info-description:\n    description: API must have a description\n    message: \"API info must include a description\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  sbd-servers-defined:\n    description: API must define at least one server\n    message: \"API must define servers with base URL\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  sbd-external-docs:\n    description: API should reference external documentation\n    message: \"API should include externalDocs pointing to official documentation\"\n \
  \   severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stanley-black-and-decker/refs/heads/main/rules/stanley-black-and-decker-rules.yml
tags:
- Tools
- Hardware
- Manufacturing
- IoT
- Connected Tools
- Spectral
- Linting
- API Governance
---

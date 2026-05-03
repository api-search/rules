---
api_specs:
- filename: target-target-api-openapi.yml
  format: yaml
  label: Target API
  slug: target-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/target/refs/heads/main/openapi/target-target-api-openapi.yml
categories:
- target
description: Spectral linting rules defining API design standards and conventions for target.
layout: rules
name: target API Rules
provider_name: target
provider_slug: target
rule_count: 12
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: target-operation-ids-camel-case
  severity: warn
- description: Tags must use Title Case
  given: $.tags[*].name
  name: target-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: target-path-kebab-case
  severity: warn
- description: All paths must include a version prefix (e.g., /v1/, /v3/)
  given: $.paths[*]~
  name: target-paths-versioned
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: target-operation-summary-exists
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: target-operation-description-exists
  severity: warn
- description: All operations must have a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: target-responses-200-exists
  severity: error
- description: Secured operations must document 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: target-responses-401-exists
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: target-parameters-description
  severity: warn
- description: bearerAuth security scheme must be defined
  given: $.components.securitySchemes
  name: target-bearer-auth-defined
  severity: error
- description: API must include contact information
  given: $.info
  name: target-info-contact
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: target-schema-properties-described
  severity: info
rules_file: rules/target-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/target/refs/heads/main/rules/target-spectral-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 8
slug: target-spectral-rules
source_filename: target-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  target-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"operationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  target-tags-title-case:\n    description: Tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  target-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path segment must use kebab-case: {{path}}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*$\"\n\n  target-paths-versioned:\n    description: All paths must include a version prefix (e.g., /v1/, /v3/)\n\
  \    message: \"Path '{{value}}' must include a version prefix like /v1/ or /v3/\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z]+/v[0-9]+\"\n\n  target-operation-summary-exists:\n    description: All operations must have a summary\n    message: \"Operation at '{{path}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  target-operation-description-exists:\n    description: All operations must have a description\n    message: \"Operation at '{{path}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  target-responses-200-exists:\n    description: All operations must have a 200 response\n    message: \"Operation at '{{path}}' must define a 200 response\"\n    severity: error\n \
  \   given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  target-responses-401-exists:\n    description: Secured operations must document 401 response\n    message: \"Operation at '{{path}}' should define a 401 response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  target-parameters-description:\n    description: All parameters must have descriptions\n    message: \"Parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  target-bearer-auth-defined:\n    description: bearerAuth security scheme must be defined\n    message: \"bearerAuth security scheme must be defined in components.securitySchemes\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n\
  \      function: truthy\n\n  target-info-contact:\n    description: API must include contact information\n    message: \"API info must include contact details\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  target-schema-properties-described:\n    description: Schema properties should have descriptions\n    message: \"Schema property at '{{path}}' should have a description\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/target/refs/heads/main/rules/target-spectral-rules.yml
tags:
- E-Commerce
- Retail
- Products
- Inventory
- Fortune 100
- Stores
- Orders
- Spectral
- Linting
- API Governance
---

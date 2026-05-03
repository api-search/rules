---
api_specs:
- filename: samsung-smartthings-openapi.yml
  format: yaml
  label: SmartThings API
  slug: smartthings
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/samsung/refs/heads/main/openapi/samsung-smartthings-openapi.yml
categories:
- samsung
description: Spectral linting rules defining API design standards and conventions for Samsung.
layout: rules
name: Samsung API Rules
provider_name: Samsung
provider_slug: samsung
rule_count: 13
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: samsung-operation-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase naming convention.
  given: $.paths[*][*].operationId
  name: samsung-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case (lowercase with hyphens).
  given: $.paths
  name: samsung-path-kebab-case
  severity: warn
- description: All 200 responses must include a schema definition.
  given: $.paths[*][get,post,put,patch].responses['200']
  name: samsung-response-200-schema
  severity: warn
- description: SmartThings API uses OAuth 2.0 Bearer token authentication.
  given: $.components.securitySchemes
  name: samsung-bearer-auth
  severity: error
- description: Device IDs, location IDs, and room IDs must use UUID format.
  given: $.components.schemas[*].properties[?(@.description =~ /[Uu]nique.*identifier/)]
  name: samsung-uuid-format
  severity: warn
- description: Collection endpoints should return pagination links.
  given: $.paths[*][get].responses['200'].content['application/json'].schema.properties
  name: samsung-pagination-links
  severity: info
- description: API paths must not end with a trailing slash.
  given: $.paths
  name: samsung-no-trailing-slash
  severity: error
- description: All operations must have at least one tag for categorization.
  given: $.paths[*][get,post,put,patch,delete]
  name: samsung-tags-required
  severity: warn
- description: All operations must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: samsung-description-required
  severity: warn
- description: DELETE operations must not include a request body.
  given: $.paths[*][delete]
  name: samsung-delete-no-request-body
  severity: error
- description: POST operations that create resources must have a request body.
  given: $.paths[*][post]
  name: samsung-post-request-body-required
  severity: warn
- description: All secured operations must declare a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: samsung-401-defined
  severity: warn
rules_file: rules/samsung-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/samsung/refs/heads/main/rules/samsung-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 9
slug: samsung-rules
source_filename: samsung-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: \"spectral:oas\"\n\nrules:\n  # Samsung SmartThings API conventions\n\n  samsung-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case (capitalize each word).\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  samsung-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  samsung-path-kebab-case:\n    description: Path segments must use kebab-case (lowercase with hyphens).\n    message: \"Path segment '{{value}}' must use kebab-case.\"\n    severity: warn\n    given: \"$.paths\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z0-9-]+|\\\\{[a-zA-Z][a-zA-Z0-9_]*\\\\}))*$\"\n\n  samsung-response-200-schema:\n    description: All 200 responses must include a schema definition.\n    message: \"Operation '{{path}}' 200 response should include a content schema.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses['200']\"\n    then:\n      field: content\n      function: truthy\n\n  samsung-bearer-auth:\n    description: SmartThings API uses OAuth 2.0 Bearer token authentication.\n    message: \"API must declare BearerAuth security scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  samsung-uuid-format:\n    description: Device IDs, location IDs, and room IDs must use UUID format.\n    message: \"ID parameter '{{path}}' should use format: uuid.\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[?(@.description\
  \ =~ /[Uu]nique.*identifier/)]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - uuid\n          - uri\n\n  samsung-pagination-links:\n    description: Collection endpoints should return pagination links.\n    message: \"Collection schema '{{path}}' should include _links for pagination.\"\n    severity: info\n    given: \"$.paths[*][get].responses['200'].content['application/json'].schema.properties\"\n    then:\n      field: _links\n      function: truthy\n\n  samsung-no-trailing-slash:\n    description: API paths must not end with a trailing slash.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  samsung-tags-required:\n    description: All operations must have at least one tag for categorization.\n    message: \"Operation '{{path}}' must declare at least one\
  \ tag.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  samsung-description-required:\n    description: All operations must have a description.\n    message: \"Operation '{{path}}' must include a description.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  samsung-delete-no-request-body:\n    description: DELETE operations must not include a request body.\n    message: \"DELETE operation '{{path}}' must not have a request body.\"\n    severity: error\n    given: \"$.paths[*][delete]\"\n    then:\n      field: requestBody\n      function: falsy\n\n  samsung-post-request-body-required:\n    description: POST operations that create resources must have a request body.\n    message: \"POST operation '{{path}}' must include a request\
  \ body.\"\n    severity: warn\n    given: \"$.paths[*][post]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  samsung-401-defined:\n    description: All secured operations must declare a 401 Unauthorized response.\n    message: \"Operation '{{path}}' must define a 401 response for authentication errors.\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/samsung/refs/heads/main/rules/samsung-rules.yml
tags:
- Consumer Electronics
- Developer Platform
- IoT
- Mobile
- Smart Home
- Smart TV
- Wearables
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: streamone-ion-openapi.yml
  format: yaml
  label: TD SYNNEX StreamOne Ion API
  slug: streamone-ion-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tech-data/refs/heads/main/openapi/streamone-ion-openapi.yml
categories:
- td
description: Spectral linting rules defining API design standards and conventions for Tech Data.
layout: rules
name: Tech Data API Rules
provider_name: Tech Data
provider_slug: tech-data
rule_count: 11
rules:
- description: All resource paths must include accountId path parameter
  given: $.paths[?(@property =~ /\/v3\/accounts\//)].get.parameters[?(@.name == 'accountId')]
  name: td-synnex-account-id-required
  severity: warn
- description: Operation IDs should be camelCase (StreamOne convention)
  given: $.paths.*.*.operationId
  name: td-synnex-operationid-kebab-case
  severity: warn
- description: All API paths must include a version prefix (v3)
  given: $.paths
  name: td-synnex-versioned-paths
  severity: error
- description: List operations should support page and pageSize query parameters
  given: $.paths[?(@property =~ /(?<!\{[a-zA-Z]+\})$/)].get
  name: td-synnex-pagination-list-operations
  severity: warn
- description: Successful GET operations must have a 200 response
  given: $.paths.*.get
  name: td-synnex-response-200-required
  severity: error
- description: POST create operations should return 201 Created
  given: $.paths.*.post
  name: td-synnex-response-201-for-post
  severity: warn
- description: Security scheme must be BearerAuth (OAuth2 token)
  given: $.components.securitySchemes
  name: td-synnex-bearer-security-defined
  severity: error
- description: Error responses must use the Error schema
  given: $.paths.*.*.responses[?(@property >= '400')].content.application/json.schema
  name: td-synnex-error-schema
  severity: warn
- description: All operations must have tags for grouping
  given: $.paths.*.*
  name: td-synnex-tags-required
  severity: error
- description: All operations must have descriptions
  given: $.paths.*.*
  name: td-synnex-description-required
  severity: warn
- description: Schema objects should define properties
  given: $.components.schemas[?(@.type == 'object')]
  name: td-synnex-schemas-have-properties
  severity: warn
rules_file: rules/streamone-ion-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tech-data/refs/heads/main/rules/streamone-ion-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 7
slug: streamone-ion-rules
source_filename: streamone-ion-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Naming conventions\n  td-synnex-account-id-required:\n    description: All resource paths must include accountId path parameter\n    message: \"{{description}}: {{path}}\"\n    severity: warn\n    given: \"$.paths[?(@property =~ /\\\\/v3\\\\/accounts\\\\//)].get.parameters[?(@.name == 'accountId')]\"\n    then:\n      function: truthy\n\n  td-synnex-operationid-kebab-case:\n    description: Operation IDs should be camelCase (StreamOne convention)\n    message: \"Operation ID '{{value}}' should use camelCase: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  td-synnex-versioned-paths:\n    description: All API paths must include a version prefix (v3)\n    message: \"Path '{{path}}' must begin with /v3/ or /oauth/: {{path}}\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^\\\\/(v[0-9]+|oauth)\\\\/\"\n\n  td-synnex-pagination-list-operations:\n    description: List operations should support page and pageSize query parameters\n    message: \"{{description}}: {{path}}\"\n    severity: warn\n    given: \"$.paths[?(@property =~ /(?<!\\\\{[a-zA-Z]+\\\\})$/)].get\"\n    then:\n      - field: operationId\n        function: pattern\n        functionOptions:\n          match: \"^(list|get[A-Z])\"\n\n  td-synnex-response-200-required:\n    description: Successful GET operations must have a 200 response\n    message: \"GET operation missing 200 response: {{path}}\"\n    severity: error\n    given: \"$.paths.*.get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  td-synnex-response-201-for-post:\n    description: POST create operations should return 201 Created\n    message: \"POST operation should return 201 Created: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.post\"\n    then:\n      field: responses.201\n      function:\
  \ defined\n\n  td-synnex-bearer-security-defined:\n    description: Security scheme must be BearerAuth (OAuth2 token)\n    message: \"Missing BearerAuth security scheme: {{path}}\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  td-synnex-error-schema:\n    description: Error responses must use the Error schema\n    message: \"Error response should reference Error schema: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*.responses[?(@property >= '400')].content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            $ref:\n              type: string\n\n  td-synnex-tags-required:\n    description: All operations must have tags for grouping\n    message: \"Operation missing tags: {{path}}\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n\
  \  td-synnex-description-required:\n    description: All operations must have descriptions\n    message: \"Operation missing description: {{path}}\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: description\n      function: truthy\n\n  td-synnex-schemas-have-properties:\n    description: Schema objects should define properties\n    message: \"Schema '{{path}}' should define properties\"\n    severity: warn\n    given: \"$.components.schemas[?(@.type == 'object')]\"\n    then:\n      field: properties\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tech-data/refs/heads/main/rules/streamone-ion-rules.yml
tags:
- Cloud
- Distribution
- Information Technology
- Partner
- Spectral
- Linting
- API Governance
---

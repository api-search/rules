---
api_specs:
- filename: ternary-openapi.yml
  format: yaml
  label: Ternary API
  slug: ternary-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ternary/refs/heads/main/openapi/ternary-openapi.yml
categories:
- ternary
description: Spectral linting rules defining API design standards and conventions for Ternary.
layout: rules
name: Ternary API Rules
provider_name: Ternary
provider_slug: ternary
rule_count: 23
rules:
- description: All Ternary API operations must require authentication
  given: $.paths[*][get,post,put,patch,delete]
  name: ternary-security-defined
  severity: false
- description: Global security must be defined for Ternary API
  given: $
  name: ternary-global-security
  severity: error
- description: All Ternary API paths must start with /v1/
  given: $.paths[*]~
  name: ternary-path-versioned
  severity: error
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: ternary-path-kebab-case
  severity: warn
- description: Collection endpoints should use plural nouns
  given: $.paths[*]~
  name: ternary-collection-plural-nouns
  severity: false
- description: List operations must use GET method
  given: $.paths[*][get].operationId
  name: ternary-list-uses-get
  severity: warn
- description: Create operations should use POST
  given: $.paths[*][post].operationId
  name: ternary-create-uses-post
  severity: warn
- description: Update operations should use PUT
  given: $.paths[*][put].operationId
  name: ternary-update-uses-put
  severity: warn
- description: Delete operations must use DELETE
  given: $.paths[*][delete].operationId
  name: ternary-delete-uses-delete
  severity: error
- description: List and GET operations must return 200
  given: $.paths[*][get].responses
  name: ternary-list-response-200
  severity: error
- description: Create operations should return 201
  given: $.paths[*][post].responses
  name: ternary-create-response-201
  severity: warn
- description: Delete operations should return 204
  given: $.paths[*][delete].responses
  name: ternary-delete-response-204
  severity: warn
- description: All operations must define a 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: ternary-401-defined
  severity: error
- description: Operations with path parameters should define 404
  given: $.paths[*~'/{[^}]+}'][get,put,delete].responses
  name: ternary-404-for-resource-ops
  severity: warn
- description: List endpoints should support pagination parameters
  given: $.paths[*][get][?(@.operationId && @.operationId.startsWith('list'))]
  name: ternary-pagination-params
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: ternary-operation-summary
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: ternary-summary-title-case
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: ternary-operation-description
  severity: warn
- description: All operations must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: ternary-tags-defined
  severity: error
- description: Schema objects should have descriptions
  given: $.components.schemas[*]
  name: ternary-schema-description
  severity: warn
- description: Prefer reusable schemas in components over inline definitions
  given: $.paths[*][*].responses[*].content[*].schema
  name: ternary-no-inline-schemas
  severity: warn
- description: Cost and amount fields should be numeric type
  given: $.components.schemas[*].properties[?(@key =~ /cost|amount|spend|budget/i)]
  name: ternary-cost-fields-numeric
  severity: warn
- description: Date fields should use ISO 8601 format
  given: $.components.schemas[*].properties[?(@key =~ /date|_at$/i)]
  name: ternary-date-fields-format
  severity: warn
rules_file: rules/ternary-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ternary/refs/heads/main/rules/ternary-rules.yml
severity_counts:
  error: 7
  warn: 14
  info: 0
  hint: 0
  false: 2
slug: ternary-rules
source_filename: ternary-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # API Key Security\n  ternary-security-defined:\n    description: All Ternary API operations must require authentication\n    message: \"Operation '{{path}}' must require API key authentication\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n    severity: off\n\n  ternary-global-security:\n    description: Global security must be defined for Ternary API\n    message: \"Ternary API must define global security with API key\"\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n    severity: error\n\n  # Versioning\n  ternary-path-versioned:\n    description: All Ternary API paths must start with /v1/\n    message: \"Path '{{property}}' must start with /v1/\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n    severity: error\n\n  # Path Conventions\n  ternary-path-kebab-case:\n    description:\
  \ Path segments must use kebab-case\n    message: \"Path segment in '{{property}}' must use kebab-case\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/v1/[a-z0-9-/{}_]+)$\"\n    severity: warn\n\n  ternary-collection-plural-nouns:\n    description: Collection endpoints should use plural nouns\n    message: \"Collection path should use plural nouns\"\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/v1/[a-z]+-[a-z]+$\"\n    severity: off\n\n  # HTTP Methods\n  ternary-list-uses-get:\n    description: List operations must use GET method\n    message: \"List operations should use GET, not POST\"\n    given: \"$.paths[*][get].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(list|get)[A-Z]\"\n    severity: warn\n\n  ternary-create-uses-post:\n    description: Create operations should use POST\n    message: \"Create operations\
  \ should use POST\"\n    given: \"$.paths[*][post].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(create|trigger|run|acknowledge)[A-Z]\"\n    severity: warn\n\n  ternary-update-uses-put:\n    description: Update operations should use PUT\n    message: \"Full update operations should use PUT\"\n    given: \"$.paths[*][put].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^update[A-Z]\"\n    severity: warn\n\n  ternary-delete-uses-delete:\n    description: Delete operations must use DELETE\n    message: \"Delete operations must use DELETE method\"\n    given: \"$.paths[*][delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^delete[A-Z]\"\n    severity: error\n\n  # Response Codes\n  ternary-list-response-200:\n    description: List and GET operations must return 200\n    message: \"GET operation must define a 200 response\"\n    given: \"$.paths[*][get].responses\"\
  \n    then:\n      field: \"200\"\n      function: truthy\n    severity: error\n\n  ternary-create-response-201:\n    description: Create operations should return 201\n    message: \"POST create operations should return 201 Created\"\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"201\"\n      function: truthy\n    severity: warn\n\n  ternary-delete-response-204:\n    description: Delete operations should return 204\n    message: \"DELETE operations should return 204 No Content\"\n    given: \"$.paths[*][delete].responses\"\n    then:\n      field: \"204\"\n      function: truthy\n    severity: warn\n\n  ternary-401-defined:\n    description: All operations must define a 401 Unauthorized response\n    message: \"Operation must define a 401 Unauthorized response\"\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n    severity: error\n\n  ternary-404-for-resource-ops:\n    description: Operations\
  \ with path parameters should define 404\n    message: \"Resource operations with path parameters should define 404 Not Found\"\n    given: \"$.paths[*~'/{[^}]+}'][get,put,delete].responses\"\n    then:\n      field: \"404\"\n      function: truthy\n    severity: warn\n\n  # Pagination\n  ternary-pagination-params:\n    description: List endpoints should support pagination parameters\n    message: \"List endpoint should include page_token and page_size query parameters\"\n    given: \"$.paths[*][get][?(@.operationId && @.operationId.startsWith('list'))]\"\n    then:\n      field: parameters\n      function: truthy\n    severity: warn\n\n  # Documentation\n  ternary-operation-summary:\n    description: All operations must have a summary\n    message: \"Operation '{{path}}' is missing a summary\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n    severity: error\n\n  ternary-summary-title-case:\n    description: Operation summaries\
  \ must use Title Case\n    message: \"Summary '{{value}}' must start with a capital letter (Title Case)\"\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n    severity: warn\n\n  ternary-operation-description:\n    description: All operations should have a description\n    message: \"Operation is missing a description\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  ternary-tags-defined:\n    description: All operations must have tags\n    message: \"Operation is missing tags\"\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n    severity: error\n\n  # Schema Quality\n  ternary-schema-description:\n    description: Schema objects should have descriptions\n    message: \"Schema component '{{path}}' is missing a description\"\n    given:\
  \ \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n    severity: warn\n\n  ternary-no-inline-schemas:\n    description: Prefer reusable schemas in components over inline definitions\n    message: \"Use $ref to reusable schemas instead of inline definitions\"\n    given: \"$.paths[*][*].responses[*].content[*].schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n    severity: warn\n\n  # FinOps Domain Conventions\n  ternary-cost-fields-numeric:\n    description: Cost and amount fields should be numeric type\n    message: \"Cost/amount field should be type: number\"\n    given: \"$.components.schemas[*].properties[?(@key =~ /cost|amount|spend|budget/i)]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - number\n          - integer\n    severity: warn\n\n  ternary-date-fields-format:\n    description: Date fields should use ISO 8601 format\n    message: \"Date field should\
  \ have format: date or format: date-time\"\n    given: \"$.components.schemas[*].properties[?(@key =~ /date|_at$/i)]\"\n    then:\n      field: format\n      function: truthy\n    severity: warn\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ternary/refs/heads/main/rules/ternary-rules.yml
tags:
- Cloud Cost Management
- Cost Optimization
- FinOps
- Google Cloud
- Kubernetes
- Multi-Cloud
- Spectral
- Linting
- API Governance
---

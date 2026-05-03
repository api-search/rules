---
api_specs:
- filename: turbonomic-rest-api-openapi.yml
  format: yaml
  label: Turbonomic REST API
  slug: turbonomic-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/turbonomic/refs/heads/main/openapi/turbonomic-rest-api-openapi.yml
categories:
- turbonomic
description: Spectral linting rules defining API design standards and conventions for IBM Turbonomic.
layout: rules
name: IBM Turbonomic API Rules
provider_name: IBM Turbonomic
provider_slug: turbonomic
rule_count: 12
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: turbonomic-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: turbonomic-operation-id-required
  severity: error
- description: Turbonomic uses 'uuid' as the identifier parameter name for all entity paths. Path parameters referencing entity identifiers should be named 'uuid'.
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: turbonomic-uuid-path-parameter
  severity: warn
- description: All Turbonomic endpoints (except /login and /logout) must require bearer token authentication.
  given: $.paths[?(!@property.match('/(login|logout)'))][get,post,put,delete,patch]
  name: turbonomic-bearer-auth-required
  severity: warn
- description: All operations should define a 200 success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: turbonomic-200-response-defined
  severity: warn
- description: Success responses should define a response schema
  given: $.paths[*][get,post,put].responses.200
  name: turbonomic-response-schema-defined
  severity: info
- description: All operations must be tagged for Swagger UI grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: turbonomic-tag-required
  severity: error
- description: All operations should have a description for documentation completeness
  given: $.paths[*][get,post,put,delete,patch]
  name: turbonomic-description-required
  severity: warn
- description: All parameters should have a description
  given: $.paths[*][*].parameters[*]
  name: turbonomic-parameter-description
  severity: warn
- description: Operations should define specific error responses (401, 404) not just generic errors
  given: $.paths[*][get,post,put,delete,patch].responses
  name: turbonomic-no-generic-error
  severity: info
- description: API must define reusable schemas in components/schemas
  given: $.components
  name: turbonomic-components-schemas-defined
  severity: warn
- description: Turbonomic action and entity endpoints use UUID as path parameter. Ensure UUID parameters use the correct format.
  given: $.paths[*][*].parameters[?(@.name == 'uuid')]
  name: turbonomic-action-uuid-in-path
  severity: info
rules_file: rules/turbonomic-rest-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/turbonomic/refs/heads/main/rules/turbonomic-rest-api-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 3
  warn: 7
slug: turbonomic-rest-api-rules
source_filename: turbonomic-rest-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Turbonomic API Convention: All paths use /api/v3 prefix (enforced at server level)\n  turbonomic-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  turbonomic-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId for Turbonomic SDK generation\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  turbonomic-uuid-path-parameter:\n    description: >-\n      Turbonomic uses 'uuid' as the identifier parameter name for all entity paths.\n      Path parameters referencing entity identifiers should be named 'uuid'.\n    message:\
  \ \"Path parameter for entity identifier should be named 'uuid'\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^(uuid|ticketId|taskId|deviceId|ruleId|userId|groupId|policyId|templateId|marketId)$\"\n\n  turbonomic-bearer-auth-required:\n    description: >-\n      All Turbonomic endpoints (except /login and /logout) must require bearer token authentication.\n    message: \"Non-authentication endpoints must declare bearerAuth security requirement\"\n    severity: warn\n    given: \"$.paths[?(!@property.match('/(login|logout)'))][get,post,put,delete,patch]\"\n    then:\n      field: security\n      function: truthy\n\n  turbonomic-200-response-defined:\n    description: All operations should define a 200 success response\n    message: \"Operation should define a 200 success response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\
  \n    then:\n      field: \"200\"\n      function: truthy\n\n  turbonomic-response-schema-defined:\n    description: Success responses should define a response schema\n    message: \"200 response should include a content schema\"\n    severity: info\n    given: \"$.paths[*][get,post,put].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  turbonomic-tag-required:\n    description: All operations must be tagged for Swagger UI grouping\n    message: \"Operation must have at least one tag\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  turbonomic-description-required:\n    description: All operations should have a description for documentation completeness\n    message: \"Operation should include a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  turbonomic-parameter-description:\n\
  \    description: All parameters should have a description\n    message: \"Parameter '{{value}}' should have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  turbonomic-no-generic-error:\n    description: Operations should define specific error responses (401, 404) not just generic errors\n    message: \"Operation should define specific error responses\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"401\"]\n            - required: [\"404\"]\n            - required: [\"400\"]\n\n  turbonomic-components-schemas-defined:\n    description: API must define reusable schemas in components/schemas\n    message: \"API should define schemas in components/schemas\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n\
  \      function: truthy\n\n  turbonomic-action-uuid-in-path:\n    description: >-\n      Turbonomic action and entity endpoints use UUID as path parameter.\n      Ensure UUID parameters use the correct format.\n    message: \"UUID path parameters should document string type\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'uuid')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/turbonomic/refs/heads/main/rules/turbonomic-rest-api-rules.yml
tags:
- Application Resource Management
- Cloud Cost Optimization
- Cloud Management
- Hybrid Cloud
- IBM
- Kubernetes
- Multi-Cloud
- Workload Optimization
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: red-hat-3scale-service-management-openapi.yml
  format: yaml
  label: Red Hat 3scale Service Management API
  slug: service-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/openapi/red-hat-3scale-service-management-openapi.yml
- filename: red-hat-3scale-account-management-openapi.yml
  format: yaml
  label: Red Hat 3scale Account Management API
  slug: account-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/openapi/red-hat-3scale-account-management-openapi.yml
- filename: red-hat-3scale-analytics-openapi.yml
  format: yaml
  label: Red Hat 3scale Analytics API
  slug: analytics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/openapi/red-hat-3scale-analytics-openapi.yml
- filename: red-hat-3scale-billing-openapi.yml
  format: yaml
  label: Red Hat 3scale Billing API
  slug: billing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/openapi/red-hat-3scale-billing-openapi.yml
- filename: red-hat-3scale-apicast-management-openapi.yml
  format: yaml
  label: Red Hat 3scale APIcast Management API
  slug: apicast-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/openapi/red-hat-3scale-apicast-management-openapi.yml
categories:
- 3scale
description: Spectral linting rules defining API design standards and conventions for Red Hat 3scale.
layout: rules
name: Red Hat 3scale API Rules
provider_name: Red Hat 3scale
provider_slug: red-hat-3scale
rule_count: 12
rules:
- description: 3scale Account Management API endpoints require an access_token query parameter for authentication. All endpoints on the admin domain must include this parameter.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: 3scale-access-token-required
  severity: error
- description: 3scale management endpoints should return application/json content type for consistency with REST API conventions.
  given: $.paths[*][get,post,put,patch].responses[200,201].content
  name: 3scale-json-responses
  severity: warn
- description: All operations must have an operationId to support SDK code generation and documentation linking.
  given: $.paths[*][get,post,put,delete,patch]
  name: 3scale-operation-id-required
  severity: error
- description: 3scale API operation IDs must use camelCase naming convention (e.g., listAccounts, createApplication).
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: 3scale-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case formatting to match the 3scale documentation style.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: 3scale-summary-title-case
  severity: warn
- description: All operation tags must reference tags defined in the global tags array for consistency.
  given: $.paths[*][get,post,put,delete,patch].tags[*]
  name: 3scale-tags-defined
  severity: warn
- description: All operations must include a description explaining what the endpoint does, required parameters, and expected behavior.
  given: $.paths[*][get,post,put,delete,patch]
  name: 3scale-operation-description-required
  severity: warn
- description: API info must include a version number following semantic versioning conventions.
  given: $.info
  name: 3scale-api-versioned
  severity: error
- description: All parameters must include a description to help API consumers understand what values to provide.
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: 3scale-parameter-descriptions
  severity: warn
- description: Schema properties in response bodies should include descriptions to document the meaning of each field.
  given: $.components.schemas[*].properties[*]
  name: 3scale-schema-property-descriptions
  severity: info
- description: Endpoints with path parameters should include a 404 response to handle the case where the specified resource does not exist.
  given: $.paths[*~@contains('{')][get,put,delete]
  name: 3scale-not-found-response
  severity: warn
- description: List endpoints should support pagination via page and per_page parameters to control result set size.
  given: $.paths[?@property.endsWith('.json')][get]
  name: 3scale-pagination-parameters
  severity: info
rules_file: rules/red-hat-3scale-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/rules/red-hat-3scale-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 7
slug: red-hat-3scale-rules
source_filename: red-hat-3scale-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # 3scale uses admin access tokens - require access_token in query parameters\n  3scale-access-token-required:\n    description: >-\n      3scale Account Management API endpoints require an access_token query\n      parameter for authentication. All endpoints on the admin domain must\n      include this parameter.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^access_token$\"\n\n  # 3scale API responses should return JSON\n  3scale-json-responses:\n    description: >-\n      3scale management endpoints should return application/json content type\n      for consistency with REST API conventions.\n    severity: warn\n    given: $.paths[*][get,post,put,patch].responses[200,201].content\n    then:\n      field: application/json\n      function: truthy\n\n  # Operation IDs are required for SDK generation\n  3scale-operation-id-required:\n\
  \    description: >-\n      All operations must have an operationId to support SDK code generation\n      and documentation linking.\n    severity: error\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: operationId\n      function: truthy\n\n  # Operation IDs must use camelCase\n  3scale-operation-id-camel-case:\n    description: >-\n      3scale API operation IDs must use camelCase naming convention\n      (e.g., listAccounts, createApplication).\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries must use Title Case\n  3scale-summary-title-case:\n    description: >-\n      Operation summaries must use Title Case formatting to match the\n      3scale documentation style.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n      \
  \  match: \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # Tags must be defined in the global tags section\n  3scale-tags-defined:\n    description: >-\n      All operation tags must reference tags defined in the global tags array\n      for consistency.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].tags[*]\n    then:\n      function: truthy\n\n  # All paths must include descriptions\n  3scale-operation-description-required:\n    description: >-\n      All operations must include a description explaining what the endpoint\n      does, required parameters, and expected behavior.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch]\n    then:\n      field: description\n      function: truthy\n\n  # Version in path or info should be present\n  3scale-api-versioned:\n    description: >-\n      API info must include a version number following semantic versioning\n      conventions.\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function:\
  \ truthy\n\n  # Parameters must have descriptions\n  3scale-parameter-descriptions:\n    description: >-\n      All parameters must include a description to help API consumers understand\n      what values to provide.\n    severity: warn\n    given: $.paths[*][get,post,put,delete,patch].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  # Schema properties must have descriptions\n  3scale-schema-property-descriptions:\n    description: >-\n      Schema properties in response bodies should include descriptions to\n      document the meaning of each field.\n    severity: info\n    given: $.components.schemas[*].properties[*]\n    then:\n      field: description\n      function: defined\n\n  # 404 responses for parameterized paths\n  3scale-not-found-response:\n    description: >-\n      Endpoints with path parameters should include a 404 response to handle\n      the case where the specified resource does not exist.\n    severity: warn\n    given: $.paths[*~@contains('{')][get,put,delete]\n\
  \    then:\n      field: responses.404\n      function: truthy\n\n  # Use structured pagination\n  3scale-pagination-parameters:\n    description: >-\n      List endpoints should support pagination via page and per_page parameters\n      to control result set size.\n    severity: info\n    given: $.paths[?@property.endsWith('.json')][get]\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/red-hat-3scale/refs/heads/main/rules/red-hat-3scale-rules.yml
tags:
- API Gateway
- API Management
- Developer Portal
- Enterprise
- Red Hat
- Spectral
- Linting
- API Governance
---

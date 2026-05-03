---
api_specs:
- filename: webmethods-api-gateway-openapi.yml
  format: yaml
  label: webMethods API Gateway Service Management API
  slug: webmethods-api-gateway
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/software-ag/refs/heads/main/openapi/webmethods-api-gateway-openapi.yml
categories:
- webmethods
description: Spectral linting rules defining API design standards and conventions for Software AG.
layout: rules
name: Software AG API Rules
provider_name: Software AG
provider_slug: software-ag
rule_count: 12
rules:
- description: API names must use camelCase format consistent with webMethods conventions
  given: $.paths[*][*].operationId
  name: webmethods-api-naming-convention
  severity: warn
- description: All operations must have an operationId for code generation
  given: $.paths[*][*]
  name: webmethods-require-operation-id
  severity: error
- description: All operations must have a summary for developer portal display
  given: $.paths[*][*]
  name: webmethods-require-summary
  severity: error
- description: All operations must be tagged for Developer Portal categorization
  given: $.paths[*][*]
  name: webmethods-require-tags
  severity: warn
- description: Resource-specific paths must use {apiId} as the primary identifier
  given: $.paths
  name: webmethods-api-id-path-parameter
  severity: info
- description: GET operations must define a 200 response
  given: $.paths[*].get
  name: webmethods-require-response-200
  severity: error
- description: Successful responses should define a content schema
  given: $.paths[*][*].responses.200
  name: webmethods-require-response-content
  severity: warn
- description: All operations should reference security schemes (Basic Auth required)
  given: $.paths[*][*]
  name: webmethods-security-required
  severity: warn
- description: API Gateway REST paths use the /rest/apigateway base path
  given: $.servers[*].url
  name: webmethods-rest-v1-prefix
  severity: info
- description: All parameters should include descriptions for Developer Portal display
  given: $.paths[*][*].parameters[*]
  name: webmethods-parameter-descriptions
  severity: warn
- description: Request bodies must specify a content type
  given: $.paths[*][*].requestBody
  name: webmethods-request-body-content-type
  severity: error
- description: Schema objects should define their properties
  given: $.components.schemas[*]
  name: webmethods-schema-properties
  severity: warn
rules_file: rules/webmethods-api-gateway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/software-ag/refs/heads/main/rules/webmethods-api-gateway-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 6
slug: webmethods-api-gateway-rules
source_filename: webmethods-api-gateway-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  webmethods-api-naming-convention:\n    description: API names must use camelCase format consistent with webMethods conventions\n    message: \"API names should use camelCase (e.g., getAPIs, createAPI)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  webmethods-require-operation-id:\n    description: All operations must have an operationId for code generation\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  webmethods-require-summary:\n    description: All operations must have a summary for developer portal display\n    message: \"Operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  webmethods-require-tags:\n    description: All operations\
  \ must be tagged for Developer Portal categorization\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  webmethods-api-id-path-parameter:\n    description: Resource-specific paths must use {apiId} as the primary identifier\n    message: \"API resource paths should use {apiId} pattern for consistency\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  webmethods-require-response-200:\n    description: GET operations must define a 200 response\n    message: \"GET operations must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  webmethods-require-response-content:\n    description: Successful responses should define a content schema\n    message: \"200 responses should define content\
  \ schema\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  webmethods-security-required:\n    description: All operations should reference security schemes (Basic Auth required)\n    message: \"Operations should define security requirements\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  webmethods-rest-v1-prefix:\n    description: API Gateway REST paths use the /rest/apigateway base path\n    message: \"Paths should follow the /rest/apigateway convention\"\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*/rest/apigateway.*\"\n\n  webmethods-parameter-descriptions:\n    description: All parameters should include descriptions for Developer Portal display\n    message: \"Parameters must include a description\"\n    severity:\
  \ warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  webmethods-request-body-content-type:\n    description: Request bodies must specify a content type\n    message: \"Request bodies must define content type\"\n    severity: error\n    given: \"$.paths[*][*].requestBody\"\n    then:\n      field: content\n      function: truthy\n\n  webmethods-schema-properties:\n    description: Schema objects should define their properties\n    message: \"Schema objects should define properties\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: properties\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/software-ag/refs/heads/main/rules/webmethods-api-gateway-rules.yml
tags:
- API Management
- Enterprise Integration
- iPaaS
- webMethods
- Integration Platform
- API Gateway
- Spectral
- Linting
- API Governance
---

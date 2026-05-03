---
api_specs:
- filename: torii-torii-openapi.yml
  format: yaml
  label: Torii SaaS Management API
  slug: torii
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/torii/refs/heads/main/openapi/torii-torii-openapi.yml
categories:
- torii
description: Spectral linting rules defining API design standards and conventions for Torii.
layout: rules
name: Torii API Rules
provider_name: Torii
provider_slug: torii
rule_count: 10
rules:
- description: Operation summaries should start with "Torii" prefix
  given: $.paths[*][get,post,put,patch,delete].summary
  name: torii-operation-summary-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: torii-operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: torii-operation-summary-required
  severity: error
- description: BearerAuth security scheme must be defined
  given: $.components.securitySchemes
  name: torii-bearer-auth-defined
  severity: error
- description: API version header should be consistently defined via $ref
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'X-API-Version')]
  name: torii-api-version-header
  severity: hint
- description: Collection GET endpoints should support size and cursor pagination
  given: $.paths[?(!@property.match(/\{/))]..get.parameters[?(@.name=='size')]
  name: torii-pagination-parameters
  severity: warn
- description: Protected endpoints should document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: torii-unauthorized-response
  severity: warn
- description: Endpoints should document 429 Rate Limited response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: torii-rate-limited-response
  severity: warn
- description: Request bodies for write operations must be marked required
  given: $.paths[*][post,put,patch].requestBody
  name: torii-request-body-required
  severity: error
- description: Path parameters should have descriptions
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: torii-path-param-description
  severity: warn
rules_file: rules/torii-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/torii/refs/heads/main/rules/torii-rules.yml
severity_counts:
  error: 4
  hint: 1
  info: 0
  warn: 5
slug: torii-rules
source_filename: torii-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n  # Torii API operation summaries start with \"Torii\" prefix\n  torii-operation-summary-prefix:\n    description: Operation summaries should start with \"Torii\" prefix\n    message: \"Operation summary '{{value}}' should start with 'Torii'\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Torii [A-Z]\"\n\n  # All operations must have operationId\n  torii-operation-id-required:\n    description: All operations must have an operationId\n    message: \"Operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # All operations must have a summary\n  torii-operation-summary-required:\n    description: All operations must have a summary\n    message: \"Operation is missing a summary\"\n    severity: error\n    given:\
  \ \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Bearer authentication must be defined\n  torii-bearer-auth-defined:\n    description: BearerAuth security scheme must be defined\n    message: \"bearerAuth security scheme should be defined\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  # X-API-Version header parameter should be documented consistently\n  torii-api-version-header:\n    description: API version header should be consistently defined via $ref\n    message: \"Operations should reference the apiVersion parameter\"\n    severity: hint\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'X-API-Version')]\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  # GET list endpoints should support pagination parameters\n  torii-pagination-parameters:\n    description: Collection GET endpoints should support\
  \ size and cursor pagination\n    message: \"List endpoints should document pagination parameters (size, cursor)\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/\\\\{/))]..get.parameters[?(@.name=='size')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n          - integer\n\n  # Responses should document 401 Unauthorized\n  torii-unauthorized-response:\n    description: Protected endpoints should document 401 Unauthorized response\n    message: \"Endpoint should document 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Responses should document 429 Rate Limited\n  torii-rate-limited-response:\n    description: Endpoints should document 429 Rate Limited response\n    message: \"Endpoint should document 429 Rate Limited response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\
  \n    then:\n      field: \"429\"\n      function: truthy\n\n  # PUT/POST/PATCH request bodies should be marked required\n  torii-request-body-required:\n    description: Request bodies for write operations must be marked required\n    message: \"Request body should be marked required=true\"\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: required\n      function: truthy\n\n  # Path parameters should have descriptions\n  torii-path-param-description:\n    description: Path parameters should have descriptions\n    message: \"Path parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/torii/refs/heads/main/rules/torii-rules.yml
tags:
- Apps
- Compliance
- Cost Optimization
- Governance
- IT Management
- SaaS Management
- Spectral
- Linting
- API Governance
---

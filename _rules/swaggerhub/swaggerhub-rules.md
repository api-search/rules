---
api_specs:
- filename: swaggerhub-registry-api-openapi.yml
  format: yaml
  label: SwaggerHub Registry API
  slug: swaggerhub-registry-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swaggerhub/refs/heads/main/openapi/swaggerhub-registry-api-openapi.yml
- filename: swaggerhub-user-management-openapi.yml
  format: yaml
  label: SwaggerHub User Management API
  slug: swaggerhub-user-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swaggerhub/refs/heads/main/openapi/swaggerhub-user-management-openapi.yml
categories:
- swaggerhub
description: Spectral linting rules defining API design standards and conventions for SwaggerHub.
layout: rules
name: SwaggerHub API Rules
provider_name: SwaggerHub
provider_slug: swaggerhub
rule_count: 9
rules:
- description: All SwaggerHub API operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: swaggerhub-operations-have-tags
  severity: warn
- description: All SwaggerHub API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: swaggerhub-operations-have-summaries
  severity: error
- description: SwaggerHub operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: swaggerhub-summaries-title-case
  severity: warn
- description: All SwaggerHub API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: swaggerhub-operations-have-operation-ids
  severity: error
- description: All SwaggerHub API operations should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: swaggerhub-operations-have-descriptions
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: swaggerhub-path-params-required
  severity: error
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: swaggerhub-schemas-have-descriptions
  severity: warn
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: swaggerhub-responses-have-descriptions
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: swaggerhub-security-scheme-defined
  severity: error
rules_file: rules/swaggerhub-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/swaggerhub/refs/heads/main/rules/swaggerhub-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: swaggerhub-rules
source_filename: swaggerhub-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  swaggerhub-operations-have-tags:\n    description: All SwaggerHub API operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  swaggerhub-operations-have-summaries:\n    description: All SwaggerHub API operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  swaggerhub-summaries-title-case:\n    description: SwaggerHub operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  swaggerhub-operations-have-operation-ids:\n    description: All SwaggerHub API operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: operationId\n      function: truthy\n\n  swaggerhub-operations-have-descriptions:\n    description: All SwaggerHub API operations should have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  swaggerhub-path-params-required:\n    description: Path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  swaggerhub-schemas-have-descriptions:\n    description: All component schemas must have a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  swaggerhub-responses-have-descriptions:\n    description: All response objects must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  swaggerhub-security-scheme-defined:\n    description: API must define at least one security scheme\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/swaggerhub/refs/heads/main/rules/swaggerhub-rules.yml
tags:
- API Design
- API Management
- API Registry
- Documentation
- OpenAPI
- SmartBear
- Spectral
- Linting
- API Governance
---

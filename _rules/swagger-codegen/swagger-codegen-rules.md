---
api_specs:
- filename: swagger-generator-openapi.yml
  format: yaml
  label: Swagger Generator API
  slug: swagger-generator-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swagger-codegen/refs/heads/main/openapi/swagger-generator-openapi.yml
categories:
- swagger
description: Spectral linting rules defining API design standards and conventions for Swagger Codegen.
layout: rules
name: Swagger Codegen API Rules
provider_name: Swagger Codegen
provider_slug: swagger-codegen
rule_count: 9
rules:
- description: All Generator API operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: swagger-codegen-operations-have-tags
  severity: warn
- description: All Generator API operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: swagger-codegen-operations-have-summaries
  severity: error
- description: Generator API operation summaries must use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: swagger-codegen-summaries-title-case
  severity: warn
- description: All Generator API operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: swagger-codegen-operations-have-operation-ids
  severity: error
- description: All Generator API operations must have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: swagger-codegen-operations-have-descriptions
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: swagger-codegen-path-params-required
  severity: error
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: swagger-codegen-schemas-have-descriptions
  severity: warn
- description: GenerationRequest schema must require lang field
  given: $.components.schemas.GenerationRequest
  name: swagger-codegen-generation-request-lang-required
  severity: error
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: swagger-codegen-responses-have-descriptions
  severity: warn
rules_file: rules/swagger-codegen-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/swagger-codegen/refs/heads/main/rules/swagger-codegen-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: swagger-codegen-rules
source_filename: swagger-codegen-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  swagger-codegen-operations-have-tags:\n    description: All Generator API operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  swagger-codegen-operations-have-summaries:\n    description: All Generator API operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  swagger-codegen-summaries-title-case:\n    description: Generator API operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  swagger-codegen-operations-have-operation-ids:\n    description: All Generator API operations must have an operationId\n    severity: error\n\
  \    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  swagger-codegen-operations-have-descriptions:\n    description: All Generator API operations must have a description\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  swagger-codegen-path-params-required:\n    description: Path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  swagger-codegen-schemas-have-descriptions:\n    description: All component schemas must have a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  swagger-codegen-generation-request-lang-required:\n    description: GenerationRequest schema must require lang field\n    severity: error\n    given:\
  \ \"$.components.schemas.GenerationRequest\"\n    then:\n      field: required\n      function: truthy\n\n  swagger-codegen-responses-have-descriptions:\n    description: All response objects must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/swagger-codegen/refs/heads/main/rules/swagger-codegen-rules.yml
tags:
- Client Libraries
- Code Generation
- Open Source
- OpenAPI
- SDK
- Spectral
- Linting
- API Governance
---

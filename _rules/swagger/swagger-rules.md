---
categories:
- swagger
description: Spectral linting rules defining API design standards and conventions for Swagger.
layout: rules
name: Swagger API Rules
provider_name: Swagger
provider_slug: swagger
rule_count: 10
rules:
- description: All OpenAPI operations must have at least one tag for organization
  given: $.paths[*][get,put,post,delete,patch,options,head,trace]
  name: swagger-oas-operations-have-tags
  severity: warn
- description: All OpenAPI operations must have a summary in Title Case
  given: $.paths[*][get,put,post,delete,patch,options,head,trace]
  name: swagger-oas-operations-have-summaries
  severity: error
- description: OpenAPI operation summaries should use Title Case
  given: $.paths[*][get,put,post,delete,patch,options,head,trace].summary
  name: swagger-oas-summaries-title-case
  severity: warn
- description: All OpenAPI operations must have an operationId for code generation
  given: $.paths[*][get,put,post,delete,patch,options,head,trace]
  name: swagger-oas-operations-have-operation-ids
  severity: error
- description: All OpenAPI operations should have a description
  given: $.paths[*][get,put,post,delete,patch,options,head,trace]
  name: swagger-oas-operations-have-descriptions
  severity: warn
- description: All path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: swagger-oas-path-params-required
  severity: error
- description: All component schemas must have a description
  given: $.components.schemas[*]
  name: swagger-oas-schemas-have-descriptions
  severity: warn
- description: API info object must have title, description, and version
  given: $.info
  name: swagger-oas-info-required-fields
  severity: error
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: swagger-oas-responses-have-descriptions
  severity: warn
- description: API paths should use kebab-case (lowercase with hyphens, no underscores)
  given: $.paths[*]~
  name: swagger-oas-paths-kebab-case
  severity: warn
rules_file: rules/swagger-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/swagger/refs/heads/main/rules/swagger-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: swagger-rules
source_filename: swagger-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  swagger-oas-operations-have-tags:\n    description: All OpenAPI operations must have at least one tag for organization\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch,options,head,trace]\"\n    then:\n      field: tags\n      function: truthy\n\n  swagger-oas-operations-have-summaries:\n    description: All OpenAPI operations must have a summary in Title Case\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch,options,head,trace]\"\n    then:\n      field: summary\n      function: truthy\n\n  swagger-oas-summaries-title-case:\n    description: OpenAPI operation summaries should use Title Case\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch,options,head,trace].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  swagger-oas-operations-have-operation-ids:\n    description: All OpenAPI operations\
  \ must have an operationId for code generation\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch,options,head,trace]\"\n    then:\n      field: operationId\n      function: truthy\n\n  swagger-oas-operations-have-descriptions:\n    description: All OpenAPI operations should have a description\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch,options,head,trace]\"\n    then:\n      field: description\n      function: truthy\n\n  swagger-oas-path-params-required:\n    description: All path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  swagger-oas-schemas-have-descriptions:\n    description: All component schemas must have a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  swagger-oas-info-required-fields:\n    description: API\
  \ info object must have title, description, and version\n    severity: error\n    given: \"$.info\"\n    then:\n      - field: title\n        function: truthy\n      - field: version\n        function: truthy\n\n  swagger-oas-responses-have-descriptions:\n    description: All response objects must have a description\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  swagger-oas-paths-kebab-case:\n    description: API paths should use kebab-case (lowercase with hyphens, no underscores)\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}]*)*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/swagger/refs/heads/main/rules/swagger-rules.yml
tags:
- API Design
- Documentation
- Open Source
- OpenAPI
- REST
- Standard
- Swagger
- Spectral
- Linting
- API Governance
---

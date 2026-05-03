---
api_specs:
- filename: traceable-platform-openapi.yml
  format: yaml
  label: Traceable Platform GraphQL API
  slug: traceable-platform-graphql
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traceable/refs/heads/main/openapi/traceable-platform-openapi.yml
categories:
- traceable
description: Spectral linting rules defining API design standards and conventions for Traceable.
layout: rules
name: Traceable API Rules
provider_name: Traceable
provider_slug: traceable
rule_count: 10
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: traceable-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: traceable-operation-ids-required
  severity: error
- description: All operations must have a description.
  given: $.paths[*][*]
  name: traceable-operation-description-required
  severity: warn
- description: All operations must require Bearer token authentication.
  given: $.components.securitySchemes.bearerAuth
  name: traceable-bearer-auth-required
  severity: error
- description: All operations must be tagged.
  given: $.paths[*][*]
  name: traceable-tags-required
  severity: warn
- description: GraphQL endpoint must define a requestBody with query field.
  given: $.paths['/graphql'][post]
  name: traceable-graphql-request-body
  severity: error
- description: All operations must define a 200 or 201 success response.
  given: $.paths[*][*].responses
  name: traceable-response-200-defined
  severity: error
- description: All operations must define a 401 unauthorized response.
  given: $.paths[*][*].responses
  name: traceable-response-401-defined
  severity: warn
- description: GraphQLRequest schema must define the query field as required.
  given: $.components.schemas.GraphQLRequest.required
  name: traceable-graphql-schema-required
  severity: error
- description: MCPRequest tool field must enumerate valid tool names.
  given: $.components.schemas.MCPRequest.properties.tool
  name: traceable-mcp-tool-enum
  severity: warn
rules_file: rules/traceable-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/traceable/refs/heads/main/rules/traceable-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 5
slug: traceable-rules
source_filename: traceable-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  traceable-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  traceable-operation-ids-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: defined\n\n  traceable-operation-description-required:\n    description: All operations must have a description.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: defined\n\n  traceable-bearer-auth-required:\n    description: All operations must require Bearer token authentication.\n    severity: error\n    given: \"$.components.securitySchemes.bearerAuth\"\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: object\n          properties:\n            type:\n              const: http\n            scheme:\n              const: bearer\n\n  traceable-tags-required:\n    description: All operations must be tagged.\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: defined\n\n  traceable-graphql-request-body:\n    description: GraphQL endpoint must define a requestBody with query field.\n    severity: error\n    given: \"$.paths['/graphql'][post]\"\n    then:\n      field: requestBody\n      function: defined\n\n  traceable-response-200-defined:\n    description: All operations must define a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  traceable-response-401-defined:\n    description:\
  \ All operations must define a 401 unauthorized response.\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  traceable-graphql-schema-required:\n    description: GraphQLRequest schema must define the query field as required.\n    severity: error\n    given: \"$.components.schemas.GraphQLRequest.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: query\n\n  traceable-mcp-tool-enum:\n    description: MCPRequest tool field must enumerate valid tool names.\n    severity: warn\n    given: \"$.components.schemas.MCPRequest.properties.tool\"\n    then:\n      field: enum\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/traceable/refs/heads/main/rules/traceable-rules.yml
tags:
- API Discovery
- API Protection
- API Security
- API Testing
- Observability
- Security
- Threat Detection
- Spectral
- Linting
- API Governance
---

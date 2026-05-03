---
api_specs:
- filename: secureworks-taegis-xdr-openapi.yml
  format: yaml
  label: Secureworks Taegis XDR API
  slug: secureworks-taegis-xdr-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/secureworks/refs/heads/main/openapi/secureworks-taegis-xdr-openapi.yml
categories:
- secureworks
description: Spectral linting rules defining API design standards and conventions for Secureworks.
layout: rules
name: Secureworks API Rules
provider_name: Secureworks
provider_slug: secureworks
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: secureworks-operation-ids-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: secureworks-tags-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: secureworks-summaries-title-case
  severity: warn
- description: All operations except token endpoint require bearer authentication
  given: $.paths['/graphql'][*]
  name: secureworks-bearer-auth-required
  severity: error
- description: GraphQL endpoint must define requestBody with query field
  given: $.paths['/graphql'][post]
  name: secureworks-graphql-request-body
  severity: error
- description: API should document all regional server URLs
  given: $.servers
  name: secureworks-multi-region-servers
  severity: info
- description: Operations should document 401 and 429 error responses
  given: $.paths[*][*].responses
  name: secureworks-response-errors-documented
  severity: warn
- description: GraphQL request schema should type variables as object
  given: $.components.schemas.GraphQLRequest.properties.variables
  name: secureworks-graphql-variables-typed
  severity: info
rules_file: rules/secureworks-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/secureworks/refs/heads/main/rules/secureworks-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 3
slug: secureworks-rules
source_filename: secureworks-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  secureworks-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  secureworks-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  secureworks-summaries-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  secureworks-bearer-auth-required:\n    description: All operations except token endpoint require bearer authentication\n    severity: error\n    given: \"$.paths['/graphql'][*]\"\n    then:\n      field: security\n      function:\
  \ truthy\n\n  secureworks-graphql-request-body:\n    description: GraphQL endpoint must define requestBody with query field\n    severity: error\n    given: \"$.paths['/graphql'][post]\"\n    then:\n      field: requestBody\n      function: truthy\n\n  secureworks-multi-region-servers:\n    description: API should document all regional server URLs\n    severity: info\n    given: \"$.servers\"\n    then:\n      function: truthy\n\n  secureworks-response-errors-documented:\n    description: Operations should document 401 and 429 error responses\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  secureworks-graphql-variables-typed:\n    description: GraphQL request schema should type variables as object\n    severity: info\n    given: \"$.components.schemas.GraphQLRequest.properties.variables\"\n    then:\n      field: type\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/secureworks/refs/heads/main/rules/secureworks-rules.yml
tags:
- Cybersecurity
- XDR
- Threat Detection
- Security Operations
- Incident Response
- MDR
- Threat Intelligence
- Spectral
- Linting
- API Governance
---

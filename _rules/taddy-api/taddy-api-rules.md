---
api_specs:
- filename: taddy-podcast-openapi.yml
  format: yaml
  label: Taddy Podcast API
  slug: taddy-podcast-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/taddy-api/refs/heads/main/openapi/taddy-podcast-openapi.yml
categories:
- taddy
description: Spectral linting rules defining API design standards and conventions for Taddy API.
layout: rules
name: Taddy API API Rules
provider_name: Taddy API
provider_slug: taddy-api
rule_count: 8
rules:
- description: Taddy GraphQL API only accepts POST requests
  given: $.paths['/'].get
  name: taddy-graphql-endpoint-must-be-post
  severity: error
- description: All GraphQL requests must include a query field
  given: $.paths['/'].post.requestBody.content['application/json'].schema
  name: taddy-request-must-include-query
  severity: error
- description: API must document X-API-KEY and X-USER-ID authentication headers
  given: $.components.securitySchemes
  name: taddy-auth-headers-documented
  severity: warn
- description: GraphQL operations should include request examples
  given: $.paths['/'].post.requestBody.content['application/json'].examples
  name: taddy-operations-have-examples
  severity: info
- description: GraphQL responses should document the data wrapper
  given: $.paths['/'].post.responses['200'].content['application/json'].schema.properties
  name: taddy-response-includes-data-field
  severity: warn
- description: All schema components should have descriptions
  given: $.components.schemas[*]
  name: taddy-schemas-have-descriptions
  severity: warn
- description: UUID identifier fields must be typed as string
  given: $.components.schemas[*].properties.uuid
  name: taddy-uuid-fields-are-strings
  severity: error
- description: URL fields should use format uri
  given: $.components.schemas[*].properties[*Url]
  name: taddy-url-fields-use-uri-format
  severity: warn
rules_file: rules/taddy-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/taddy-api/refs/heads/main/rules/taddy-api-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: taddy-api-rules
source_filename: taddy-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  taddy-graphql-endpoint-must-be-post:\n    description: Taddy GraphQL API only accepts POST requests\n    message: \"GraphQL endpoints must use POST method\"\n    severity: error\n    given: \"$.paths['/'].get\"\n    then:\n      function: undefined\n\n  taddy-request-must-include-query:\n    description: All GraphQL requests must include a query field\n    message: \"Request body must include a 'query' property\"\n    severity: error\n    given: \"$.paths['/'].post.requestBody.content['application/json'].schema\"\n    then:\n      field: required\n      function: truthy\n\n  taddy-auth-headers-documented:\n    description: API must document X-API-KEY and X-USER-ID authentication headers\n    message: \"API key authentication headers must be documented in securitySchemes\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  taddy-operations-have-examples:\n    description: GraphQL operations\
  \ should include request examples\n    message: \"Request body should include examples for key GraphQL queries\"\n    severity: info\n    given: \"$.paths['/'].post.requestBody.content['application/json'].examples\"\n    then:\n      function: truthy\n\n  taddy-response-includes-data-field:\n    description: GraphQL responses should document the data wrapper\n    message: \"Response schema should include a 'data' property\"\n    severity: warn\n    given: \"$.paths['/'].post.responses['200'].content['application/json'].schema.properties\"\n    then:\n      field: data\n      function: truthy\n\n  taddy-schemas-have-descriptions:\n    description: All schema components should have descriptions\n    message: \"{{property}} is missing a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  taddy-uuid-fields-are-strings:\n    description: UUID identifier fields must be typed as string\n    message: \"UUID\
  \ field '{{property}}' should be type: string\"\n    severity: error\n    given: \"$.components.schemas[*].properties.uuid\"\n    then:\n      field: type\n      function: pattern\n      functionOptions:\n        match: \"^string$\"\n\n  taddy-url-fields-use-uri-format:\n    description: URL fields should use format uri\n    message: \"URL field '{{property}}' should use format: uri\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*Url]\"\n    then:\n      field: format\n      function: pattern\n      functionOptions:\n        match: \"^uri$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/taddy-api/refs/heads/main/rules/taddy-api-rules.yml
tags:
- Audio
- Comics
- GraphQL
- Media
- Podcasts
- Transcripts
- Webhooks
- Spectral
- Linting
- API Governance
---

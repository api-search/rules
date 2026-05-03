---
api_specs:
- filename: warner-music-group-licensing-openapi.yml
  format: yaml
  label: Warner Music Group Licensing API
  slug: wmg-licensing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/warner-music-group/refs/heads/main/openapi/warner-music-group-licensing-openapi.yml
categories:
- wmg
description: Spectral linting rules defining API design standards and conventions for Warner Music Group.
layout: rules
name: Warner Music Group API Rules
provider_name: Warner Music Group
provider_slug: warner-music-group
rule_count: 10
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: wmg-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: wmg-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: wmg-operation-tags-required
  severity: error
- description: All API paths must include a version prefix
  given: $.paths
  name: wmg-paths-versioned
  severity: error
- description: WMG API uses OAuth2 authentication
  given: $.components.securitySchemes
  name: wmg-oauth2-required
  severity: error
- description: Operations must define a successful response
  given: $.paths[*][*].responses
  name: wmg-response-success-defined
  severity: error
- description: Protected operations must define a 401 response
  given: $.paths[*][*].responses
  name: wmg-response-401-defined
  severity: warn
- description: Catalog search must have at least a query parameter
  given: $.paths['/v1/catalog/search'].get.parameters
  name: wmg-catalog-search-params
  severity: error
- description: Track endpoints should use ISRC as the path parameter
  given: $.paths./v1/tracks/{isrc}.get.parameters[*]
  name: wmg-isrc-path-pattern
  severity: info
- description: List operations should support limit and offset parameters
  given: $.paths[*].get.parameters[*].name
  name: wmg-pagination-on-lists
  severity: warn
rules_file: rules/warner-music-group-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/warner-music-group/refs/heads/main/rules/warner-music-group-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 3
slug: warner-music-group-rules
source_filename: warner-music-group-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  wmg-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wmg-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  wmg-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  wmg-paths-versioned:\n    description: All API paths must include a version prefix\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v[0-9]+\"\n\n  wmg-oauth2-required:\n    description: WMG API\
  \ uses OAuth2 authentication\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  wmg-response-success-defined:\n    description: Operations must define a successful response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  wmg-response-401-defined:\n    description: Protected operations must define a 401 response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"401\"\n\n  wmg-catalog-search-params:\n    description: Catalog search must have at least a query parameter\n    severity: error\n    given:\
  \ \"$.paths['/v1/catalog/search'].get.parameters\"\n    then:\n      function: truthy\n\n  wmg-isrc-path-pattern:\n    description: Track endpoints should use ISRC as the path parameter\n    severity: info\n    given: \"$.paths./v1/tracks/{isrc}.get.parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            name:\n              enum:\n                - isrc\n\n  wmg-pagination-on-lists:\n    description: List operations should support limit and offset parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - limit\n          - offset\n          - page\n          - cursor\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/warner-music-group/refs/heads/main/rules/warner-music-group-rules.yml
tags:
- Music
- Entertainment
- Streaming
- Licensing
- Publishing
- Spectral
- Linting
- API Governance
---

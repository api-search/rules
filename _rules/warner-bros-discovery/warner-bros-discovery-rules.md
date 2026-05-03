---
api_specs:
- filename: warner-bros-discovery-content-partner-openapi.yml
  format: yaml
  label: Warner Bros. Discovery Content Partner API
  slug: wbd-content-partner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/warner-bros-discovery/refs/heads/main/openapi/warner-bros-discovery-content-partner-openapi.yml
categories:
- wbd
description: Spectral linting rules defining API design standards and conventions for Warner Bros. Discovery.
layout: rules
name: Warner Bros. Discovery API Rules
provider_name: Warner Bros. Discovery
provider_slug: warner-bros-discovery
rule_count: 10
rules:
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: wbd-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: wbd-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: wbd-operation-tags-required
  severity: error
- description: All API paths must include a version prefix (/v1/, /v2/, etc.)
  given: $.paths
  name: wbd-paths-versioned
  severity: error
- description: WBD APIs use OAuth2 client credentials for authentication
  given: $.components.securitySchemes
  name: wbd-oauth2-security
  severity: error
- description: All operations must define a successful 2xx response
  given: $.paths[*][*].responses
  name: wbd-response-200-or-201
  severity: error
- description: Operations should define 401 and 404 error responses
  given: $.paths[*][*].responses
  name: wbd-error-responses-defined
  severity: warn
- description: Info object must have a description
  given: $.info
  name: wbd-info-description
  severity: error
- description: Successful responses must define a schema
  given: $.paths[*][*].responses['200'].content['application/json']
  name: wbd-response-schema
  severity: warn
- description: Collection GET endpoints should support limit and offset parameters
  given: $.paths[*].get.parameters[*].name
  name: wbd-pagination-parameters
  severity: warn
rules_file: rules/warner-bros-discovery-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/warner-bros-discovery/refs/heads/main/rules/warner-bros-discovery-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 4
slug: warner-bros-discovery-rules
source_filename: warner-bros-discovery-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  wbd-operation-ids-required:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wbd-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  wbd-operation-tags-required:\n    description: All operations must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  wbd-paths-versioned:\n    description: All API paths must include a version prefix (/v1/, /v2/, etc.)\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v[0-9]+\"\n\n  wbd-oauth2-security:\n    description:\
  \ WBD APIs use OAuth2 client credentials for authentication\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  wbd-response-200-or-201:\n    description: All operations must define a successful 2xx response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n\n  wbd-error-responses-defined:\n    description: Operations should define 401 and 404 error responses\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"401\"\n\n  wbd-info-description:\n    description: Info object\
  \ must have a description\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  wbd-response-schema:\n    description: Successful responses must define a schema\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json']\"\n    then:\n      field: schema\n      function: truthy\n\n  wbd-pagination-parameters:\n    description: Collection GET endpoints should support limit and offset parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - limit\n          - offset\n          - page\n          - pageSize\n          - cursor\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/warner-bros-discovery/refs/heads/main/rules/warner-bros-discovery-rules.yml
tags:
- Entertainment
- Media
- Streaming
- Content
- Television
- Film
- Spectral
- Linting
- API Governance
---

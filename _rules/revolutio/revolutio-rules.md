---
api_specs:
- filename: revolutio-hazard-api-openapi.yml
  format: yaml
  label: Revolutio Hazard API
  slug: revolutio-hazard-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/revolutio/refs/heads/main/openapi/revolutio-hazard-api-openapi.yml
categories:
- revolutio
description: Spectral linting rules defining API design standards and conventions for Revolutio.
layout: rules
name: Revolutio API Rules
provider_name: Revolutio
provider_slug: revolutio
rule_count: 8
rules:
- description: All operationIds must use camelCase format
  given: $.paths.*.*
  name: revolutio-operation-id-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: revolutio-tags-title-case
  severity: warn
- description: All GET endpoints must include apiKey as a query parameter
  given: $.paths.*.get.parameters[?(@.name == 'apiKey')]
  name: revolutio-api-key-required
  severity: error
- description: All hazard analysis endpoints must include latitude and longitude parameters
  given: $.paths.*.get
  name: revolutio-coordinates-required
  severity: error
- description: Hazard API endpoints must offer both GET and POST variants
  given: $.paths.*
  name: revolutio-get-post-parity
  severity: warn
- description: All 200 responses must define a content schema
  given: $.paths.*.*.responses.200.content
  name: revolutio-response-schema-defined
  severity: error
- description: API paths must not end with a trailing slash
  given: $.paths
  name: revolutio-no-trailing-slash
  severity: warn
- description: Query parameter names should use camelCase for consistency with API convention
  given: $.paths.*.*.parameters[?(@.in == 'query')].name
  name: revolutio-snake-case-query-params
  severity: info
rules_file: rules/revolutio-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/revolutio/refs/heads/main/rules/revolutio-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: revolutio-rules
source_filename: revolutio-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  revolutio-operation-id-camel-case:\n    description: All operationIds must use camelCase format\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  revolutio-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /]*$\"\n\n  revolutio-api-key-required:\n    description: All GET endpoints must include apiKey as a query parameter\n    severity: error\n    given: \"$.paths.*.get.parameters[?(@.name == 'apiKey')]\"\n    then:\n      field: required\n      function: truthy\n\n  revolutio-coordinates-required:\n    description: All hazard analysis endpoints must include latitude and longitude parameters\n    severity: error\n    given: \"$.paths.*.get\"\n    then:\n      field: parameters\n  \
  \    function: truthy\n\n  revolutio-get-post-parity:\n    description: Hazard API endpoints must offer both GET and POST variants\n    severity: warn\n    given: \"$.paths.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            get:\n              type: object\n            post:\n              type: object\n\n  revolutio-response-schema-defined:\n    description: All 200 responses must define a content schema\n    severity: error\n    given: \"$.paths.*.*.responses.200.content\"\n    then:\n      function: truthy\n\n  revolutio-no-trailing-slash:\n    description: API paths must not end with a trailing slash\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  revolutio-snake-case-query-params:\n    description: Query parameter names should use camelCase for consistency with API convention\n    severity: info\n    given: \"$.paths.*.*.parameters[?(@.in\
  \ == 'query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/revolutio/refs/heads/main/rules/revolutio-rules.yml
tags:
- Engineering
- Hazard
- Weather
- Structural Engineering
- Wind Analysis
- Construction
- Spectral
- Linting
- API Governance
---

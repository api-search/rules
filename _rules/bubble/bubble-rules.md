---
api_specs:
- filename: bubble-data-api-openapi.yml
  format: yaml
  label: Bubble Data API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/bubble/refs/heads/main/openapi/bubble-data-api-openapi.yml
- filename: bubble-workflow-api-openapi.yml
  format: yaml
  label: Bubble Workflow API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/bubble/refs/heads/main/openapi/bubble-workflow-api-openapi.yml
- filename: bubble-plugin-api-openapi.yml
  format: yaml
  label: Bubble Plugin API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/bubble/refs/heads/main/openapi/bubble-plugin-api-openapi.yml
categories:
- bubble
description: Spectral linting rules defining API design standards and conventions for Bubble.
layout: rules
name: Bubble API Rules
provider_name: Bubble
provider_slug: bubble
rule_count: 12
rules:
- description: Bubble OpenAPI specs must declare info.title.
  given: $.info
  name: bubble-info-title-required
  severity: error
- description: Bubble OpenAPI specs must declare info.version.
  given: $.info
  name: bubble-info-version-required
  severity: error
- description: Bubble OpenAPI specs should declare a license block referencing Bubble Terms or Plugin Marketplace Terms.
  given: $.info
  name: bubble-info-license-required
  severity: warn
- description: Bubble OpenAPI specs must declare at least one server.
  given: $.servers
  name: bubble-server-required
  severity: error
- description: Bubble Data API and Workflow API must define bearer authentication via components.securitySchemes.
  given: $.components.securitySchemes.BearerAuth
  name: bubble-bearer-auth-required
  severity: error
- description: Operation summaries should use Title Case (first letter of each major word capitalized).
  given: $.paths..[?(@.summary)]
  name: bubble-operation-summary-title-case
  severity: warn
- description: operationId should be camelCase (createThing, searchThings, triggerWorkflow).
  given: $.paths..[?(@.operationId)]
  name: bubble-operation-id-camel-case
  severity: warn
- description: 'Each operation should be tagged with one of: Data, Workflow, Action, Element, Thing, Context.'
  given: $.paths..[?(@.operationId)]
  name: bubble-tag-required
  severity: warn
- description: Operations on the Data API and Workflow API should declare a 429 response (rate limited).
  given: $.paths[?(@property.match(/^\/obj/) || @property.match(/^\/wf/))]..responses
  name: bubble-rate-limited-response
  severity: warn
- description: Authenticated operations should declare a 401 response.
  given: $.paths[?(@property.match(/^\/obj/))]..responses
  name: bubble-unauthorized-response
  severity: warn
- description: The {typename} path parameter must be documented as lowercase with no spaces.
  given: $..parameters[?(@.name=='typename')]
  name: bubble-typename-lowercase
  severity: info
- description: The /bulk endpoint description should mention the 1,000-record cap per request.
  given: $.paths['/obj/{typename}/bulk'].post
  name: bubble-bulk-payload-cap
  severity: info
rules_file: rules/bubble-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bubble/refs/heads/main/rules/bubble-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 6
slug: bubble-rules
source_filename: bubble-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: ['spectral:oas']\ndocumentationUrl: https://manual.bubble.io/core-resources/api/the-bubble-api.md\nfunctions: []\nrules:\n  bubble-info-title-required:\n    description: 'Bubble OpenAPI specs must declare info.title.'\n    message: '{{path}} must declare info.title.'\n    severity: error\n    given: '$.info'\n    then:\n      field: title\n      function: truthy\n\n  bubble-info-version-required:\n    description: 'Bubble OpenAPI specs must declare info.version.'\n    message: '{{path}} must declare info.version.'\n    severity: error\n    given: '$.info'\n    then:\n      field: version\n      function: truthy\n\n  bubble-info-license-required:\n    description: 'Bubble OpenAPI specs should declare a license block referencing Bubble Terms or Plugin Marketplace Terms.'\n    message: '{{path}} should declare info.license.'\n    severity: warn\n    given: '$.info'\n    then:\n      field: license\n      function: truthy\n\n  bubble-server-required:\n    description:\
  \ 'Bubble OpenAPI specs must declare at least one server.'\n    message: '{{path}} must declare a servers array with at least one entry.'\n    severity: error\n    given: '$.servers'\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  bubble-bearer-auth-required:\n    description: 'Bubble Data API and Workflow API must define bearer authentication via components.securitySchemes.'\n    message: '{{path}} must define a bearer security scheme named BearerAuth.'\n    severity: error\n    given: '$.components.securitySchemes.BearerAuth'\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: '^bearer$'\n\n  bubble-operation-summary-title-case:\n    description: 'Operation summaries should use Title Case (first letter of each major word capitalized).'\n    message: '{{path}} summary should use Title Case.'\n    severity: warn\n    given: '$.paths..[?(@.summary)]'\n    then:\n      field: summary\n      function: pattern\n \
  \     functionOptions:\n        match: '^[A-Z][^.]*$'\n\n  bubble-operation-id-camel-case:\n    description: 'operationId should be camelCase (createThing, searchThings, triggerWorkflow).'\n    message: '{{path}}.operationId should be camelCase.'\n    severity: warn\n    given: '$.paths..[?(@.operationId)]'\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  bubble-tag-required:\n    description: 'Each operation should be tagged with one of: Data, Workflow, Action, Element, Thing, Context.'\n    message: '{{path}} must declare at least one tag.'\n    severity: warn\n    given: '$.paths..[?(@.operationId)]'\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  bubble-rate-limited-response:\n    description: 'Operations on the Data API and Workflow API should declare a 429 response (rate limited).'\n    message: '{{path}} should declare a 429 (rate limited) response.'\n\
  \    severity: warn\n    given: \"$.paths[?(@property.match(/^\\\\/obj/) || @property.match(/^\\\\/wf/))]..responses\"\n    then:\n      field: '429'\n      function: truthy\n\n  bubble-unauthorized-response:\n    description: 'Authenticated operations should declare a 401 response.'\n    message: '{{path}} should declare a 401 response.'\n    severity: warn\n    given: \"$.paths[?(@property.match(/^\\\\/obj/))]..responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  bubble-typename-lowercase:\n    description: 'The {typename} path parameter must be documented as lowercase with no spaces.'\n    message: 'typename description must note lowercase / no-spaces convention.'\n    severity: info\n    given: \"$..parameters[?(@.name=='typename')]\"\n    then:\n      field: description\n      function: pattern\n      functionOptions:\n        match: 'lowercase|no spaces|removed'\n\n  bubble-bulk-payload-cap:\n    description: 'The /bulk endpoint description should mention the 1,000-record\
  \ cap per request.'\n    message: '{{path}} should call out the 1,000-record bulk cap.'\n    severity: info\n    given: \"$.paths['/obj/{typename}/bulk'].post\"\n    then:\n      field: description\n      function: pattern\n      functionOptions:\n        match: '1,000|1000'\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/bubble/refs/heads/main/rules/bubble-rules.yml
tags:
- No-Code
- Application Platform
- Database
- Workflow Automation
- Plugins
- Spectral
- Linting
- API Governance
---

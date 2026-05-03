---
api_specs:
- filename: reolink-camera-api-openapi.yml
  format: yaml
  label: Reolink Camera HTTP API
  slug: camera-http-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/reolink/refs/heads/main/openapi/reolink-camera-api-openapi.yml
categories:
- reolink
description: Spectral linting rules defining API design standards and conventions for Reolink.
layout: rules
name: Reolink API Rules
provider_name: Reolink
provider_slug: reolink
rule_count: 8
rules:
- description: Reolink API uses token query parameter for authentication
  given: $.components.securitySchemes
  name: reolink-api-key-auth
  severity: error
- description: All Reolink API endpoints use POST method only
  given: $.paths[*]
  name: reolink-post-only-paths
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][post].summary
  name: reolink-summaries-title-case
  severity: warn
- description: Operations must have tags for categorization
  given: $.paths[*][post]
  name: reolink-operation-tags
  severity: warn
- description: All POST operations must include a request body
  given: $.paths[*].post
  name: reolink-request-body-required
  severity: error
- description: All operations must define a 200 response
  given: $.paths[*][post].responses
  name: reolink-response-200-defined
  severity: error
- description: Reolink command paths should include cmd parameter pattern
  given: $.paths
  name: reolink-cmd-param-in-path
  severity: hint
- description: Reolink operation IDs must use camelCase
  given: $.paths[*][post].operationId
  name: reolink-operation-id-camel-case
  severity: warn
rules_file: rules/reolink-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/reolink/refs/heads/main/rules/reolink-rules.yml
severity_counts:
  error: 3
  hint: 1
  info: 0
  warn: 4
slug: reolink-rules
source_filename: reolink-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n\n  reolink-api-key-auth:\n    description: Reolink API uses token query parameter for authentication\n    message: \"API must declare tokenAuth security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: tokenAuth\n\n  reolink-post-only-paths:\n    description: All Reolink API endpoints use POST method only\n    message: \"Reolink camera API only supports POST requests\"\n    severity: warn\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          additionalProperties: false\n          properties:\n            post: {}\n            parameters: {}\n\n  reolink-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][post].summary\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^[A-Z][a-zA-Z0-9 &()/.-]*$\"\n\n  reolink-operation-tags:\n    description: Operations must have tags for categorization\n    message: \"Operation must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][post]\"\n    then:\n      function: truthy\n      field: tags\n\n  reolink-request-body-required:\n    description: All POST operations must include a request body\n    message: \"POST operation must define a requestBody\"\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      function: truthy\n      field: requestBody\n\n  reolink-response-200-defined:\n    description: All operations must define a 200 response\n    message: \"Operation must define a 200 response\"\n    severity: error\n    given: \"$.paths[*][post].responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  reolink-cmd-param-in-path:\n    description: Reolink command paths should include cmd parameter pattern\n    message: \"Reolink paths should follow\
  \ the /cgi-bin/api.cgi?cmd={Command} pattern\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/cgi-bin/api\\\\.cgi\"\n\n  reolink-operation-id-camel-case:\n    description: Reolink operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][post].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/reolink/refs/heads/main/rules/reolink-rules.yml
tags:
- IoT
- Security Cameras
- Surveillance
- Smart Home
- AI Detection
- Spectral
- Linting
- API Governance
---

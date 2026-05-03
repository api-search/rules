---
api_specs:
- filename: rainbow-application-openapi.yml
  format: yaml
  label: Rainbow Application Portal API
  slug: rainbow-application-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rainbow/refs/heads/main/openapi/rainbow-application-openapi.yml
- filename: rainbow-messaging-openapi.yml
  format: yaml
  label: Rainbow Messaging API
  slug: rainbow-messaging-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rainbow/refs/heads/main/openapi/rainbow-messaging-openapi.yml
- filename: rainbow-contacts-openapi.yml
  format: yaml
  label: Rainbow Contacts API
  slug: rainbow-contacts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rainbow/refs/heads/main/openapi/rainbow-contacts-openapi.yml
categories:
- rainbow
description: Spectral linting rules defining API design standards and conventions for Rainbow.
layout: rules
name: Rainbow API Rules
provider_name: Rainbow
provider_slug: rainbow
rule_count: 7
rules:
- description: Rainbow APIs must use Bearer token authentication
  given: $.components.securitySchemes[*]
  name: rainbow-bearer-auth
  severity: error
- description: All Rainbow API paths must include a version segment (v1.0, v2.0, etc.)
  given: $.paths
  name: rainbow-versioned-paths
  severity: warn
- description: Collection endpoints should support limit and offset pagination
  given: $.paths[*].get.parameters[*].name
  name: rainbow-pagination-params
  severity: warn
- description: All operations must have an operationId in camelCase
  given: $.paths[*][*]
  name: rainbow-operation-ids
  severity: error
- description: Rainbow API responses should wrap primary data in a data field
  given: $.components.schemas[?(@.properties.data)]
  name: rainbow-response-data-wrapper
  severity: warn
- description: Error responses must include code and msg fields
  given: $.components.schemas[?(@.title == 'ErrorResponse' || contains(@, 'Error'))].properties
  name: rainbow-error-code-msg
  severity: warn
- description: All operations must include at least one tag
  given: $.paths[*][*].tags
  name: rainbow-tags-required
  severity: warn
rules_file: rules/rainbow-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rainbow/refs/heads/main/rules/rainbow-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 5
slug: rainbow-rules
source_filename: rainbow-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rainbow-bearer-auth:\n    description: Rainbow APIs must use Bearer token authentication\n    message: Security scheme must use HTTP Bearer authentication\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type:\n              enum: [http, oauth2]\n          required: [type]\n\n  rainbow-versioned-paths:\n    description: All Rainbow API paths must include a version segment (v1.0, v2.0, etc.)\n    message: \"API path must include version segment like /v1.0/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z]+/v[0-9]+\\\\.[0-9]+\"\n\n  rainbow-pagination-params:\n    description: Collection endpoints should support limit and offset pagination\n    message: GET collection endpoints should include limit and offset\
  \ query parameters\n    severity: warn\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n      function: truthy\n\n  rainbow-operation-ids:\n    description: All operations must have an operationId in camelCase\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  rainbow-response-data-wrapper:\n    description: Rainbow API responses should wrap primary data in a data field\n    message: API response should use data envelope pattern\n    severity: warn\n    given: \"$.components.schemas[?(@.properties.data)]\"\n    then:\n      function: truthy\n\n  rainbow-error-code-msg:\n    description: Error responses must include code and msg fields\n    message: Error schema must have code (integer) and msg (string) fields\n    severity: warn\n    given: \"$.components.schemas[?(@.title == 'ErrorResponse' || contains(@, 'Error'))].properties\"\n    then:\n      function: truthy\n\
  \n  rainbow-tags-required:\n    description: All operations must include at least one tag\n    message: Operation must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rainbow/refs/heads/main/rules/rainbow-rules.yml
tags:
- Communications
- CPaaS
- Chat
- Voice
- Video
- Telephony
- Messaging
- Collaboration
- Unified Communications
- Spectral
- Linting
- API Governance
---

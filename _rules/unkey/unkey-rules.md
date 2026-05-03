---
api_specs:
- filename: unkey-openapi.yml
  format: yaml
  label: Unkey API
  slug: unkey-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unkey/refs/heads/main/openapi/unkey-openapi.yml
categories:
- unkey
description: Spectral linting rules defining API design standards and conventions for Unkey.
layout: rules
name: Unkey API Rules
provider_name: Unkey
provider_slug: unkey
rule_count: 10
rules:
- description: Management endpoints should use POST method with dot-notation operationId
  given: $.paths[*]
  name: unkey-post-only-management
  severity: warn
- description: Operation IDs must use dot-notation (e.g. keys.createKey, ratelimit.limit)
  given: $.paths[*][*].operationId
  name: unkey-operation-id-dot-notation
  severity: error
- description: All API paths must start with /v2/
  given: $.paths[*]~
  name: unkey-path-versioning
  severity: error
- description: All operations (except liveness) must require rootKey authentication
  given: $.paths[?(!@property.match(/liveness/))][*]
  name: unkey-bearer-auth
  severity: warn
- description: Success responses must use the meta+data envelope structure
  given: $.paths[*][*].responses['200'].content['application/json'].schema
  name: unkey-response-envelope
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: unkey-title-case-summary
  severity: warn
- description: Operations must use defined API resource tags
  given: $.paths[*][*].tags[*]
  name: unkey-valid-tags
  severity: warn
- description: Request bodies must use application/json media type
  given: $.paths[*][*].requestBody.content
  name: unkey-json-request-body
  severity: error
- description: Operations requiring auth must define 401 responses
  given: $.paths[?(!@property.match(/liveness/))][*]
  name: unkey-error-response-401
  severity: warn
- description: Operations with permissions must define 403 responses
  given: $.paths[*][*]
  name: unkey-error-response-403
  severity: warn
rules_file: rules/unkey-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unkey/refs/heads/main/rules/unkey-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 7
slug: unkey-rules
source_filename: unkey-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n\n  # Unkey uses POST for all management endpoints with dot-notation operation IDs\n  unkey-post-only-management:\n    description: Management endpoints should use POST method with dot-notation operationId\n    message: \"{{description}}: {{path}}\"\n    severity: warn\n    given: \"$.paths[*]\"\n    then:\n      - field: post\n        function: truthy\n\n  # Operation IDs must use dot-notation (resource.action pattern)\n  unkey-operation-id-dot-notation:\n    description: Operation IDs must use dot-notation (e.g. keys.createKey, ratelimit.limit)\n    message: \"OperationId '{{value}}' should use dot-notation like 'resource.action'\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*\\\\.[a-z][a-zA-Z0-9]+$\"\n\n  # All paths must start with /v2/\n  unkey-path-versioning:\n    description: All API paths must start with /v2/\n\
  \    message: \"Path '{{path}}' must be versioned with /v2/ prefix\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2/\"\n\n  # All operations must use rootKey security\n  unkey-bearer-auth:\n    description: All operations (except liveness) must require rootKey authentication\n    message: \"{{description}}: {{path}}\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/liveness/))][*]\"\n    then:\n      - field: security\n        function: truthy\n\n  # Responses must wrap data in envelope with meta.requestId\n  unkey-response-envelope:\n    description: Success responses must use the meta+data envelope structure\n    message: \"200 response must include meta and data properties\"\n    severity: warn\n    given: \"$.paths[*][*].responses['200'].content['application/json'].schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\
  \ [meta]\n          properties:\n            meta:\n              type: object\n\n  # Operation summaries must be in Title Case\n  unkey-title-case-summary:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Tags must be one of the defined resource groups\n  unkey-valid-tags:\n    description: Operations must use defined API resource tags\n    message: \"Tag '{{value}}' must be one of: analytics, apis, deploy, identities, keys, liveness, permissions, ratelimit\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - analytics\n          - apis\n          - deploy\n          - identities\n          - keys\n          - liveness\n          - permissions\n          - ratelimit\n\n\
  \  # Request bodies must use application/json\n  unkey-json-request-body:\n    description: Request bodies must use application/json media type\n    message: \"{{description}}: {{path}}\"\n    severity: error\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: truthy\n      field: \"application/json\"\n\n  # Error responses must use consistent error response schemas\n  unkey-error-response-401:\n    description: Operations requiring auth must define 401 responses\n    message: \"Authenticated operation missing 401 response\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/liveness/))][*]\"\n    then:\n      field: \"responses.401\"\n      function: truthy\n\n  # 403 responses for permission-gated operations\n  unkey-error-response-403:\n    description: Operations with permissions must define 403 responses\n    message: \"Permission-gated operation missing 403 response\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: \"\
  responses.403\"\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unkey/refs/heads/main/rules/unkey-rules.yml
tags:
- API Keys
- Rate Limiting
- Authentication
- Developer Platform
- Access Control
- Identity
- Analytics
- Spectral
- Linting
- API Governance
---

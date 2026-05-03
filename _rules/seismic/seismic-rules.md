---
api_specs:
- filename: seismic-content-openapi.yml
  format: yaml
  label: Seismic Content API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/openapi/seismic-content-openapi.yml
- filename: seismic-livedocs-openapi.yml
  format: yaml
  label: Seismic LiveDocs API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/openapi/seismic-livedocs-openapi.yml
- filename: seismic-analytics-openapi.yml
  format: yaml
  label: Seismic Analytics API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/openapi/seismic-analytics-openapi.yml
- filename: seismic-user-management-openapi.yml
  format: yaml
  label: Seismic User Management API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/openapi/seismic-user-management-openapi.yml
categories:
- seismic
description: Spectral linting rules defining API design standards and conventions for Seismic.
layout: rules
name: Seismic API Rules
provider_name: Seismic
provider_slug: seismic
rule_count: 14
rules:
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: seismic-operation-summary-title-case
  severity: warn
- description: Operation summaries must not start with the provider name.
  given: $.paths[*][*].summary
  name: seismic-no-provider-prefix-in-summary
  severity: error
- description: OperationId must be camelCase.
  given: $.paths[*][*].operationId
  name: seismic-operationid-camelcase
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths[*]~
  name: seismic-paths-kebab-case
  severity: warn
- description: All operations must use bearerAuth security.
  given: $.paths[*][*]
  name: seismic-bearer-auth-required
  severity: warn
- description: List operations should support offset and limit pagination.
  given: $.paths[*].get
  name: seismic-pagination-offset-limit
  severity: info
- description: GET operations must define a 200 response with content.
  given: $.paths[*].get.responses
  name: seismic-response-200-content
  severity: error
- description: Operations should define 401 and 403 error responses.
  given: $.paths[*][*].responses
  name: seismic-error-responses
  severity: warn
- description: Operations should define 429 Too Many Requests response.
  given: $.paths[*][*].responses
  name: seismic-rate-limit-response
  severity: info
- description: API info must include contact information.
  given: $.info
  name: seismic-info-contact
  severity: warn
- description: API info must include license information.
  given: $.info
  name: seismic-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: seismic-server-https
  severity: error
- description: Operations must include at least one tag.
  given: $.paths[*][*].tags
  name: seismic-tags-required
  severity: warn
- description: API should define reusable schemas in components.
  given: $
  name: seismic-components-schemas-defined
  severity: info
rules_file: rules/seismic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/rules/seismic-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 3
  warn: 8
slug: seismic-rules
source_filename: seismic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Seismic API Naming Conventions\n  seismic-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*(\\\\s([A-Za-z][a-z]*|[A-Z]+))*)(\\\\s([A-Z][a-z]*(\\\\s([A-Za-z][a-z]*|[A-Z]+))*))*$\"\n\n  seismic-no-provider-prefix-in-summary:\n    description: Operation summaries must not start with the provider name.\n    message: \"Summary '{{value}}' must not start with 'Seismic'.\"\n    severity: error\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^Seismic\\\\s\"\n\n  seismic-operationid-camelcase:\n    description: OperationId must be camelCase.\n    message: \"OperationId '{{value}}' must be camelCase.\"\n    severity: warn\n    given: \"\
  $.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  seismic-paths-kebab-case:\n    description: Path segments must use kebab-case.\n    message: \"Path '{{path}}' segments must use kebab-case.\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z][a-z0-9\\\\-]*(\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})?)*$\"\n\n  seismic-bearer-auth-required:\n    description: All operations must use bearerAuth security.\n    message: \"Operation must define security with bearerAuth.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  seismic-pagination-offset-limit:\n    description: List operations should support offset and limit pagination.\n    message: \"GET list operations should include offset and limit query parameters.\"\n    severity: info\n    given: \"$.paths[*].get\"\n   \
  \ then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  seismic-response-200-content:\n    description: GET operations must define a 200 response with content.\n    message: \"GET operation must have a 200 response with application/json content.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  seismic-error-responses:\n    description: Operations should define 401 and 403 error responses.\n    message: \"Operations should define 401 Unauthorized and 403 Forbidden responses.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"401\"\n            - \"403\"\n\n  seismic-rate-limit-response:\n    description: Operations should define 429 Too Many Requests response.\n    message: \"Operations should define 429 Too Many Requests\
  \ response for rate limiting.\"\n    severity: info\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - \"429\"\n\n  seismic-info-contact:\n    description: API info must include contact information.\n    message: \"API info.contact must be defined with name, url, and email.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  seismic-info-license:\n    description: API info must include license information.\n    message: \"API info.license must be defined.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: defined\n\n  seismic-server-https:\n    description: All server URLs must use HTTPS.\n    message: \"Server URL '{{value}}' must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n      \
  \  match: \"^https://\"\n\n  seismic-tags-required:\n    description: Operations must include at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*].tags\"\n    then:\n      function: length\n      functionOptions:\n        min: 1\n\n  seismic-components-schemas-defined:\n    description: API should define reusable schemas in components.\n    message: \"API should define schemas in components/schemas.\"\n    severity: info\n    given: \"$\"\n    then:\n      field: \"components.schemas\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/seismic/refs/heads/main/rules/seismic-rules.yml
tags:
- Spectral
- Linting
- API Governance
---

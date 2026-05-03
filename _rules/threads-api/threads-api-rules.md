---
api_specs:
- filename: threads-api-openapi.yml
  format: yaml
  label: Threads API
  slug: threads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/threads-api/refs/heads/main/openapi/threads-api-openapi.yml
categories:
- threads
description: Spectral linting rules defining API design standards and conventions for Threads.
layout: rules
name: Threads API Rules
provider_name: Threads
provider_slug: threads-api
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: threads-api-operation-summary-title-case
  severity: warn
- description: Operations must use OAuth2 security scheme.
  given: $.components.securitySchemes
  name: threads-api-oauth2-required
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,delete]
  name: threads-api-tag-defined
  severity: error
- description: User-specific endpoints should use /me prefix pattern.
  given: $.paths
  name: threads-api-me-prefix-paths
  severity: info
- description: GET operations retrieving media objects should support fields parameter.
  given: $.paths[*][get].parameters[*]
  name: threads-api-fields-query-param
  severity: warn
- description: All operations must define at least one response.
  given: $.paths[*][*]
  name: threads-api-response-defined
  severity: error
- description: Operation IDs should use camelCase.
  given: $.paths[*][*].operationId
  name: threads-api-operation-id-camel-case
  severity: warn
rules_file: rules/threads-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/threads-api/refs/heads/main/rules/threads-api-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 3
slug: threads-api-rules
source_filename: threads-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Threads API (Meta) specific Spectral rules\n\n  threads-api-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ -][A-Z0-9][a-z0-9]*)*)$\"\n\n  threads-api-oauth2-required:\n    description: Operations must use OAuth2 security scheme.\n    message: \"Threads API operations require OAuth2 authentication.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: oauth2Auth\n      function: truthy\n\n  threads-api-tag-defined:\n    description: All operations must have at least one tag.\n    message: \"Operations must have at least one tag for categorization.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n     \
  \ field: tags\n      function: truthy\n\n  threads-api-me-prefix-paths:\n    description: User-specific endpoints should use /me prefix pattern.\n    message: \"User-specific Threads endpoints should use /me/ path prefix.\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: truthy\n\n  threads-api-fields-query-param:\n    description: GET operations retrieving media objects should support fields parameter.\n    message: \"Threads API GET operations should support fields query parameter for selective field retrieval.\"\n    severity: warn\n    given: \"$.paths[*][get].parameters[*]\"\n    then:\n      function: truthy\n\n  threads-api-response-defined:\n    description: All operations must define at least one response.\n    message: \"Operations must define response schemas.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses\n      function: truthy\n\n  threads-api-operation-id-camel-case:\n    description: Operation IDs should use\
  \ camelCase.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/threads-api/refs/heads/main/rules/threads-api-rules.yml
tags:
- Social
- Social Networks
- Meta
- Publishing
- Media
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: trelica-rest-api-openapi.yml
  format: yaml
  label: Trelica REST API
  slug: trelica
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trelica/refs/heads/main/openapi/trelica-rest-api-openapi.yml
categories:
- trelica
description: Spectral linting rules defining API design standards and conventions for Trelica.
layout: rules
name: Trelica API Rules
provider_name: Trelica
provider_slug: trelica
rule_count: 13
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: trelica-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trelica-operation-summary-title-case
  severity: warn
- description: List operations should support cursor-based pagination with 'after' parameter
  given: $.paths[*].get
  name: trelica-pagination-cursor-pattern
  severity: info
- description: List operations should include a limit parameter
  given: $.paths[*].get.parameters[*]
  name: trelica-limit-parameter
  severity: info
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: trelica-security-defined
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: trelica-response-200-defined
  severity: error
- description: Operations using OAuth must define a 401 response
  given: $.paths[*][get,post,put,patch,delete]
  name: trelica-response-401-defined
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: trelica-tag-defined
  severity: warn
- description: API paths must use kebab-case
  given: $.paths[*]~
  name: trelica-path-kebab-case
  severity: warn
- description: API paths should include a version segment (v1, v2, etc.)
  given: $.paths[*]~
  name: trelica-versioned-paths
  severity: warn
- description: SCIM endpoints use startIndex/count pagination, not cursor-based
  given: $.paths['/scim/v2/Users'].get
  name: trelica-scim-users-separate-pagination
  severity: info
- description: POST operations should define a request body
  given: $.paths[*].post
  name: trelica-request-body-post
  severity: warn
- description: The 'since' filter parameter should be ISO 8601 date-time format
  given: $.paths[*][*].parameters[?(@.name=='since')].schema
  name: trelica-since-filter-datetime
  severity: info
rules_file: rules/trelica-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trelica/refs/heads/main/rules/trelica-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 4
  warn: 7
slug: trelica-spectral-rules
source_filename: trelica-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  trelica-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trelica-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ()-]*$\"\n\n  trelica-pagination-cursor-pattern:\n    description: List operations should support cursor-based pagination with 'after' parameter\n    message: \"List operations should include 'after' pagination cursor parameter\"\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n\
  \          properties:\n            parameters:\n              type: array\n\n  trelica-limit-parameter:\n    description: List operations should include a limit parameter\n    message: \"List endpoints should support a 'limit' query parameter\"\n    severity: info\n    given: \"$.paths[*].get.parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  trelica-security-defined:\n    description: All operations must define security requirements\n    message: \"Operation '{{path}}' must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  trelica-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: \"GET operation must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n\
  \  trelica-response-401-defined:\n    description: Operations using OAuth must define a 401 response\n    message: \"Authenticated operation should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: defined\n\n  trelica-tag-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  trelica-path-kebab-case:\n    description: API paths must use kebab-case\n    message: \"Path '{{path}}' should use kebab-case segments\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-z0-9-]*(/[a-z0-9][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)+$\"\n\n  trelica-versioned-paths:\n    description: API paths\
  \ should include a version segment (v1, v2, etc.)\n    message: \"Path '{{path}}' should include a version segment\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z]+/v[0-9]\"\n\n  trelica-scim-users-separate-pagination:\n    description: SCIM endpoints use startIndex/count pagination, not cursor-based\n    message: \"SCIM endpoints use startIndex and count parameters\"\n    severity: info\n    given: \"$.paths['/scim/v2/Users'].get\"\n    then:\n      function: defined\n\n  trelica-request-body-post:\n    description: POST operations should define a request body\n    message: \"POST operation should include a requestBody\"\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  trelica-since-filter-datetime:\n    description: The 'since' filter parameter should be ISO 8601 date-time format\n    message: \"Parameter 'since' should use format:\
  \ date-time\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name=='since')].schema\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - date-time\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trelica/refs/heads/main/rules/trelica-spectral-rules.yml
tags:
- Contract Management
- IT Management
- License Management
- SaaS Management
- Software Asset Management
- Spectral
- Linting
- API Governance
---

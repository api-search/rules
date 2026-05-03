---
api_specs:
- filename: swetrix-events-api-openapi.yml
  format: yaml
  label: Swetrix Events API
  slug: swetrix-events-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-events-api-openapi.yml
- filename: swetrix-statistics-api-openapi.yml
  format: yaml
  label: Swetrix Statistics API
  slug: swetrix-statistics-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-statistics-api-openapi.yml
- filename: swetrix-admin-api-openapi.yml
  format: yaml
  label: Swetrix Admin API
  slug: swetrix-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-admin-api-openapi.yml
categories:
- swetrix
description: Spectral linting rules defining API design standards and conventions for Swetrix.
layout: rules
name: Swetrix API Rules
provider_name: Swetrix
provider_slug: swetrix
rule_count: 9
rules:
- description: Admin and Statistics API endpoints must use X-Api-Key security scheme
  given: $.components.securitySchemes
  name: swetrix-api-key-header
  severity: warn
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][get,post,put,patch,delete]
  name: swetrix-operation-id-camel-case
  severity: warn
- description: Events API paths should use /log prefix
  given: $.paths
  name: swetrix-events-path-prefix
  severity: hint
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: swetrix-summary-title-case
  severity: warn
- description: POST operations must define a requestBody
  given: $.paths[*].post
  name: swetrix-post-request-body
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: swetrix-operation-tags
  severity: warn
- description: The pid parameter must be marked as required
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'pid')]
  name: swetrix-pid-required
  severity: error
- description: Mutating operations should document 400 error responses
  given: $.paths[*][post,put,patch].responses
  name: swetrix-error-responses
  severity: warn
- description: Success responses (200/201) should define content schema
  given: $.paths[*][get,post,put,patch].responses[200,201]
  name: swetrix-success-response-content
  severity: warn
rules_file: rules/swetrix-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/rules/swetrix-rules.yml
severity_counts:
  error: 2
  hint: 1
  info: 0
  warn: 6
slug: swetrix-rules
source_filename: swetrix-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n  # Swetrix uses X-Api-Key header authentication for admin/statistics APIs\n  swetrix-api-key-header:\n    description: Admin and Statistics API endpoints must use X-Api-Key security scheme\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: ApiKeyAuth\n      function: truthy\n\n  # All operation IDs must use camelCase\n  swetrix-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Events API uses /log prefix for all paths\n  swetrix-events-path-prefix:\n    description: Events API paths should use /log prefix\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\
  \n  # All operations must have summaries in Title Case\n  swetrix-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # Request bodies for POST operations must be defined\n  swetrix-post-request-body:\n    description: POST operations must define a requestBody\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  # Tags must be defined at operation level\n  swetrix-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # pid parameter must be required when present\n  swetrix-pid-required:\n    description: The pid parameter must be marked as required\n    severity:\
  \ error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'pid')]\"\n    then:\n      field: required\n      function: truthy\n\n  # Responses must include 400 for POST/PUT/PATCH\n  swetrix-error-responses:\n    description: Mutating operations should document 400 error responses\n    severity: warn\n    given: \"$.paths[*][post,put,patch].responses\"\n    then:\n      field: '400'\n      function: truthy\n\n  # Successful responses must have content defined\n  swetrix-success-response-content:\n    description: Success responses (200/201) should define content schema\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses[200,201]\"\n    then:\n      field: content\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/rules/swetrix-rules.yml
tags:
- Analytics
- Cookieless Tracking
- GDPR Compliant
- Open Source
- Privacy
- Real-Time Analytics
- Web Analytics
- Spectral
- Linting
- API Governance
---

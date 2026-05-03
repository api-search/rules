---
api_specs:
- filename: unleash-admin-api-openapi.yml
  format: yaml
  label: Unleash Admin API
  slug: admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unleash/refs/heads/main/openapi/unleash-admin-api-openapi.yml
- filename: unleash-client-api-openapi.yml
  format: yaml
  label: Unleash Client API
  slug: client-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unleash/refs/heads/main/openapi/unleash-client-api-openapi.yml
- filename: unleash-frontend-api-openapi.yml
  format: yaml
  label: Unleash Frontend API
  slug: frontend-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/unleash/refs/heads/main/openapi/unleash-frontend-api-openapi.yml
categories:
- unleash
description: Spectral linting rules defining API design standards and conventions for Unleash.
layout: rules
name: Unleash API Rules
provider_name: Unleash
provider_slug: unleash
rule_count: 8
rules:
- description: Admin API paths must start with /api/admin/
  given: $.paths[*]~
  name: unleash-admin-path-prefix
  severity: info
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: unleash-title-case-summary
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: unleash-operation-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][*]
  name: unleash-operation-id
  severity: error
- description: Admin API operations must require Authorization header
  given: $.paths[/api/admin*][*]
  name: unleash-auth-header
  severity: info
- description: Feature flag paths should be scoped under /projects/{projectId}/
  given: $.paths[/api/admin/features*]~
  name: unleash-feature-project-scope
  severity: info
- description: Resource endpoints should define 404 responses
  given: $.paths[*][get,delete,put,patch]
  name: unleash-not-found-response
  severity: warn
- description: Protected operations should define 401 responses
  given: $.paths[/api/admin*][*]
  name: unleash-unauthorized-response
  severity: warn
rules_file: rules/unleash-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/unleash/refs/heads/main/rules/unleash-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 3
  warn: 4
slug: unleash-rules
source_filename: unleash-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n\n  # Unleash Admin API paths use kebab-case prefixed with /api/admin/\n  unleash-admin-path-prefix:\n    description: Admin API paths must start with /api/admin/\n    message: \"Path '{{path}}' should be prefixed with /api/admin/\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/(admin|client|frontend)\"\n\n  # Operation summaries must be Title Case\n  unleash-title-case-summary:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operations must have tags for grouping\n  unleash-operation-tags:\n    description: All operations must have at least one tag\n    message: \"{{description}}: {{path}}\"\n    severity: warn\n    given: \"$.paths[*][*]\"\
  \n    then:\n      field: tags\n      function: truthy\n\n  # All operations must have operationIds\n  unleash-operation-id:\n    description: All operations must have an operationId\n    message: \"Operation at {{path}} missing operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Authorization header for admin API operations\n  unleash-auth-header:\n    description: Admin API operations must require Authorization header\n    message: \"Admin operation may require Authorization header parameter\"\n    severity: info\n    given: \"$.paths[/api/admin*][*]\"\n    then:\n      field: security\n      function: defined\n\n  # Features paths use project-scoped routes\n  unleash-feature-project-scope:\n    description: Feature flag paths should be scoped under /projects/{projectId}/\n    message: \"Feature path should be scoped: /api/admin/projects/{projectId}/features\"\n    severity: info\n    given: \"$.paths[/api/admin/features*]~\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^/api/admin/features\"\n\n  # 404 responses for resource paths\n  unleash-not-found-response:\n    description: Resource endpoints should define 404 responses\n    message: \"Missing 404 response for resource operation\"\n    severity: warn\n    given: \"$.paths[*][get,delete,put,patch]\"\n    then:\n      field: \"responses.404\"\n      function: defined\n\n  # 401 for unauthenticated requests\n  unleash-unauthorized-response:\n    description: Protected operations should define 401 responses\n    message: \"Protected operation should define 401 response\"\n    severity: warn\n    given: \"$.paths[/api/admin*][*]\"\n    then:\n      field: \"responses.401\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/unleash/refs/heads/main/rules/unleash-rules.yml
tags:
- Feature Flags
- Feature Management
- Progressive Delivery
- A/B Testing
- Open Source
- Developer Tools
- Spectral
- Linting
- API Governance
---

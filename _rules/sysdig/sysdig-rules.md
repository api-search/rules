---
api_specs:
- filename: sysdig-monitor-openapi.yml
  format: yaml
  label: Sysdig Monitor
  slug: sysdig-monitor
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sysdig/refs/heads/main/openapi/sysdig-monitor-openapi.yml
- filename: sysdig-secure-openapi.yml
  format: yaml
  label: Sysdig Secure
  slug: sysdig-secure
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sysdig/refs/heads/main/openapi/sysdig-secure-openapi.yml
categories:
- sysdig
description: Spectral linting rules defining API design standards and conventions for Sysdig.
layout: rules
name: Sysdig API Rules
provider_name: Sysdig
provider_slug: sysdig
rule_count: 10
rules:
- description: All operations must have an operationId defined.
  given: $.paths[*][get,post,put,delete,patch]
  name: sysdig-operation-ids-required
  severity: error
- description: All operations must have a summary.
  given: $.paths[*][get,post,put,delete,patch]
  name: sysdig-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,delete,patch].summary
  name: sysdig-operation-summary-title-case
  severity: warn
- description: API must define Bearer token authentication.
  given: $.components.securitySchemes
  name: sysdig-bearer-auth-required
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,delete,patch]
  name: sysdig-tags-defined
  severity: warn
- description: GET operations must have a 200 response.
  given: $.paths[*].get
  name: sysdig-responses-200-defined
  severity: error
- description: Operations should define 401 or error responses.
  given: $.paths[*][post,put,delete]
  name: sysdig-error-responses-defined
  severity: warn
- description: POST operations should have a request body.
  given: $.paths[*].post
  name: sysdig-request-body-post
  severity: warn
- description: API paths should include a version prefix (/api/v1/, /api/v2/, /api/v3/).
  given: $.paths[*]~
  name: sysdig-path-versioned
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: sysdig-schema-descriptions
  severity: info
rules_file: rules/sysdig-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sysdig/refs/heads/main/rules/sysdig-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: sysdig-rules
source_filename: sysdig-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  sysdig-operation-ids-required:\n    description: All operations must have an operationId defined.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sysdig-operation-summary-required:\n    description: All operations must have a summary.\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  sysdig-operation-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-z]*(\\\\s[A-Z][a-z]*)*$\"\n\n  sysdig-bearer-auth-required:\n    description: API must define Bearer token authentication.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  sysdig-tags-defined:\n    description: All operations must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  sysdig-responses-200-defined:\n    description: GET operations must have a 200 response.\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  sysdig-error-responses-defined:\n    description: Operations should define 401 or error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,delete]\"\n    then:\n      field: responses\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 2\n\n  sysdig-request-body-post:\n    description: POST operations should have a request body.\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n     \
  \ field: requestBody\n      function: truthy\n\n  sysdig-path-versioned:\n    description: API paths should include a version prefix (/api/v1/, /api/v2/, /api/v3/).\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/(v[0-9]+|scanning|secure|compliance|notificationChannels)\"\n\n  sysdig-schema-descriptions:\n    description: Schema properties should have descriptions.\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sysdig/refs/heads/main/rules/sysdig-rules.yml
tags:
- Cloud Security
- Containers
- Kubernetes
- Runtime Security
- Security
- Vulnerability Management
- Monitoring
- Observability
- CSPM
- Compliance
- Spectral
- Linting
- API Governance
---

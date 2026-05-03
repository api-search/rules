---
api_specs:
- filename: client-server
  format: yaml
  label: Synapse Client-Server API
  slug: synapse-client-server-api
  spec_type: OpenAPI
  url: https://github.com/matrix-org/matrix-spec/tree/main/data/api/client-server
- filename: server-server
  format: yaml
  label: Synapse Server-Server API
  slug: synapse-server-server-api
  spec_type: OpenAPI
  url: https://github.com/matrix-org/matrix-spec/tree/main/data/api/server-server
- filename: synapse-admin-api-openapi.yml
  format: yaml
  label: Synapse Admin API
  slug: synapse-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/synapse/refs/heads/main/openapi/synapse-admin-api-openapi.yml
categories:
- synapse
description: Spectral linting rules defining API design standards and conventions for Synapse.
layout: rules
name: Synapse API Rules
provider_name: Synapse
provider_slug: synapse
rule_count: 8
rules:
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: synapse-operation-summary-title-case
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: synapse-operation-has-operation-id
  severity: error
- description: Admin API paths should be prefixed with /v1/ or /v2/
  given: $.paths
  name: synapse-matrix-path-prefix
  severity: warn
- description: All Admin API operations require Bearer token authentication
  given: $.paths[*][get,post,put,delete,patch]
  name: synapse-bearer-auth-required
  severity: warn
- description: Operations should define error responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: synapse-error-response-defined
  severity: warn
- description: Matrix user IDs should follow @localpart:domain format
  given: $.components.schemas.*.properties.name
  name: synapse-matrix-user-id-format
  severity: hint
- description: List operations should support pagination parameters
  given: $.paths[*][get].parameters[?(@.name == 'limit')]
  name: synapse-pagination-token
  severity: hint
- description: All operations must define a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: synapse-response-200-defined
  severity: error
rules_file: rules/synapse-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/synapse/refs/heads/main/rules/synapse-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 4
slug: synapse-rules
source_filename: synapse-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  synapse-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  synapse-operation-has-operation-id:\n    description: All operations must have an operationId\n    message: Operation is missing operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  synapse-matrix-path-prefix:\n    description: Admin API paths should be prefixed with /v1/ or /v2/\n    message: \"Path '{{property}}' should start with a version prefix (e.g. /v1/)\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/v[0-9]\"\n\n  synapse-bearer-auth-required:\n\
  \    description: All Admin API operations require Bearer token authentication\n    message: Operation should reference BearerAuth security scheme\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"security\"]\n            - type: object\n\n  synapse-error-response-defined:\n    description: Operations should define error responses\n    message: Operation is missing error response definitions\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n\n  synapse-matrix-user-id-format:\n    description: Matrix user IDs should follow @localpart:domain format\n    message: User ID parameters\
  \ should document Matrix user ID format\n    severity: hint\n    given: \"$.components.schemas.*.properties.name\"\n    then:\n      field: description\n      function: truthy\n\n  synapse-pagination-token:\n    description: List operations should support pagination parameters\n    message: List operations should include limit and from pagination parameters\n    severity: hint\n    given: \"$.paths[*][get].parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema\n      function: truthy\n\n  synapse-response-200-defined:\n    description: All operations must define a success response\n    message: Operation is missing a success response\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/synapse/refs/heads/main/rules/synapse-rules.yml
tags:
- Chat
- Collaboration
- Decentralized
- Federation
- Matrix
- Messaging
- Open-Source
- Real-Time
- Spectral
- Linting
- API Governance
---

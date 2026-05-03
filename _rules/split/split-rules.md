---
api_specs:
- filename: split-admin-api-openapi.yml
  format: yaml
  label: Split Admin API
  slug: split-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/split/refs/heads/main/openapi/split-admin-api-openapi.yml
- filename: split-feature-flag-api-openapi.yml
  format: yaml
  label: Split Feature Flag API
  slug: split-feature-flag-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/split/refs/heads/main/openapi/split-feature-flag-api-openapi.yml
- filename: split-evaluator-api-openapi.yml
  format: yaml
  label: Split Evaluator API
  slug: split-evaluator-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/split/refs/heads/main/openapi/split-evaluator-api-openapi.yml
categories:
- split
description: Spectral linting rules defining API design standards and conventions for Split.
layout: rules
name: Split API Rules
provider_name: Split
provider_slug: split
rule_count: 11
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: split-operation-id-required
  severity: error
- description: operationId must start with a standard REST verb.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: split-operation-id-verb-prefix
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: split-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: split-tags-required
  severity: warn
- description: Operations must use bearerAuth security scheme.
  given: $.components.securitySchemes
  name: split-bearer-auth-required
  severity: error
- description: Every operation must define a 200 or 201 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: split-response-200-required
  severity: error
- description: Every operation must define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: split-401-response-required
  severity: warn
- description: List operations should support limit and offset query parameters.
  given: $.paths[*].get.operationId
  name: split-pagination-params
  severity: info
- description: Workspace-scoped paths must use workspaceId path parameter.
  given: $.paths[~/ws/{workspaceId}]
  name: split-workspace-id-path-param
  severity: info
- description: The API must define at least one server.
  given: $
  name: split-servers-required
  severity: error
- description: The info object must include a contact entry.
  given: $.info
  name: split-info-contact-required
  severity: warn
rules_file: rules/split-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/split/refs/heads/main/rules/split-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 5
slug: split-rules
source_filename: split-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  split-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  split-operation-id-verb-prefix:\n    description: operationId must start with a standard REST verb.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(get|list|create|update|delete|enable|restore|kill|add|remove|upload|approve|deactivate|invite|track)[A-Z][a-zA-Z0-9]+$\"\n\n  split-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /()-]+$\"\n\n  split-tags-required:\n  \
  \  description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  split-bearer-auth-required:\n    description: Operations must use bearerAuth security scheme.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  split-response-200-required:\n    description: Every operation must define a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  split-401-response-required:\n    description: Every operation must define a 401 Unauthorized response.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          required: [\"401\"]\n\n  split-pagination-params:\n    description: List operations should support limit and offset query parameters.\n    severity: info\n    given: \"$.paths[*].get.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^list\"\n\n  split-workspace-id-path-param:\n    description: Workspace-scoped paths must use workspaceId path parameter.\n    severity: info\n    given: \"$.paths[~/ws/{workspaceId}]\"\n    then:\n      function: truthy\n\n  split-servers-required:\n    description: The API must define at least one server.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  split-info-contact-required:\n    description: The info object must include a contact entry.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/split/refs/heads/main/rules/split-rules.yml
tags:
- Experimentation
- Feature Flags
- Feature Management
- Rollouts
- SDKs
- Spectral
- Linting
- API Governance
---

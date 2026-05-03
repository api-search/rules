---
api_specs:
- filename: spire-workload-asyncapi.yml
  format: yaml
  label: SPIRE Workload API
  slug: spire-workload-api
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/asyncapi/spire-workload-asyncapi.yml
- filename: spire-health-openapi.yml
  format: yaml
  label: SPIRE Agent API
  slug: spire-agent-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/openapi/spire-health-openapi.yml
- filename: spire-oidc-discovery-openapi.yml
  format: yaml
  label: SPIRE OIDC Discovery API
  slug: spire-oidc-discovery-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/openapi/spire-oidc-discovery-openapi.yml
categories:
- spire
description: Spectral linting rules defining API design standards and conventions for SPIRE.
layout: rules
name: SPIRE API Rules
provider_name: SPIRE
provider_slug: spire
rule_count: 9
rules:
- description: All operations must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: spire-operation-id-required
  severity: error
- description: operationId must use camelCase starting with a verb (get, list, create, update, delete, enable, restore, kill).
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: spire-operation-id-kebab-case
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: spire-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: spire-tags-required
  severity: warn
- description: Every operation must define a 200 or 201 success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: spire-response-200-required
  severity: error
- description: The API must define at least one server.
  given: $
  name: spire-servers-required
  severity: error
- description: The info object must include a contact entry.
  given: $.info
  name: spire-info-contact-required
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths
  name: spire-no-trailing-slash
  severity: warn
- description: Health check paths should follow the /live or /ready convention.
  given: $.paths
  name: spire-health-path-naming
  severity: info
rules_file: rules/spire-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/rules/spire-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 5
slug: spire-rules
source_filename: spire-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  spire-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete,head,options]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spire-operation-id-kebab-case:\n    description: operationId must use camelCase starting with a verb (get, list, create, update, delete, enable, restore, kill).\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(get|list|create|update|delete|enable|restore|kill|add|remove|upload|approve|deactivate|invite|track)[A-Z][a-zA-Z0-9]+$\"\n\n  spire-summary-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match:\
  \ \"^[A-Z][a-zA-Z0-9 /-]+$\"\n\n  spire-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  spire-response-200-required:\n    description: Every operation must define a 200 or 201 success response.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  spire-servers-required:\n    description: The API must define at least one server.\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  spire-info-contact-required:\n    description: The info object must include a contact entry.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  spire-no-trailing-slash:\n\
  \    description: Paths must not have a trailing slash.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  spire-health-path-naming:\n    description: Health check paths should follow the /live or /ready convention.\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/live|/ready|/.well-known|/keys|/admin|/client)\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spire/refs/heads/main/rules/spire-rules.yml
tags:
- Authentication
- Cloud Native
- Graduated
- Identity
- Security
- Zero Trust
- Spectral
- Linting
- API Governance
---

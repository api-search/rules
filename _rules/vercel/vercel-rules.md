---
api_specs:
- filename: openapi.yaml
  format: yaml
  label: Vercel REST API
  slug: vercel-rest-api
  spec_type: OpenAPI
  url: https://openapi.vercel.sh/
- filename: vercel-ai-gateway-openapi.yml
  format: yaml
  label: Vercel AI Gateway API
  slug: vercel-ai-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vercel/refs/heads/main/openapi/vercel-ai-gateway-openapi.yml
- filename: vercel-v0-platform-openapi.yml
  format: yaml
  label: V0 Platform API
  slug: v0-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vercel/refs/heads/main/openapi/vercel-v0-platform-openapi.yml
categories:
- vercel
description: Spectral linting rules defining API design standards and conventions for Vercel.
layout: rules
name: Vercel API Rules
provider_name: Vercel
provider_slug: vercel
rule_count: 11
rules:
- description: Vercel APIs must use Bearer token authentication
  given: $.components.securitySchemes[*]
  name: vercel-bearer-auth
  severity: error
- description: All operations must define an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: vercel-operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: vercel-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: vercel-summary-title-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: vercel-summary-required
  severity: error
- description: AI Gateway paths must use /v1/ prefix
  given: $.paths[*]~
  name: vercel-ai-gateway-path-version
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: vercel-401-response
  severity: error
- description: Operations should document 429 rate limit response
  given: $.paths[*][post].responses
  name: vercel-429-response
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: vercel-path-kebab-case
  severity: warn
- description: API info must include contact information
  given: $.info
  name: vercel-info-contact
  severity: warn
- description: API must define server URLs
  given: $
  name: vercel-servers-defined
  severity: error
rules_file: rules/vercel-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vercel/refs/heads/main/rules/vercel-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 6
slug: vercel-rules
source_filename: vercel-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Vercel APIs use Bearer token authentication\n  vercel-bearer-auth:\n    description: Vercel APIs must use Bearer token authentication\n    message: Security scheme must use Bearer scheme\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: \"^bearer$\"\n\n  # All operations must have operationId\n  vercel-operation-id-required:\n    description: All operations must define an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # operationId should be camelCase\n  vercel-operation-id-camel-case:\n    description: operationId should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Summaries must be Title Case\n  vercel-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # All operations need summaries\n  vercel-summary-required:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # API Gateway endpoints use /v1/ prefix\n  vercel-ai-gateway-path-version:\n    description: AI Gateway paths must use /v1/ prefix\n    message: \"Path '{{value}}' must start with /v1/\"\n    severity: warn\n    given:\
  \ \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  # Must define 401 response\n  vercel-401-response:\n    description: All operations must document 401 Unauthorized response\n    message: Operation must define a 401 response\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  # Must define 429 rate limit response for AI APIs\n  vercel-429-response:\n    description: Operations should document 429 rate limit response\n    message: Operation should define a 429 Too Many Requests response\n    severity: warn\n    given: \"$.paths[*][post].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  # Use kebab-case for path segments\n  vercel-path-kebab-case:\n    description: Path segments should use kebab-case\n    message: \"Path segment should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n\
  \      function: pattern\n      functionOptions:\n        match: \"^(/v[0-9]+)?(/[a-z0-9-]+(/{[a-zA-Z]+})?)*$\"\n\n  # Contact info required\n  vercel-info-contact:\n    description: API info must include contact information\n    message: API info must include contact details\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  # Servers must be defined\n  vercel-servers-defined:\n    description: API must define server URLs\n    message: API must define at least one server\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vercel/refs/heads/main/rules/vercel-rules.yml
tags:
- AI Gateways
- Gateways
- Observability
- Spectral
- Linting
- API Governance
---

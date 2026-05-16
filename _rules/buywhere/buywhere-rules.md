---
api_specs:
- filename: buywhere-openapi.yml
  format: yaml
  label: BuyWhere Product Catalog API
  slug: product-catalog-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/buywhere/refs/heads/main/openapi/buywhere-openapi.yml
categories:
- buywhere
description: Spectral linting rules defining API design standards and conventions for BuyWhere.
layout: rules
name: BuyWhere API Rules
provider_name: BuyWhere
provider_slug: buywhere
rule_count: 14
rules:
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,put,post,delete,patch].summary
  name: buywhere-summary-title-case
  severity: warn
- description: operationId should be lowerCamelCase verbNoun.
  given: $.paths[*][get,put,post,delete,patch].operationId
  name: buywhere-operation-id-camelcase
  severity: error
- description: All operations must have an operationId.
  given: $.paths[*][get,put,post,delete,patch]
  name: buywhere-operation-id-required
  severity: error
- description: Every operation must be tagged for Documentation grouping.
  given: $.paths[*][get,put,post,delete,patch]
  name: buywhere-operation-tagged
  severity: warn
- description: Path segments should be lowercase kebab-case (allows {paramName}).
  given: $.paths
  name: buywhere-paths-kebab-case
  severity: warn
- description: Server URLs must include a version segment (e.g. /v1).
  given: $.servers[*].url
  name: buywhere-server-url-versioned
  severity: error
- description: Non-auth operations must require BearerAuth security.
  given: $.paths[?(@property != '/auth/register' && @property != '/auth')][get,put,post,delete,patch]
  name: buywhere-bearer-required
  severity: warn
- description: Product `id` path parameters must be format uuid.
  given: $.paths[*][get,put,post,delete,patch].parameters[?(@.in=='path' && @.name=='id')].schema
  name: buywhere-product-id-uuid
  severity: warn
- description: limit parameters should declare a maximum.
  given: $.paths[*][get].parameters[?(@.name=='limit')].schema
  name: buywhere-limit-bounded
  severity: warn
- description: Currency parameter examples should be in the supported set (SGD, USD, VND, THB, MYR).
  given: $.paths[*][get].parameters[?(@.name=='currency')].schema.default
  name: buywhere-currency-enum
  severity: info
- description: Authenticated operations must document a 401 response.
  given: $.paths[?(@property != '/auth/register' && @property != '/auth')][get,put,post,delete,patch].responses
  name: buywhere-401-response
  severity: warn
- description: Search endpoints must document a 429 (rate limit) response.
  given: $.paths['/products/search'][get].responses
  name: buywhere-429-on-search
  severity: warn
- description: API info must include contact email.
  given: $.info.contact
  name: buywhere-info-contact
  severity: warn
- description: API should reference MCP / external documentation.
  given: $
  name: buywhere-external-docs
  severity: info
rules_file: rules/buywhere-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/buywhere/refs/heads/main/rules/buywhere-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 2
  warn: 9
slug: buywhere-rules
source_filename: buywhere-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nfunctions: []\n\nrules:\n  # Style\n  buywhere-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Operation summary should use Title Case: {{value}}\"\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z0-9][A-Za-z0-9-]*)([ /-][A-Z0-9][A-Za-z0-9-]*)*( By [A-Z][A-Za-z]*)?$\"\n\n  buywhere-operation-id-camelcase:\n    description: operationId should be lowerCamelCase verbNoun.\n    message: \"operationId should be lowerCamelCase: {{value}}\"\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  buywhere-operation-id-required:\n    description: All operations must have an operationId.\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch]\"\
  \n    then:\n      field: operationId\n      function: truthy\n\n  buywhere-operation-tagged:\n    description: Every operation must be tagged for Documentation grouping.\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  buywhere-paths-kebab-case:\n    description: Path segments should be lowercase kebab-case (allows {paramName}).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9{}\\\\-/_]*$\"\n      field: \"@key\"\n\n  buywhere-server-url-versioned:\n    description: Server URLs must include a version segment (e.g. /v1).\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v[0-9]+(/|$)\"\n\n  buywhere-bearer-required:\n    description: Non-auth operations must require BearerAuth security.\n    severity: warn\n    given: \"$.paths[?(@property !=\
  \ '/auth/register' && @property != '/auth')][get,put,post,delete,patch]\"\n    then:\n      field: security\n      function: truthy\n\n  buywhere-product-id-uuid:\n    description: Product `id` path parameters must be format uuid.\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch].parameters[?(@.in=='path' && @.name=='id')].schema\"\n    then:\n      field: format\n      function: pattern\n      functionOptions:\n        match: \"^uuid$\"\n\n  buywhere-limit-bounded:\n    description: limit parameters should declare a maximum.\n    severity: warn\n    given: \"$.paths[*][get].parameters[?(@.name=='limit')].schema\"\n    then:\n      field: maximum\n      function: truthy\n\n  buywhere-currency-enum:\n    description: Currency parameter examples should be in the supported set (SGD, USD, VND, THB, MYR).\n    severity: info\n    given: \"$.paths[*][get].parameters[?(@.name=='currency')].schema.default\"\n    then:\n      function: enumeration\n      functionOptions:\n\
  \        values: [\"SGD\", \"USD\", \"VND\", \"THB\", \"MYR\"]\n\n  buywhere-401-response:\n    description: Authenticated operations must document a 401 response.\n    severity: warn\n    given: \"$.paths[?(@property != '/auth/register' && @property != '/auth')][get,put,post,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: truthy\n\n  buywhere-429-on-search:\n    description: Search endpoints must document a 429 (rate limit) response.\n    severity: warn\n    given: \"$.paths['/products/search'][get].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n\n  buywhere-info-contact:\n    description: API info must include contact email.\n    severity: warn\n    given: \"$.info.contact\"\n    then:\n      field: email\n      function: truthy\n\n  buywhere-external-docs:\n    description: API should reference MCP / external documentation.\n    severity: info\n    given: \"$\"\n    then:\n      field: externalDocs\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/buywhere/refs/heads/main/rules/buywhere-rules.yml
tags:
- E-commerce
- Shopping
- Price Comparison
- SEA
- Southeast Asia
- AI Agents
- Product Catalog
- Spectral
- Linting
- API Governance
---

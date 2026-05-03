---
api_specs:
- filename: shopify-api-openapi.yml
  format: yaml
  label: Shopify Admin REST API
  slug: shopify-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/openapi/shopify-api-openapi.yml
- filename: shopify-ajax-api-openapi.yml
  format: yaml
  label: Shopify Ajax API
  slug: ajax-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/openapi/shopify-ajax-api-openapi.yml
- filename: shopify-webhooks-api-openapi.yml
  format: yaml
  label: Shopify Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/openapi/shopify-webhooks-api-openapi.yml
- filename: shopify-multipass-api-openapi.yml
  format: yaml
  label: Shopify Multipass API
  slug: multipass-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/openapi/shopify-multipass-api-openapi.yml
categories:
- shopify
description: Spectral linting rules defining API design standards and conventions for Shopify.
layout: rules
name: Shopify API Rules
provider_name: Shopify
provider_slug: shopify
rule_count: 13
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: shopify-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case or curly-brace parameters (Shopify uses .json suffix)
  given: $.paths
  name: shopify-path-kebab-case
  severity: info
- description: Shopify Admin REST API paths use .json suffix for resource endpoints
  given: $.paths
  name: shopify-path-json-suffix
  severity: info
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: shopify-must-have-summary
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: shopify-must-have-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: shopify-must-have-operation-id
  severity: error
- description: GET operations must return 200 response
  given: $.paths[*].get
  name: shopify-get-must-return-200
  severity: error
- description: Shopify Admin REST API uses X-Shopify-Access-Token header authentication
  given: $.components.securitySchemes[*]
  name: shopify-access-token-auth
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths
  name: shopify-no-trailing-slash
  severity: error
- description: Shopify Admin API servers must include version date in URL
  given: $.servers[*].url
  name: shopify-versioned-api-url
  severity: warn
- description: 200 responses must have content defined
  given: $.paths[*][get,post,put,patch,delete].responses[200]
  name: shopify-response-200-must-have-content
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: shopify-tags-title-case
  severity: warn
- description: Shopify API has rate limits (40 req/min REST, 2 req/sec Burst) - document in description
  given: $.info.description
  name: shopify-rate-limit-awareness
  severity: info
rules_file: rules/shopify-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/rules/shopify-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 4
  warn: 5
slug: shopify-rules
source_filename: shopify-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Shopify API Naming Conventions\n  shopify-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  shopify-path-kebab-case:\n    description: Path segments must use kebab-case or curly-brace parameters (Shopify uses .json suffix)\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_.-]+)+$\"\n\n  shopify-path-json-suffix:\n    description: Shopify Admin REST API paths use .json suffix for resource endpoints\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  shopify-must-have-summary:\n    description: All operations must have a summary\n    severity: error\n\
  \    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  shopify-must-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  shopify-must-have-operation-id:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  shopify-get-must-return-200:\n    description: GET operations must return 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  shopify-access-token-auth:\n    description: Shopify Admin REST API uses X-Shopify-Access-Token header authentication\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n  \
  \    functionOptions:\n        schema:\n          type: object\n\n  shopify-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*/$\"\n\n  shopify-versioned-api-url:\n    description: Shopify Admin API servers must include version date in URL\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*(admin/api/[0-9]{4}-[0-9]{2}|myshopify.com).*\"\n\n  shopify-response-200-must-have-content:\n    description: 200 responses must have content defined\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200]\"\n    then:\n      field: content\n      function: defined\n\n  shopify-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^[A-Z][a-zA-Z ]+$\"\n\n  shopify-rate-limit-awareness:\n    description: Shopify API has rate limits (40 req/min REST, 2 req/sec Burst) - document in description\n    severity: info\n    given: \"$.info.description\"\n    then:\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shopify/refs/heads/main/rules/shopify-rules.yml
tags:
- Commerce
- Ecommerce
- Payments
- Retail
- Shopping Cart
- T1
- Spectral
- Linting
- API Governance
---

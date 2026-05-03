---
api_specs:
- filename: sandp-global-capital-iq-openapi.yml
  format: yaml
  label: S&P Capital IQ API
  slug: sandp-global-capital-iq-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sandp-global/refs/heads/main/openapi/sandp-global-capital-iq-openapi.yml
- filename: sandp-global-commodity-insights-openapi.yml
  format: yaml
  label: S&P Global Commodity Insights API
  slug: sandp-global-commodity-insights-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sandp-global/refs/heads/main/openapi/sandp-global-commodity-insights-openapi.yml
categories:
- sandp
description: Spectral linting rules defining API design standards and conventions for S&P Global.
layout: rules
name: S&P Global API Rules
provider_name: S&P Global
provider_slug: sandp-global
rule_count: 7
rules:
- description: All S&P Global API endpoints must use Bearer token authentication
  given: $.paths[*][*]
  name: sandp-global-bearer-auth-required
  severity: error
- description: All S&P Global API servers must use HTTPS
  given: $.servers[*]
  name: sandp-global-https-only
  severity: error
- description: All S&P Global operations should define a 200 response
  given: $.paths[*][*].responses
  name: sandp-global-response-200-defined
  severity: warn
- description: All operations must have operationId for SDK generation
  given: $.paths[*][*]
  name: sandp-global-operation-ids-required
  severity: error
- description: All operations must have tags for grouping in developer portal
  given: $.paths[*][*]
  name: sandp-global-tags-required
  severity: warn
- description: All operations and parameters must have descriptions
  given: $.paths[*][*]
  name: sandp-global-description-required
  severity: warn
- description: S&P Global APIs use application/json content type
  given: $.paths[*][*].requestBody.content
  name: sandp-global-json-content-type
  severity: warn
rules_file: rules/sandp-global-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sandp-global/refs/heads/main/rules/sandp-global-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: sandp-global-rules
source_filename: sandp-global-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sandp-global-bearer-auth-required:\n    description: All S&P Global API endpoints must use Bearer token authentication\n    message: \"Endpoint {{path}} must use BearerAuth security scheme\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            security:\n              type: array\n          required:\n            - security\n\n  sandp-global-https-only:\n    description: All S&P Global API servers must use HTTPS\n    message: \"Server URL must use HTTPS for S&P Global APIs\"\n    severity: error\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  sandp-global-response-200-defined:\n    description: All S&P Global operations should define a 200 response\n    message: \"Operation {{path}} should define a 200 response\"\n    severity: warn\n    given:\
  \ \"$.paths[*][*].responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  sandp-global-operation-ids-required:\n    description: All operations must have operationId for SDK generation\n    message: \"Operation at {{path}} must have an operationId\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  sandp-global-tags-required:\n    description: All operations must have tags for grouping in developer portal\n    message: \"Operation {{operationId}} must have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  sandp-global-description-required:\n    description: All operations and parameters must have descriptions\n    message: \"{{path}} must have a description\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  sandp-global-json-content-type:\n    description: S&P\
  \ Global APIs use application/json content type\n    message: \"Request/response body at {{path}} should use application/json\"\n    severity: warn\n    given: \"$.paths[*][*].requestBody.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - application/json\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sandp-global/refs/heads/main/rules/sandp-global-rules.yml
tags:
- Financial Data
- Market Intelligence
- Commodity Insights
- Credit Ratings
- Analytics
- Fortune 500
- Enterprise
- Spectral
- Linting
- API Governance
---

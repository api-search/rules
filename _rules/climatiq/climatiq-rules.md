---
categories:
- climatiq
description: Spectral linting rules defining API design standards and conventions for Climatiq.
layout: rules
name: Climatiq API Rules
provider_name: Climatiq
provider_slug: climatiq
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: climatiq-info-contact
  severity: warn
- description: All Climatiq API servers MUST use HTTPS.
  given: $.servers[*].url
  name: climatiq-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: climatiq-operation-id
  severity: error
- description: Operations MUST be tagged for product-domain grouping (Search, Estimate, Travel, Freight, Energy, Computing, Procurement, Autopilot, Classifications, CBAM).
  given: $.paths[*][get,post,put,delete,patch].tags
  name: climatiq-tag-required
  severity: warn
- description: API MUST define a bearer-token security scheme since Climatiq authenticates with API keys passed as Bearer tokens.
  given: $.components.securitySchemes
  name: climatiq-bearer-auth-required
  severity: error
- description: API MUST declare at least one server URL (api.climatiq.io).
  given: $.servers
  name: climatiq-server-url
  severity: error
rules_file: rules/climatiq-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/climatiq/refs/heads/main/rules/climatiq-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: climatiq-rules
tags:
- Carbon Accounting
- Carbon Emissions
- Climate
- Energy
- Environment
- GHG Protocol
- Sustainability
- Spectral
- Linting
- API Governance
---

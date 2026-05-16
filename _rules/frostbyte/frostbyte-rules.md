---
api_specs:
- filename: frostbyte-ip-geolocation-openapi.yml
  format: yaml
  label: Frostbyte IP Geolocation API
  slug: ip-geolocation
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-ip-geolocation-openapi.yml
- filename: frostbyte-crypto-prices-openapi.yml
  format: yaml
  label: Frostbyte Crypto Prices API
  slug: crypto-prices
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-crypto-prices-openapi.yml
- filename: frostbyte-screenshot-openapi.yml
  format: yaml
  label: Frostbyte Screenshot API
  slug: screenshot
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-screenshot-openapi.yml
- filename: frostbyte-dns-lookup-openapi.yml
  format: yaml
  label: Frostbyte DNS Lookup API
  slug: dns-lookup
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-dns-lookup-openapi.yml
- filename: frostbyte-web-scraper-openapi.yml
  format: yaml
  label: Frostbyte Web Scraper API
  slug: web-scraper
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-web-scraper-openapi.yml
- filename: frostbyte-code-execution-openapi.yml
  format: yaml
  label: Frostbyte Code Execution API
  slug: code-execution
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-code-execution-openapi.yml
- filename: frostbyte-agent-gateway-openapi.yml
  format: yaml
  label: Frostbyte Agent Gateway (Full API)
  slug: agent-gateway
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/openapi/frostbyte-agent-gateway-openapi.yml
categories:
- frostbyte
description: Spectral linting rules defining API design standards and conventions for Frostbyte.
layout: rules
name: Frostbyte API Rules
provider_name: Frostbyte
provider_slug: frostbyte
rule_count: 7
rules:
- description: All Frostbyte APIs must declare a contact block pointing at the catalog.
  given: $.info
  name: frostbyte-info-contact
  severity: warn
- description: Info must declare a license.
  given: $.info
  name: frostbyte-info-license
  severity: warn
- description: Specs should declare the production gateway URL.
  given: $.servers[*]
  name: frostbyte-server-production
  severity: warn
- description: Every operation must define a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: frostbyte-operation-summary-required
  severity: warn
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: frostbyte-operation-summary-title-case
  severity: warn
- description: All non-admin paths must be versioned under /v1/ or /api/.
  given: $.paths
  name: frostbyte-path-versioned
  severity: warn
- description: Operations should document the 402 Payment Required response (x402 / USDC on Base).
  given: $.paths[*][get,post,put,patch,delete].responses
  name: frostbyte-credit-aware-402
  severity: info
rules_file: rules/frostbyte-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/rules/frostbyte-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 1
  warn: 6
slug: frostbyte-rules
source_filename: frostbyte-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  frostbyte-info-contact:\n    description: All Frostbyte APIs must declare a contact block pointing at the catalog.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  frostbyte-info-license:\n    description: Info must declare a license.\n    severity: warn\n    given: $.info\n    then:\n      field: license\n      function: truthy\n\n  frostbyte-server-production:\n    description: Specs should declare the production gateway URL.\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: 'agent-gateway-kappa\\\\.vercel\\\\.app'\n\n  frostbyte-operation-summary-required:\n    description: Every operation must define a summary.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  frostbyte-operation-summary-title-case:\n    description:\
  \ Operation summaries should use Title Case.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z]'\n\n  frostbyte-path-versioned:\n    description: All non-admin paths must be versioned under /v1/ or /api/.\n    severity: warn\n    given: $.paths\n    then:\n      function: pattern\n      functionOptions:\n        match: '^/(v1|api|health)'\n\n  frostbyte-credit-aware-402:\n    description: Operations should document the 402 Payment Required response (x402 / USDC on Base).\n    severity: info\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      field: '402'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/frostbyte/refs/heads/main/rules/frostbyte-rules.yml
tags:
- Developer Tools
- Utility APIs
- Geolocation
- Cryptocurrency
- Screenshots
- DNS
- Scraping
- AI Agents
- Spectral
- Linting
- API Governance
---

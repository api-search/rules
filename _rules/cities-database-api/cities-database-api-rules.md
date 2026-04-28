---
categories:
- cities
description: Spectral linting rules defining API design standards and conventions for Cities Database API.
layout: rules
name: Cities Database API API Rules
provider_name: Cities Database API
provider_slug: cities-database-api
rule_count: 5
rules:
- description: Cities Database API server URL MUST use HTTPS.
  given: $.servers[*].url
  name: cities-server-https
  severity: error
- description: Cities Database API server SHOULD be airlabs.co/api/v9.
  given: $.servers[*].url
  name: cities-base-url
  severity: warn
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: cities-operation-id
  severity: error
- description: Operations MUST be tagged.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: cities-tag-required
  severity: warn
- description: Cities Database API operations MUST require an api_key parameter.
  given: $.paths[*][get,post,put,delete,patch].parameters[?(@.name=='api_key')]
  name: cities-api-key-required
  severity: error
rules_file: rules/cities-database-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cities-database-api/refs/heads/main/rules/cities-database-api-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 2
slug: cities-database-api-rules
tags:
- Cities
- Data
- Geography
- Locations
- Reference Data
- Travel
- Spectral
- Linting
- API Governance
---

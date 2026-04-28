---
categories:
- climate
description: Spectral linting rules defining API design standards and conventions for Climate FieldView.
layout: rules
name: Climate FieldView API Rules
provider_name: Climate FieldView
provider_slug: climate-fieldview
rule_count: 6
rules:
- description: API info MUST contain a contact email or URL.
  given: $.info
  name: climate-fieldview-info-contact
  severity: warn
- description: All Climate FieldView API servers MUST use HTTPS.
  given: $.servers[*].url
  name: climate-fieldview-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: climate-fieldview-operation-id
  severity: error
- description: Operations MUST be tagged for agronomic-domain grouping (Fields, Planting, Harvest, Application, Soil Sampling).
  given: $.paths[*][get,post,put,delete,patch].tags
  name: climate-fieldview-tag-required
  severity: warn
- description: API MUST define an OAuth2 security scheme since FieldView authenticates with OAuth 2.0 authorization-code grant.
  given: $.components.securitySchemes
  name: climate-fieldview-oauth2-required
  severity: error
- description: API MUST declare at least one server URL pointing at api.climate.com.
  given: $.servers
  name: climate-fieldview-server-url
  severity: error
rules_file: rules/climate-fieldview-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/climate-fieldview/refs/heads/main/rules/climate-fieldview-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 2
slug: climate-fieldview-rules
tags:
- Agriculture
- Bayer
- Crop Data
- Field Boundaries
- Harvest
- OAuth2
- Planting
- Precision Ag
- Spectral
- Linting
- API Governance
---

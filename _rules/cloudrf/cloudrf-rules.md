---
categories:
- cloudrf
description: Spectral linting rules defining API design standards and conventions for CloudRF.
layout: rules
name: CloudRF API Rules
provider_name: CloudRF
provider_slug: cloudrf
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudrf-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudrf-info-license
  severity: warn
- description: All server URLs must use HTTPS for the CloudRF API.
  given: $.servers[*].url
  name: cloudrf-server-https
  severity: error
- description: Server URLs should target api.cloudrf.com or dev.cloudrf.com.
  given: $.servers[*].url
  name: cloudrf-server-host
  severity: warn
- description: An ApiKey security scheme using the `key` HTTP header must be declared.
  given: $.components.securitySchemes
  name: cloudrf-apikey-required
  severity: error
- description: The CloudRF API key is delivered via the `key` HTTP header.
  given: $.components.securitySchemes[?(@.type=='apiKey')]
  name: cloudrf-apikey-header-name
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudrf-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudrf-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudrf-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudrf-error-responses
  severity: warn
rules_file: rules/cloudrf-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudrf/refs/heads/main/rules/cloudrf-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: cloudrf-rules
tags:
- Coverage Modeling
- HF Propagation
- Mesh Network
- Radio Frequency
- RF
- Satellite
- Signal Analysis
- Telecommunications
- Wireless Planning
- Spectral
- Linting
- API Governance
---

---
categories:
- clearstream
description: Spectral linting rules defining API design standards and conventions for Clearstream.
layout: rules
name: Clearstream API Rules
provider_name: Clearstream
provider_slug: clearstream
rule_count: 11
rules:
- description: API contact information must be present.
  given: $.info
  name: clearstream-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clearstream-info-license
  severity: warn
- description: Info description should reference ISO 15022 or ISO 20022.
  given: $.info.description
  name: clearstream-info-iso-version
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clearstream-server-https
  severity: error
- description: Server URLs must point at a clearstream.com host.
  given: $.servers[*].url
  name: clearstream-server-domain
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearstream-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearstream-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearstream-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clearstream-error-responses
  severity: warn
- description: Counterparty BIC parameters should be 8 or 11 character ISO 9362 BICs.
  given: $.paths[*][*].parameters[?(@.name && @.name.match(/bic/i))].schema
  name: clearstream-bic-format
  severity: warn
- description: ISIN parameters should be 12-character ISO 6166 identifiers.
  given: $.paths[*][*].parameters[?(@.name && @.name.match(/isin/i))].schema
  name: clearstream-isin-format
  severity: warn
rules_file: rules/clearstream-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clearstream/refs/heads/main/rules/clearstream-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 8
slug: clearstream-rules
tags:
- Capital Markets
- Collateral Management
- Custody
- Financial Services
- ISO 15022
- ISO 20022
- Post-Trade Infrastructure
- Securities
- Settlement
- SWIFT
- Spectral
- Linting
- API Governance
---

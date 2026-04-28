---
categories:
- cip
description: Spectral linting rules defining API design standards and conventions for Civil Infrastructure Platform.
layout: rules
name: Civil Infrastructure Platform API Rules
provider_name: Civil Infrastructure Platform
provider_slug: civil-infrastructure-platform
rule_count: 5
rules:
- description: API info MUST contain a contact for the maintaining working group.
  given: $.info
  name: cip-info-contact
  severity: warn
- description: CIP-derived API descriptions SHOULD declare an open source license.
  given: $.info
  name: cip-info-license
  severity: warn
- description: API servers MUST use HTTPS.
  given: $.servers[*].url
  name: cip-https-only
  severity: error
- description: Operations MUST have an operationId.
  given: $.paths[*][get,post,put,delete,patch]
  name: cip-operation-id
  severity: error
- description: Operations MUST be tagged for working group grouping.
  given: $.paths[*][get,post,put,delete,patch].tags
  name: cip-tag-required
  severity: warn
rules_file: rules/civil-infrastructure-platform-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/civil-infrastructure-platform/refs/heads/main/rules/civil-infrastructure-platform-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 3
slug: civil-infrastructure-platform-rules
tags:
- Embedded
- Industrial
- Infrastructure
- Linux
- Linux Foundation
- Long-Term Support
- Open Source
- Spectral
- Linting
- API Governance
---

---
categories:
- barclays
description: Spectral linting rules defining API design standards and conventions for Barclays.
layout: rules
name: Barclays API Rules
provider_name: Barclays
provider_slug: barclays
rule_count: 7
rules:
- description: All Barclays API entries must have a Documentation property.
  given: $.apis[*]
  name: barclays-api-has-documentation
  severity: error
- description: All Barclays API entries must have a description.
  given: $.apis[*]
  name: barclays-api-has-description
  severity: error
- description: All Barclays API entries must have a name.
  given: $.apis[*]
  name: barclays-api-has-name
  severity: error
- description: All Barclays API entries must have a humanURL.
  given: $.apis[*]
  name: barclays-api-has-human-url
  severity: error
- description: All Barclays API entries must have tags.
  given: $.apis[*]
  name: barclays-api-has-tags
  severity: warn
- description: Barclays Open Banking APIs should be tagged with Open Banking or PSD2.
  given: $.apis[?(@.name =~ /Open Banking|Account|Payment|Confirmation/i)]
  name: barclays-open-banking-has-psd2-tag
  severity: info
- description: Barclays APIs.json must have a description.
  given: $
  name: barclays-apis-json-has-description
  severity: error
rules_file: rules/barclays-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/barclays/refs/heads/main/rules/barclays-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 1
slug: barclays-spectral-rules
tags:
- Banking
- Credit Cards
- Finance
- Open Banking
- Payments
- PSD2
- UK Banking
- Spectral
- Linting
- API Governance
---

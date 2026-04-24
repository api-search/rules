---
categories:
- blobr
description: Spectral linting rules defining API design standards and conventions for Blobr.
layout: rules
name: Blobr API Rules
provider_name: Blobr
provider_slug: blobr
rule_count: 5
rules:
- description: Campaign status must use Google Ads enum values
  given: $.components.schemas.Campaign.properties.status
  name: blobr-campaign-status-enum
  severity: warn
- description: Recommendation priority must be high, medium, or low
  given: $.components.schemas.Recommendation.properties.priority
  name: blobr-recommendation-priority-enum
  severity: warn
- description: Recommendation status must use defined workflow states
  given: $.components.schemas.Recommendation.properties.status
  name: blobr-recommendation-status-enum
  severity: warn
- description: Budget amounts should use Google Ads micros format
  given: $.components.schemas.Campaign.properties.budget.properties.amountMicros
  name: blobr-budget-micros
  severity: warn
- description: Timestamp fields must use ISO 8601 date-time format
  given: $.components.schemas[*].properties[?(@.description =~ /timestamp|created|applied/i)]
  name: blobr-dates-iso8601
  severity: warn
rules_file: rules/blobr-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/blobr/refs/heads/main/rules/blobr-spectral-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 5
slug: blobr-spectral-rules
tags:
- Advertising
- AI Agents
- Google Ads
- Marketing Automation
- PPC
- Spectral
- Linting
- API Governance
---

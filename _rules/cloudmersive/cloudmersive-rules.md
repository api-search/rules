---
categories:
- cloudmersive
description: Spectral linting rules defining API design standards and conventions for Cloudmersive.
layout: rules
name: Cloudmersive API Rules
provider_name: Cloudmersive
provider_slug: cloudmersive
rule_count: 8
rules:
- description: Each Cloudmersive product spec must declare a title.
  given: $.info
  name: cloudmersive-info-title
  severity: error
- description: Each Cloudmersive product spec must declare a description.
  given: $.info
  name: cloudmersive-info-description
  severity: warn
- description: A host (Swagger 2) or server (OpenAPI 3) must be declared.
  given: $
  name: cloudmersive-host-or-server
  severity: error
- description: Cloudmersive APIs must be served over HTTPS.
  given: $
  name: cloudmersive-https-only
  severity: error
- description: An Apikey security definition/scheme must be declared.
  given: $
  name: cloudmersive-apikey-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudmersive-operation-summary
  severity: warn
rules_file: rules/cloudmersive-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudmersive/refs/heads/main/rules/cloudmersive-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 3
slug: cloudmersive-rules
tags:
- Barcodes
- Conversions
- Documents
- Image Recognition
- Natural Language
- OCR
- Processing
- Validation
- Virus Scanning
- Spectral
- Linting
- API Governance
---

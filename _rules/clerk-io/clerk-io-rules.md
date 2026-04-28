---
categories:
- clerk
description: Spectral linting rules defining API design standards and conventions for Clerk.io.
layout: rules
name: Clerk.io API Rules
provider_name: Clerk.io
provider_slug: clerk-io
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: clerk-io-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clerk-io-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clerk-io-server-https
  severity: error
- description: A security scheme (apiKey for public/private keys) must be declared.
  given: $.components.securitySchemes
  name: clerk-io-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clerk-io-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clerk-io-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clerk-io-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clerk-io-error-responses
  severity: warn
rules_file: rules/clerk-io-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clerk-io/refs/heads/main/rules/clerk-io-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: clerk-io-rules
tags:
- AI
- Commerce
- E-Commerce
- Email Marketing
- Personalization
- Recommendations
- Search
- Spectral
- Linting
- API Governance
---

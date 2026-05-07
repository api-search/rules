---
api_specs:
- filename: email-verifier-api-openapi.yml
  format: yaml
  label: Email Verifier API Verification
  slug: verification
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/email-verifier-api/refs/heads/main/openapi/email-verifier-api-openapi.yml
categories:
- email
description: Spectral linting rules defining API design standards and conventions for Email Verifier API.
layout: rules
name: Email Verifier API API Rules
provider_name: Email Verifier API
provider_slug: email-verifier-api
rule_count: 9
rules:
- description: Info object must declare a contact for support.
  given: $.info
  name: email-verifier-api-info-contact
  severity: error
- description: Info object must declare a license.
  given: $.info
  name: email-verifier-api-info-license
  severity: warn
- description: All declared servers must use HTTPS.
  given: $.servers[*].url
  name: email-verifier-api-server-https
  severity: error
- description: Operation summary should use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: email-verifier-api-operation-summary-title-case
  severity: warn
- description: Every operation must be tagged.
  given: $.paths[*][get,post,put,patch,delete]
  name: email-verifier-api-operation-tagged
  severity: error
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: email-verifier-api-operation-id
  severity: error
- description: Security must be declared at the document level.
  given: $
  name: email-verifier-api-security-defined
  severity: error
- description: API key must be passed as a query parameter named apiKey.
  given: $.components.securitySchemes[*]
  name: email-verifier-api-api-key-auth
  severity: error
- description: VerificationResult schema must expose remaining credit balance and execution time.
  given: $.components.schemas.VerificationResult.properties
  name: email-verifier-api-credit-fields
  severity: warn
rules_file: rules/email-verifier-api-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/email-verifier-api/refs/heads/main/rules/email-verifier-api-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 3
slug: email-verifier-api-rules
source_filename: email-verifier-api-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  email-verifier-api-info-contact:\n    description: Info object must declare a contact for support.\n    given: $.info\n    severity: error\n    then:\n      field: contact\n      function: truthy\n  email-verifier-api-info-license:\n    description: Info object must declare a license.\n    given: $.info\n    severity: warn\n    then:\n      field: license\n      function: truthy\n  email-verifier-api-server-https:\n    description: All declared servers must use HTTPS.\n    given: $.servers[*].url\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: ^https://\n  email-verifier-api-operation-summary-title-case:\n    description: Operation summary should use Title Case.\n    given: $.paths[*][get,post,put,patch,delete].summary\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: '^([A-Z][A-Za-z0-9]*)( [A-Z0-9][A-Za-z0-9()/-]*)*$'\n  email-verifier-api-operation-tagged:\n\
  \    description: Every operation must be tagged.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: error\n    then:\n      field: tags\n      function: truthy\n  email-verifier-api-operation-id:\n    description: Every operation must have an operationId.\n    given: $.paths[*][get,post,put,patch,delete]\n    severity: error\n    then:\n      field: operationId\n      function: truthy\n  email-verifier-api-security-defined:\n    description: Security must be declared at the document level.\n    given: $\n    severity: error\n    then:\n      field: security\n      function: truthy\n  email-verifier-api-api-key-auth:\n    description: API key must be passed as a query parameter named apiKey.\n    given: $.components.securitySchemes[*]\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            type: { const: apiKey }\n            in: { const: query }\n            name: { const:\
  \ apiKey }\n          required: [type, in, name]\n  email-verifier-api-credit-fields:\n    description: VerificationResult schema must expose remaining credit balance and execution time.\n    given: $.components.schemas.VerificationResult.properties\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [remaining, execution]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/email-verifier-api/refs/heads/main/rules/email-verifier-api-rules.yml
tags:
- Email Verification
- Deliverability
- SMTP Check
- Bounce Prevention
- Lead Validation
- Disposable Detection
- Spam Trap Detection
- Catch-All Detection
- Greylisting
- Role Account Detection
- Typo Suggestion
- B2B Lead Scoring
- Spectral
- Linting
- API Governance
---

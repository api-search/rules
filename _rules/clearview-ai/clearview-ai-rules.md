---
categories:
- clearview
description: Spectral linting rules defining API design standards and conventions for Clearview AI.
layout: rules
name: Clearview AI API Rules
provider_name: Clearview AI
provider_slug: clearview-ai
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: clearview-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clearview-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clearview-server-https
  severity: error
- description: A security scheme must be defined.
  given: $.components.securitySchemes
  name: clearview-security-required
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearview-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearview-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clearview-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clearview-error-responses
  severity: warn
rules_file: rules/clearview-ai-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clearview-ai/refs/heads/main/rules/clearview-ai-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: clearview-ai-rules
source_filename: clearview-ai-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for any Clearview AI integration spec.\n# Public API documentation is intentionally minimal; these rules\n# enforce baseline hygiene appropriate for a high-risk biometric\n# vendor surface (HTTPS-only, authenticated, audited).\nrules:\n  clearview-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  clearview-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  clearview-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  clearview-security-required:\n    description: A security scheme must be defined.\n    severity: error\n \
  \   given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  clearview-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  clearview-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  clearview-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  clearview-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/clearview-ai/refs/heads/main/rules/clearview-ai-rules.yml
tags:
- Biometrics
- Facial Recognition
- Identity
- Investigations
- Law Enforcement
- Surveillance
- Spectral
- Linting
- API Governance
---

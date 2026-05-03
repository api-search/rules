---
api_specs:
- filename: symantec-sepm-api-openapi.yml
  format: yaml
  label: Symantec Endpoint Protection Manager API
  slug: sepm-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/symantec/refs/heads/main/openapi/symantec-sepm-api-openapi.yml
categories:
- symantec
description: Spectral linting rules defining API design standards and conventions for Symantec.
layout: rules
name: Symantec API Rules
provider_name: Symantec
provider_slug: symantec
rule_count: 7
rules:
- description: SEPM API must define Bearer authentication scheme
  given: $.components.securitySchemes
  name: symantec-bearer-auth
  severity: warn
- description: Operation IDs must use camelCase naming convention
  given: $.paths[*][get,post,put,patch,delete]
  name: symantec-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: symantec-summary-title-case
  severity: warn
- description: Non-authentication endpoints must require Bearer token
  given: $.paths[?(@property != '/identity/authenticate')][get,post,put,patch,delete]
  name: symantec-security-required
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: symantec-auth-response
  severity: warn
- description: List endpoints should support pageSize and pageIndex query parameters
  given: $.paths[?(@property.endsWith('s') || @property.endsWith('computers'))].get
  name: symantec-pagination-parameters
  severity: hint
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: symantec-operation-tags
  severity: warn
rules_file: rules/symantec-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/symantec/refs/heads/main/rules/symantec-rules.yml
severity_counts:
  error: 0
  hint: 1
  info: 0
  warn: 6
slug: symantec-rules
source_filename: symantec-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, all]]\n\nrules:\n  # SEPM uses Bearer token authentication\n  symantec-bearer-auth:\n    description: SEPM API must define Bearer authentication scheme\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  # Operation IDs must use camelCase\n  symantec-operation-id-camel-case:\n    description: Operation IDs must use camelCase naming convention\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Summaries must use Title Case\n  symantec-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9 ]+$\"\n\n  # All operations (except\
  \ auth) must have security defined\n  symantec-security-required:\n    description: Non-authentication endpoints must require Bearer token\n    severity: warn\n    given: \"$.paths[?(@property != '/identity/authenticate')][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # 401 response must be defined\n  symantec-auth-response:\n    description: All operations must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: '401'\n      function: truthy\n\n  # GET list endpoints should support pagination\n  symantec-pagination-parameters:\n    description: List endpoints should support pageSize and pageIndex query parameters\n    severity: hint\n    given: \"$.paths[?(@property.endsWith('s') || @property.endsWith('computers'))].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  # Operations must have tags\n  symantec-operation-tags:\n    description:\
  \ All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/symantec/refs/heads/main/rules/symantec-rules.yml
tags:
- Broadcom
- Cybersecurity
- DLP
- EDR
- Endpoint Protection
- Endpoint Security
- Security
- Symantec
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: zitadel-management-openapi.yml
  format: yaml
  label: Zitadel Management API
  slug: management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zitadel/refs/heads/main/openapi/zitadel-management-openapi.yml
categories:
- zitadel
description: Spectral linting rules defining API design standards and conventions for Zitadel.
layout: rules
name: Zitadel API Rules
provider_name: Zitadel
provider_slug: zitadel
rule_count: 7
rules:
- description: All operation summaries must start with "Zitadel"
  given: $.paths.*[get,post,put,delete,patch].summary
  name: zitadel-summary-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths.*[get,post,put,delete,patch]
  name: zitadel-operation-id
  severity: error
- description: Every operation must have at least one tag
  given: $.paths.*[get,post,put,delete,patch]
  name: zitadel-operation-tags
  severity: warn
- description: Every operation must have a description
  given: $.paths.*[get,post,put,delete,patch]
  name: zitadel-operation-description
  severity: warn
- description: Bearer auth security scheme must be defined
  given: $.components.securitySchemes.bearerAuth
  name: zitadel-bearer-auth
  severity: error
- description: Error responses must include 401, 403 references
  given: $.paths.*[get,post,put,delete,patch].responses
  name: zitadel-no-numeric-error-codes
  severity: warn
- description: Servers must be defined
  given: $.servers
  name: zitadel-server-defined
  severity: error
rules_file: rules/zitadel-spectral.yaml
rules_url: https://raw.githubusercontent.com/api-evangelist/zitadel/refs/heads/main/rules/zitadel-spectral.yaml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: zitadel-spectral
source_filename: zitadel-spectral.yaml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  zitadel-summary-prefix:\n    description: All operation summaries must start with \"Zitadel\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Zitadel \"\n  zitadel-operation-id:\n    description: Every operation must have an operationId\n    severity: error\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n  zitadel-operation-tags:\n    description: Every operation must have at least one tag\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n  zitadel-operation-description:\n    description: Every operation must have a description\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n  zitadel-bearer-auth:\n\
  \    description: Bearer auth security scheme must be defined\n    severity: error\n    given: \"$.components.securitySchemes.bearerAuth\"\n    then:\n      function: truthy\n  zitadel-no-numeric-error-codes:\n    description: Error responses must include 401, 403 references\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch].responses\"\n    then:\n      function: truthy\n  zitadel-server-defined:\n    description: Servers must be defined\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zitadel/refs/heads/main/rules/zitadel-spectral.yaml
tags:
- Authentication
- Authorization
- Identity Management
- Open Source
- OAuth 2.0
- OIDC
- Spectral
- Linting
- API Governance
---

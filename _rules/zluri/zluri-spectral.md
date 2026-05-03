---
api_specs:
- filename: zluri-api-openapi.yml
  format: yaml
  label: Zluri
  slug: zluri
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zluri/refs/heads/main/openapi/zluri-api-openapi.yml
categories:
- zluri
description: Spectral linting rules defining API design standards and conventions for Zluri.
layout: rules
name: Zluri API Rules
provider_name: Zluri
provider_slug: zluri
rule_count: 7
rules:
- description: All operation summaries must start with "Zluri"
  given: $.paths.*[get,post,put,delete,patch].summary
  name: zluri-summary-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths.*[get,post,put,delete,patch]
  name: zluri-operation-id
  severity: error
- description: Every operation must have at least one tag
  given: $.paths.*[get,post,put,delete,patch]
  name: zluri-operation-tags
  severity: warn
- description: Every operation must have a description
  given: $.paths.*[get,post,put,delete,patch]
  name: zluri-operation-description
  severity: warn
- description: Bearer auth security scheme must be defined
  given: $.components.securitySchemes.bearerAuth
  name: zluri-bearer-auth
  severity: error
- description: List operations should declare 429 rate limit responses
  given: $.paths.*[get].responses
  name: zluri-rate-limit-response
  severity: warn
- description: Servers must be defined
  given: $.servers
  name: zluri-server-defined
  severity: error
rules_file: rules/zluri-spectral.yaml
rules_url: https://raw.githubusercontent.com/api-evangelist/zluri/refs/heads/main/rules/zluri-spectral.yaml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 4
slug: zluri-spectral
source_filename: zluri-spectral.yaml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\nrules:\n  zluri-summary-prefix:\n    description: All operation summaries must start with \"Zluri\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Zluri \"\n  zluri-operation-id:\n    description: Every operation must have an operationId\n    severity: error\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n  zluri-operation-tags:\n    description: Every operation must have at least one tag\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n  zluri-operation-description:\n    description: Every operation must have a description\n    severity: warn\n    given: \"$.paths.*[get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n  zluri-bearer-auth:\n    description:\
  \ Bearer auth security scheme must be defined\n    severity: error\n    given: \"$.components.securitySchemes.bearerAuth\"\n    then:\n      function: truthy\n  zluri-rate-limit-response:\n    description: List operations should declare 429 rate limit responses\n    severity: warn\n    given: \"$.paths.*[get].responses\"\n    then:\n      field: \"429\"\n      function: truthy\n  zluri-server-defined:\n    description: Servers must be defined\n    severity: error\n    given: \"$.servers\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zluri/refs/heads/main/rules/zluri-spectral.yaml
tags:
- Access Management
- SaaS Management
- Spectral
- Linting
- API Governance
---

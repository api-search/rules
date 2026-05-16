---
api_specs:
- filename: barndoor-openapi.yml
  format: yaml
  label: Barndoor Platform API
  slug: platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/barndoor/refs/heads/main/openapi/barndoor-openapi.yml
categories:
- api
- apis
- bearer
- info
- 'no'
- operation
- organization
- response
- servers
description: Spectral linting rules defining API design standards and conventions for Barndoor.
layout: rules
name: Barndoor API Rules
provider_name: Barndoor
provider_slug: barndoor
rule_count: 14
rules:
- description: Info title must be present.
  given: $.info
  name: info-title-required
  severity: error
- description: Info description must be present.
  given: $.info
  name: info-description-required
  severity: error
- description: Info contact must be present.
  given: $.info
  name: info-contact-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should be in Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Descriptions must not be empty.
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: BearerAuth security scheme should declare bearerFormat as JWT for Barndoor.
  given: $.components.securitySchemes.BearerAuth
  name: bearer-auth-jwt
  severity: warn
- description: At least one server must be declared.
  given: $
  name: servers-required
  severity: error
- description: Server URLs should use the {organization_id} template variable.
  given: $.servers[*]
  name: organization-id-variable
  severity: warn
- description: Barndoor APIs.json must have a description.
  given: $
  name: apis-json-description
  severity: error
- description: All Barndoor API entries must have a Documentation property.
  given: $.apis[*]
  name: api-has-documentation
  severity: error
rules_file: rules/barndoor-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/barndoor/refs/heads/main/rules/barndoor-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 5
slug: barndoor-spectral-rules
source_filename: barndoor-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  info-title-required:\n    description: Info title must be present.\n    severity: error\n    given: $.info\n    then:\n      field: title\n      function: truthy\n\n  info-description-required:\n    description: Info description must be present.\n    severity: error\n    given: $.info\n    then:\n      field: description\n      function: truthy\n\n  info-contact-required:\n    description: Info contact must be present.\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  operation-operationid-required:\n    description: Every operation must have an operationId.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: operationId\n      function: truthy\n\n  operation-summary-required:\n    description: Every operation must have a summary.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function:\
  \ truthy\n\n  operation-summary-title-case:\n    description: Operation summaries should be in Title Case.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  operation-tags-required:\n    description: Every operation must have at least one tag.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  response-description-required:\n    description: Every response must have a description.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then:\n      field: description\n      function: truthy\n\n  no-empty-descriptions:\n    description: Descriptions must not be empty.\n    severity: error\n    given: $..description\n    then:\n      function: truthy\n\n  bearer-auth-jwt:\n    description: BearerAuth security scheme should declare bearerFormat as JWT for Barndoor.\n\
  \    severity: warn\n    given: $.components.securitySchemes.BearerAuth\n    then:\n      field: bearerFormat\n      function: pattern\n      functionOptions:\n        match: \"JWT\"\n\n  servers-required:\n    description: At least one server must be declared.\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  organization-id-variable:\n    description: Server URLs should use the {organization_id} template variable.\n    severity: warn\n    given: $.servers[*]\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"{organization_id}\"\n\n  apis-json-description:\n    description: Barndoor APIs.json must have a description.\n    severity: error\n    given: $\n    then:\n      field: description\n      function: truthy\n\n  api-has-documentation:\n    description: All Barndoor API entries must have a Documentation property.\n    severity: error\n    given: $.apis[*]\n    then:\n      field: properties\n\
  \      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              type:\n                const: Documentation\n            required:\n              - type\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/barndoor/refs/heads/main/rules/barndoor-spectral-rules.yml
tags:
- AI Agents
- AI Governance
- Agentic AI
- MCP
- Model Context Protocol
- Policy Enforcement
- OAuth
- Identity
- Security
- Audit
- Control Plane
- Spectral
- Linting
- API Governance
---

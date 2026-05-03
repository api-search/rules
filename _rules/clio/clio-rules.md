---
categories:
- clio
description: Spectral linting rules defining API design standards and conventions for Clio.
layout: rules
name: Clio API Rules
provider_name: Clio
provider_slug: clio
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: clio-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: clio-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: clio-server-https
  severity: error
- description: Manage API server URLs must include /api/v4.
  given: $.servers[?(@.url && @.url.indexOf('clio.com') > -1)].url
  name: clio-server-versioned
  severity: warn
- description: OAuth 2.0 must be the declared security scheme.
  given: $.components.securitySchemes[*].type
  name: clio-oauth-security
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: clio-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: clio-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: clio-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: clio-error-responses
  severity: warn
- description: List endpoints should support page, limit, fields, and order parameters.
  given: $.paths[?(@property.match(/matters$|contacts$|activities$|tasks$|bills$/))].get.parameters[*].name
  name: clio-pagination-fields
  severity: info
rules_file: rules/clio-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clio/refs/heads/main/rules/clio-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: clio-rules
source_filename: clio-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for the Clio Manage API v4.\n# https://docs.developers.clio.com/ — OAuth 2.0 secured REST API at\n# https://app.clio.com/api/v4 with regional variants for CA/EU/AU.\nrules:\n  clio-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  clio-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  clio-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  clio-server-versioned:\n    description: Manage API server URLs must include /api/v4.\n    severity: warn\n    given: \"$.servers[?(@.url && @.url.indexOf('clio.com') > -1)].url\"\n \
  \   then:\n      function: pattern\n      functionOptions:\n        match: \"/api/v4$\"\n\n  clio-oauth-security:\n    description: OAuth 2.0 must be the declared security scheme.\n    severity: error\n    given: \"$.components.securitySchemes[*].type\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - oauth2\n\n  clio-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  clio-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  clio-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n\
  \    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  clio-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n\n  clio-pagination-fields:\n    description: List endpoints should support page, limit, fields, and order parameters.\n    severity: info\n    given: \"$.paths[?(@property.match(/matters$|contacts$|activities$|tasks$|bills$/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - limit\n          - fields\n          - order\n\
  \          - query\n          - created_since\n          - updated_since\n          - ids\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/clio/refs/heads/main/rules/clio-rules.yml
tags:
- Billing
- Calendaring
- Document Management
- Law Firms
- Legal
- Matter Management
- OAuth 2.0
- Practice Management
- Time Tracking
- Trust Accounting
- Spectral
- Linting
- API Governance
---

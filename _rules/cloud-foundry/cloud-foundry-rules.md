---
categories:
- cf
description: Spectral linting rules defining API design standards and conventions for Cloud Foundry.
layout: rules
name: Cloud Foundry API Rules
provider_name: Cloud Foundry
provider_slug: cloud-foundry
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: cf-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cf-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cf-server-https
  severity: error
- description: Cloud Controller server URLs should include /v3.
  given: $.servers[*].url
  name: cf-server-versioned
  severity: warn
- description: OAuth 2.0 must be the declared security scheme.
  given: $.components.securitySchemes[*].type
  name: cf-oauth-security
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cf-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cf-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cf-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cf-error-responses
  severity: warn
- description: List endpoints should support page, per_page, and order_by parameters.
  given: $.paths[?(@property.match(/apps$|spaces$|organizations$|routes$|service_instances$/))].get.parameters[*].name
  name: cf-pagination-fields
  severity: info
rules_file: rules/cloud-foundry-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloud-foundry/refs/heads/main/rules/cloud-foundry-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: cloud-foundry-rules
source_filename: cloud-foundry-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for Cloud Foundry CAPI v3.\n# https://v3-apidocs.cloudfoundry.org/ — OAuth 2.0 secured REST API.\nrules:\n  cf-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cf-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cf-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cf-server-versioned:\n    description: Cloud Controller server URLs should include /v3.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/v3$\"\n\n  cf-oauth-security:\n    description:\
  \ OAuth 2.0 must be the declared security scheme.\n    severity: error\n    given: \"$.components.securitySchemes[*].type\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - oauth2\n          - http\n\n  cf-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cf-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cf-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n\
  \  cf-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n\n  cf-pagination-fields:\n    description: List endpoints should support page, per_page, and order_by parameters.\n    severity: info\n    given: \"$.paths[?(@property.match(/apps$|spaces$|organizations$|routes$|service_instances$/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - page\n          - per_page\n          - order_by\n          - names\n          - guids\n          - space_guids\n          - organization_guids\n          - label_selector\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloud-foundry/refs/heads/main/rules/cloud-foundry-rules.yml
tags:
- Cloud Foundry Foundation
- Containers
- Multi-Cloud
- Open Source
- PaaS
- Platform
- Spectral
- Linting
- API Governance
---

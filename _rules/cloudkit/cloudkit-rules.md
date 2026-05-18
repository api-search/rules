---
categories:
- cloudkit
description: Spectral linting rules defining API design standards and conventions for Apple CloudKit.
layout: rules
name: Apple CloudKit API Rules
provider_name: Apple CloudKit
provider_slug: cloudkit
rule_count: 12
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudkit-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudkit-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudkit-server-https
  severity: error
- description: CloudKit server URLs must point at api.apple-cloudkit.com.
  given: $.servers[*].url
  name: cloudkit-server-base
  severity: warn
- description: CloudKit paths must include /database/{version}.
  given: $.servers[*].url
  name: cloudkit-database-versioned
  severity: warn
- description: Paths should specify development or production environment.
  given: $.paths[*]
  name: cloudkit-environment
  severity: info
- description: A security scheme must be declared (apiKey or signature-based).
  given: $.components.securitySchemes
  name: cloudkit-auth
  severity: error
- description: Operations using API token auth should declare ckAPIToken.
  given: $.paths[*][get,post].parameters[?(@.in == 'query')].name
  name: cloudkit-token-param
  severity: info
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudkit-operation-id
  severity: error
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudkit-operation-summary
  severity: warn
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudkit-operation-tags
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudkit-error-responses
  severity: warn
rules_file: rules/cloudkit-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudkit/refs/heads/main/rules/cloudkit-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 6
slug: cloudkit-rules
source_filename: cloudkit-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for the Apple CloudKit Web Services API.\n# Validates CloudKit's path shape (/database/1/{container}/{env}/{db})\n# and the auth/query parameter conventions used by the web service.\nrules:\n  cloudkit-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cloudkit-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cloudkit-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cloudkit-server-base:\n    description: CloudKit server URLs must point at api.apple-cloudkit.com.\n    severity: warn\n    given: \"$.servers[*].url\"\n\
  \    then:\n      function: pattern\n      functionOptions:\n        match: \"api\\\\.apple-cloudkit\\\\.com\"\n\n  cloudkit-database-versioned:\n    description: CloudKit paths must include /database/{version}.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/database/\\\\d+(/|$)\"\n\n  cloudkit-environment:\n    description: Paths should specify development or production environment.\n    severity: info\n    given: \"$.paths[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(development|production)\"\n\n  cloudkit-auth:\n    description: A security scheme must be declared (apiKey or signature-based).\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  cloudkit-token-param:\n    description: Operations using API token auth should declare ckAPIToken.\n    severity: info\n    given: \"$.paths[*][get,post].parameters[?(@.in\
  \ == 'query')].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - ckAPIToken\n          - ckWebAuthToken\n          - ckSession\n\n  cloudkit-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cloudkit-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cloudkit-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cloudkit-error-responses:\n    description: Mutating\
  \ operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloudkit/refs/heads/main/rules/cloudkit-rules.yml
tags:
- Apple
- Cloud Storage
- CloudKit
- Database
- iCloud
- Mobile
- Sync
- Web Services
- Spectral
- Linting
- API Governance
---

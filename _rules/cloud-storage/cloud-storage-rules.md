---
categories:
- cs
description: Spectral linting rules defining API design standards and conventions for Cloud Storage.
layout: rules
name: Cloud Storage API Rules
provider_name: Cloud Storage
provider_slug: cloud-storage
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cs-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cs-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cs-server-https
  severity: error
- description: A security scheme must be defined (signed requests or token).
  given: $.components.securitySchemes
  name: cs-security-required
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cs-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cs-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cs-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cs-error-responses
  severity: warn
- description: List-objects endpoints should support pagination markers.
  given: $.paths[?(@property.match(/list$|objects$|buckets$|volumes$|snapshots$/))].get.parameters[*].name
  name: cs-list-pagination
  severity: info
rules_file: rules/cloud-storage-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloud-storage/refs/heads/main/rules/cloud-storage-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 4
slug: cloud-storage-rules
source_filename: cloud-storage-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for any Cloud Storage API in this topic\n# profile. These rules apply to S3-compatible and native object,\n# file, and block storage APIs.\nrules:\n  cs-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cs-info-license:\n    description: API license must be declared.\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cs-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cs-security-required:\n    description: A security scheme must be defined (signed requests or token).\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  cs-operation-tags:\n\
  \    description: Every operation must declare at least one tag.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cs-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cs-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cs-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type:\
  \ object\n          anyOf:\n            - required: [\"400\"]\n            - required: [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"409\"]\n\n  cs-list-pagination:\n    description: List-objects endpoints should support pagination markers.\n    severity: info\n    given: \"$.paths[?(@property.match(/list$|objects$|buckets$|volumes$|snapshots$/))].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - marker\n          - continuation-token\n          - max-keys\n          - maxResults\n          - pageToken\n          - prefix\n          - delimiter\n          - start-after\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloud-storage/refs/heads/main/rules/cloud-storage-rules.yml
tags:
- Block Storage
- Cloud
- Cloud Storage
- File Storage
- Object Storage
- S3 Compatible
- Storage
- Spectral
- Linting
- API Governance
---

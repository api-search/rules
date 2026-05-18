---
categories:
- cnb
description: Spectral linting rules defining API design standards and conventions for Cloud Native Buildpacks.
layout: rules
name: Cloud Native Buildpacks API Rules
provider_name: Cloud Native Buildpacks
provider_slug: cloud-native-buildpacks
rule_count: 8
rules:
- description: API contact information must be present.
  given: $.info
  name: cnb-info-contact
  severity: error
- description: API license must be declared (CNB is Apache-2.0).
  given: $.info
  name: cnb-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cnb-server-https
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cnb-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cnb-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cnb-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cnb-error-responses
  severity: warn
- description: Buildpack IDs should follow the reverse-DNS convention.
  given: $.paths[?(@property.match(/buildpack/))]
  name: cnb-buildpack-id-pattern
  severity: info
rules_file: rules/cloud-native-buildpacks-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloud-native-buildpacks/refs/heads/main/rules/cloud-native-buildpacks-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: cloud-native-buildpacks-rules
source_filename: cloud-native-buildpacks-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\n# Spectral linting rules for Cloud Native Buildpacks specs.\n# CNB does not expose a runtime HTTP API directly; these rules\n# apply to ancillary services such as the Buildpack Registry API\n# and any platform integrations that wrap the lifecycle.\nrules:\n  cnb-info-contact:\n    description: API contact information must be present.\n    severity: error\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n\n  cnb-info-license:\n    description: API license must be declared (CNB is Apache-2.0).\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  cnb-server-https:\n    description: All server URLs must use HTTPS.\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  cnb-operation-tags:\n    description: Every operation must declare at least one tag.\n    severity: warn\n \
  \   given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  cnb-operation-summary:\n    description: Every operation must include a short summary.\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  cnb-operation-id:\n    description: Every operation must declare a unique operationId.\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  cnb-error-responses:\n    description: Mutating operations should declare 4xx error responses.\n    severity: warn\n    given: \"$.paths[*][post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"400\"]\n            - required:\
  \ [\"401\"]\n            - required: [\"403\"]\n            - required: [\"404\"]\n            - required: [\"422\"]\n\n  cnb-buildpack-id-pattern:\n    description: Buildpack IDs should follow the reverse-DNS convention.\n    severity: info\n    given: \"$.paths[?(@property.match(/buildpack/))]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/cloud-native-buildpacks/refs/heads/main/rules/cloud-native-buildpacks-rules.yml
tags:
- Buildpacks
- CNCF
- Containers
- Images
- OCI
- Open Source
- Platform
- Reproducible Builds
- Spectral
- Linting
- API Governance
---

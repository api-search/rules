---
api_specs:
- filename: vnc-cloud-openapi.yml
  format: yaml
  label: VNC Cloud API
  slug: vnc-cloud-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/vnc/refs/heads/main/openapi/vnc-cloud-openapi.yml
categories:
- vnc
description: Spectral linting rules defining API design standards and conventions for VNC.
layout: rules
name: VNC API Rules
provider_name: VNC
provider_slug: vnc
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: vnc-operation-summary-title-case
  severity: warn
- description: Path segments must use kebab-case.
  given: $.paths
  name: vnc-path-kebab-case
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: vnc-operation-ids-camel-case
  severity: warn
- description: Each operation must have at least one tag.
  given: $.paths[*][*]
  name: vnc-tags-required
  severity: error
- description: Error responses (4xx/5xx) must reference the Error schema.
  given: $.paths[*][*].responses[4,5][0-9][0-9]
  name: vnc-error-response-schema
  severity: warn
- description: Server URLs must include an API version path segment.
  given: $.servers[*].url
  name: vnc-api-version-in-server
  severity: warn
- description: The API must declare Basic authentication as a security scheme.
  given: $.components.securitySchemes
  name: vnc-basic-auth-security
  severity: error
- description: List operations should support a limit query parameter for pagination.
  given: $.paths[*].get.parameters[?(@.name == 'limit')]
  name: vnc-pagination-limit-parameter
  severity: info
rules_file: rules/vnc-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/vnc/refs/heads/main/rules/vnc-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 5
slug: vnc-rules
source_filename: vnc-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  vnc-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z]*(\\\\s[A-Z][a-z]*)*)\"\n\n  vnc-path-kebab-case:\n    description: Path segments must use kebab-case.\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9{}-]+)+$\"\n\n  vnc-operation-ids-camel-case:\n    description: OperationIds must use camelCase.\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  vnc-tags-required:\n    description: Each operation must have at least one tag.\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  vnc-error-response-schema:\n\
  \    description: Error responses (4xx/5xx) must reference the Error schema.\n    severity: warn\n    given: \"$.paths[*][*].responses[4,5][0-9][0-9]\"\n    then:\n      field: content\n      function: truthy\n\n  vnc-api-version-in-server:\n    description: Server URLs must include an API version path segment.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\/[0-9]+\\\\.[0-9]+.*\"\n\n  vnc-basic-auth-security:\n    description: The API must declare Basic authentication as a security scheme.\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n\n  vnc-pagination-limit-parameter:\n    description: List operations should support a limit query parameter for pagination.\n    severity: info\n    given: \"$.paths[*].get.parameters[?(@.name == 'limit')]\"\n    then:\n      field: schema.type\n      function: enumeration\n      functionOptions:\n        values:\n\
  \          - integer\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/vnc/refs/heads/main/rules/vnc-rules.yml
tags:
- Remote Desktop
- Remote Access
- VNC
- Networking
- Screen Sharing
- Spectral
- Linting
- API Governance
---

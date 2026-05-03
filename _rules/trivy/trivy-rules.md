---
api_specs:
- filename: trivy-server-openapi.yml
  format: yaml
  label: Trivy Server API
  slug: trivy-server
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/trivy/refs/heads/main/openapi/trivy-server-openapi.yml
categories:
- trivy
description: Spectral linting rules defining API design standards and conventions for Trivy.
layout: rules
name: Trivy API Rules
provider_name: Trivy
provider_slug: trivy
rule_count: 6
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: trivy-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: trivy-require-tags
  severity: warn
- description: All operations must have a description
  given: $.paths[*][*]
  name: trivy-require-description
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trivy-summary-title-case
  severity: warn
- description: Trivy server supports optional token authentication via Trivy-Token header
  given: $.components.securitySchemes
  name: trivy-token-auth-optional
  severity: info
- description: Trivy server must expose a /healthz endpoint
  given: $.paths
  name: trivy-health-endpoint-present
  severity: warn
rules_file: rules/trivy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trivy/refs/heads/main/rules/trivy-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 1
  warn: 5
slug: trivy-rules
source_filename: trivy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Trivy Server API Convention Rules\n\n  trivy-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  trivy-require-tags:\n    description: All operations must have at least one tag\n    message: Operations must be tagged for organization\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  trivy-require-description:\n    description: All operations must have a description\n    message: Operations must have a description\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  trivy-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary\
  \ '{{value}}' must start with a capital letter (Title Case)\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  trivy-token-auth-optional:\n    description: Trivy server supports optional token authentication via Trivy-Token header\n    message: Trivy-Token authentication scheme should be defined when auth is documented\n    severity: info\n    given: \"$.components.securitySchemes\"\n    then:\n      field: TrivyToken\n      function: truthy\n\n  trivy-health-endpoint-present:\n    description: Trivy server must expose a /healthz endpoint\n    message: The /healthz health check endpoint should be documented\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: /healthz\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trivy/refs/heads/main/rules/trivy-rules.yml
tags:
- Containers
- Kubernetes
- SBOM
- Security
- Vulnerability Scanning
- Open Source
- DevSecOps
- Cloud Security
- Spectral
- Linting
- API Governance
---

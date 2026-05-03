---
api_specs:
- filename: snyk-container-openapi.yml
  format: yaml
  label: Snyk Container
  slug: snyk-container
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/snyk-container/refs/heads/main/openapi/snyk-container-openapi.yml
categories:
- snyk
description: Spectral linting rules defining API design standards and conventions for Snyk Container.
layout: rules
name: Snyk Container API Rules
provider_name: Snyk Container
provider_slug: snyk-container
rule_count: 9
rules:
- description: All Snyk REST API requests must include a version query parameter
  given: $.paths.*.*.parameters[?(@.name == 'version')]
  name: snyk-container-version-required
  severity: error
- description: Organization IDs must be UUID format
  given: $.paths[*].parameters[?(@.name == 'org_id')].schema
  name: snyk-container-org-id-uuid
  severity: error
- description: Snyk APIs must use Bearer token authentication
  given: $.components.securitySchemes[*]
  name: snyk-container-bearer-auth
  severity: error
- description: Responses must use JSON:API content type
  given: $.paths.*.*.responses.*.content
  name: snyk-container-jsonapi-content-type
  severity: warn
- description: Severity values must follow Snyk severity levels
  given: $.components.schemas..severity
  name: snyk-container-severity-enum
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths.*.*.operationId
  name: snyk-container-operation-id-camel-case
  severity: warn
- description: Collection responses should include pagination links
  given: $.components.schemas.*Response.properties
  name: snyk-container-pagination-links
  severity: info
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: snyk-container-tags-required
  severity: error
- description: Path segments should use kebab-case
  given: $.paths
  name: snyk-container-path-kebab-case
  severity: warn
rules_file: rules/snyk-container-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/snyk-container/refs/heads/main/rules/snyk-container-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 3
slug: snyk-container-rules
source_filename: snyk-container-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  snyk-container-version-required:\n    description: All Snyk REST API requests must include a version query parameter\n    message: \"The 'version' query parameter is required for all Snyk REST API endpoints.\"\n    severity: error\n    given: \"$.paths.*.*.parameters[?(@.name == 'version')]\"\n    then:\n      field: required\n      function: truthy\n\n  snyk-container-org-id-uuid:\n    description: Organization IDs must be UUID format\n    message: \"org_id path parameter must use UUID format.\"\n    severity: error\n    given: \"$.paths[*].parameters[?(@.name == 'org_id')].schema\"\n    then:\n      field: format\n      function: pattern\n      functionOptions:\n        match: \"^uuid$\"\n\n  snyk-container-bearer-auth:\n    description: Snyk APIs must use Bearer token authentication\n    message: \"Security scheme must be Bearer HTTP authentication.\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field:\
  \ type\n      function: enumeration\n      functionOptions:\n        values:\n          - http\n\n  snyk-container-jsonapi-content-type:\n    description: Responses must use JSON:API content type\n    message: \"Container API responses should use application/vnd.api+json content type.\"\n    severity: warn\n    given: \"$.paths.*.*.responses.*.content\"\n    then:\n      function: truthy\n\n  snyk-container-severity-enum:\n    description: Severity values must follow Snyk severity levels\n    message: \"Severity must be one of: critical, high, medium, low.\"\n    severity: error\n    given: \"$.components.schemas..severity\"\n    then:\n      field: enum\n      function: truthy\n\n  snyk-container-operation-id-camel-case:\n    description: Operation IDs should use camelCase\n    message: \"{{property}} operationId '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"\
  ^[a-z][a-zA-Z0-9]*$\"\n\n  snyk-container-pagination-links:\n    description: Collection responses should include pagination links\n    message: \"Responses returning arrays should include pagination links.\"\n    severity: info\n    given: \"$.components.schemas.*Response.properties\"\n    then:\n      field: links\n      function: truthy\n\n  snyk-container-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation '{{path}}' must have at least one tag.\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  snyk-container-path-kebab-case:\n    description: Path segments should use kebab-case\n    message: \"Path '{{path}}' should use kebab-case segments.\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/snyk-container/refs/heads/main/rules/snyk-container-rules.yml
tags:
- Container Images
- Containers
- Kubernetes
- Security
- Vulnerability Management
- DevSecOps
- Open Source
- Spectral
- Linting
- API Governance
---

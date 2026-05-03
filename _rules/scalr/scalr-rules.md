---
api_specs:
- filename: scalr-user-openapi.yml
  format: yaml
  label: Scalr User API
  slug: scalr-user-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scalr/refs/heads/main/openapi/scalr-user-openapi.yml
- filename: scalr-account-openapi.yml
  format: yaml
  label: Scalr Account API
  slug: scalr-account-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scalr/refs/heads/main/openapi/scalr-account-openapi.yml
- filename: scalr-global-openapi.yml
  format: yaml
  label: Scalr Global API
  slug: scalr-global-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scalr/refs/heads/main/openapi/scalr-global-openapi.yml
categories:
- scalr
description: Spectral linting rules defining API design standards and conventions for Scalr.
layout: rules
name: Scalr API Rules
provider_name: Scalr
provider_slug: scalr
rule_count: 10
rules:
- description: Scalr operation summaries should use Title Case
  given: $.paths[*][*].summary
  name: scalr-summary-title-case
  severity: warn
- description: Scalr API paths should use kebab-case for resource names
  given: $.paths
  name: scalr-path-kebab-case
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: scalr-response-200-defined
  severity: error
- description: Scalr legacy API uses Swagger 2.0
  given: $
  name: scalr-swagger-version
  severity: info
- description: Scalr APIs use envId path parameter for environment scoping
  given: $.paths
  name: scalr-env-id-path-param
  severity: info
- description: List operations should support filtering and pagination
  given: $.paths[*].get.parameters[*]
  name: scalr-pagination-filter
  severity: warn
- description: Scalr API uses API key Bearer token authentication
  given: $.securityDefinitions
  name: scalr-bearer-auth
  severity: warn
- description: API info must include a description
  given: $.info
  name: scalr-info-description
  severity: error
- description: Scalr farm resources use consistent naming conventions
  given: $.paths
  name: scalr-farm-resource-naming
  severity: hint
- description: Scalr uses /actions/ sub-path for operations like launch, terminate, clone
  given: $.paths
  name: scalr-actions-sub-path
  severity: hint
rules_file: rules/scalr-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scalr/refs/heads/main/rules/scalr-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 2
  warn: 4
slug: scalr-rules
source_filename: scalr-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  scalr-summary-title-case:\n    description: Scalr operation summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  scalr-path-kebab-case:\n    description: Scalr API paths should use kebab-case for resource names\n    message: \"Path should use lowercase kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/\"\n\n  scalr-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: \"GET operation missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  scalr-swagger-version:\n    description: Scalr legacy API uses Swagger 2.0\n    message: \"Scalr legacy API uses Swagger\
  \ 2.0 format\"\n    severity: info\n    given: \"$\"\n    then:\n      field: swagger\n      function: defined\n\n  scalr-env-id-path-param:\n    description: Scalr APIs use envId path parameter for environment scoping\n    message: \"Environment-scoped operations should use envId path parameter\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"envId\"\n\n  scalr-pagination-filter:\n    description: List operations should support filtering and pagination\n    message: \"List operations should include filter and page parameters\"\n    severity: warn\n    given: \"$.paths[*].get.parameters[*]\"\n    then:\n      function: defined\n\n  scalr-bearer-auth:\n    description: Scalr API uses API key Bearer token authentication\n    message: \"Scalr API should use API key authentication\"\n    severity: warn\n    given: \"$.securityDefinitions\"\n    then:\n      function: defined\n\n  scalr-info-description:\n    description:\
  \ API info must include a description\n    message: \"API info.description is required\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: description\n      function: defined\n\n  scalr-farm-resource-naming:\n    description: Scalr farm resources use consistent naming conventions\n    message: \"Farm-related operations should follow farmId/farmRoleId naming\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: defined\n\n  scalr-actions-sub-path:\n    description: Scalr uses /actions/ sub-path for operations like launch, terminate, clone\n    message: \"Non-CRUD operations should be under /actions/ sub-path\"\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/actions/\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scalr/refs/heads/main/rules/scalr-rules.yml
tags:
- FinOps
- GitOps
- Infrastructure as Code
- Kubernetes
- OPA
- OpenTofu
- Policy
- Terraform
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: scaleway-instance-openapi.yml
  format: yaml
  label: Scaleway Instance API
  slug: scaleway-instance-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-instance-openapi.yml
- filename: scaleway-kubernetes-openapi.yml
  format: yaml
  label: Scaleway Kubernetes API
  slug: scaleway-kubernetes-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-kubernetes-openapi.yml
- filename: scaleway-iam-openapi.yml
  format: yaml
  label: Scaleway IAM API
  slug: scaleway-iam-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-iam-openapi.yml
- filename: scaleway-load-balancer-openapi.yml
  format: yaml
  label: Scaleway Load Balancer API
  slug: scaleway-load-balancer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-load-balancer-openapi.yml
- filename: scaleway-database-openapi.yml
  format: yaml
  label: Scaleway Managed Database API
  slug: scaleway-database-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-database-openapi.yml
- filename: scaleway-vpc-openapi.yml
  format: yaml
  label: Scaleway VPC API
  slug: scaleway-vpc-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-vpc-openapi.yml
- filename: scaleway-serverless-containers-openapi.yml
  format: yaml
  label: Scaleway Serverless Containers API
  slug: scaleway-serverless-containers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-serverless-containers-openapi.yml
- filename: scaleway-serverless-functions-openapi.yml
  format: yaml
  label: Scaleway Serverless Functions API
  slug: scaleway-serverless-functions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-serverless-functions-openapi.yml
- filename: scaleway-secret-manager-openapi.yml
  format: yaml
  label: Scaleway Secret Manager API
  slug: scaleway-secret-manager-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-secret-manager-openapi.yml
- filename: scaleway-transactional-email-openapi.yml
  format: yaml
  label: Scaleway Transactional Email API
  slug: scaleway-transactional-email-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/openapi/scaleway-transactional-email-openapi.yml
categories:
- scaleway
description: Spectral linting rules defining API design standards and conventions for Scaleway.
layout: rules
name: Scaleway API Rules
provider_name: Scaleway
provider_slug: scaleway
rule_count: 10
rules:
- description: Scaleway operation IDs use PascalCase (e.g., ListInstances, CreateCluster)
  given: $.paths[*][*].operationId
  name: scaleway-operation-id-pascal-case
  severity: warn
- description: Scaleway operation summaries should use Title Case
  given: $.paths[*][*].summary
  name: scaleway-summary-title-case
  severity: warn
- description: Scaleway API paths use kebab-case for resource names
  given: $.paths
  name: scaleway-path-kebab-case
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: scaleway-response-200-defined
  severity: error
- description: Scaleway API uses X-Auth-Token header authentication
  given: $.components.securitySchemes
  name: scaleway-bearer-auth-defined
  severity: warn
- description: Scaleway APIs use zone and region path parameters for geographic isolation
  given: $.paths[*][*].parameters[*]
  name: scaleway-zone-region-params
  severity: hint
- description: List operations should support page and page_size query parameters
  given: $.paths[*].get
  name: scaleway-pagination-params
  severity: warn
- description: Scaleway resources should support tags as arrays for resource organization
  given: $.components.schemas[*].properties
  name: scaleway-tags-array
  severity: hint
- description: Scaleway uses OpenAPI 3.1.0
  given: $
  name: scaleway-openapi-version
  severity: warn
- description: API info must include a description
  given: $.info
  name: scaleway-info-description
  severity: error
rules_file: rules/scaleway-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/rules/scaleway-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 6
slug: scaleway-rules
source_filename: scaleway-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  scaleway-operation-id-pascal-case:\n    description: Scaleway operation IDs use PascalCase (e.g., ListInstances, CreateCluster)\n    message: \"Operation ID '{{value}}' should use PascalCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n\n  scaleway-summary-title-case:\n    description: Scaleway operation summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  scaleway-path-kebab-case:\n    description: Scaleway API paths use kebab-case for resource names\n    message: \"Path segment '{{value}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9-{}/]+)+$\"\n\n\
  \  scaleway-response-200-defined:\n    description: All GET operations must define a 200 response\n    message: \"GET operation missing 200 response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  scaleway-bearer-auth-defined:\n    description: Scaleway API uses X-Auth-Token header authentication\n    message: \"Scaleway API should define X-Auth-Token security scheme\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: defined\n\n  scaleway-zone-region-params:\n    description: Scaleway APIs use zone and region path parameters for geographic isolation\n    message: \"Consider using zone or region path parameters for geographic resource management\"\n    severity: hint\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  scaleway-pagination-params:\n    description: List operations\
  \ should support page and page_size query parameters\n    message: \"List operations should include pagination parameters\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      function: defined\n\n  scaleway-tags-array:\n    description: Scaleway resources should support tags as arrays for resource organization\n    message: \"Resource should support tags array property\"\n    severity: hint\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: defined\n\n  scaleway-openapi-version:\n    description: Scaleway uses OpenAPI 3.1.0\n    message: \"Scaleway APIs should use OpenAPI version 3.1.0\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.1\\\\.\"\n\n  scaleway-info-description:\n    description: API info must include a description\n    message: \"API info.description is required\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field:\
  \ description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/scaleway/refs/heads/main/rules/scaleway-rules.yml
tags:
- AI
- Cloud Computing
- Containers
- Database
- European Cloud
- Infrastructure
- Kubernetes
- Serverless
- Storage
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: spot-by-netapp-openapi.yml
  format: yaml
  label: Spot by NetApp API
  slug: spot-by-netapp
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/spot-by-netapp/refs/heads/main/openapi/spot-by-netapp-openapi.yml
categories:
- spot
description: Spectral linting rules defining API design standards and conventions for Spot by NetApp.
layout: rules
name: Spot by NetApp API Rules
provider_name: Spot by NetApp
provider_slug: spot-by-netapp
rule_count: 11
rules:
- description: Spot API must use Bearer token authentication.
  given: $.components.securitySchemes
  name: spot-bearer-auth
  severity: error
- description: Spot API responses should use the request/response envelope pattern.
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: spot-response-envelope
  severity: warn
- description: Cloud provider paths should be prefixed with the provider name.
  given: $.paths
  name: spot-cloud-path-prefix
  severity: warn
- description: All operations must have an operationId.
  given: $.paths[*][*]
  name: spot-operation-id
  severity: error
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: spot-operation-id-camel-case
  severity: error
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: spot-operation-tags
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: spot-summary-title-case
  severity: warn
- description: Operations that are account-scoped should accept an accountId query parameter.
  given: $.paths[*].get
  name: spot-account-id-param
  severity: warn
- description: All operations must define a 200 response.
  given: $.paths[*][*]
  name: spot-200-response
  severity: error
- description: Operations should document the 401 unauthorized response.
  given: $.paths[*][*]
  name: spot-401-response
  severity: warn
- description: API must define the Spot production server URL.
  given: $.servers[*].url
  name: spot-server-production
  severity: error
rules_file: rules/spot-by-netapp-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/spot-by-netapp/refs/heads/main/rules/spot-by-netapp-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 0
  warn: 5
slug: spot-by-netapp-rules
source_filename: spot-by-netapp-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Spot by NetApp API-specific conventions\n\n  spot-bearer-auth:\n    description: Spot API must use Bearer token authentication.\n    message: \"API must define BearerAuth security scheme using HTTP Bearer scheme.\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: BearerAuth\n      function: truthy\n\n  spot-response-envelope:\n    description: Spot API responses should use the request/response envelope pattern.\n    message: \"GET responses should include a response object wrapping the result items.\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\n    then:\n      field: properties.response\n      function: truthy\n\n  spot-cloud-path-prefix:\n    description: Cloud provider paths should be prefixed with the provider name.\n    message: \"Path '{{property}}' for cloud providers should be prefixed with /aws/, /azure/, or /gcp/.\"\n    severity: warn\n\
  \    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/(aws|azure|gcp|ocean|setup|audit|events|healthCheck|insights|connect|security|cbi|cloudBilling|mcs|notificationCenter)\\\\/.*\"\n\n  spot-operation-id:\n    description: All operations must have an operationId.\n    message: \"Operation must have an operationId.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  spot-operation-id-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: error\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spot-operation-tags:\n    description: All operations must have at least one tag.\n    message: \"Operation must have at least one tag.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n\
  \      field: tags\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          minItems: 1\n\n  spot-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  spot-account-id-param:\n    description: Operations that are account-scoped should accept an accountId query parameter.\n    message: \"Account-scoped list operations should accept an accountId query parameter.\"\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  spot-200-response:\n    description: All operations must define a 200 response.\n    message: \"Operation must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field:\
  \ responses.200\n      function: truthy\n\n  spot-401-response:\n    description: Operations should document the 401 unauthorized response.\n    message: \"Operation should define a 401 response.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  spot-server-production:\n    description: API must define the Spot production server URL.\n    message: \"API must use https://api.spotinst.io as the production server.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.spotinst\\\\.io$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/spot-by-netapp/refs/heads/main/rules/spot-by-netapp-rules.yml
tags:
- Cloud Optimization
- FinOps
- Kubernetes
- Azure
- GCP
- Cost Optimization
- Auto Scaling
- Spectral
- Linting
- API Governance
---

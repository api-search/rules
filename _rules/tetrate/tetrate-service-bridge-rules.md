---
api_specs:
- filename: tetrate-service-bridge-openapi.yml
  format: yaml
  label: Tetrate Service Bridge REST API
  slug: tsb-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tetrate/refs/heads/main/openapi/tetrate-service-bridge-openapi.yml
categories:
- tsb
description: Spectral linting rules defining API design standards and conventions for Tetrate.
layout: rules
name: Tetrate API Rules
provider_name: Tetrate
provider_slug: tetrate
rule_count: 9
rules:
- description: All TSB REST API paths must start with /v2/
  given: $.paths[*]~
  name: tsb-path-version-prefix
  severity: error
- description: Organization-scoped resources must include {organization} path parameter
  given: $.paths[?(@property.startsWith('/v2/organizations/'))]
  name: tsb-org-scoped-paths
  severity: warn
- description: All operationIds must be camelCase
  given: $.paths[*][*].operationId
  name: tsb-operation-id-camel-case
  severity: warn
- description: Successful responses must return application/json content type
  given: $.paths[*][get,post,put].responses.200
  name: tsb-200-content-type-json
  severity: warn
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: tsb-delete-no-body
  severity: warn
- description: All named schemas must have a description
  given: $.components.schemas[*]
  name: tsb-schema-description
  severity: warn
- description: POST, PUT, DELETE operations must have security defined
  given: $.paths[*][post,put,delete]
  name: tsb-security-on-mutations
  severity: error
- description: Tags must use Title Case format
  given: $.paths[*][*].tags[*]
  name: tsb-tags-title-case
  severity: warn
- description: List operations (operationId starting with 'list') must return an array property
  given: $.paths[*].get[?(@.operationId && @.operationId.startsWith('list'))]
  name: tsb-list-returns-array
  severity: info
rules_file: rules/tetrate-service-bridge-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tetrate/refs/heads/main/rules/tetrate-service-bridge-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: tetrate-service-bridge-rules
source_filename: tetrate-service-bridge-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # TSB-specific: All paths must start with /v2/\n  tsb-path-version-prefix:\n    description: All TSB REST API paths must start with /v2/\n    message: Path \"{{value}}\" must start with /v2/\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v2/\"\n\n  # TSB resource hierarchy: org-scoped resources must include organization param\n  tsb-org-scoped-paths:\n    description: Organization-scoped resources must include {organization} path parameter\n    message: Paths scoped to an organization must contain {organization} parameter\n    severity: warn\n    given: \"$.paths[?(@property.startsWith('/v2/organizations/'))]\"\n    then:\n      function: truthy\n\n  # TSB: operationIds must be camelCase\n  tsb-operation-id-camel-case:\n    description: All operationIds must be camelCase\n    message: OperationId \"{{value}}\" should be camelCase\n    severity: warn\n    given:\
  \ \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # TSB: responses must include etag for mutable resources\n  tsb-200-content-type-json:\n    description: Successful responses must return application/json content type\n    message: Response 200 must have application/json content\n    severity: warn\n    given: \"$.paths[*][get,post,put].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  # TSB: DELETE operations should not have a request body\n  tsb-delete-no-body:\n    description: DELETE operations should not have a request body\n    message: DELETE operation should not include requestBody\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: requestBody\n      function: falsy\n\n  # TSB: All schemas must have descriptions\n  tsb-schema-description:\n    description: All named schemas must have a description\n    message: Schema \"{{path}}\" must have\
  \ a description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # TSB: Security must be defined on all mutating operations\n  tsb-security-on-mutations:\n    description: POST, PUT, DELETE operations must have security defined\n    message: Mutating operation must define security requirements\n    severity: error\n    given: \"$.paths[*][post,put,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [security]\n            - {}\n\n  # TSB: Tags must use Title Case\n  tsb-tags-title-case:\n    description: Tags must use Title Case format\n    message: Tag \"{{value}}\" should use Title Case\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z]*(\\\\s[A-Z][a-zA-Z]*)*$\"\n\n  # TSB: Resource list operations must return arrays\n  tsb-list-returns-array:\n\
  \    description: List operations (operationId starting with 'list') must return an array property\n    message: List operation should return a response with an array property\n    severity: info\n    given: \"$.paths[*].get[?(@.operationId && @.operationId.startsWith('list'))]\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tetrate/refs/heads/main/rules/tetrate-service-bridge-rules.yml
tags:
- Enterprise
- Envoy
- Istio
- Kubernetes
- Service Mesh
- Spectral
- Linting
- API Governance
---

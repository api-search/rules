---
api_specs:
- filename: hcp-terraform-openapi.yml
  format: yaml
  label: HCP Terraform API
  slug: hcp-terraform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/terraform/refs/heads/main/openapi/hcp-terraform-openapi.yml
- filename: terraform-registry-openapi.yml
  format: yaml
  label: Terraform Registry API
  slug: terraform-registry-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/terraform/refs/heads/main/openapi/terraform-registry-openapi.yml
categories:
- terraform
description: Spectral linting rules defining API design standards and conventions for Terraform.
layout: rules
name: Terraform API Rules
provider_name: Terraform
provider_slug: terraform
rule_count: 10
rules:
- description: HCP Terraform API endpoints should use JSON API content type (application/vnd.api+json)
  given: $.paths..content
  name: terraform-jsonapi-content-type
  severity: warn
- description: All operations must have operationId defined
  given: $.paths.*[get,post,put,patch,delete]
  name: terraform-operation-ids-present
  severity: error
- description: Operation IDs should use PascalCase
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: terraform-operation-id-casing
  severity: warn
- description: URL path segments should use kebab-case or path parameters
  given: $.paths
  name: terraform-path-kebab-case
  severity: warn
- description: HCP Terraform API uses bearer token authentication
  given: $.components.securitySchemes.*
  name: terraform-bearer-auth
  severity: warn
- description: Non-delete operations should have 200 or 201 responses
  given: $.paths.*[get,post,patch]
  name: terraform-response-200-or-201
  severity: warn
- description: DELETE operations should return 204 No Content
  given: $.paths.*.delete
  name: terraform-delete-204
  severity: warn
- description: Path and query parameters should have descriptions
  given: $.paths..parameters[*]
  name: terraform-parameter-descriptions
  severity: warn
- description: Each operation should have at least one tag
  given: $.paths.*[get,post,put,patch,delete]
  name: terraform-tags-required
  severity: warn
- description: GET list operations should support pagination parameters
  given: $.paths.*[get]
  name: terraform-pagination-parameters
  severity: info
rules_file: rules/hcp-terraform-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/terraform/refs/heads/main/rules/hcp-terraform-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 8
slug: hcp-terraform-rules
source_filename: hcp-terraform-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  terraform-jsonapi-content-type:\n    description: HCP Terraform API endpoints should use JSON API content type (application/vnd.api+json)\n    message: \"{{description}}: {{value}} should be application/vnd.api+json\"\n    severity: warn\n    given: \"$.paths..content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            \"application/vnd.api+json\":\n              type: object\n\n  terraform-operation-ids-present:\n    description: All operations must have operationId defined\n    message: \"Operation at {{path}} is missing operationId\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  terraform-operation-id-casing:\n    description: Operation IDs should use PascalCase\n    message: \"Operation ID '{{value}}' should use PascalCase (e.g., ListWorkspaces, CreateRun)\"\n\
  \    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][A-Za-z0-9]+$\"\n\n  terraform-path-kebab-case:\n    description: URL path segments should use kebab-case or path parameters\n    message: \"Path segment '{{value}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-zA-Z_]+\\\\}))*$\"\n\n  terraform-bearer-auth:\n    description: HCP Terraform API uses bearer token authentication\n    message: \"Security scheme should be bearer type\"\n    severity: warn\n    given: \"$.components.securitySchemes.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - properties:\n                type:\n                  const: http\n                scheme:\n                  const:\
  \ bearer\n            - properties:\n                type:\n                  const: apiKey\n\n  terraform-response-200-or-201:\n    description: Non-delete operations should have 200 or 201 responses\n    message: \"Operation should define a 200 or 201 response\"\n    severity: warn\n    given: \"$.paths.*[get,post,patch]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n              anyOf:\n                - required: [\"200\"]\n                - required: [\"201\"]\n\n  terraform-delete-204:\n    description: DELETE operations should return 204 No Content\n    message: \"DELETE operation should return 204 No Content\"\n    severity: warn\n    given: \"$.paths.*.delete\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            responses:\n              type: object\n            \
  \  required: [\"204\"]\n\n  terraform-parameter-descriptions:\n    description: Path and query parameters should have descriptions\n    message: \"Parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths..parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  terraform-tags-required:\n    description: Each operation should have at least one tag\n    message: \"Operation at {{path}} should have at least one tag\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  terraform-pagination-parameters:\n    description: GET list operations should support pagination parameters\n    message: \"List endpoints should support page[number] or page[size] parameters\"\n    severity: info\n    given: \"$.paths.*[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/terraform/refs/heads/main/rules/hcp-terraform-rules.yml
tags:
- Infrastructure As Code
- Cloud Infrastructure
- DevOps
- Open Source
- HashiCorp
- Spectral
- Linting
- API Governance
---

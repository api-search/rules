---
categories:
- deprecation
- info
- method
- 'no'
- openapi
- operation
- parameter
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for AWS App Mesh.
layout: rules
name: AWS App Mesh API Rules
provider_name: AWS App Mesh
provider_slug: aws-app-mesh
rule_count: 19
rules:
- description: API title must start with "AWS App Mesh"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: Info object must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Info object must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: All specs must use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "AWS App Mesh"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationIds should use PascalCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-pascal-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All responses must have descriptions
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description
  severity: warn
- description: Security schemes should be defined in components
  given: $
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: method-get-no-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: Deprecated operations should have a description
  given: $.paths[*][*][?(@.deprecated == true)]
  name: deprecation-documented
  severity: warn
rules_file: rules/aws-app-mesh-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-app-mesh/refs/heads/main/rules/aws-app-mesh-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 0
  warn: 8
slug: aws-app-mesh-spectral-rules
tags:
- AWS
- Deprecated
- Envoy
- Microservices
- Networking
- Service Mesh
- Spectral
- Linting
- API Governance
---

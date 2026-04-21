---
categories:
- info
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Azure Container Apps.
layout: rules
name: Azure Container Apps API Rules
provider_name: Azure Container Apps
provider_slug: azure-container-apps
rule_count: 17
rules:
- description: API title must start with "Azure Container Apps"
  given: $.info.title
  name: info-title-format
  severity: warn
- description: Operation summaries must start with "Azure Container Apps"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: All operations must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: error
- description: Must use OpenAPI 3.x
  given: $.openapi
  name: openapi-version
  severity: error
- description: Servers must be defined
  given: $
  name: servers-defined
  severity: error
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: error
- description: Security schemes must be defined
  given: $.components.securitySchemes
  name: security-defined
  severity: warn
- description: Operations must define at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All schemas must define a type
  given: $.components.schemas[*]
  name: schema-type-required
  severity: warn
- description: Global tag names should use Title Case
  given: $.tags[*].name
  name: tags-title-case
  severity: info
- description: OperationIds should use PascalCase with underscore separator
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: info
rules_file: rules/azure-container-apps-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/azure-container-apps/refs/heads/main/rules/azure-container-apps-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 2
  warn: 8
slug: azure-container-apps-spectral-rules
tags:
- Azure
- Containers
- Dapr
- Kubernetes
- Microservices
- Serverless
- Spectral
- Linting
- API Governance
---

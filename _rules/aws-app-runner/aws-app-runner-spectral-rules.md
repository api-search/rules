---
categories:
- info
- method
- 'no'
- openapi
- operation
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for AWS App Runner.
layout: rules
name: AWS App Runner API Rules
provider_name: AWS App Runner
provider_slug: aws-app-runner
rule_count: 17
rules:
- description: API title must start with "AWS App Runner"
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
- description: Operation summaries must start with "AWS App Runner"
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
- description: All responses must have descriptions
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description
  severity: warn
- description: Security schemes should be defined
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
rules_file: rules/aws-app-runner-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/aws-app-runner/refs/heads/main/rules/aws-app-runner-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 0
  warn: 5
slug: aws-app-runner-spectral-rules
tags:
- AWS
- CI/CD
- Containers
- Deployment
- Microservices
- Serverless
- Spectral
- Linting
- API Governance
---

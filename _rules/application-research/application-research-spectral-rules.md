---
categories:
- http
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Application Research.
layout: rules
name: Application Research API Rules
provider_name: Application Research
provider_slug: application-research
rule_count: 19
rules:
- description: API title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: API description should be present
  given: $.info
  name: info-description-required
  severity: warn
- description: License should be specified (research specs use Apache 2.0)
  given: $.info
  name: info-license-required
  severity: warn
- description: OpenAPI version must be 3.0.x or 3.1.x
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Each server must have a description
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not end with trailing slash
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: operation-success-response-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas must have a title
  given: $.components.schemas[*]
  name: schema-title-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: http-get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/application-research-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/application-research/refs/heads/main/rules/application-research-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 10
slug: application-research-spectral-rules
tags:
- Application Dependencies
- Cloud Native
- Integration
- Research
- Specifications
- Workload Specifications
- Spectral
- Linting
- API Governance
---

---
categories:
- get
- info
- 'no'
- operation
- parameter
- paths
- response
- security
description: Spectral linting rules defining API design standards and conventions for Argo CD.
layout: rules
name: Argo CD API Rules
provider_name: Argo CD
provider_slug: argo-cd
rule_count: 18
rules:
- description: API title must start with "Argo CD"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: API must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Argo CD"
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-title-case
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: All paths should be versioned with /api/v1/
  given: $.paths[*]~
  name: paths-versioned
  severity: info
- description: All parameters must have a description
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a success response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: API must define security schemes
  given: $
  name: security-definitions-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Summaries must not be empty strings
  given: $.paths[*][get,post,put,delete,patch].summary
  name: no-empty-summaries
  severity: error
- description: OperationIds should use camelCase or ServiceName_MethodName pattern
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: operation-id-camel-case
  severity: info
rules_file: rules/argo-cd-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/argo-cd/refs/heads/main/rules/argo-cd-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 2
  warn: 9
slug: argo-cd-spectral-rules
tags:
- Continuous Delivery
- Containers
- Deployment
- GitOps
- Kubernetes
- CNCF
- Open Source
- Spectral
- Linting
- API Governance
---

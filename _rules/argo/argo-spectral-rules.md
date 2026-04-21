---
categories:
- info
- 'no'
- operation
- paths
- response
description: Spectral linting rules defining API design standards and conventions for Argo.
layout: rules
name: Argo API Rules
provider_name: Argo
provider_slug: argo
rule_count: 9
rules:
- description: API title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: Operations should be tagged
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: All paths should be versioned
  given: $.paths[*]~
  name: paths-versioned
  severity: info
- description: Every operation must define at least one response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Summaries must not be empty
  given: $.paths[*][get,post,put,delete,patch].summary
  name: no-empty-summaries
  severity: error
rules_file: rules/argo-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/argo/refs/heads/main/rules/argo-spectral-rules.yml
severity_counts:
  error: 6
  hint: 0
  info: 1
  warn: 2
slug: argo-spectral-rules
tags:
- CNCF
- CI/CD
- GitOps
- Kubernetes
- Open Source
- Progressive Delivery
- Workflow Engine
- Spectral
- Linting
- API Governance
---

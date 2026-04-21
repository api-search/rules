---
categories:
- info
- 'no'
- operation
- parameter
- paths
- response
- security
description: Spectral linting rules defining API design standards and conventions for Argo Workflows.
layout: rules
name: Argo Workflows API Rules
provider_name: Argo Workflows
provider_slug: argo-workflows
rule_count: 13
rules:
- description: API title must start with "Argo Workflows"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Argo Workflows"
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: All paths should be versioned
  given: $.paths[*]~
  name: paths-versioned
  severity: info
- description: Path segments should use kebab-case or camelCase
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: Every operation must define at least one response
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
- description: Summaries must not be empty
  given: $.paths[*][get,post,put,delete,patch].summary
  name: no-empty-summaries
  severity: error
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
rules_file: rules/argo-workflows-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/argo-workflows/refs/heads/main/rules/argo-workflows-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 6
slug: argo-workflows-spectral-rules
tags:
- CNCF
- Containers
- Data Processing
- Kubernetes
- Machine Learning
- Open Source
- Workflow Engine
- Spectral
- Linting
- API Governance
---

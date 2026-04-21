---
categories:
- info
- 'no'
- operation
- parameter
- paths
- response
- schema
- security
description: Spectral linting rules defining API design standards and conventions for ARGUS Enterprise.
layout: rules
name: ARGUS Enterprise API Rules
provider_name: ARGUS Enterprise
provider_slug: argus-enterprise
rule_count: 14
rules:
- description: API title should start with "Argus Enterprise"
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
- description: Summaries should start with "Argus Enterprise"
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationid-required
  severity: error
- description: Operations must be tagged
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Paths should be versioned
  given: $.paths[*]~
  name: paths-versioned
  severity: info
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Every operation must define responses
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: API must define security schemes
  given: $
  name: security-definitions-required
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-description
  severity: info
- description: Summaries must not be empty
  given: $.paths[*][get,post,put,delete,patch].summary
  name: no-empty-summaries
  severity: error
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
rules_file: rules/argus-enterprise-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/argus-enterprise/refs/heads/main/rules/argus-enterprise-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 7
slug: argus-enterprise-spectral-rules
tags:
- Altus Group
- Asset Management
- Cash Flow Modeling
- Commercial Real Estate
- Portfolio Management
- Valuation
- Spectral
- Linting
- API Governance
---

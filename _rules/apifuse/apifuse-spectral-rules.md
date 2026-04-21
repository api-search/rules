---
categories:
- info
- operation
- parameter
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apifuse.
layout: rules
name: Apifuse API Rules
provider_name: Apifuse
provider_slug: apifuse
rule_count: 10
rules:
- description: API title must start with 'Apifuse'.
  given: $.info
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Operation summaries must start with 'Apifuse'.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: OperationId must use camelCase.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-camelcase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Schema properties must have a type defined.
  given: $.components.schemas[*].properties[*]
  name: schema-property-type-required
  severity: warn
rules_file: rules/apifuse-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apifuse/refs/heads/main/rules/apifuse-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: apifuse-spectral-rules
tags:
- Embedded Integrations
- Integration Platform
- Integrations
- iPaaS
- Marketplace
- SaaS
- Workflow Automation
- Spectral
- Linting
- API Governance
---

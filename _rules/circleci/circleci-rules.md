---
categories:
- circleci
description: Spectral linting rules defining API design standards and conventions for CircleCI.
layout: rules
name: CircleCI API Rules
provider_name: CircleCI
provider_slug: circleci
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: circleci-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: circleci-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: circleci-server-https
  severity: error
- description: REST v2 server URLs must include /api/v2.
  given: $.servers[?(@.url && @.url.indexOf('circleci.com') > -1)].url
  name: circleci-server-versioned
  severity: warn
- description: A Circle-Token API key security scheme must be defined.
  given: $.components.securitySchemes
  name: circleci-token-security
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: circleci-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: circleci-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: circleci-operation-id
  severity: error
- description: Mutating operations should declare 4xx/5xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: circleci-error-responses
  severity: warn
- description: List endpoints should support page-token pagination.
  given: $.paths[?(@property.match(/list$|projects$|workflows$|jobs$|pipelines$/))].get.parameters[*].name
  name: circleci-pagination-cursor
  severity: info
rules_file: rules/circleci-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/circleci/refs/heads/main/rules/circleci-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: circleci-rules
tags:
- CI/CD
- Continuous Integration
- Continuous Deployment
- DevOps
- Pipelines
- Workflows
- Spectral
- Linting
- API Governance
---

---
categories:
- cloudbees
description: Spectral linting rules defining API design standards and conventions for CloudBees.
layout: rules
name: CloudBees API Rules
provider_name: CloudBees
provider_slug: cloudbees
rule_count: 12
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudbees-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudbees-info-license
  severity: warn
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cloudbees-server-https
  severity: error
- description: CloudBees Feature Management server URLs must point at x-api.rollout.io.
  given: $.servers[?(@.url && @.url.indexOf('rollout.io') > -1)].url
  name: cloudbees-feature-mgmt-base
  severity: warn
- description: CloudBees CD/RO server URLs must include /rest/v1.0.
  given: $.servers[?(@.url && @.url.indexOf('cloudbees') > -1 && @.url.indexOf('cd') > -1)].url
  name: cloudbees-cd-versioned
  severity: warn
- description: A bearer or basic security scheme must be declared.
  given: $.components.securitySchemes
  name: cloudbees-bearer-or-basic
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudbees-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudbees-operation-summary
  severity: warn
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudbees-operation-id
  severity: error
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudbees-error-responses
  severity: warn
- description: Feature Management endpoints should document the 555 rate-limit response.
  given: $.paths[?(@property.match(/applications|environments|flags|experiments/))][*].responses
  name: cloudbees-rate-limit-555
  severity: info
- description: List endpoints should support page/limit pagination params.
  given: $.paths[?(@property.match(/applications$|environments$|flags$|experiments$|audit$/))].get.parameters[*].name
  name: cloudbees-pagination
  severity: info
rules_file: rules/cloudbees-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudbees/refs/heads/main/rules/cloudbees-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 2
  warn: 6
slug: cloudbees-rules
tags:
- CI/CD
- Continuous Delivery
- Continuous Integration
- DevOps
- Feature Flags
- Feature Management
- Jenkins
- Release Orchestration
- Software Delivery
- Spectral
- Linting
- API Governance
---

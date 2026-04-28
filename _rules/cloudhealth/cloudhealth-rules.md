---
categories:
- cloudhealth
description: Spectral linting rules defining API design standards and conventions for CloudHealth.
layout: rules
name: CloudHealth API Rules
provider_name: CloudHealth
provider_slug: cloudhealth
rule_count: 10
rules:
- description: API contact information must be present.
  given: $.info
  name: cloudhealth-info-contact
  severity: error
- description: API license must be declared.
  given: $.info
  name: cloudhealth-info-license
  severity: warn
- description: All server URLs must use HTTPS for the chapi.cloudhealthtech.com control plane.
  given: $.servers[*].url
  name: cloudhealth-server-https
  severity: error
- description: Server URLs should target chapi.cloudhealthtech.com.
  given: $.servers[*].url
  name: cloudhealth-server-host
  severity: warn
- description: CloudHealth REST API paths should be versioned (/v{N}/) where applicable.
  given: $.paths
  name: cloudhealth-versioned-paths
  severity: warn
- description: A bearer security scheme must be declared.
  given: $.components.securitySchemes
  name: cloudhealth-auth-required
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudhealth-operation-id
  severity: error
- description: Every operation must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudhealth-operation-tags
  severity: warn
- description: Every operation must include a short summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: cloudhealth-operation-summary
  severity: warn
- description: Mutating operations should declare 4xx error responses.
  given: $.paths[*][post,put,patch,delete].responses
  name: cloudhealth-error-responses
  severity: warn
rules_file: rules/cloudhealth-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cloudhealth/refs/heads/main/rules/cloudhealth-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 6
slug: cloudhealth-rules
tags:
- Cloud Cost
- Cloud Governance
- Cloud Management
- Cost Optimization
- FinOps
- Multi-Cloud
- Spectral
- Linting
- API Governance
---

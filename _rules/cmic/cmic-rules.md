---
categories:
- cmic
description: Spectral linting rules defining API design standards and conventions for CMiC.
layout: rules
name: CMiC API Rules
provider_name: CMiC
provider_slug: cmic
rule_count: 9
rules:
- description: API contact information must be present.
  given: $.info
  name: cmic-info-contact
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: cmic-server-https
  severity: error
- description: Production server should target api.cmic.ca.
  given: $.servers[*].url
  name: cmic-server-host
  severity: warn
- description: An OAuth 2.0 security scheme must be defined.
  given: $.components.securitySchemes[*]
  name: cmic-oauth-security
  severity: error
- description: Every operation must declare a unique operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: cmic-operation-id
  severity: error
- description: Operations must declare at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: cmic-operation-tags
  severity: warn
- description: List GET operations should accept limit and offset parameters.
  given: $.paths[*].get[?(@.operationId && @.operationId.match(/^list/))]
  name: cmic-list-pagination
  severity: warn
- description: Operations must declare 401 and 403 responses.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: cmic-error-responses
  severity: warn
- description: Server URLs should include the /rest base path.
  given: $.servers[?(@.url && @.url.indexOf('api.cmic.ca') > -1)].url
  name: cmic-rest-base-path
  severity: warn
rules_file: rules/cmic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/cmic/refs/heads/main/rules/cmic-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: cmic-rules
tags:
- Construction
- ERP
- Finance
- Project Management
- Spectral
- Linting
- API Governance
---

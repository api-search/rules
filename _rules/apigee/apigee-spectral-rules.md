---
categories:
- delete
- info
- operation
- parameter
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apigee.
layout: rules
name: Apigee API Rules
provider_name: Apigee
provider_slug: apigee
rule_count: 14
rules:
- description: API title must start with 'Apigee'.
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
- description: Apigee API servers should be on *.googleapis.com.
  given: $.servers[*]
  name: servers-googleapis
  severity: info
- description: Operation summaries must be in Title Case.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-title-case
  severity: warn
- description: Operation summaries must start with 'Apigee'.
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
- description: DELETE operations should return 200 or 204.
  given: $.paths[*].delete.responses
  name: delete-returns-200-or-204
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: Apigee APIs must define OAuth2 security.
  given: $.components.securitySchemes
  name: security-oauth2-required
  severity: error
rules_file: rules/apigee-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apigee/refs/heads/main/rules/apigee-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 7
slug: apigee-spectral-rules
tags:
- Analytics
- API Gateway
- API Governance
- API Hub
- API Management
- Developer Portal
- Enterprise
- Hybrid
- Integrations
- Microservices
- Monetization
- Spectral
- Linting
- API Governance
---

---
categories:
- external
- http
- info
- 'no'
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apple Pay.
layout: rules
name: Apple Pay API Rules
provider_name: Apple Pay
provider_slug: apple-pay
rule_count: 24
rules:
- description: API title should start with "Apple Pay"
  given: $.info
  name: info-title-apple-prefix
  severity: warn
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: API description must be present
  given: $.info
  name: info-description-required
  severity: warn
- description: Contact information should be provided
  given: $.info
  name: info-contact-required
  severity: info
- description: Terms of service URL should be provided for payment APIs
  given: $.info
  name: info-terms-of-service
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS for payment APIs
  given: $.servers[*]
  name: servers-https
  severity: error
- description: Each server must have a description distinguishing production from sandbox
  given: $.servers[*]
  name: servers-description-required
  severity: warn
- description: Global security scheme must be defined for payment APIs
  given: $
  name: security-defined
  severity: error
- description: Security schemes must be defined in components
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Path segments must use camelCase or kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: operation-success-response-required
  severity: error
- description: Payment APIs must define 401 Unauthorized responses
  given: $.paths[*][post].responses
  name: response-401-for-payment-apis
  severity: warn
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas must have a title
  given: $.components.schemas[*]
  name: schema-title-required
  severity: warn
- description: Component schemas should have a description
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: http-get-no-request-body
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: External documentation links are encouraged for payment APIs
  given: $
  name: external-docs-encouraged
  severity: info
rules_file: rules/apple-pay-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apple-pay/refs/heads/main/rules/apple-pay-spectral-rules.yml
severity_counts:
  error: 10
  hint: 0
  info: 2
  warn: 12
slug: apple-pay-spectral-rules
tags:
- Apple
- Contactless Payments
- Digital Wallet
- E-Commerce
- Mobile Payments
- Payments
- Spectral
- Linting
- API Governance
---

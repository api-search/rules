---
categories:
- atandt
description: Spectral linting rules defining API design standards and conventions for AT&T.
layout: rules
name: AT&T API Rules
provider_name: AT&T
provider_slug: atandt
rule_count: 27
rules:
- description: AT&T APIs must have a title in the info object
  given: $.info
  name: atandt-info-title-required
  severity: error
- description: AT&T APIs must include a description
  given: $.info
  name: atandt-info-description-required
  severity: error
- description: AT&T APIs must specify a version
  given: $.info
  name: atandt-info-version-required
  severity: error
- description: AT&T APIs must include contact information
  given: $.info
  name: atandt-info-contact-required
  severity: warn
- description: AT&T APIs must include terms of service
  given: $.info
  name: atandt-info-terms-required
  severity: warn
- description: AT&T APIs must use OpenAPI 3.0.x
  given: $
  name: atandt-openapi-version
  severity: error
- description: AT&T APIs must define at least one server
  given: $
  name: atandt-servers-required
  severity: error
- description: AT&T API servers must use HTTPS
  given: $.servers[*]
  name: atandt-server-url-https
  severity: error
- description: AT&T API servers should use att.com domains
  given: $.servers[*]
  name: atandt-server-att-domain
  severity: warn
- description: All AT&T API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: atandt-operation-id-required
  severity: error
- description: All AT&T API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: atandt-operation-summary-required
  severity: error
- description: All AT&T API operations must have a description
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: atandt-operation-description-required
  severity: warn
- description: All AT&T API operations must have tags
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: atandt-operation-tags-required
  severity: warn
- description: All AT&T API parameters must have a description
  given: $.paths[*][*].parameters[*]
  name: atandt-parameter-description-required
  severity: warn
- description: Path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: atandt-path-parameter-required
  severity: error
- description: AT&T API request bodies must define content
  given: $.paths[*][*].requestBody
  name: atandt-request-body-content-required
  severity: error
- description: AT&T API request bodies should support application/json
  given: $.paths[*][*].requestBody.content
  name: atandt-request-body-json
  severity: warn
- description: All AT&T API responses must have a description
  given: $.paths[*][*].responses[*]
  name: atandt-response-description-required
  severity: error
- description: AT&T API operations must define at least one success response
  given: $.paths[*][get,post,put,patch,delete]
  name: atandt-success-response-required
  severity: error
- description: AT&T POST/PUT/PATCH operations should define 400 response
  given: $.paths[*][post,put,patch].responses
  name: atandt-error-400-defined
  severity: warn
- description: AT&T API operations should define 401 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: atandt-error-401-defined
  severity: warn
- description: AT&T API component schemas must have a type
  given: $.components.schemas[*]
  name: atandt-schema-type-required
  severity: warn
- description: AT&T API component schemas must have a description
  given: $.components.schemas[*]
  name: atandt-schema-description-required
  severity: warn
- description: AT&T APIs must define security schemes
  given: $.components
  name: atandt-security-schemes-required
  severity: error
- description: AT&T APIs should use OAuth 2.0
  given: $.components.securitySchemes[*]
  name: atandt-security-oauth2
  severity: warn
- description: AT&T CAMARA APIs must use E.164 format for phone numbers
  given: $.components.schemas[*].properties.phoneNumber
  name: atandt-phone-number-e164
  severity: warn
- description: AT&T APIs must define top-level tags
  given: $
  name: atandt-tags-defined
  severity: warn
rules_file: rules/atandt-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/atandt/refs/heads/main/rules/atandt-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 0
  warn: 14
slug: atandt-spectral-rules
tags:
- Telecommunications
- Fortune 100
- Wireless
- Wireline
- Broadband
- Enterprise
- 5G
- Network
- Spectral
- Linting
- API Governance
---

---
categories:
- get
- info
- microcks
- openapi
- operation
- parameter
- paths
- rate
- request
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Ariba Sourcing.
layout: rules
name: Ariba Sourcing API Rules
provider_name: Ariba Sourcing
provider_slug: ariba-sourcing
rule_count: 28
rules:
- description: API title must be defined and follow the "Ariba Sourcing - {API Name}" pattern.
  given: $.info
  name: info-title-required
  severity: error
- description: API title should start with "Ariba Sourcing".
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API info must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: API version must be defined.
  given: $.info
  name: info-version-required
  severity: error
- description: APIs must use OpenAPI 3.0.x.
  given: $
  name: openapi-version-3
  severity: error
- description: Servers must be defined.
  given: $
  name: servers-required
  severity: error
- description: All server URLs must use HTTPS.
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Production server should use openapi.ariba.com host.
  given: $.servers[*].url
  name: servers-openapi-ariba-host
  severity: warn
- description: Paths must not have a trailing slash.
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Ariba Sourcing".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: error
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: All parameters must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: error
- description: SAP Ariba APIs require a realm query parameter.
  given: $.paths[*][get,post,put,patch,delete].parameters[?(@.name == 'realm')]
  name: parameter-realm-required
  severity: info
- description: Request bodies should have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description-recommended
  severity: warn
- description: Every operation must have a success response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Operations should define a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-recommended
  severity: warn
- description: Operations should define a 500 Internal Server Error response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-500-recommended
  severity: warn
- description: All responses must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: schema-property-description-recommended
  severity: info
- description: Security schemes must be defined in components.
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: error
- description: OAuth2 token URL should use api.ariba.com.
  given: $.components.securitySchemes.OAuth2.flows.clientCredentials.tokenUrl
  name: security-oauth2-token-url
  severity: warn
- description: Rate limit information should be documented in the API description.
  given: $.info.description
  name: rate-limits-documented
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Operations should include x-microcks-operation.
  given: $.paths[*][get,post,put,patch,delete]
  name: microcks-operation-extension
  severity: info
rules_file: rules/ariba-sourcing-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ariba-sourcing/refs/heads/main/rules/ariba-sourcing-spectral-rules.yml
severity_counts:
  error: 15
  hint: 0
  info: 4
  warn: 9
slug: ariba-sourcing-spectral-rules
tags:
- Approvals
- Auctions
- B2B
- Contracts
- Procurement
- RFx
- SAP
- Sourcing
- Supplier Management
- Supply Chain
- Spectral
- Linting
- API Governance
---

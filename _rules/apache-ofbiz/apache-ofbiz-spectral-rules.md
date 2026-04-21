---
categories:
- auth
- get
- info
- 'no'
- openapi
- operation
- parameter
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Apache OFBiz.
layout: rules
name: Apache OFBiz API Rules
provider_name: Apache OFBiz
provider_slug: apache-ofbiz
rule_count: 31
rules:
- description: OpenAPI info must have a title.
  given: $.info
  name: info-title-required
  severity: error
- description: OpenAPI info must have a description.
  given: $.info
  name: info-description-required
  severity: warn
- description: OpenAPI info must define a version.
  given: $.info
  name: info-version-required
  severity: error
- description: OpenAPI info should include contact information.
  given: $.info
  name: info-contact-required
  severity: warn
- description: OpenAPI info should include license information.
  given: $.info
  name: info-license-required
  severity: warn
- description: Specs must use OpenAPI 3.x.
  given: $
  name: openapi-version-3
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Server URLs should use HTTPS.
  given: $.servers[*].url
  name: servers-https
  severity: warn
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Operation summaries should start with "Apache OFBiz".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-apache-ofbiz-prefix
  severity: info
- description: Global tags array should be defined.
  given: $
  name: tags-global-defined
  severity: warn
- description: Each global tag should have a description.
  given: $.tags[*]
  name: tags-description
  severity: warn
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Secured operations should document 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level component schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: error
- description: Global security requirements should be defined.
  given: $
  name: security-global-defined
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Bearer authentication should specify JWT format.
  given: $.components.securitySchemes[?(@.scheme == 'bearer')]
  name: auth-bearer-jwt
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: OFBiz API responses should include statusCode, statusDescription, and data fields.
  given: $.components.schemas[*].properties
  name: response-status-code-standard
  severity: info
rules_file: rules/apache-ofbiz-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-ofbiz/refs/heads/main/rules/apache-ofbiz-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 4
  warn: 15
slug: apache-ofbiz-spectral-rules
tags:
- ERP
- CRM
- E-Commerce
- Business Applications
- Apache
- Java
- Open Source
- Supply Chain
- Spectral
- Linting
- API Governance
---

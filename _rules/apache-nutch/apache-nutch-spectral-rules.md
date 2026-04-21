---
categories:
- delete
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- security
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Apache Nutch.
layout: rules
name: Apache Nutch API Rules
provider_name: Apache Nutch
provider_slug: apache-nutch
rule_count: 33
rules:
- description: OpenAPI info must have a title.
  given: $.info
  name: info-title-required
  severity: error
- description: OpenAPI info must have a non-empty description.
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
- description: Each server should have a description.
  given: $.servers[*]
  name: servers-description
  severity: warn
- description: Path segments must use kebab-case (lowercase letters, numbers, hyphens).
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths should not have trailing slashes (except root).
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationid-required
  severity: error
- description: operationId should use camelCase.
  given: $.paths[*][get,post,put,patch,delete,head,options].operationId
  name: operation-operationid-camel-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Operation summaries should start with "Apache Nutch".
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-apache-nutch-prefix
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
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema.
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should have a description.
  given: $.paths[*][post,put,patch].requestBody
  name: request-body-description
  severity: warn
- description: Request bodies should support application/json content type.
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-json
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Secured operations should document 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-401-required
  severity: warn
- description: Operations should document 500 Internal Server Error response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-500-defined
  severity: info
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Top-level component schemas should have a description.
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: Schema properties should define a type.
  given: $.components.schemas[*].properties[*]
  name: schema-property-type-required
  severity: warn
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
- description: DELETE operations should not have a request body.
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-nutch-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-nutch/refs/heads/main/rules/apache-nutch-spectral-rules.yml
severity_counts:
  error: 12
  hint: 0
  info: 2
  warn: 19
slug: apache-nutch-spectral-rules
tags:
- Web Crawler
- Indexing
- Search
- Apache
- Java
- Hadoop
- Open Source
- Spectral
- Linting
- API Governance
---

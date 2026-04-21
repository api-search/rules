---
categories:
- delete
- examples
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Iceberg.
layout: rules
name: Apache Iceberg API Rules
provider_name: Apache Iceberg
provider_slug: apache-iceberg
rule_count: 28
rules:
- description: Info title must be present and start with Apache Iceberg
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a description with at least 20 characters
  given: $.info
  name: info-description-required
  severity: warn
- description: Info must have a version field
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version
  severity: error
- description: Servers must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs should use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Each server should have a description
  given: $.servers[*]
  name: servers-description-required
  severity: info
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache Iceberg
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-prefix
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every parameter must have a schema
  given: $.paths[*][get,post,put,patch,delete,head,options].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[*]
  name: response-description-required
  severity: error
- description: Operations should document 400 Bad Request responses
  given: $.paths[*][post,put,patch].responses
  name: response-error-400
  severity: info
- description: Operations should document 404 Not Found responses
  given: $.paths[*][get,delete].responses
  name: response-error-404
  severity: info
- description: Top-level schema objects should have descriptions
  given: $.components.schemas[*]
  name: schema-property-description
  severity: info
- description: Schema properties should have a type defined
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
- description: Security schemes must be defined
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Schema properties should include examples
  given: $.components.schemas[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/apache-iceberg-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-iceberg/refs/heads/main/rules/apache-iceberg-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 5
  warn: 12
slug: apache-iceberg-spectral-rules
tags:
- ACID
- Analytics
- Apache
- Data Lake
- Lakehouse
- Open Source
- Table Format
- Spectral
- Linting
- API Governance
---

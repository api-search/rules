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
- request
- response
- schema
- security
- servers
- tag
description: Spectral linting rules defining API design standards and conventions for Apache CouchDB.
layout: rules
name: Apache CouchDB API Rules
provider_name: Apache CouchDB
provider_slug: apache-couchdb
rule_count: 28
rules:
- description: OpenAPI info title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: OpenAPI info must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: OpenAPI info must include a version
  given: $.info
  name: info-version-required
  severity: error
- description: All specs must use OpenAPI 3.0.x
  given: $
  name: openapi-version-3
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Production servers should use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Path segments should use kebab-case (lowercase, hyphens allowed)
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: operationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationid-camel-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "Apache CouchDB"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: Every operation should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: All tags used in operations should be defined globally
  given: $
  name: tag-global-defined
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-schema-required
  severity: error
- description: Request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-type
  severity: warn
- description: Every operation must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: GET operations on resource paths should include a 404 response
  given: $.paths[*].get.responses
  name: response-404-for-get
  severity: warn
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
- description: Top-level schemas should have a type defined
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Security schemes must be defined if security is declared
  given: $
  name: security-schemes-defined
  severity: error
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
- description: Schema properties are encouraged to have examples
  given: $.components.schemas[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/apache-couchdb-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-couchdb/refs/heads/main/rules/apache-couchdb-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 2
  warn: 15
slug: apache-couchdb-spectral-rules
tags:
- Apache
- Database
- Document Store
- JSON
- NoSQL
- Open Source
- Replication
- REST
- Spectral
- Linting
- API Governance
---

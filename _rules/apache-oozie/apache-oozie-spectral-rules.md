---
categories:
- get
- info
- 'no'
- oozie
- openapi
- operation
- parameter
- paths
- request
- response
- schema
- servers
- tags
description: Spectral linting rules defining API design standards and conventions for Apache Oozie.
layout: rules
name: Apache Oozie API Rules
provider_name: Apache Oozie
provider_slug: apache-oozie
rule_count: 27
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
- description: Path segments should use kebab-case or path parameters.
  given: $.paths[*]~
  name: paths-kebab-case
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
- description: Operation summaries should start with "Apache Oozie".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-apache-oozie-prefix
  severity: info
- description: Global tags array should be defined.
  given: $
  name: tags-global-defined
  severity: warn
- description: Each global tag should have a description.
  given: $.tags[*]
  name: tags-description
  severity: warn
- description: Every parameter should have a description.
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
- description: Operations should document 500 Internal Server Error response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-500-defined
  severity: warn
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
  severity: info
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: PUT operations on /job paths should use an action query parameter.
  given: $.paths['/v1/job/{job-id}'].put.parameters[*]
  name: oozie-action-query-param
  severity: info
- description: Descriptions must not be empty strings.
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-oozie-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-oozie/refs/heads/main/rules/apache-oozie-spectral-rules.yml
severity_counts:
  error: 11
  hint: 0
  info: 3
  warn: 13
slug: apache-oozie-spectral-rules
tags:
- Workflow
- Hadoop
- Orchestration
- Scheduling
- Big Data
- Apache
- Java
- Open Source
- Spectral
- Linting
- API Governance
---

---
categories:
- get
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Kafka.
layout: rules
name: Apache Kafka API Rules
provider_name: Apache Kafka
provider_slug: apache-kafka
rule_count: 16
rules:
- description: Info title should start with Kafka or Apache Kafka
  given: $.info
  name: info-title-prefix
  severity: warn
- description: Info must have a version
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
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Responses must have descriptions
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-2xx-required
  severity: error
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Path segments should use kebab-case or snake_case
  given: $.paths
  name: paths-kebab-case
  severity: info
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: GET operations should document 404 responses
  given: $.paths[*].get.responses
  name: response-error-404
  severity: info
- description: POST operations should document 400 responses
  given: $.paths[*].post.responses
  name: response-error-400
  severity: info
rules_file: rules/apache-kafka-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-kafka/refs/heads/main/rules/apache-kafka-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 4
  warn: 3
slug: apache-kafka-spectral-rules
tags:
- Distributed Systems
- Event Streaming
- Messaging
- Open Source
- Pub-Sub
- Spectral
- Linting
- API Governance
---

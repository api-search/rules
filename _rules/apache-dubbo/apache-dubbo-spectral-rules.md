---
categories:
- info
- 'no'
- operation
- parameter
- paths
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache Dubbo.
layout: rules
name: Apache Dubbo API Rules
provider_name: Apache Dubbo
provider_slug: apache-dubbo
rule_count: 15
rules:
- description: Info title must be defined
  given: $.info
  name: info-title-required
  severity: error
- description: Info description must be present
  given: $.info
  name: info-description-required
  severity: warn
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache Dubbo
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-dubbo-prefix
  severity: warn
- description: All operations must have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-operationId-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-tags-required
  severity: warn
- description: Path segments should use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Operations must define at least one 2xx response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: response-success-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schema properties should have descriptions
  given: $.definitions[*].properties[*]
  name: schema-property-description
  severity: info
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-dubbo-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-dubbo/refs/heads/main/rules/apache-dubbo-spectral-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 1
  warn: 9
slug: apache-dubbo-spectral-rules
tags:
- Apache
- Go
- Java
- Microservices
- Open Source
- RPC
- Service Discovery
- Service Mesh
- Spectral
- Linting
- API Governance
---

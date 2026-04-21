---
categories:
- info
- operation
- parameter
- paths
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache EventMesh.
layout: rules
name: Apache EventMesh API Rules
provider_name: Apache EventMesh
provider_slug: apache-event-mesh
rule_count: 10
rules:
- description: Info title must be defined
  given: $.info
  name: info-title-required
  severity: error
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with Apache EventMesh
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-eventmesh-prefix
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
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All responses must have descriptions
  given: $.paths[*][get,post,put,delete,patch].responses[*]
  name: response-description-required
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-property-description
  severity: info
rules_file: rules/apache-event-mesh-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-event-mesh/refs/heads/main/rules/apache-event-mesh-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: apache-event-mesh-spectral-rules
tags:
- Apache
- CloudEvents
- Event-Driven
- Messaging
- Open Source
- Pub-Sub
- Serverless
- Spectral
- Linting
- API Governance
---

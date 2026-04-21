---
categories:
- info
- 'no'
- openapi
- operation
- parameter
- paths
- response
- schema
- servers
- sparql
description: Spectral linting rules defining API design standards and conventions for Apache Jena.
layout: rules
name: Apache Jena API Rules
provider_name: Apache Jena
provider_slug: apache-jena
rule_count: 15
rules:
- description: Info title should start with Apache Jena
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
- description: SPARQL endpoints should document 400 for invalid queries
  given: $.paths[*].post.responses
  name: response-400-sparql
  severity: warn
- description: SPARQL query endpoints should support sparql-results+json
  given: $.paths[*].get.responses.200.content
  name: sparql-media-types
  severity: info
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][get,post].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: info
rules_file: rules/apache-jena-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-jena/refs/heads/main/rules/apache-jena-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 3
  warn: 4
slug: apache-jena-spectral-rules
tags:
- Java
- Linked Data
- OWL
- Ontology
- Open Source
- RDF
- Semantic Web
- SPARQL
- Spectral
- Linting
- API Governance
---

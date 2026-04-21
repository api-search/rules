---
categories:
- info
- operation
- paths
- request
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Apache OpenNLP.
layout: rules
name: Apache OpenNLP API Rules
provider_name: Apache OpenNLP
provider_slug: apache-opennlp
rule_count: 10
rules:
- description: API must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: API must have a description
  given: $.info
  name: info-description-required
  severity: warn
- description: Operations must have summaries
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: Operations must have operationIds
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: Operations must have tags
  given: $.paths[*][*]
  name: operation-tags-required
  severity: warn
- description: Summaries should start with Apache OpenNLP
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Request bodies should use application/json
  given: $.paths[*][post,put,patch].requestBody.content
  name: request-body-content-type
  severity: warn
- description: Operations must have a 200 success response
  given: $.paths[*][*].responses
  name: response-success-required
  severity: error
- description: Schema properties should have types defined
  given: $.components.schemas[*].properties[*]
  name: schema-type-defined
  severity: warn
rules_file: rules/apache-opennlp-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-opennlp/refs/heads/main/rules/apache-opennlp-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 1
  warn: 5
slug: apache-opennlp-spectral-rules
tags:
- Machine Learning
- Natural Language Processing
- NLP
- Text Processing
- Apache
- Open Source
- Java
- Spectral
- Linting
- API Governance
---

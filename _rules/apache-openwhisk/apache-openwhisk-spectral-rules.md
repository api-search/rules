---
categories:
- info
- operation
- paths
- response
- schema
- security
description: Spectral linting rules defining API design standards and conventions for Apache OpenWhisk.
layout: rules
name: Apache OpenWhisk API Rules
provider_name: Apache OpenWhisk
provider_slug: apache-openwhisk
rule_count: 10
rules:
- description: API must have a title
  given: $.info
  name: info-title-required
  severity: error
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
- description: Summaries should start with Apache OpenWhisk
  given: $.paths[*][get,post,put,delete,patch].summary
  name: operation-summary-apache-prefix
  severity: info
- description: Paths should be versioned under /api/v1
  given: $.servers[*].url
  name: paths-api-versioned
  severity: info
- description: API should use HTTP Basic authentication
  given: $.components.securitySchemes
  name: security-basic-auth
  severity: warn
- description: Operations must have a 200 success response
  given: $.paths[*][get,post,put].responses
  name: response-success-required
  severity: error
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: schema-properties-described
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: operation-parameters-described
  severity: warn
rules_file: rules/apache-openwhisk-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-openwhisk/refs/heads/main/rules/apache-openwhisk-spectral-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 3
  warn: 3
slug: apache-openwhisk-spectral-rules
tags:
- Cloud Native
- Event-Driven
- FaaS
- Serverless
- Apache
- Open Source
- Functions
- Spectral
- Linting
- API Governance
---

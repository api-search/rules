---
categories:
- get
- info
- openapi
- operation
- parameter
- paths
- response
- schema
description: Spectral linting rules defining API design standards and conventions for Ballerina.
layout: rules
name: Ballerina API Rules
provider_name: Ballerina
provider_slug: ballerina
rule_count: 11
rules:
- description: Info must have a title
  given: $.info
  name: info-title-required
  severity: error
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Must use OpenAPI 3.x
  given: $
  name: openapi-version-3
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
  severity: warn
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: All parameters must have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: All schemas should have a type
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Path segments should use kebab-case or snake_case
  given: $.paths
  name: paths-kebab-case
  severity: info
rules_file: rules/ballerina-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ballerina/refs/heads/main/rules/ballerina-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 1
  warn: 3
slug: ballerina-spectral-rules
tags:
- Integrations
- Orchestrations
- Open Source
- Programming Language
- Spectral
- Linting
- API Governance
---

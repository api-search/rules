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
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache James.
layout: rules
name: Apache James API Rules
provider_name: Apache James
provider_slug: apache-james
rule_count: 20
rules:
- description: Info title should start with Apache James
  given: $.info
  name: info-title-prefix
  severity: warn
- description: Info must have a description
  given: $.info
  name: info-description-required
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
- description: Summaries should start with Apache James WebAdmin
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-prefix
  severity: warn
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
- description: GET operations must not have request bodies
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: Paths must not have trailing slashes
  given: $.paths
  name: paths-no-trailing-slash
  severity: warn
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-2xx-required
  severity: error
- description: Security schemes should be defined
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: warn
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: GET operations should document 404 responses
  given: $.paths[*].get.responses
  name: response-error-404
  severity: info
- description: POST operations should document 400 responses
  given: $.paths[*].post.responses
  name: response-error-400
  severity: info
- description: Operations should have descriptions
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-recommended
  severity: info
rules_file: rules/apache-james-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-james/refs/heads/main/rules/apache-james-spectral-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 4
  warn: 7
slug: apache-james-spectral-rules
tags:
- Email
- IMAP
- Java
- JMAP
- Mail Server
- Open Source
- SMTP
- Spectral
- Linting
- API Governance
---

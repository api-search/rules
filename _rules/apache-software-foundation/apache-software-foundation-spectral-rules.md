---
categories:
- info
- 'no'
- openapi
- operation
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Apache Software Foundation.
layout: rules
name: Apache Software Foundation API Rules
provider_name: Apache Software Foundation
provider_slug: apache-software-foundation
rule_count: 18
rules:
- description: Info title is required
  given: $.info
  name: info-title-required
  severity: error
- description: Info description is required and should be at least 30 characters
  given: $.info
  name: info-description-required
  severity: warn
- description: API version is required
  given: $.info
  name: info-version-required
  severity: error
- description: License information is required for ASF projects
  given: $.info
  name: info-license-required
  severity: warn
- description: Use OpenAPI 3.x
  given: $
  name: openapi-version-3
  severity: error
- description: Servers array is required
  given: $
  name: servers-required
  severity: error
- description: All server URLs should use HTTPS
  given: $.servers[*].url
  name: servers-https
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-operationid-required
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: warn
- description: Operation summaries should start with "Apache Software Foundation"
  given: $.paths[*][get,post,put,patch,delete,head,options].summary
  name: operation-summary-prefix
  severity: info
- description: Every operation should have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete,head,options].responses
  name: response-success-required
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete,head,options].responses[*]
  name: response-description-required
  severity: error
- description: All schema properties should have a type
  given: $.components.schemas[*].properties[*]
  name: schema-type-required
  severity: warn
- description: Top-level schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-required
  severity: info
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: info
- description: Descriptions should not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/apache-software-foundation-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-software-foundation/refs/heads/main/rules/apache-software-foundation-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 3
  warn: 7
slug: apache-software-foundation-spectral-rules
tags:
- ASF
- Open Source
- Governance
- Projects
- Apache
- Spectral
- Linting
- API Governance
---

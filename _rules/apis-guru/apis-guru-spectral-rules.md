---
categories:
- delete
- examples
- external
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
- tag
- tags
description: Spectral linting rules defining API design standards and conventions for APIs.guru.
layout: rules
name: APIs.guru API Rules
provider_name: APIs.guru
provider_slug: apis-guru
rule_count: 30
rules:
- description: Info title should start with "APIs.guru"
  given: $.info.title
  name: info-title-format
  severity: warn
- description: Info must have a description
  given: $.info
  name: info-description-required
  severity: error
- description: Info must have a version
  given: $.info
  name: info-version-required
  severity: error
- description: Info should have contact information
  given: $.info
  name: info-contact-required
  severity: warn
- description: Info should have license information
  given: $.info
  name: info-license-required
  severity: warn
- description: Specs should use OpenAPI 3.0.x
  given: $.openapi
  name: openapi-version-3
  severity: warn
- description: Servers array must be defined
  given: $
  name: servers-defined
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*].url
  name: servers-https-only
  severity: error
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: paths-kebab-case
  severity: warn
- description: Paths must not have a trailing slash
  given: $.paths[*]~
  name: paths-no-trailing-slash
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-summary-required
  severity: error
- description: Operation summaries should start with "APIs.guru"
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-prefix
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-description-required
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-id-required
  severity: error
- description: OperationId should use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete,head,options]
  name: operation-tags-required
  severity: error
- description: Global tags array should be defined
  given: $
  name: tags-defined
  severity: warn
- description: All tags should have descriptions
  given: $.tags[*]
  name: tag-description-required
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: error
- description: All parameters must have a schema type
  given: $.paths[*][*].parameters[*].schema
  name: parameter-schema-type-required
  severity: error
- description: Operations must have at least one 2xx response
  given: $.paths[*][get,post,put,patch,delete]
  name: response-success-required
  severity: error
- description: All responses must have descriptions
  given: $.paths[*][*].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas should have descriptions
  given: $.components.schemas[*]
  name: schema-description-recommended
  severity: info
- description: Schema objects should have a type defined
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
- description: Security defined at operation or global level
  given: $
  name: no-global-security-required
  severity: info
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should not have a request body
  given: $.paths[*].delete
  name: delete-no-request-body
  severity: warn
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: error
- description: External documentation is encouraged
  given: $
  name: external-docs-encouraged
  severity: info
- description: Schema properties should have examples
  given: $.components.schemas[*].properties[*]
  name: examples-encouraged
  severity: info
rules_file: rules/apis-guru-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apis-guru/refs/heads/main/rules/apis-guru-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 4
  warn: 13
slug: apis-guru-spectral-rules
tags:
- API Catalog
- API Directory
- API Discovery
- Community
- GraphQL
- Open Source
- OpenAPI
- Spectral
- Linting
- API Governance
---

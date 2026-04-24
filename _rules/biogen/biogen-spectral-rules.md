---
categories:
- biogen
description: Spectral linting rules defining API design standards and conventions for Biogen.
layout: rules
name: Biogen API Rules
provider_name: Biogen
provider_slug: biogen
rule_count: 23
rules:
- description: API title must start with "Biogen"
  given: $.info.title
  name: biogen-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: biogen-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: biogen-info-contact-present
  severity: warn
- description: Operation summaries must start with "Biogen"
  given: $.paths[*][*].summary
  name: biogen-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: biogen-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: biogen-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: biogen-operation-description-present
  severity: warn
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: biogen-response-success-present
  severity: error
- description: Operations should define a 401 response
  given: $.paths[*][*].responses
  name: biogen-response-401-present
  severity: warn
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: biogen-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: biogen-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: biogen-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: biogen-security-scheme-present
  severity: error
- description: Biogen API uses X-API-Key header authentication
  given: $.components.securitySchemes[*]
  name: biogen-api-key-auth
  severity: warn
- description: Operations must declare security
  given: $.paths[*][get,post,put,patch,delete]
  name: biogen-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: biogen-tags-defined
  severity: warn
- description: API must define servers
  given: $
  name: biogen-servers-present
  severity: error
- description: Server URL must use HTTPS
  given: $.servers[*].url
  name: biogen-server-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: biogen-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: biogen-microcks-operation-present
  severity: warn
- description: All components should be referenced
  given: $.components.schemas
  name: biogen-unused-components
  severity: warn
- description: API info must include license
  given: $.info
  name: biogen-license-present
  severity: warn
- description: Path segments should be lowercase
  given: $.paths
  name: biogen-path-kebab-case
  severity: warn
rules_file: rules/biogen-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/biogen/refs/heads/main/rules/biogen-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 16
slug: biogen-spectral-rules
tags:
- Biotechnology
- Healthcare
- Life Sciences
- Pharmaceuticals
- Neurology
- Spectral
- Linting
- API Governance
---

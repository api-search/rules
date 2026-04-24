---
categories:
- bifrost
description: Spectral linting rules defining API design standards and conventions for Bifrost.
layout: rules
name: Bifrost API Rules
provider_name: Bifrost
provider_slug: bifrost
rule_count: 24
rules:
- description: API title must start with "Bifrost"
  given: $.info.title
  name: bifrost-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: bifrost-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: bifrost-info-contact-present
  severity: warn
- description: Operation summaries must start with "Bifrost"
  given: $.paths[*][*].summary
  name: bifrost-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: bifrost-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: bifrost-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: bifrost-operation-description-present
  severity: warn
- description: Paths must use kebab-case segments
  given: $.paths
  name: bifrost-path-kebab-case
  severity: warn
- description: POST operations must have a request body
  given: $.paths[*].post
  name: bifrost-request-body-required
  severity: error
- description: Every operation must define a 200 or 201 response
  given: $.paths[*][*].responses
  name: bifrost-response-200-present
  severity: error
- description: Error responses must reference ErrorResponse schema
  given: $.paths[*][*].responses[?(@property >= '400')].content.application/json.schema
  name: bifrost-response-error-schema
  severity: warn
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: bifrost-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: bifrost-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: bifrost-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: bifrost-security-scheme-present
  severity: error
- description: Operations should reference a security scheme
  given: $.paths[*][post,put,patch,delete]
  name: bifrost-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: bifrost-tags-defined
  severity: warn
- description: Top-level tags must have a description
  given: $.tags[*]
  name: bifrost-tag-description-present
  severity: warn
- description: API must define servers
  given: $
  name: bifrost-servers-present
  severity: error
- description: Chat completion model must use provider/model format
  given: $.components.schemas.ChatCompletionRequest.properties.model
  name: bifrost-chat-model-format
  severity: warn
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: bifrost-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: bifrost-microcks-operation-present
  severity: warn
- description: API info must include license
  given: $.info
  name: bifrost-license-present
  severity: warn
- description: License must be Apache 2.0
  given: $.info.license.name
  name: bifrost-license-apache
  severity: warn
rules_file: rules/bifrost-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bifrost/refs/heads/main/rules/bifrost-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 17
slug: bifrost-spectral-rules
tags:
- AI Gateway
- LLM
- Load Balancing
- Open Source
- OpenAI Compatible
- MCP
- Spectral
- Linting
- API Governance
---

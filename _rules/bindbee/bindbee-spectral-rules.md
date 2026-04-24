---
categories:
- bindbee
description: Spectral linting rules defining API design standards and conventions for Bindbee.
layout: rules
name: Bindbee API Rules
provider_name: Bindbee
provider_slug: bindbee
rule_count: 24
rules:
- description: API title must start with "Bindbee"
  given: $.info.title
  name: bindbee-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: bindbee-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: bindbee-info-contact-present
  severity: warn
- description: Operation summaries must start with "Bindbee"
  given: $.paths[*][*].summary
  name: bindbee-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: bindbee-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: bindbee-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: bindbee-operation-description-present
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: bindbee-path-kebab-case
  severity: warn
- description: Operations must require x-connector-token header
  given: $.paths[*][*].parameters[?(@.name=='x-connector-token')]
  name: bindbee-connector-token-header
  severity: error
- description: Every operation must define a 200 response
  given: $.paths[*][*].responses
  name: bindbee-response-200-present
  severity: error
- description: Operations should define a 401 unauthorized response
  given: $.paths[*][*].responses
  name: bindbee-response-401-present
  severity: warn
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: bindbee-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: bindbee-schema-description-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: bindbee-schema-properties-described
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: bindbee-security-scheme-present
  severity: error
- description: Operations must declare security
  given: $.paths[*][get,post,put,patch,delete]
  name: bindbee-operation-security-present
  severity: warn
- description: All tags must be defined at top level
  given: $.tags
  name: bindbee-tags-defined
  severity: warn
- description: API must define servers
  given: $
  name: bindbee-servers-present
  severity: error
- description: Server URL must use HTTPS
  given: $.servers[*].url
  name: bindbee-server-https
  severity: error
- description: List endpoints should support cursor-based pagination
  given: $.paths[?(@property.startsWith('/hris/') || @property.startsWith('/ats/'))][get].parameters[?(@.name=='cursor')]
  name: bindbee-pagination-cursor
  severity: warn
- description: List responses should return data in a data array
  given: $.components.schemas[?(@property.endsWith('Response'))].properties
  name: bindbee-response-data-array
  severity: warn
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: bindbee-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: bindbee-microcks-operation-present
  severity: warn
- description: API info must include license
  given: $.info
  name: bindbee-license-present
  severity: warn
rules_file: rules/bindbee-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/bindbee/refs/heads/main/rules/bindbee-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 16
slug: bindbee-spectral-rules
tags:
- ATS
- HR Integration
- HRIS
- Workforce
- Spectral
- Linting
- API Governance
---

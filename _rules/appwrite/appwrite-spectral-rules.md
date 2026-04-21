---
categories:
- http
- info
- 'no'
- operation
- parameter
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Appwrite.
layout: rules
name: Appwrite API Rules
provider_name: Appwrite
provider_slug: appwrite
rule_count: 17
rules:
- description: API title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: API version must be specified
  given: $.info
  name: info-version-required
  severity: error
- description: API description should be present
  given: $.info
  name: info-description-required
  severity: warn
- description: Open source APIs should specify a license
  given: $.info
  name: info-license-required
  severity: warn
- description: At least one server must be defined
  given: $
  name: servers-required
  severity: error
- description: Server URLs must use HTTPS
  given: $.servers[*]
  name: servers-https
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: paths-kebab-case
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-id-required
  severity: error
- description: Every operation must have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every parameter must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must have a 2xx response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: operation-success-response-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Component schemas should have a title
  given: $.components.schemas[*]
  name: schema-title-required
  severity: warn
- description: GET operations must not have a request body
  given: $.paths[*].get
  name: http-get-no-request-body
  severity: error
- description: Descriptions must not be empty strings
  given: $..description
  name: no-empty-descriptions
  severity: warn
rules_file: rules/appwrite-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/appwrite/refs/heads/main/rules/appwrite-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 9
slug: appwrite-spectral-rules
tags:
- Applications
- Backends
- Mobile
- Open Source
- Spectral
- Linting
- API Governance
---

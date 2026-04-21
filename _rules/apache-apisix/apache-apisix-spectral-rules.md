---
categories:
- apikey
- delete
- get
- info
- operation
- parameter
- paths
- response
- schema
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Apache APISIX.
layout: rules
name: Apache APISIX API Rules
provider_name: Apache APISIX
provider_slug: apache-apisix
rule_count: 19
rules:
- description: API title must start with "Apache APISIX"
  given: $.info.title
  name: info-title-prefix
  severity: warn
- description: API must have a description.
  given: $.info
  name: info-description-required
  severity: error
- description: API must declare a version.
  given: $.info
  name: info-version-required
  severity: error
- description: At least one server must be defined.
  given: $
  name: servers-defined
  severity: error
- description: Every operation must have a summary.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Operation summaries must start with "Apache APISIX".
  given: $.paths[*][get,post,put,patch,delete].summary
  name: operation-summary-starts-with-apache-apisix
  severity: warn
- description: Every operation must have an operationId.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationId-required
  severity: error
- description: operationId must be camelCase.
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: operation-operationId-camelCase
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: warn
- description: Every operation should have a description.
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-description-required
  severity: warn
- description: Path segments must use kebab-case or standard patterns.
  given: $.paths
  name: paths-kebab-case
  severity: info
- description: Every parameter must have a description.
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: parameter-description-required
  severity: warn
- description: Every operation must define at least one 2xx response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: response-success-required
  severity: error
- description: Every response must have a description.
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Security schemes must be defined in components.
  given: $.components
  name: security-schemes-defined
  severity: warn
- description: API key authentication should use a header, not a query parameter.
  given: $.components.securitySchemes[?(@.type=='apiKey')]
  name: apikey-in-header
  severity: warn
- description: GET operations must not have a request body.
  given: $.paths[*].get
  name: get-no-request-body
  severity: error
- description: DELETE operations should return 200 or 204.
  given: $.paths[*].delete.responses
  name: delete-returns-200-or-204
  severity: info
- description: Schema components must have a type defined.
  given: $.components.schemas[*]
  name: schema-type-defined
  severity: warn
rules_file: rules/apache-apisix-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/apache-apisix/refs/heads/main/rules/apache-apisix-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 2
  warn: 9
slug: apache-apisix-spectral-rules
tags:
- Apache
- API Gateway
- Cloud Native
- Kubernetes
- Lua
- NGINX
- Open Source
- Traffic Management
- Spectral
- Linting
- API Governance
---

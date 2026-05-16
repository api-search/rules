---
api_specs:
- filename: traefik-proxy-openapi.yml
  format: yaml
  label: Traefik Proxy
  slug: traefik-proxy
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traefik/refs/heads/main/openapi/traefik-proxy-openapi.yml
- filename: traefik-proxy-openapi.yml
  format: yaml
  label: Traefik Proxy REST API
  slug: traefik-proxy-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traefik/refs/heads/main/openapi/traefik-proxy-openapi.yml
categories:
- get
- info
- operation
- parameter
- path
- paths
- response
- schema
- servers
description: Spectral linting rules defining API design standards and conventions for Traefik Labs.
layout: rules
name: Traefik Labs API Rules
provider_name: Traefik Labs
provider_slug: traefik
rule_count: 16
rules:
- description: ''
  given: $.info
  name: info-title-required
  severity: error
- description: ''
  given: $.info.title
  name: info-title-format
  severity: warn
- description: ''
  given: $.info
  name: info-description-required
  severity: error
- description: ''
  given: $.info
  name: info-version-required
  severity: error
- description: ''
  given: $
  name: servers-defined
  severity: error
- description: ''
  given: $.paths
  name: paths-no-trailing-slash
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-operationId-required
  severity: error
- description: ''
  given: $.paths[*][*]
  name: operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*].summary
  name: operation-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: operation-description-required
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*][get]
  name: response-200-defined
  severity: error
- description: ''
  given: $.paths
  name: path-name-pattern
  severity: warn
- description: ''
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: schema-description-required
  severity: warn
- description: ''
  given: $.paths[*].get.responses[200].content
  name: get-responses-json
  severity: warn
rules_file: rules/traefik-proxy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/traefik/refs/heads/main/rules/traefik-proxy-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 0
  warn: 8
slug: traefik-proxy-rules
source_filename: traefik-proxy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  info-title-required:\n    severity: error\n    given: $.info\n    then: {field: title, function: truthy}\n  info-title-format:\n    severity: warn\n    given: $.info.title\n    then: {function: pattern, functionOptions: {match: \"^Traefik \"}}\n  info-description-required:\n    severity: error\n    given: $.info\n    then: {field: description, function: truthy}\n  info-version-required:\n    severity: error\n    given: $.info\n    then: {field: version, function: truthy}\n  servers-defined:\n    severity: error\n    given: $\n    then: {field: servers, function: truthy}\n  paths-no-trailing-slash:\n    severity: error\n    given: $.paths\n    then: {field: \"@key\", function: pattern, functionOptions: {notMatch: \"\\\\/$\"}}\n  operation-operationId-required:\n    severity: error\n    given: $.paths[*][*]\n    then: {field: operationId, function: truthy}\n  operation-summary-required:\n    severity: error\n    given: $.paths[*][*]\n    then: {field: summary, function:\
  \ truthy}\n  operation-summary-title-case:\n    severity: warn\n    given: $.paths[*][*].summary\n    then: {function: pattern, functionOptions: {match: \"^[A-Z][a-z]\"}}\n  operation-description-required:\n    severity: warn\n    given: $.paths[*][*]\n    then: {field: description, function: truthy}\n  operation-tags-required:\n    severity: warn\n    given: $.paths[*][*]\n    then: {field: tags, function: truthy}\n  response-200-defined:\n    severity: error\n    given: $.paths[*][get]\n    then: {field: responses, function: truthy}\n  path-name-pattern:\n    severity: warn\n    given: $.paths\n    then: {field: \"@key\", function: pattern, functionOptions: {match: \"^\\\\/[a-z\\\\/{]\"}}\n  parameter-description-required:\n    severity: warn\n    given: $.paths[*][*].parameters[*]\n    then: {field: description, function: truthy}\n  schema-description-required:\n    severity: warn\n    given: $.components.schemas[*]\n    then: {field: description, function: truthy}\n  get-responses-json:\n\
  \    severity: warn\n    given: $.paths[*].get.responses[200].content\n    then: {field: \"application/json\", function: truthy}\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/traefik/refs/heads/main/rules/traefik-proxy-rules.yml
tags:
- AI Gateway
- API Gateway
- API Management
- Developer Portal
- GitOps
- Kubernetes
- Load Balancer
- MCP Gateway
- Open Source
- Reverse Proxy
- WAF
- Spectral
- Linting
- API Governance
---

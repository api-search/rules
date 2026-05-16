---
api_specs:
- filename: kong-gateway-admin-api.yml
  format: yaml
  label: Kong Gateway Admin API
  slug: kong-admin-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kong/refs/heads/main/openapi/kong-gateway-admin-api.yml
- filename: kong-konnect-platform-api.yml
  format: yaml
  label: Kong Konnect Platform API
  slug: kong-konnect-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/kong/refs/heads/main/openapi/kong-konnect-platform-api.yml
- filename: openapi.yaml
  format: yaml
  label: Kong Event Gateway
  slug: kong-event-gateway
  spec_type: OpenAPI
  url: https://developer.konghq.com/api/konnect/event-gateway/v1/
categories:
- info
- 'no'
- operation
- response
description: Spectral linting rules defining API design standards and conventions for Kong.
layout: rules
name: Kong API Rules
provider_name: Kong
provider_slug: kong
rule_count: 7
rules:
- description: Info title must be present
  given: $.info
  name: info-title-required
  severity: error
- description: Info description must be present
  given: $.info
  name: info-description-required
  severity: error
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-operationid-required
  severity: error
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-summary-required
  severity: error
- description: Every operation must have tags
  given: $.paths[*][get,post,put,patch,delete]
  name: operation-tags-required
  severity: error
- description: Every response must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: response-description-required
  severity: error
- description: Descriptions must not be empty
  given: $..description
  name: no-empty-descriptions
  severity: error
rules_file: rules/kong-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/kong/refs/heads/main/rules/kong-spectral-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 0
slug: kong-spectral-rules
source_filename: kong-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  info-title-required:\n    description: Info title must be present\n    severity: error\n    given: $.info\n    then: {field: title, function: truthy}\n  info-description-required:\n    description: Info description must be present\n    severity: error\n    given: $.info\n    then: {field: description, function: truthy}\n  operation-operationid-required:\n    description: Every operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then: {field: operationId, function: truthy}\n  operation-summary-required:\n    description: Every operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then: {field: summary, function: truthy}\n  operation-tags-required:\n    description: Every operation must have tags\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then: {field: tags, function: truthy}\n  response-description-required:\n    description:\
  \ Every response must have a description\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].responses[*]\n    then: {field: description, function: truthy}\n  no-empty-descriptions:\n    description: Descriptions must not be empty\n    severity: error\n    given: $..description\n    then: {function: truthy}\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/kong/refs/heads/main/rules/kong-spectral-rules.yml
tags:
- API Gateway
- AI Gateway
- AI Connectivity
- Agent Gateway
- Event Gateway
- MCP Registry
- Service Mesh
- LLM
- Kafka
- Konnect
- Open Source
- Spectral
- Linting
- API Governance
---

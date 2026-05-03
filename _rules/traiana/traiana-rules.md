---
api_specs:
- filename: traiana-harmony-trade-processing-openapi.yml
  format: yaml
  label: Traiana Harmony Trade Processing API
  slug: harmony-trade-processing
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traiana/refs/heads/main/openapi/traiana-harmony-trade-processing-openapi.yml
- filename: traiana-harmony-creditlink-openapi.yml
  format: yaml
  label: Traiana Harmony CreditLink API
  slug: harmony-creditlink
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traiana/refs/heads/main/openapi/traiana-harmony-creditlink-openapi.yml
- filename: traiana-harmony-netlink-openapi.yml
  format: yaml
  label: Traiana Harmony NetLink API
  slug: harmony-netlink
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/traiana/refs/heads/main/openapi/traiana-harmony-netlink-openapi.yml
categories:
- info
- operation
- parameter
- paths
- response
- security
- servers
description: Spectral linting rules defining API design standards and conventions for Traiana.
layout: rules
name: Traiana API Rules
provider_name: Traiana
provider_slug: traiana
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
  given: $.servers[*].url
  name: servers-https-only
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
  name: paths-use-kebab-case
  severity: warn
- description: ''
  given: $.paths[*][*].parameters[*]
  name: parameter-description-required
  severity: warn
- description: ''
  given: $.components.securitySchemes
  name: security-schemes-defined
  severity: warn
rules_file: rules/traiana-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/traiana/refs/heads/main/rules/traiana-rules.yml
severity_counts:
  error: 9
  hint: 0
  info: 0
  warn: 7
slug: traiana-rules
source_filename: traiana-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  info-title-required:\n    severity: error\n    given: $.info\n    then: {field: title, function: truthy}\n  info-title-format:\n    severity: warn\n    given: $.info.title\n    then: {function: pattern, functionOptions: {match: \"^Traiana \"}}\n  info-description-required:\n    severity: error\n    given: $.info\n    then: {field: description, function: truthy}\n  info-version-required:\n    severity: error\n    given: $.info\n    then: {field: version, function: truthy}\n  servers-defined:\n    severity: error\n    given: $\n    then: {field: servers, function: truthy}\n  servers-https-only:\n    severity: error\n    given: $.servers[*].url\n    then: {function: pattern, functionOptions: {match: \"^https://\"}}\n  paths-no-trailing-slash:\n    severity: error\n    given: $.paths\n    then: {field: \"@key\", function: pattern, functionOptions: {notMatch: \"\\\\/$\"}}\n  operation-operationId-required:\n    severity: error\n    given: $.paths[*][*]\n    then: {field:\
  \ operationId, function: truthy}\n  operation-summary-required:\n    severity: error\n    given: $.paths[*][*]\n    then: {field: summary, function: truthy}\n  operation-summary-title-case:\n    severity: warn\n    given: $.paths[*][*].summary\n    then: {function: pattern, functionOptions: {match: \"^[A-Z][a-z]\"}}\n  operation-description-required:\n    severity: warn\n    given: $.paths[*][*]\n    then: {field: description, function: truthy}\n  operation-tags-required:\n    severity: warn\n    given: $.paths[*][*]\n    then: {field: tags, function: truthy}\n  response-200-defined:\n    severity: error\n    given: $.paths[*][get]\n    then: {field: responses, function: truthy}\n  paths-use-kebab-case:\n    severity: warn\n    given: $.paths\n    then: {field: \"@key\", function: pattern, functionOptions: {match: \"^\\\\/[a-z0-9\\\\-\\\\/{]\"}}\n  parameter-description-required:\n    severity: warn\n    given: $.paths[*][*].parameters[*]\n    then: {field: description, function: truthy}\n\
  \  security-schemes-defined:\n    severity: warn\n    given: $.components.securitySchemes\n    then: {function: truthy}\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/traiana/refs/heads/main/rules/traiana-rules.yml
tags:
- Fintech
- Foreign Exchange
- Post-Trade Processing
- Risk Management
- Spectral
- Linting
- API Governance
---

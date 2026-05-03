---
api_specs:
- filename: smartproxy-openapi.yml
  format: yaml
  label: Smartproxy Account Management API
  slug: proxy-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smartproxy/refs/heads/main/openapi/smartproxy-openapi.yml
categories:
- smartproxy
description: Spectral linting rules defining API design standards and conventions for Smartproxy.
layout: rules
name: Smartproxy API Rules
provider_name: Smartproxy
provider_slug: smartproxy
rule_count: 6
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: smartproxy-operation-id-camel-case
  severity: warn
- description: User-scoped endpoints must use {userId} path parameter
  given: $.paths[*]~
  name: smartproxy-user-id-path-param
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smartproxy-operation-summary-title-case
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: smartproxy-response-200-get
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: smartproxy-tags-required
  severity: error
- description: DELETE operations should return 204 No Content
  given: $.paths[*].delete
  name: smartproxy-delete-returns-204
  severity: warn
rules_file: rules/smartproxy-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smartproxy/refs/heads/main/rules/smartproxy-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 4
slug: smartproxy-rules
source_filename: smartproxy-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  smartproxy-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' should use camelCase (e.g., getSubUsers)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  smartproxy-user-id-path-param:\n    description: User-scoped endpoints must use {userId} path parameter\n    message: \"User-scoped endpoints should use {userId}\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/users(\\\\/\\\\{userId\\\\}|$)|^\\\\/auth|^\\\\/endpoints\"\n\n  smartproxy-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n \
  \     functionOptions:\n        match: \"^[A-Z][A-Za-z]*(\\\\s[A-Z][A-Za-z]*)*$\"\n\n  smartproxy-response-200-get:\n    description: All GET operations must define a 200 response\n    message: \"GET operations must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  smartproxy-tags-required:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smartproxy-delete-returns-204:\n    description: DELETE operations should return 204 No Content\n    message: \"DELETE operations should define a 204 response\"\n    severity: warn\n    given: \"$.paths[*].delete\"\n    then:\n      field: responses.204\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smartproxy/refs/heads/main/rules/smartproxy-rules.yml
tags:
- Proxies
- Web Scraping
- Data Collection
- Residential Proxies
- Datacenter Proxies
- Mobile Proxies
- Network Infrastructure
- Spectral
- Linting
- API Governance
---

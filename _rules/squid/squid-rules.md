---
api_specs:
- filename: squid-cache-manager-openapi.yml
  format: yaml
  label: Squid Cache Manager API
  slug: squid-cache-manager
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/squid/refs/heads/main/openapi/squid-cache-manager-openapi.yml
categories:
- squid
description: Spectral linting rules defining API design standards and conventions for Squid.
layout: rules
name: Squid API Rules
provider_name: Squid
provider_slug: squid
rule_count: 6
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: squid-operation-summary-title-case
  severity: warn
- description: operationId must use camelCase
  given: $.paths[*][*].operationId
  name: squid-operationid-kebab-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: squid-tags-required
  severity: error
- description: Descriptions must not be empty
  given: $.paths[*][*].description
  name: squid-no-empty-descriptions
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: squid-response-200-required
  severity: error
- description: Path segments must use lowercase characters
  given: $.paths
  name: squid-paths-lowercase
  severity: warn
rules_file: rules/squid-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/squid/refs/heads/main/rules/squid-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 4
slug: squid-rules
source_filename: squid-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  squid-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s?)+$\"\n\n  squid-operationid-kebab-case:\n    description: operationId must use camelCase\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  squid-tags-required:\n    description: Every operation must have at least one tag\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  squid-no-empty-descriptions:\n    description: Descriptions must not be empty\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  squid-response-200-required:\n    description: All GET operations must\
  \ define a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  squid-paths-lowercase:\n    description: Path segments must use lowercase characters\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/[a-z0-9_{}\\\\-]*)+$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/squid/refs/heads/main/rules/squid-rules.yml
tags:
- Caching Proxy
- Proxy
- HTTP Proxy
- Web Cache
- Access Control
- Content Filtering
- Spectral
- Linting
- API Governance
---

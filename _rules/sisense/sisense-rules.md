---
api_specs:
- filename: sisense-rest-api-openapi.yml
  format: yaml
  label: Sisense REST API v1
  slug: rest-api-v1
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sisense/refs/heads/main/openapi/sisense-rest-api-openapi.yml
categories:
- sisense
description: Spectral linting rules defining API design standards and conventions for Sisense.
layout: rules
name: Sisense API Rules
provider_name: Sisense
provider_slug: sisense
rule_count: 7
rules:
- description: All Sisense API operations (except login) must use Bearer token authentication
  given: $.paths[?(!@property.match(/login/))].*.security
  name: sisense-bearer-auth
  severity: warn
- description: All operation summaries must use Title Case
  given: $.paths.*.*.summary
  name: sisense-title-case-summaries
  severity: warn
- description: All operationId values must use camelCase
  given: $.paths.*.*.operationId
  name: sisense-camel-case-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: sisense-tags-required
  severity: warn
- description: API must define servers with host variable
  given: $
  name: sisense-servers-defined
  severity: error
- description: Collection GET operations should support limit and skip pagination
  given: $.paths[?(!@property.match(/{.*}/))].get.parameters[*].name
  name: sisense-pagination-params
  severity: info
- description: API info must include contact information
  given: $.info
  name: sisense-contact-info
  severity: warn
rules_file: rules/sisense-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sisense/refs/heads/main/rules/sisense-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 4
slug: sisense-rules
source_filename: sisense-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  sisense-bearer-auth:\n    description: All Sisense API operations (except login) must use Bearer token authentication\n    message: \"Operation is missing Bearer token security requirement\"\n    severity: warn\n    given: \"$.paths[?(!@property.match(/login/))].*.security\"\n    then:\n      function: truthy\n\n  sisense-title-case-summaries:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths.*.*.summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  sisense-camel-case-operation-ids:\n    description: All operationId values must use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: error\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  sisense-tags-required:\n    description:\
  \ All operations must have at least one tag\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  sisense-servers-defined:\n    description: API must define servers with host variable\n    message: \"API is missing server definitions\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  sisense-pagination-params:\n    description: Collection GET operations should support limit and skip pagination\n    message: \"GET collection endpoint should support limit and skip parameters\"\n    severity: info\n    given: \"$.paths[?(!@property.match(/{.*}/))].get.parameters[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(limit|skip|fields|sort|expand)$\"\n\n  sisense-contact-info:\n    description: API info must include contact information\n    message: \"API info is missing contact details\"\n    severity: warn\n\
  \    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sisense/refs/heads/main/rules/sisense-rules.yml
tags:
- Analytics
- Business Intelligence
- Dashboards
- Data Models
- Embedded Analytics
- Spectral
- Linting
- API Governance
---

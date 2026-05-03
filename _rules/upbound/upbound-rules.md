---
api_specs:
- filename: upbound-openapi.yml
  format: yaml
  label: Upbound API
  slug: upbound
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/upbound/refs/heads/main/openapi/upbound-openapi.yml
categories:
- upbound
description: Spectral linting rules defining API design standards and conventions for Upbound.
layout: rules
name: Upbound API Rules
provider_name: Upbound
provider_slug: upbound
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: upbound-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case (excluding path params)
  given: $.paths[*]~
  name: upbound-path-kebab-case
  severity: warn
- description: Organization-scoped paths must include orgName path parameter
  given: $.paths[?(@property.match(/\/organizations\//))]
  name: upbound-org-name-path-param
  severity: warn
- description: All operations must require bearer token authentication
  given: $.paths[*][get,post,put,delete]
  name: upbound-bearer-auth
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: upbound-summaries-title-case
  severity: warn
- description: List operations should return an items array
  given: $.paths[*].get.responses.200.content.application/json.schema
  name: upbound-list-responses-items-array
  severity: warn
- description: DELETE operations must return 204 No Content
  given: $.paths[*].delete.responses
  name: upbound-delete-returns-204
  severity: warn
- description: Collection path segments should be plural nouns
  given: $.paths[*]~
  name: upbound-resource-naming-plural
  severity: info
rules_file: rules/upbound-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/upbound/refs/heads/main/rules/upbound-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 1
  warn: 7
slug: upbound-rules
source_filename: upbound-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  upbound-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  upbound-path-kebab-case:\n    description: Path segments must use kebab-case (excluding path params)\n    message: \"Path '{{path}}' should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+$\"\n\n  upbound-org-name-path-param:\n    description: Organization-scoped paths must include orgName path parameter\n    message: \"Organization-scoped path must include {orgName} path parameter\"\n    severity: warn\n    given: \"$.paths[?(@property.match(/\\\\/organizations\\\\//))]\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \".*/\\\\{orgName\\\\}.*\"\n\n  upbound-bearer-auth:\n    description: All operations must require bearer token authentication\n    message: \"Operation should use BearerToken security scheme\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [security]\n            - properties: {}\n\n  upbound-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]* ?)+$\"\n\n  upbound-list-responses-items-array:\n    description: List operations should return an items array\n    message: \"List response should contain an items array\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content.application/json.schema\"\
  \n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            properties:\n              type: object\n              required: [items]\n\n  upbound-delete-returns-204:\n    description: DELETE operations must return 204 No Content\n    message: \"DELETE operation should return 204\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: ['204']\n\n  upbound-resource-naming-plural:\n    description: Collection path segments should be plural nouns\n    message: \"Collection path segment should be plural\"\n    severity: info\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*s(/|$|\\\\{).*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/upbound/refs/heads/main/rules/upbound-rules.yml
tags:
- Cloud Infrastructure
- Crossplane
- Developer Experience
- Internal Developer Platform
- Platform Engineering
- Spectral
- Linting
- API Governance
---

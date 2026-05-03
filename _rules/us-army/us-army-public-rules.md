---
api_specs:
- filename: us-army-public-openapi.yml
  format: yaml
  label: US Army Public API
  slug: us-army-public-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/us-army/refs/heads/main/openapi/us-army-public-openapi.yml
categories:
- army
description: Spectral linting rules defining API design standards and conventions for US Army.
layout: rules
name: US Army API Rules
provider_name: US Army
provider_slug: us-army
rule_count: 7
rules:
- description: All US Army API operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: army-operations-have-tags
  severity: warn
- description: All Army API paths should use the /api/v1 prefix via servers configuration
  given: $.servers[*].url
  name: army-paths-use-v1-prefix
  severity: info
- description: All GET operations must define a 200 response
  given: $.paths[*][get]
  name: army-get-operations-have-200
  severity: error
- description: All Army API operations must have operationId for SDK generation
  given: $.paths[*][get,post,put,patch,delete]
  name: army-operations-have-operation-ids
  severity: warn
- description: All parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: army-parameters-have-descriptions
  severity: warn
- description: All 200 responses should define a content schema
  given: $.paths[*][*].responses.200
  name: army-responses-have-schemas
  severity: warn
- description: US Army API servers must use HTTPS
  given: $.servers[*].url
  name: army-server-https
  severity: error
rules_file: rules/us-army-public-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/us-army/refs/heads/main/rules/us-army-public-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 4
slug: us-army-public-rules
source_filename: us-army-public-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  army-operations-have-tags:\n    description: All US Army API operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  army-paths-use-v1-prefix:\n    description: All Army API paths should use the /api/v1 prefix via servers configuration\n    severity: info\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\/v[0-9].*\"\n\n  army-get-operations-have-200:\n    description: All GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  army-operations-have-operation-ids:\n    description: All Army API operations must have operationId for SDK generation\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n     \
  \ function: truthy\n\n  army-parameters-have-descriptions:\n    description: All parameters should have descriptions\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  army-responses-have-schemas:\n    description: All 200 responses should define a content schema\n    severity: warn\n    given: \"$.paths[*][*].responses.200\"\n    then:\n      field: content\n      function: truthy\n\n  army-server-https:\n    description: US Army API servers must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/us-army/refs/heads/main/rules/us-army-public-rules.yml
tags:
- Army
- Federal Government
- Military
- Defense
- Open Data
- News
- Spectral
- Linting
- API Governance
---

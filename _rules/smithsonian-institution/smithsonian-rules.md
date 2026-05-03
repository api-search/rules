---
api_specs:
- filename: smithsonian-open-access-openapi.yml
  format: yaml
  label: Smithsonian Open Access API
  slug: open-access-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/smithsonian-institution/refs/heads/main/openapi/smithsonian-open-access-openapi.yml
categories:
- smithsonian
description: Spectral linting rules defining API design standards and conventions for Smithsonian Institution.
layout: rules
name: Smithsonian Institution API Rules
provider_name: Smithsonian Institution
provider_slug: smithsonian-institution
rule_count: 8
rules:
- description: All operations must have an operationId in camelCase
  given: $.paths[*][*]
  name: smithsonian-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: smithsonian-operation-tags
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: smithsonian-summary-title-case
  severity: warn
- description: All operations must require an api_key query parameter
  given: $.paths[*].get
  name: smithsonian-api-key-required
  severity: error
- description: Search endpoints should support start/rows pagination
  given: $.paths[*search*].get
  name: smithsonian-pagination-support
  severity: warn
- description: All successful responses should return application/json
  given: $.paths[*][*].responses.200.content
  name: smithsonian-json-response
  severity: warn
- description: API paths must not have trailing slashes
  given: $.paths
  name: smithsonian-no-trailing-slashes
  severity: warn
- description: All operations must document 401 Unauthorized response
  given: $.paths[*][*].responses
  name: smithsonian-error-401
  severity: warn
rules_file: rules/smithsonian-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/smithsonian-institution/refs/heads/main/rules/smithsonian-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: smithsonian-rules
source_filename: smithsonian-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  smithsonian-operation-ids:\n    description: All operations must have an operationId in camelCase\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: operationId\n      function: truthy\n\n  smithsonian-operation-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  smithsonian-summary-title-case:\n    description: Operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  smithsonian-api-key-required:\n    description: All operations must require an api_key query parameter\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  smithsonian-pagination-support:\n    description: Search endpoints should\
  \ support start/rows pagination\n    severity: warn\n    given: \"$.paths[*search*].get\"\n    then:\n      field: parameters\n      function: truthy\n\n  smithsonian-json-response:\n    description: All successful responses should return application/json\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - 'application/json'\n\n  smithsonian-no-trailing-slashes:\n    description: API paths must not have trailing slashes\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  smithsonian-error-401:\n    description: All operations must document 401 Unauthorized response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: '401'\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/smithsonian-institution/refs/heads/main/rules/smithsonian-rules.yml
tags:
- Collections
- Cultural Heritage
- Museums
- Open Data
- Art
- Natural History
- Research
- Spectral
- Linting
- API Governance
---

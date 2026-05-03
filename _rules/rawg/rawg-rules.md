---
api_specs:
- filename: rawg-openapi.yml
  format: yaml
  label: RAWG Video Games Database API
  slug: rawg
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rawg/refs/heads/main/openapi/rawg-openapi.yml
categories:
- rawg
description: Spectral linting rules defining API design standards and conventions for RAWG.
layout: rules
name: RAWG API Rules
provider_name: RAWG
provider_slug: rawg
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: rawg-operation-summary-title-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: rawg-operation-must-have-tags
  severity: error
- description: Path segments should use kebab-case
  given: $.paths[*]~
  name: rawg-path-kebab-case
  severity: warn
- description: All operations must declare the key query parameter
  given: $.paths[*][get].parameters[*]
  name: rawg-apikey-required
  severity: warn
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: rawg-responses-200-required
  severity: error
- description: List operations should support page and page_size parameters
  given: $.paths[*].get
  name: rawg-pagination-parameters
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths[*]~
  name: rawg-no-trailing-slash
  severity: warn
- description: OperationIds should follow provider pattern of resource_action
  given: $.paths[*][*].operationId
  name: rawg-operationid-consistent-naming
  severity: info
rules_file: rules/rawg-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rawg/refs/heads/main/rules/rawg-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 4
slug: rawg-rules
source_filename: rawg-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rawg-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Summary '{{value}}' must be Title Case\"\n    given: \"$.paths[*][*].summary\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ ][A-Z][a-z0-9]*)*|[A-Z]+)$\"\n\n  rawg-operation-must-have-tags:\n    description: Every operation must have at least one tag\n    message: Operations must include at least one tag\n    given: \"$.paths[*][*]\"\n    severity: error\n    then:\n      field: tags\n      function: truthy\n\n  rawg-path-kebab-case:\n    description: Path segments should use kebab-case\n    message: \"Path '{{path}}' should use kebab-case segments\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*|\\\\{[a-zA-Z_]+\\\\}))+$\"\n\n  rawg-apikey-required:\n    description:\
  \ All operations must declare the key query parameter\n    message: Operations must include the API key query parameter\n    given: \"$.paths[*][get].parameters[*]\"\n    severity: warn\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          if:\n            properties:\n              name:\n                const: key\n          then:\n            properties:\n              in:\n                const: query\n\n  rawg-responses-200-required:\n    description: All GET operations must define a 200 response\n    message: GET operations must have a 200 response defined\n    given: \"$.paths[*].get\"\n    severity: error\n    then:\n      field: responses.200\n      function: truthy\n\n  rawg-pagination-parameters:\n    description: List operations should support page and page_size parameters\n    message: List operations should include pagination parameters\n    given: \"$.paths[*].get\"\n    severity: info\n    then:\n      function: schema\n\
  \      functionOptions:\n        schema:\n          type: object\n          properties:\n            operationId:\n              pattern: \"_list$\"\n\n  rawg-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    message: \"Path '{{path}}' must not have a trailing slash\"\n    given: \"$.paths[*]~\"\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"\\\\/$\"\n\n  rawg-operationid-consistent-naming:\n    description: OperationIds should follow provider pattern of resource_action\n    message: \"OperationId '{{value}}' should follow the pattern resource_action\"\n    given: \"$.paths[*][*].operationId\"\n    severity: info\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9-]*_[a-z][a-z0-9-]*\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rawg/refs/heads/main/rules/rawg-rules.yml
tags:
- Database
- Entertainment
- Game Discovery
- Games
- Gaming
- Metadata
- Video Games
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: shell-b2b-mobility-openapi.yml
  format: yaml
  label: Shell B2B Mobility Card Management API
  slug: b2b-mobility-card-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-b2b-mobility-openapi.yml
- filename: shell-b2b-mobility-openapi.yml
  format: yaml
  label: Shell B2B Mobility Card Transaction Data API
  slug: b2b-mobility-card-transaction-data
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-b2b-mobility-openapi.yml
- filename: shell-b2b-mobility-openapi.yml
  format: yaml
  label: Shell B2B Mobility Invoice API
  slug: b2b-mobility-invoice
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-b2b-mobility-openapi.yml
- filename: shell-loyalty-openapi.yml
  format: yaml
  label: Shell Loyalty Catalogue API
  slug: loyalty-catalogue
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-loyalty-openapi.yml
- filename: shell-loyalty-openapi.yml
  format: yaml
  label: Shell Loyalty Account Management API
  slug: loyalty-account-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-loyalty-openapi.yml
- filename: shell-loyalty-openapi.yml
  format: yaml
  label: Shell Loyalty Points Balance API
  slug: loyalty-points-balance
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-loyalty-openapi.yml
- filename: shell-loyalty-openapi.yml
  format: yaml
  label: Shell Loyalty Points Redemption API
  slug: loyalty-points-redemption
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-loyalty-openapi.yml
- filename: shell-lubricants-openapi.yml
  format: yaml
  label: Shell Lubricants Order Management API
  slug: lubricants-order-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-lubricants-openapi.yml
- filename: shell-b2b-mobility-openapi.yml
  format: yaml
  label: Shell B2B Mobility Sites API
  slug: b2b-mobility-sites
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/openapi/shell-b2b-mobility-openapi.yml
categories:
- shell
description: Spectral linting rules defining API design standards and conventions for Shell.
layout: rules
name: Shell API Rules
provider_name: Shell
provider_slug: shell
rule_count: 13
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: shell-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case or curly-brace parameters
  given: $.paths
  name: shell-path-kebab-case
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: shell-must-have-summary
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: shell-must-have-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: shell-must-have-operation-id
  severity: error
- description: Shell APIs use OAuth2 client credentials for authentication
  given: $.components.securitySchemes[*]
  name: shell-oauth2-security
  severity: info
- description: B2B Mobility endpoints require colCoCode (Collecting Company Code) parameter
  given: $.paths[*][get,post].parameters[*]
  name: shell-colcocode-required
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths
  name: shell-no-trailing-slash
  severity: error
- description: All parameters should have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: shell-parameters-have-description
  severity: info
- description: 200 responses must have content defined
  given: $.paths[*][get,post,put,patch,delete].responses[200]
  name: shell-response-200-must-have-content
  severity: warn
- description: Schema property names should use camelCase
  given: $.components.schemas[*].properties
  name: shell-schemas-use-camel-case
  severity: info
- description: Paginated list responses should include totalCount, currentPage, pageCount
  given: $.components.schemas[*ListResponse]
  name: shell-pagination-fields
  severity: info
- description: Shell API servers must include version in the URL path
  given: $.servers[*].url
  name: shell-versioned-servers
  severity: warn
rules_file: rules/shell-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/rules/shell-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 5
  warn: 5
slug: shell-rules
source_filename: shell-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Shell API Naming Conventions\n  shell-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  shell-path-kebab-case:\n    description: Path segments must use kebab-case or curly-brace parameters\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_/-]+)+$\"\n\n  shell-must-have-summary:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  shell-must-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field:\
  \ tags\n      function: defined\n\n  shell-must-have-operation-id:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  shell-oauth2-security:\n    description: Shell APIs use OAuth2 client credentials for authentication\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  shell-colcocode-required:\n    description: B2B Mobility endpoints require colCoCode (Collecting Company Code) parameter\n    severity: info\n    given: \"$.paths[*][get,post].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  shell-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        notMatch: \".*/$\"\n\n  shell-parameters-have-description:\n    description: All parameters should have a description\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: defined\n\n  shell-response-200-must-have-content:\n    description: 200 responses must have content defined\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200]\"\n    then:\n      field: content\n      function: defined\n\n  shell-schemas-use-camel-case:\n    description: Schema property names should use camelCase\n    severity: info\n    given: \"$.components.schemas[*].properties\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  shell-pagination-fields:\n    description: Paginated list responses should include totalCount, currentPage, pageCount\n    severity: info\n    given: \"$.components.schemas[*ListResponse]\"\
  \n    then:\n      field: properties\n      function: defined\n\n  shell-versioned-servers:\n    description: Shell API servers must include version in the URL path\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"https://api.shell.com/[a-z-]+/v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shell/refs/heads/main/rules/shell-rules.yml
tags:
- Aviation
- Electric Vehicle Charging
- Energy
- Fleet Management
- Fuel
- Gas
- Loyalty
- Lubricants
- Mobility
- Oil and Gas
- Renewable Energy
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: shipstation-v1-openapi.yml
  format: yaml
  label: ShipStation V1 API
  slug: shipstation-v1-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shipstation/refs/heads/main/openapi/shipstation-v1-openapi.yml
categories:
- shipstation
description: Spectral linting rules defining API design standards and conventions for ShipStation.
layout: rules
name: ShipStation API Rules
provider_name: ShipStation
provider_slug: shipstation
rule_count: 13
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: shipstation-operation-id-camel-case
  severity: warn
- description: Path segments must be lowercase (ShipStation uses lowercase paths)
  given: $.paths
  name: shipstation-path-lowercase
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: shipstation-must-have-summary
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: shipstation-must-have-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: shipstation-must-have-operation-id
  severity: error
- description: GET operations must return 200 response
  given: $.paths[*].get
  name: shipstation-get-must-return-200
  severity: error
- description: POST operations should return 200 response (ShipStation uses 200 for creates)
  given: $.paths[*].post
  name: shipstation-post-must-return-200
  severity: warn
- description: ShipStation uses HTTP Basic authentication
  given: $.components.securitySchemes[*]
  name: shipstation-basic-auth
  severity: info
- description: Paginated list responses should include items array, total, page, and pages
  given: $.components.schemas[*PaginatedList]
  name: shipstation-paginated-list-fields
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths
  name: shipstation-no-trailing-slash
  severity: error
- description: All parameters must have a schema defined
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: shipstation-parameters-have-schema
  severity: error
- description: ShipStation enforces 40 req/min rate limit - document in description
  given: $.info
  name: shipstation-rate-limit-header
  severity: info
- description: ShipStation V1 API base URL must be ssapi.shipstation.com
  given: $.servers[*].url
  name: shipstation-ssapi-base-url
  severity: warn
rules_file: rules/shipstation-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shipstation/refs/heads/main/rules/shipstation-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 3
  warn: 5
slug: shipstation-rules
source_filename: shipstation-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # ShipStation API Naming Conventions\n  shipstation-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  shipstation-path-lowercase:\n    description: Path segments must be lowercase (ShipStation uses lowercase paths)\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_/-]+)+$\"\n\n  shipstation-must-have-summary:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: defined\n\n  shipstation-must-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: tags\n      function: defined\n\n  shipstation-must-have-operation-id:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  shipstation-get-must-return-200:\n    description: GET operations must return 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  shipstation-post-must-return-200:\n    description: POST operations should return 200 response (ShipStation uses 200 for creates)\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: responses.200\n      function: defined\n\n  shipstation-basic-auth:\n    description: ShipStation uses HTTP Basic authentication\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n         \
  \ type: object\n\n  shipstation-paginated-list-fields:\n    description: Paginated list responses should include items array, total, page, and pages\n    severity: info\n    given: \"$.components.schemas[*PaginatedList]\"\n    then:\n      field: properties\n      function: defined\n\n  shipstation-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \".*/$\"\n\n  shipstation-parameters-have-schema:\n    description: All parameters must have a schema defined\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: defined\n\n  shipstation-rate-limit-header:\n    description: ShipStation enforces 40 req/min rate limit - document in description\n    severity: info\n    given: \"$.info\"\n    then:\n      field: description\n      function: defined\n\n  shipstation-ssapi-base-url:\n\
  \    description: ShipStation V1 API base URL must be ssapi.shipstation.com\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"https://ssapi.shipstation.com\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shipstation/refs/heads/main/rules/shipstation-rules.yml
tags:
- Ecommerce
- Labels
- Logistics
- Order Management
- Shipping
- Warehousing
- Spectral
- Linting
- API Governance
---

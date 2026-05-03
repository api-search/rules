---
api_specs:
- filename: shippo-openapi.yml
  format: yaml
  label: Shippo API
  slug: shippo-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/shippo/refs/heads/main/openapi/shippo-openapi.yml
categories:
- shippo
description: Spectral linting rules defining API design standards and conventions for Shippo.
layout: rules
name: Shippo API Rules
provider_name: Shippo
provider_slug: shippo
rule_count: 14
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: shippo-operation-id-camel-case
  severity: warn
- description: Path segments must use kebab-case or curly-brace parameters
  given: $.paths
  name: shippo-path-kebab-case
  severity: warn
- description: Resource identifiers in paths should use Id suffix (e.g., AddressId, ParcelId)
  given: $.paths
  name: shippo-object-id-suffix
  severity: info
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: shippo-must-have-summary
  severity: error
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: shippo-must-have-tags
  severity: warn
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: shippo-must-have-operation-id
  severity: error
- description: 200 responses must have a content schema
  given: $.paths[*][get,post,put,patch,delete].responses[200]
  name: shippo-response-200-must-have-schema
  severity: warn
- description: POST operations should have a request body
  given: $.paths[*].post
  name: shippo-post-must-have-request-body
  severity: warn
- description: All operations should have security defined at root or operation level
  given: $.paths[*][get,post,put,patch,delete]
  name: shippo-security-defined
  severity: warn
- description: Shippo uses bearer token authentication (ShippoToken prefix)
  given: $.components.securitySchemes[*]
  name: shippo-bearer-token-auth
  severity: info
- description: Paginated list responses should include count, next, previous, and results fields
  given: $.components.schemas[*PaginatedList]
  name: shippo-paginated-response-fields
  severity: info
- description: Paths must not have trailing slashes
  given: $.paths
  name: shippo-no-trailing-slash
  severity: error
- description: All parameters should have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: shippo-parameters-have-description
  severity: info
- description: OpenAPI spec should define component schemas
  given: $.components
  name: shippo-components-schemas-exist
  severity: warn
rules_file: rules/shippo-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/shippo/refs/heads/main/rules/shippo-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 4
  warn: 7
slug: shippo-rules
source_filename: shippo-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Shippo API Naming Conventions\n  shippo-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  shippo-path-kebab-case:\n    description: Path segments must use kebab-case or curly-brace parameters\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}_-]+)+$\"\n\n  shippo-object-id-suffix:\n    description: Resource identifiers in paths should use Id suffix (e.g., AddressId, ParcelId)\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^.*$\"\n\n  shippo-must-have-summary:\n    description: All operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\
  \n    then:\n      field: summary\n      function: defined\n\n  shippo-must-have-tags:\n    description: All operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  shippo-must-have-operation-id:\n    description: All operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: defined\n\n  shippo-response-200-must-have-schema:\n    description: 200 responses must have a content schema\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].responses[200]\"\n    then:\n      field: content\n      function: defined\n\n  shippo-post-must-have-request-body:\n    description: POST operations should have a request body\n    severity: warn\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: defined\n\n  shippo-security-defined:\n\
  \    description: All operations should have security defined at root or operation level\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          oneOf:\n            - required: [security]\n\n  shippo-bearer-token-auth:\n    description: Shippo uses bearer token authentication (ShippoToken prefix)\n    severity: info\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n\n  shippo-paginated-response-fields:\n    description: Paginated list responses should include count, next, previous, and results fields\n    severity: info\n    given: \"$.components.schemas[*PaginatedList]\"\n    then:\n      field: properties\n      function: defined\n\n  shippo-no-trailing-slash:\n    description: Paths must not have trailing slashes\n    severity: error\n    given: \"$.paths\"\n    then:\n      function:\
  \ pattern\n      functionOptions:\n        notMatch: \".*/$\"\n\n  shippo-parameters-have-description:\n    description: All parameters should have a description\n    severity: info\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: defined\n\n  shippo-components-schemas-exist:\n    description: OpenAPI spec should define component schemas\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/shippo/refs/heads/main/rules/shippo-rules.yml
tags:
- Ecommerce
- Labels
- Logistics
- Returns
- Shipping
- Tracking
- Spectral
- Linting
- API Governance
---

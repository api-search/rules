---
api_specs:
- filename: rentcast-openapi.json
  format: json
  label: RentCast API
  slug: rentcast-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rentcast/refs/heads/main/openapi/rentcast-openapi.json
categories:
- rentcast
description: Spectral linting rules defining API design standards and conventions for RentCast.
layout: rules
name: RentCast API Rules
provider_name: RentCast
provider_slug: rentcast
rule_count: 7
rules:
- description: RentCast API uses X-Api-Key header authentication
  given: $.components.securitySchemes
  name: rentcast-api-key-auth
  severity: error
- description: RentCast API operations are read-only (GET)
  given: $.paths[*]
  name: rentcast-get-only-operations
  severity: warn
- description: Property lookup endpoints accept address or lat/lon
  given: $.paths[*].get.parameters[*].name
  name: rentcast-address-or-coordinates
  severity: hint
- description: List endpoints should support pagination
  given: $.paths['/properties'].get.parameters[*].name
  name: rentcast-pagination-params
  severity: warn
- description: propertyType parameter should use standard enum values
  given: $.paths[*].get.parameters[?(@.name == 'propertyType')].schema.enum[*]
  name: rentcast-property-type-enum
  severity: hint
- description: All operations must define a 200 response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: rentcast-response-200-defined
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: rentcast-summaries-title-case
  severity: warn
rules_file: rules/rentcast-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rentcast/refs/heads/main/rules/rentcast-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 3
slug: rentcast-rules
source_filename: rentcast-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\n\nrules:\n\n  rentcast-api-key-auth:\n    description: RentCast API uses X-Api-Key header authentication\n    message: \"API must declare X-Api-Key security scheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: truthy\n      field: ApiKeyAuth\n\n  rentcast-get-only-operations:\n    description: RentCast API operations are read-only (GET)\n    message: \"RentCast endpoints should be GET requests only\"\n    severity: warn\n    given: \"$.paths[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          additionalProperties: false\n          properties:\n            get: {}\n            parameters: {}\n\n  rentcast-address-or-coordinates:\n    description: Property lookup endpoints accept address or lat/lon\n    message: \"Property endpoints should support address or latitude/longitude parameters\"\n    severity: hint\n    given: \"$.paths[*].get.parameters[*].name\"\n    then:\n\
  \      function: enumeration\n      functionOptions:\n        values:\n          - address\n          - latitude\n          - longitude\n          - city\n          - state\n          - zipCode\n          - radius\n          - id\n\n  rentcast-pagination-params:\n    description: List endpoints should support pagination\n    message: \"List operations should include limit and offset parameters\"\n    severity: warn\n    given: \"$.paths['/properties'].get.parameters[*].name\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - limit\n          - offset\n          - includeTotalCount\n\n  rentcast-property-type-enum:\n    description: propertyType parameter should use standard enum values\n    message: \"propertyType should be one of the standard property type values\"\n    severity: hint\n    given: \"$.paths[*].get.parameters[?(@.name == 'propertyType')].schema.enum[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n       \
  \ values:\n          - Single Family\n          - Condo\n          - Townhouse\n          - Manufactured\n          - Multi-Family\n          - Apartment\n          - Land\n\n  rentcast-response-200-defined:\n    description: All operations must define a 200 response\n    message: \"Operation must define a 200 response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: truthy\n      field: \"200\"\n\n  rentcast-summaries-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &()/-]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rentcast/refs/heads/main/rules/rentcast-rules.yml
tags:
- Real Estate
- Property Data
- Valuation
- Rental Market
- AVM
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: starwood-hotel-search-openapi.yml
  format: yaml
  label: Hotel Search API
  slug: hotel-search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/starwood-hotels-and-resorts/refs/heads/main/openapi/starwood-hotel-search-openapi.yml
categories:
- starwood
description: Spectral linting rules defining API design standards and conventions for Starwood Hotels and Resorts.
layout: rules
name: Starwood Hotels and Resorts API Rules
provider_name: Starwood Hotels and Resorts
provider_slug: starwood-hotels-and-resorts
rule_count: 13
rules:
- description: All Starwood APIs must include contact information
  given: $.info
  name: starwood-info-contact-required
  severity: error
- description: All operations must have at least one tag for categorization
  given: $.paths[*][get,post,put,patch,delete]
  name: starwood-operation-tags-required
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: starwood-operation-summary-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: starwood-operation-summary-title-case
  severity: warn
- description: Operation IDs must use camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: starwood-operation-id-kebab-case
  severity: warn
- description: API paths must use kebab-case for path segments
  given: $.paths
  name: starwood-path-kebab-case
  severity: warn
- description: Date and date-time fields must declare the appropriate format
  given: $.components.schemas[*].properties[*date*,*Date*]
  name: starwood-dates-use-format
  severity: warn
- description: Hotel search must always include country parameter validation
  given: $.paths['/v1/hotels/search'].get.parameters[?(@.name=='country')]
  name: starwood-hotel-search-country-required
  severity: error
- description: Successful GET responses must define a response schema
  given: $.paths[*].get.responses['200'].content['application/json']
  name: starwood-response-200-schema
  severity: error
- description: All operations must define at least one error response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: starwood-response-error-defined
  severity: warn
- description: All schema components must include a description
  given: $.components.schemas[*]
  name: starwood-components-schemas-description
  severity: warn
- description: All parameters must have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: starwood-parameter-description
  severity: warn
- description: APIs must have security schemes defined
  given: $.components
  name: starwood-security-schemes-defined
  severity: warn
rules_file: rules/starwood-hotels-and-resorts-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/starwood-hotels-and-resorts/refs/heads/main/rules/starwood-hotels-and-resorts-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 9
slug: starwood-hotels-and-resorts-rules
source_filename: starwood-hotels-and-resorts-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n\n  starwood-info-contact-required:\n    description: All Starwood APIs must include contact information\n    message: API info object must include a contact with URL\n    severity: error\n    given: $.info\n    then:\n      - field: contact\n        function: truthy\n      - field: contact.url\n        function: truthy\n\n  starwood-operation-tags-required:\n    description: All operations must have at least one tag for categorization\n    message: Operation must include at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  starwood-operation-summary-required:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: summary\n      function: truthy\n\n  starwood-operation-summary-title-case:\n    description: Operation\
  \ summaries must use Title Case\n    message: Operation summary must use Title Case (e.g., \"Search Hotels\" not \"search hotels\")\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*(?: [A-Z][a-zA-Z0-9]*)*$'\n\n  starwood-operation-id-kebab-case:\n    description: Operation IDs must use camelCase\n    message: OperationId should use camelCase\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].operationId\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[a-z][a-zA-Z0-9]*$'\n\n  starwood-path-kebab-case:\n    description: API paths must use kebab-case for path segments\n    message: Path segments should use kebab-case (lowercase with hyphens)\n    severity: warn\n    given: $.paths\n    then:\n      field: '@key'\n      function: pattern\n      functionOptions:\n        match: '^(/([a-z][a-z0-9-]*|{[a-zA-Z][a-zA-Z0-9]*}))*/?$'\n\
  \n  starwood-dates-use-format:\n    description: Date and date-time fields must declare the appropriate format\n    message: Properties named with 'date' or 'Date' should use format date or date-time\n    severity: warn\n    given: $.components.schemas[*].properties[*date*,*Date*]\n    then:\n      field: format\n      function: truthy\n\n  starwood-hotel-search-country-required:\n    description: Hotel search must always include country parameter validation\n    message: Hotel search path GET /hotels/search must have country as a required parameter\n    severity: error\n    given: $.paths['/v1/hotels/search'].get.parameters[?(@.name=='country')]\n    then:\n      field: required\n      function: truthy\n\n  starwood-response-200-schema:\n    description: Successful GET responses must define a response schema\n    message: GET operations must have a schema defined for 200 response\n    severity: error\n    given: $.paths[*].get.responses['200'].content['application/json']\n    then:\n\
  \      field: schema\n      function: truthy\n\n  starwood-response-error-defined:\n    description: All operations must define at least one error response\n    message: Operations should define at least a 400 or 404 error response\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required:\n                - '400'\n            - required:\n                - '404'\n            - required:\n                - '401'\n            - required:\n                - '500'\n\n  starwood-components-schemas-description:\n    description: All schema components must include a description\n    message: Schema component must have a description field\n    severity: warn\n    given: $.components.schemas[*]\n    then:\n      field: description\n      function: truthy\n\n  starwood-parameter-description:\n    description: All parameters must have\
  \ a description\n    message: Parameter must have a description\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].parameters[*]\n    then:\n      field: description\n      function: truthy\n\n  starwood-security-schemes-defined:\n    description: APIs must have security schemes defined\n    message: API must define security schemes for authentication\n    severity: warn\n    given: $.components\n    then:\n      field: securitySchemes\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/starwood-hotels-and-resorts/refs/heads/main/rules/starwood-hotels-and-resorts-rules.yml
tags:
- Spectral
- Linting
- API Governance
---

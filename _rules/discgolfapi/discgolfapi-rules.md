---
api_specs:
- filename: discgolfapi-openapi.yml
  format: yaml
  label: DiscGolfAPI REST API
  slug: discgolfapi-rest-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/discgolfapi/refs/heads/main/openapi/discgolfapi-openapi.yml
categories:
- discgolfapi
description: Spectral linting rules defining API design standards and conventions for DiscGolfAPI.
layout: rules
name: DiscGolfAPI API Rules
provider_name: DiscGolfAPI
provider_slug: discgolfapi
rule_count: 15
rules:
- description: All DiscGolfAPI operations must have at least one tag
  given: $.paths[*][get,put,post,delete,patch]
  name: discgolfapi-operations-have-tags
  severity: warn
- description: All DiscGolfAPI operations must have a summary
  given: $.paths[*][get,put,post,delete,patch]
  name: discgolfapi-operations-have-summaries
  severity: error
- description: All DiscGolfAPI operations must have an operationId
  given: $.paths[*][get,put,post,delete,patch]
  name: discgolfapi-operations-have-operation-ids
  severity: error
- description: DiscGolfAPI operation summaries must use Title Case
  given: $.paths[*][get,put,post,delete,patch].summary
  name: discgolfapi-summaries-title-case
  severity: warn
- description: All DiscGolfAPI operations must have a description
  given: $.paths[*][get,put,post,delete,patch]
  name: discgolfapi-operations-have-descriptions
  severity: warn
- description: Public read endpoints should document a 429 Too Many Requests response so clients can implement backoff
  given: $.paths[*][get]
  name: discgolfapi-operations-define-429
  severity: warn
- description: Public read endpoints should document a 500 server error response
  given: $.paths[*][get]
  name: discgolfapi-operations-define-500
  severity: warn
- description: All response objects must have a description
  given: $.paths[*][*].responses[*]
  name: discgolfapi-responses-have-descriptions
  severity: warn
- description: All path parameters must be marked as required
  given: $.paths[*][*].parameters[?(@.in == 'path')]
  name: discgolfapi-path-parameters-required
  severity: error
- description: All component schemas should have either a description or a clear structural shape
  given: $.components.schemas[*]
  name: discgolfapi-components-schemas-described
  severity: info
- description: List endpoints (limit/offset) must define both Limit and Offset parameters
  given: $.paths['/courses'].get.parameters
  name: discgolfapi-list-endpoints-use-pagination
  severity: info
- description: List and detail responses should advertise the attribution and licence fields in the common envelope schema
  given: $.components.schemas.CommonEnvelope.required
  name: discgolfapi-response-envelope-attribution
  severity: info
- description: Course path parameter must declare the stable crs_ ID pattern
  given: $.components.parameters.CourseId.schema
  name: discgolfapi-stable-id-pattern
  severity: warn
- description: The info object must declare a licence so consumers know reuse terms
  given: $.info
  name: discgolfapi-info-license-required
  severity: error
- description: The info object must declare a contact so consumers can reach the provider
  given: $.info
  name: discgolfapi-info-contact-required
  severity: warn
rules_file: rules/discgolfapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/discgolfapi/refs/heads/main/rules/discgolfapi-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 3
  warn: 8
slug: discgolfapi-rules
source_filename: discgolfapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  discgolfapi-operations-have-tags:\n    description: All DiscGolfAPI operations must have at least one tag\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: tags\n      function: truthy\n\n  discgolfapi-operations-have-summaries:\n    description: All DiscGolfAPI operations must have a summary\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  discgolfapi-operations-have-operation-ids:\n    description: All DiscGolfAPI operations must have an operationId\n    severity: error\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  discgolfapi-summaries-title-case:\n    description: DiscGolfAPI operation summaries must use Title Case\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch].summary\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  discgolfapi-operations-have-descriptions:\n    description: All DiscGolfAPI operations must have a description\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  discgolfapi-operations-define-429:\n    description: Public read endpoints should document a 429 Too Many Requests response so clients can implement backoff\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: \"responses.429\"\n      function: truthy\n\n  discgolfapi-operations-define-500:\n    description: Public read endpoints should document a 500 server error response\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      field: \"responses.500\"\n      function: truthy\n\n  discgolfapi-responses-have-descriptions:\n    description: All response objects must have a description\n    severity: warn\n    given:\
  \ \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  discgolfapi-path-parameters-required:\n    description: All path parameters must be marked as required\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')]\"\n    then:\n      field: required\n      function: truthy\n\n  discgolfapi-components-schemas-described:\n    description: All component schemas should have either a description or a clear structural shape\n    severity: info\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  discgolfapi-list-endpoints-use-pagination:\n    description: List endpoints (limit/offset) must define both Limit and Offset parameters\n    severity: info\n    given: \"$.paths['/courses'].get.parameters\"\n    then:\n      function: length\n      functionOptions:\n        min: 4\n\n  discgolfapi-response-envelope-attribution:\n    description: List and detail responses should advertise\
  \ the attribution and licence fields in the common envelope schema\n    severity: info\n    given: \"$.components.schemas.CommonEnvelope.required\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            const: attribution\n\n  discgolfapi-stable-id-pattern:\n    description: Course path parameter must declare the stable crs_ ID pattern\n    severity: warn\n    given: \"$.components.parameters.CourseId.schema\"\n    then:\n      field: pattern\n      function: truthy\n\n  discgolfapi-info-license-required:\n    description: The info object must declare a licence so consumers know reuse terms\n    severity: error\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  discgolfapi-info-contact-required:\n    description: The info object must declare a contact so consumers can reach the provider\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function:\
  \ truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/discgolfapi/refs/heads/main/rules/discgolfapi-rules.yml
tags:
- Disc Golf
- Sports
- Courses
- Open Data
- Recreation
- Spectral
- Linting
- API Governance
---

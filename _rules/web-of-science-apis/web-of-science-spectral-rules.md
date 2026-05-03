---
api_specs:
- filename: web-of-science-starter-openapi.yml
  format: yaml
  label: Web of Science Starter API
  slug: web-of-science-starter-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/web-of-science-apis/refs/heads/main/openapi/web-of-science-starter-openapi.yml
- filename: web-of-science-expanded-openapi.yml
  format: yaml
  label: Web of Science API Expanded
  slug: web-of-science-expanded-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/web-of-science-apis/refs/heads/main/openapi/web-of-science-expanded-openapi.yml
categories:
- wos
description: Spectral linting rules defining API design standards and conventions for Web of Science APIs.
layout: rules
name: Web of Science APIs API Rules
provider_name: Web of Science APIs
provider_slug: web-of-science-apis
rule_count: 22
rules:
- description: Web of Science API specs must use OpenAPI 3.0.x
  given: $
  name: wos-openapi-version
  severity: error
- description: API must have a title
  given: $.info
  name: wos-info-title
  severity: error
- description: API must have a description
  given: $.info
  name: wos-info-description
  severity: warn
- description: API must have a version
  given: $.info
  name: wos-info-version
  severity: error
- description: All operations must have a summary
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-operation-summary
  severity: warn
- description: All operations should have a description
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-operation-description
  severity: info
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-operation-operationid
  severity: error
- description: All operations must have tags
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-operation-tags
  severity: warn
- description: All operations must have responses defined
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-operation-responses
  severity: error
- description: GET operations must have a 200 response
  given: $.paths[*][get]
  name: wos-response-200
  severity: error
- description: All operations should have a 401 response
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-response-401
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: wos-schema-properties-description
  severity: info
- description: Parameters should have descriptions
  given: $.paths[*][get,post,put,delete,patch].parameters[*]
  name: wos-parameter-description
  severity: warn
- description: API must define API key security scheme
  given: $.components.securitySchemes
  name: wos-apikey-security
  severity: error
- description: API must have global security defined
  given: $
  name: wos-security-defined
  severity: warn
- description: Operations should use valid Web of Science tags
  given: $.paths[*][get,post].tags[*]
  name: wos-operation-tags-valid
  severity: info
- description: API must define servers
  given: $
  name: wos-servers-defined
  severity: error
- description: Search operations should support limit/count parameter
  given: $.paths.~1documents[get]
  name: wos-pagination-limit
  severity: info
- description: Operations should have Microcks extensions for testing
  given: $.paths[*][get,post,put,delete,patch]
  name: wos-microcks-operation
  severity: info
- description: Search endpoints should have query parameter
  given: $.paths.~1documents[get].parameters[*]
  name: wos-search-query-parameter
  severity: warn
- description: UID parameters should describe Web of Science identifier format
  given: $.paths[*][get].parameters[?(@.name == 'uniqueId')]
  name: wos-uid-format
  severity: info
- description: API info should include contact details
  given: $.info
  name: wos-info-contact
  severity: info
rules_file: rules/web-of-science-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/web-of-science-apis/refs/heads/main/rules/web-of-science-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 7
  warn: 7
slug: web-of-science-spectral-rules
source_filename: web-of-science-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  wos-openapi-version:\n    description: Web of Science API specs must use OpenAPI 3.0.x\n    message: \"OpenAPI version must be 3.0.x\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.0\\\\.\"\n\n  wos-info-title:\n    description: API must have a title\n    message: \"Info object must have a title\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  wos-info-description:\n    description: API must have a description\n    message: \"Info object must have a description\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  wos-info-version:\n    description: API must have a version\n    message: \"Info object must have a version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  wos-operation-summary:\n   \
  \ description: All operations must have a summary\n    message: \"Operation must have a summary\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: summary\n      function: truthy\n\n  wos-operation-description:\n    description: All operations should have a description\n    message: \"Operation should have a description\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: description\n      function: truthy\n\n  wos-operation-operationid:\n    description: All operations must have an operationId\n    message: \"Operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: truthy\n\n  wos-operation-tags:\n    description: All operations must have tags\n    message: \"Operation must have tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field:\
  \ tags\n      function: truthy\n\n  wos-operation-responses:\n    description: All operations must have responses defined\n    message: \"Operation must have responses defined\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: responses\n      function: truthy\n\n  wos-response-200:\n    description: GET operations must have a 200 response\n    message: \"GET operations must define a 200 response\"\n    severity: error\n    given: \"$.paths[*][get]\"\n    then:\n      field: responses.200\n      function: truthy\n\n  wos-response-401:\n    description: All operations should have a 401 response\n    message: \"Operations should define a 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: responses.401\n      function: truthy\n\n  wos-schema-properties-description:\n    description: Schema properties should have descriptions\n    message: \"Schema properties should\
  \ have descriptions\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wos-parameter-description:\n    description: Parameters should have descriptions\n    message: \"Parameter should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  wos-apikey-security:\n    description: API must define API key security scheme\n    message: \"API must require API key authentication\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: ApiKeyAuth\n      function: truthy\n\n  wos-security-defined:\n    description: API must have global security defined\n    message: \"API must have security defined at global level\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  wos-operation-tags-valid:\n    description:\
  \ Operations should use valid Web of Science tags\n    message: \"Operations should use standard WOS API tags\"\n    severity: info\n    given: \"$.paths[*][get,post].tags[*]\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - documents\n          - journals\n          - search\n          - records\n          - citations\n          - reports\n\n  wos-servers-defined:\n    description: API must define servers\n    message: \"Servers array must be defined\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  wos-pagination-limit:\n    description: Search operations should support limit/count parameter\n    message: \"Search/list operations should support pagination limit parameter\"\n    severity: info\n    given: \"$.paths.~1documents[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required: [parameters]\n\n  wos-microcks-operation:\n    description:\
  \ Operations should have Microcks extensions for testing\n    message: \"Operation should include x-microcks-operation extension\"\n    severity: info\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  wos-search-query-parameter:\n    description: Search endpoints should have query parameter\n    message: \"Search operations must have a query parameter\"\n    severity: warn\n    given: \"$.paths.~1documents[get].parameters[*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            name:\n              type: string\n          required: [name]\n\n  wos-uid-format:\n    description: UID parameters should describe Web of Science identifier format\n    message: \"UID parameters should describe WOS unique identifier format\"\n    severity: info\n    given: \"$.paths[*][get].parameters[?(@.name == 'uniqueId')]\"\n    then:\n      field: description\n      function:\
  \ truthy\n\n  wos-info-contact:\n    description: API info should include contact details\n    message: \"Info object should have contact information\"\n    severity: info\n    given: \"$.info\"\n    then:\n      field: contact\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/web-of-science-apis/refs/heads/main/rules/web-of-science-spectral-rules.yml
tags:
- Research
- Academic
- Bibliometrics
- Citations
- Science
- Scholarly
- Spectral
- Linting
- API Governance
---

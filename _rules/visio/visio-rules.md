---
api_specs:
- filename: visio-javascript-openapi.yml
  format: yaml
  label: Visio JavaScript API
  slug: visio-javascript-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/visio/refs/heads/main/openapi/visio-javascript-openapi.yml
categories:
- visio
description: Spectral linting rules defining API design standards and conventions for Microsoft Visio API.
layout: rules
name: Microsoft Visio API API Rules
provider_name: Microsoft Visio API
provider_slug: visio
rule_count: 10
rules:
- description: ''
  given: $.paths[*][*].operationId
  name: visio-operationid-camelcase
  severity: warn
- description: ''
  given: $.paths[*][*]
  name: visio-operation-summary-required
  severity: error
- description: ''
  given: $.paths[*][*].summary
  name: visio-summary-title-case
  severity: warn
- description: ''
  given: $.paths[*][*].responses[*]
  name: visio-response-description-required
  severity: warn
- description: ''
  given: $.paths[*][*].parameters[?(@.in=='path')]
  name: visio-path-param-described
  severity: warn
- description: ''
  given: $.components.schemas[*]
  name: visio-schema-description
  severity: hint
- description: ''
  given: $.paths[*][*]
  name: visio-operation-tags-required
  severity: warn
- description: ''
  given: $.paths[*].get.responses
  name: visio-get-success-200
  severity: warn
- description: ''
  given: $.paths[*][*].responses['500'].content['application/json'].schema
  name: visio-error-schema-ref
  severity: hint
- description: ''
  given: $.paths[*].patch
  name: visio-patch-has-request-body
  severity: error
rules_file: rules/visio-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/visio/refs/heads/main/rules/visio-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 6
slug: visio-rules
source_filename: visio-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  # Visio API conventions: all operation IDs must follow camelCase\n  visio-operationid-camelcase:\n    message: \"Operation IDs must use camelCase (e.g. getDocument, listShapes)\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # All operations must have a summary\n  visio-operation-summary-required:\n    message: \"All Visio API operations must have a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  # Summaries must use Title Case\n  visio-summary-title-case:\n    message: \"Operation summaries must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]+$\"\n\n  # All responses must have descriptions\n  visio-response-description-required:\n\
  \    message: \"All response codes must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Path parameters must be documented\n  visio-path-param-described:\n    message: \"All path parameters must have a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in=='path')]\"\n    then:\n      field: description\n      function: truthy\n\n  # Schemas must have descriptions\n  visio-schema-description:\n    message: \"All named schemas must have a description\"\n    severity: hint\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # Operations must be tagged\n  visio-operation-tags-required:\n    message: \"All operations must be assigned at least one tag\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Use 200 for successful GET responses\n  visio-get-success-200:\n\
  \    message: \"GET operations must return 200 for success\"\n    severity: warn\n    given: \"$.paths[*].get.responses\"\n    then:\n      field: \"200\"\n      function: truthy\n\n  # Error responses should reference the Error schema\n  visio-error-schema-ref:\n    message: \"500 error responses should reference the Error schema component\"\n    severity: hint\n    given: \"$.paths[*][*].responses['500'].content['application/json'].schema\"\n    then:\n      field: \"$ref\"\n      function: truthy\n\n  # PATCH operations must have a request body\n  visio-patch-has-request-body:\n    message: \"PATCH operations must include a requestBody\"\n    severity: error\n    given: \"$.paths[*].patch\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/visio/refs/heads/main/rules/visio-rules.yml
tags:
- Business Process
- Collaboration
- Diagrams
- Enterprise
- Flowcharts
- Microsoft 365
- Visualization
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: sumo-logic-openapi.yml
  format: yaml
  label: Sumo Logic API
  slug: sumo-logic
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/sumo-logic/refs/heads/main/openapi/sumo-logic-openapi.yml
categories:
- sumo
description: Spectral linting rules defining API design standards and conventions for Sumo Logic.
layout: rules
name: Sumo Logic API Rules
provider_name: Sumo Logic
provider_slug: sumo-logic
rule_count: 9
rules:
- description: Sumo Logic API paths must be versioned with /v1/ or /v2/
  given: $.paths
  name: sumo-logic-versioned-paths
  severity: warn
- description: All Sumo Logic operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: sumo-logic-operation-summary-required
  severity: error
- description: All Sumo Logic operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: sumo-logic-operation-id-required
  severity: error
- description: Sumo Logic operationIds should use camelCase
  given: $.paths[*][*].operationId
  name: sumo-logic-operation-id-camel-case
  severity: warn
- description: Sumo Logic uses Basic authentication (accessId:accessKey)
  given: $.components.securitySchemes
  name: sumo-logic-basic-auth
  severity: warn
- description: All Sumo Logic operations must be tagged
  given: $.paths[*][get,post,put,patch,delete]
  name: sumo-logic-operation-tags-required
  severity: warn
- description: Sumo Logic error responses should include errorCode
  given: $.components.schemas[?(@.properties.errorCode)]
  name: sumo-logic-error-response-code
  severity: info
- description: Sumo Logic GET operations should have a 200 response schema
  given: $.paths[*].get.responses['200']
  name: sumo-logic-get-response-schema
  severity: warn
- description: Sumo Logic uses 'limit' for pagination page size
  given: $.paths[*][*].parameters[?(@.name == 'pageSize' || @.name == 'count')]
  name: sumo-logic-pagination-limit
  severity: info
rules_file: rules/sumo-logic-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/sumo-logic/refs/heads/main/rules/sumo-logic-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 5
slug: sumo-logic-rules
source_filename: sumo-logic-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Sumo Logic uses versioned paths /v1/ and /v2/\n  sumo-logic-versioned-paths:\n    description: Sumo Logic API paths must be versioned with /v1/ or /v2/\n    message: \"{{description}} - path '{{property}}' must start with /v1/ or /v2/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[12]/\"\n\n  # All operations must have summaries\n  sumo-logic-operation-summary-required:\n    description: All Sumo Logic operations must have a summary\n    message: \"{{description}} - operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # All operations must have an operationId\n  sumo-logic-operation-id-required:\n    description: All Sumo Logic operations must have an operationId\n    message: \"{{description}} - operation is missing an operationId\"\
  \n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Sumo Logic uses camelCase operationIds\n  sumo-logic-operation-id-camel-case:\n    description: Sumo Logic operationIds should use camelCase\n    message: \"{{description}} - '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  # Basic authentication is required\n  sumo-logic-basic-auth:\n    description: Sumo Logic uses Basic authentication (accessId:accessKey)\n    message: \"{{description}} - security scheme should reference basicAuth\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      field: basicAuth\n      function: truthy\n\n  # All operations must have tags\n  sumo-logic-operation-tags-required:\n    description: All Sumo Logic operations must be tagged\n  \
  \  message: \"{{description}} - operation is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # Response error models should have errorCode\n  sumo-logic-error-response-code:\n    description: Sumo Logic error responses should include errorCode\n    message: \"{{description}} - error response schema should include errorCode field\"\n    severity: info\n    given: \"$.components.schemas[?(@.properties.errorCode)]\"\n    then:\n      field: properties.errorCode\n      function: truthy\n\n  # 200 responses for GET should have schema\n  sumo-logic-get-response-schema:\n    description: Sumo Logic GET operations should have a 200 response schema\n    message: \"{{description}} - GET operation should return a schema\"\n    severity: warn\n    given: \"$.paths[*].get.responses['200']\"\n    then:\n      field: content\n      function: truthy\n\n  # Pagination parameters should use standard names\n\
  \  sumo-logic-pagination-limit:\n    description: Sumo Logic uses 'limit' for pagination page size\n    message: \"{{description}} - use 'limit' for pagination (not 'pageSize' or 'count')\"\n    severity: info\n    given: \"$.paths[*][*].parameters[?(@.name == 'pageSize' || @.name == 'count')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        notMatch: \"pageSize|count\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/sumo-logic/refs/heads/main/rules/sumo-logic-rules.yml
tags:
- Logging
- Observability
- Security
- Monitoring
- Analytics
- DevOps
- SIEM
- Spectral
- Linting
- API Governance
---

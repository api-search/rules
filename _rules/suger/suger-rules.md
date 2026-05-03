---
api_specs:
- filename: suger-openapi.yml
  format: yaml
  label: Suger API
  slug: suger
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/suger/refs/heads/main/openapi/suger-openapi.yml
categories:
- suger
description: Spectral linting rules defining API design standards and conventions for Suger.
layout: rules
name: Suger API Rules
provider_name: Suger
provider_slug: suger
rule_count: 9
rules:
- description: All Suger API paths must be scoped to an organization via /org/{orgId}
  given: $.paths
  name: suger-org-scoped-paths
  severity: error
- description: Suger operationIds must use PascalCase
  given: $.paths[*][*].operationId
  name: suger-operation-id-pascal-case
  severity: warn
- description: All Suger API operations must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: suger-operation-summary-required
  severity: error
- description: All Suger API operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: suger-operation-tags-required
  severity: warn
- description: All Suger API operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: suger-operation-id-required
  severity: error
- description: Suger API uses APIKeyAuth - all operations must declare security
  given: $.paths[*][get,post,put,patch,delete]
  name: suger-security-api-key
  severity: warn
- description: Suger path parameters should use camelCase naming
  given: $.paths[*][*].parameters[?(@.in == 'path')].name
  name: suger-path-param-camel-case
  severity: warn
- description: Suger request bodies should use application/json content type
  given: $.paths[*][post,put,patch].requestBody.content
  name: suger-request-body-json
  severity: warn
- description: Suger API 200 responses should have a schema defined
  given: $.paths[*][get,post,put,patch].responses['200'].content
  name: suger-response-schema-defined
  severity: warn
rules_file: rules/suger-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/suger/refs/heads/main/rules/suger-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 6
slug: suger-rules
source_filename: suger-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\n\nrules:\n  # Suger API Convention: All paths must be under /org/{orgId}/\n  suger-org-scoped-paths:\n    description: All Suger API paths must be scoped to an organization via /org/{orgId}\n    message: \"{{description}} - path '{{property}}' must start with /org/{orgId}\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/org/\\\\{orgId\\\\}\"\n\n  # Suger uses camelCase for path parameters and operationIds\n  suger-operation-id-pascal-case:\n    description: Suger operationIds must use PascalCase\n    message: \"{{description}} - '{{value}}' should be PascalCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]+$\"\n\n  # All operations must have summaries\n  suger-operation-summary-required:\n    description: All Suger API operations must have a summary\n\
  \    message: \"{{description}} - operation is missing a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  # All operations must have at least one tag\n  suger-operation-tags-required:\n    description: All Suger API operations must have at least one tag\n    message: \"{{description}} - operation is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  # All operations must have an operationId\n  suger-operation-id-required:\n    description: All Suger API operations must have an operationId\n    message: \"{{description}} - operation is missing an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  # Suger uses API key auth - must be declared\n  suger-security-api-key:\n    description: Suger API\
  \ uses APIKeyAuth - all operations must declare security\n    message: \"{{description}} - operation should declare security requirements\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  # Path parameters must use camelCase\n  suger-path-param-camel-case:\n    description: Suger path parameters should use camelCase naming\n    message: \"{{description}} - path parameter '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # Request bodies should have application/json content type\n  suger-request-body-json:\n    description: Suger request bodies should use application/json content type\n    message: \"{{description}} - request body should use application/json\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody.content\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"application/json\"\n\n  # Response schemas should be defined\n  suger-response-schema-defined:\n    description: Suger API 200 responses should have a schema defined\n    message: \"{{description}} - 200 response should have a schema\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch].responses['200'].content\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/suger/refs/heads/main/rules/suger-rules.yml
tags:
- Cloud Marketplace
- GTM
- SaaS
- Billing
- Entitlement
- Revenue
- Co-Sell
- Spectral
- Linting
- API Governance
---

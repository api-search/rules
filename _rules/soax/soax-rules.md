---
api_specs:
- filename: soax-web-data-api-openapi.yml
  format: yaml
  label: SOAX Web Data API
  slug: soax-web-data-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/soax/refs/heads/main/openapi/soax-web-data-api-openapi.yml
- filename: soax-proxy-management-api-openapi.yml
  format: yaml
  label: SOAX Proxy Management API
  slug: soax-proxy-management-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/soax/refs/heads/main/openapi/soax-proxy-management-api-openapi.yml
categories:
- soax
description: Spectral linting rules defining API design standards and conventions for SOAX.
layout: rules
name: SOAX API Rules
provider_name: SOAX
provider_slug: soax
rule_count: 9
rules:
- description: SOAX APIs use API key authentication
  given: $.components.securitySchemes[*]
  name: soax-api-key-auth
  severity: error
- description: All SOAX API operations must have tags
  given: $.paths.*.*
  name: soax-tags-required
  severity: error
- description: Operation IDs should use camelCase
  given: $.paths.*.*.operationId
  name: soax-operation-id-camel-case
  severity: warn
- description: All SOAX API paths must include a version prefix
  given: $.paths
  name: soax-path-versioned
  severity: error
- description: POST endpoints should accept JSON
  given: $.paths.*.post.requestBody.content
  name: soax-request-body-json
  severity: warn
- description: All operations should define a 200/201 success response
  given: $.paths.*.*
  name: soax-response-200-defined
  severity: error
- description: Authenticated endpoints should define 401 response
  given: $.paths.*.*
  name: soax-error-401-defined
  severity: warn
- description: Package management paths should use package_key parameter
  given: $.paths[*].parameters[?(@.in == 'path')].name
  name: soax-package-key-path-param
  severity: warn
- description: Responses should reference a schema
  given: $.paths.*.*.responses.*.content.*.schema
  name: soax-response-schema-defined
  severity: warn
rules_file: rules/soax-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/soax/refs/heads/main/rules/soax-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 5
slug: soax-rules
source_filename: soax-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  soax-api-key-auth:\n    description: SOAX APIs use API key authentication\n    message: \"SOAX endpoints must use API key authentication via X-SOAX-API-Secret or api-key header.\"\n    severity: error\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - apiKey\n\n  soax-tags-required:\n    description: All SOAX API operations must have tags\n    message: \"Operation '{{path}}' must include at least one tag.\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  soax-operation-id-camel-case:\n    description: Operation IDs should use camelCase\n    message: \"operationId '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  soax-path-versioned:\n\
  \    description: All SOAX API paths must include a version prefix\n    message: \"Path '{{path}}' must include a version prefix (/v1/, /v2/, etc.).\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n\n  soax-request-body-json:\n    description: POST endpoints should accept JSON\n    message: \"POST operations should accept application/json content type.\"\n    severity: warn\n    given: \"$.paths.*.post.requestBody.content\"\n    then:\n      function: truthy\n\n  soax-response-200-defined:\n    description: All operations should define a 200/201 success response\n    message: \"Operation must define at least one success response (200 or 201).\"\n    severity: error\n    given: \"$.paths.*.*\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            responses:\n              anyOf:\n                - required: ['200']\n                - required:\
  \ ['201']\n\n  soax-error-401-defined:\n    description: Authenticated endpoints should define 401 response\n    message: \"Endpoints with security should document a 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: responses\n      function: truthy\n\n  soax-package-key-path-param:\n    description: Package management paths should use package_key parameter\n    message: \"Proxy management paths must parameterize the package identifier as 'package_key'.\"\n    severity: warn\n    given: \"$.paths[*].parameters[?(@.in == 'path')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(package_key|[a-z][a-z_]*)$\"\n\n  soax-response-schema-defined:\n    description: Responses should reference a schema\n    message: \"Response content should define a schema for documentation clarity.\"\n    severity: warn\n    given: \"$.paths.*.*.responses.*.content.*.schema\"\n    then:\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/soax/refs/heads/main/rules/soax-rules.yml
tags:
- Proxy
- Web Scraping
- Residential Proxies
- Mobile Proxies
- Datacenter Proxies
- Data Extraction
- Anti-Bot Bypass
- Spectral
- Linting
- API Governance
---

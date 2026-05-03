---
api_specs:
- filename: rapidapi-rest-platform-api-openapi.yml
  format: yaml
  label: RapidAPI REST Platform API
  slug: rapidapi-rest-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-rest-platform-api-openapi.yml
- filename: rapidapi-graphql-platform-api-openapi.yml
  format: yaml
  label: RapidAPI GraphQL Platform API
  slug: rapidapi-graphql-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-graphql-platform-api-openapi.yml
- filename: rapidapi-hub-api-openapi.yml
  format: yaml
  label: RapidAPI Hub API
  slug: rapidapi-hub-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-hub-api-openapi.yml
- filename: rapidapi-testing-api-openapi.yml
  format: yaml
  label: RapidAPI Testing API
  slug: rapidapi-testing-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-testing-api-openapi.yml
- filename: rapidapi-studio-api-openapi.yml
  format: yaml
  label: RapidAPI Studio API
  slug: rapidapi-studio-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-studio-api-openapi.yml
- filename: rapidapi-gateway-api-openapi.yml
  format: yaml
  label: RapidAPI Gateway API
  slug: rapidapi-gateway-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/openapi/rapidapi-gateway-api-openapi.yml
categories:
- rapidapi
description: Spectral linting rules defining API design standards and conventions for RapidAPI.
layout: rules
name: RapidAPI API Rules
provider_name: RapidAPI
provider_slug: rapidapi
rule_count: 8
rules:
- description: All operationIds must use camelCase to match the RapidAPI Platform API convention.
  given: $.paths[*][*].operationId
  name: rapidapi-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.paths[*][*].tags[*]
  name: rapidapi-tags-title-case
  severity: warn
- description: All RapidAPI platform endpoints should use the rapidApiKey security scheme.
  given: $.components.securitySchemes
  name: rapidapi-apikey-security-defined
  severity: warn
- description: List operations should support offset and limit pagination.
  given: $.paths[*].get
  name: rapidapi-pagination-support
  severity: hint
- description: API paths must not end with a trailing slash.
  given: $.paths
  name: rapidapi-no-trailing-slashes
  severity: error
- description: DELETE operations should return 204 No Content.
  given: $.paths[*].delete.responses
  name: rapidapi-delete-returns-204
  severity: warn
- description: Operations requiring authentication should define a 401 response.
  given: $.paths[*][*].responses
  name: rapidapi-responses-include-401
  severity: warn
- description: POST and PUT operations should define a request body.
  given: $.paths[*][post,put]
  name: rapidapi-request-body-required
  severity: warn
rules_file: rules/rapidapi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/rules/rapidapi-rules.yml
severity_counts:
  error: 1
  hint: 1
  info: 0
  warn: 6
slug: rapidapi-rules
source_filename: rapidapi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  rapidapi-operation-ids-camel-case:\n    description: All operationIds must use camelCase to match the RapidAPI Platform API convention.\n    message: \"OperationId '{{value}}' must be camelCase (e.g., listApis, createTest).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rapidapi-tags-title-case:\n    description: All tags must use Title Case.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]*$\"\n\n  rapidapi-apikey-security-defined:\n    description: All RapidAPI platform endpoints should use the rapidApiKey security scheme.\n    message: \"RapidAPI platform operations should specify rapidApiKey security.\"\n    severity: warn\n    given: \"$.components.securitySchemes\"\
  \n    then:\n      field: rapidApiKey\n      function: truthy\n\n  rapidapi-pagination-support:\n    description: List operations should support offset and limit pagination.\n    message: \"List operation should support 'offset' and 'limit' parameters.\"\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: truthy\n\n  rapidapi-no-trailing-slashes:\n    description: API paths must not end with a trailing slash.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  rapidapi-delete-returns-204:\n    description: DELETE operations should return 204 No Content.\n    message: \"DELETE operation at '{{path}}' should define a 204 response.\"\n    severity: warn\n    given: \"$.paths[*].delete.responses\"\n    then:\n      field: 204\n      function: truthy\n\n  rapidapi-responses-include-401:\n    description: Operations\
  \ requiring authentication should define a 401 response.\n    message: \"Authenticated operation should define a 401 Unauthorized response.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: 401\n      function: truthy\n\n  rapidapi-request-body-required:\n    description: POST and PUT operations should define a request body.\n    message: \"POST/PUT operation at '{{path}}' should define a requestBody.\"\n    severity: warn\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rapidapi/refs/heads/main/rules/rapidapi-rules.yml
tags:
- API Marketplace
- API Management
- API Testing
- API Gateway
- API Design
- Enterprise
- Spectral
- Linting
- API Governance
---

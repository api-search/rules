---
api_specs:
- filename: xiaomi-open-api-openapi.yml
  format: yaml
  label: Xiaomi Open API
  slug: xiaomi-open-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/xiaomi/refs/heads/main/openapi/xiaomi-open-api-openapi.yml
- filename: xiaomi-galaxy-fds-openapi.yml
  format: yaml
  label: Xiaomi Galaxy FDS API
  slug: xiaomi-galaxy-fds
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/xiaomi/refs/heads/main/openapi/xiaomi-galaxy-fds-openapi.yml
- filename: xiaomi-mimo-api-openapi.yml
  format: yaml
  label: Xiaomi MiMo AI API
  slug: xiaomi-mimo-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/xiaomi/refs/heads/main/openapi/xiaomi-mimo-api-openapi.yml
categories:
- xiaomi
description: Spectral linting rules defining API design standards and conventions for Xiaomi.
layout: rules
name: Xiaomi API Rules
provider_name: Xiaomi
provider_slug: xiaomi
rule_count: 8
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: xiaomi-operation-summary-title-case
  severity: warn
- description: All operationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: xiaomi-operation-id-camel-case
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][*]
  name: xiaomi-tags-required
  severity: warn
- description: All operations must define a 200 or 201 response.
  given: $.paths[*][*].responses
  name: xiaomi-response-200-required
  severity: warn
- description: All operations must define security requirements.
  given: $.paths[*][*]
  name: xiaomi-security-defined
  severity: info
- description: All operations must have a description.
  given: $.paths[*][*].description
  name: xiaomi-description-required
  severity: warn
- description: All parameters must have descriptions.
  given: $.paths[*][*].parameters[*].description
  name: xiaomi-parameter-description
  severity: info
- description: API paths should be prefixed with a version segment like /v1/.
  given: $.paths
  name: xiaomi-api-version-prefix
  severity: info
rules_file: rules/xiaomi-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/xiaomi/refs/heads/main/rules/xiaomi-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 3
  warn: 5
slug: xiaomi-rules
source_filename: xiaomi-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  xiaomi-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  xiaomi-operation-id-camel-case:\n    description: All operationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  xiaomi-tags-required:\n    description: All operations must have at least one tag.\n    message: \"Operation is missing tags.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  xiaomi-response-200-required:\n    description:\
  \ All operations must define a 200 or 201 response.\n    message: \"Operation must define a success (200/201) response.\"\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  xiaomi-security-defined:\n    description: All operations must define security requirements.\n    message: \"Operation should define security requirements.\"\n    severity: info\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: truthy\n\n  xiaomi-description-required:\n    description: All operations must have a description.\n    message: \"Operation is missing a description.\"\n    severity: warn\n    given: \"$.paths[*][*].description\"\n    then:\n      function: truthy\n\n  xiaomi-parameter-description:\n    description: All parameters must have descriptions.\n    message: \"Parameter '{{value}}' is missing a description.\"\
  \n    severity: info\n    given: \"$.paths[*][*].parameters[*].description\"\n    then:\n      function: truthy\n\n  xiaomi-api-version-prefix:\n    description: API paths should be prefixed with a version segment like /v1/.\n    message: \"Path '{{property}}' should begin with a version prefix (e.g., /v1/).\"\n    severity: info\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/xiaomi/refs/heads/main/rules/xiaomi-rules.yml
tags:
- Consumer Electronics
- IoT
- Smart Home
- Mobile
- Artificial Intelligence
- Cloud Storage
- Machine Learning
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: watchguard-cloud-platform-openapi.yml
  format: yaml
  label: WatchGuard Cloud Platform API
  slug: watchguard-cloud-platform-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/watchguard/refs/heads/main/openapi/watchguard-cloud-platform-openapi.yml
- filename: watchguard-endpoint-security-openapi.yml
  format: yaml
  label: WatchGuard Endpoint Security Management API
  slug: watchguard-endpoint-security-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/watchguard/refs/heads/main/openapi/watchguard-endpoint-security-openapi.yml
categories:
- wg
description: Spectral linting rules defining API design standards and conventions for WatchGuard.
layout: rules
name: WatchGuard API Rules
provider_name: WatchGuard
provider_slug: watchguard
rule_count: 7
rules:
- description: All WatchGuard API operations must declare both bearerAuth and apiKeyAuth security.
  given: $.paths[*][get,post,put,patch,delete]
  name: wg-dual-security-required
  severity: error
- description: Operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: wg-summary-title-case
  severity: warning
- description: WatchGuard API operation IDs must use camelCase.
  given: $.paths[*][*].operationId
  name: wg-operation-id-camel-case
  severity: warning
- description: WatchGuard Cloud API paths with {accountId} must mark it as required.
  given: $.paths[*][*].parameters[?(@.name == 'accountId')]
  name: wg-account-id-required
  severity: error
- description: All WatchGuard API operations must document a 401 Unauthorized response.
  given: $.paths[*][get,post,put,patch,delete].responses
  name: wg-401-response-required
  severity: warning
- description: All WatchGuard API server URLs must use HTTPS.
  given: $.servers[*].url
  name: wg-https-servers
  severity: error
- description: WatchGuard API specs must include a contact object in info.
  given: $.info
  name: wg-info-contact
  severity: warning
rules_file: rules/watchguard-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/watchguard/refs/heads/main/rules/watchguard-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 0
  warning: 4
slug: watchguard-rules
source_filename: watchguard-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # WatchGuard APIs require both bearerAuth and apiKeyAuth security schemes\n  wg-dual-security-required:\n    description: All WatchGuard API operations must declare both bearerAuth and apiKeyAuth security.\n    message: \"Operation '{{title}}' must declare both bearerAuth and apiKeyAuth security requirements.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  # Summaries must use Title Case\n  wg-summary-title-case:\n    description: Operation summaries must use Title Case.\n    message: \"Summary '{{value}}' should use Title Case.\"\n    severity: warning\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*([ ][A-Z][a-zA-Z0-9]*)*$\"\n\n  # Operation IDs must use camelCase\n  wg-operation-id-camel-case:\n    description: WatchGuard API operation IDs must use camelCase.\n \
  \   message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warning\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: casing\n      functionOptions:\n        type: camel\n\n  # accountId path parameters are required in all WatchGuard Cloud endpoints\n  wg-account-id-required:\n    description: WatchGuard Cloud API paths with {accountId} must mark it as required.\n    message: \"Path parameter 'accountId' must be required.\"\n    severity: error\n    given: \"$.paths[*][*].parameters[?(@.name == 'accountId')]\"\n    then:\n      field: required\n      function: truthy\n\n  # All responses must include a 401 Unauthorized\n  wg-401-response-required:\n    description: All WatchGuard API operations must document a 401 Unauthorized response.\n    message: \"Operation '{{title}}' is missing a 401 Unauthorized response.\"\n    severity: warning\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      field: \"401\"\n      function:\
  \ defined\n\n  # API servers must use HTTPS\n  wg-https-servers:\n    description: All WatchGuard API server URLs must use HTTPS.\n    message: \"Server URL '{{value}}' must use HTTPS.\"\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # Ensure the API has a contact object\n  wg-info-contact:\n    description: WatchGuard API specs must include a contact object in info.\n    message: \"API spec is missing an info.contact object.\"\n    severity: warning\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/watchguard/refs/heads/main/rules/watchguard-rules.yml
tags:
- Cloud Security
- Endpoint Security
- Firewall
- MFA
- Network Security
- Zero Trust
- Spectral
- Linting
- API Governance
---

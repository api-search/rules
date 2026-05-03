---
categories:
- trellix
description: Spectral linting rules defining API design standards and conventions for Trellix.
layout: rules
name: Trellix API Rules
provider_name: Trellix
provider_slug: trellix
rule_count: 9
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: trellix-operation-id-camel-case
  severity: warn
- description: Operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: trellix-summary-title-case
  severity: warn
- description: All operations must define security requirements
  given: $.paths[*][get,post,put,patch,delete]
  name: trellix-security-defined
  severity: error
- description: All GET operations must define a 200 response
  given: $.paths[*].get
  name: trellix-response-200-get
  severity: error
- description: Authenticated operations should define a 401 response
  given: $.paths[*][get,post,put,patch,delete]
  name: trellix-response-401-defined
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: trellix-tag-defined
  severity: warn
- description: Trellix APIs use OAuth 2.0 Bearer token authentication
  given: $.components.securitySchemes
  name: trellix-oauth2-bearer
  severity: info
- description: API paths should use kebab-case
  given: $.paths[*]~
  name: trellix-path-kebab-case
  severity: warn
- description: POST and PUT operations should define a request body
  given: $.paths[*][post,put]
  name: trellix-post-request-body
  severity: warn
rules_file: rules/trellix-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/trellix/refs/heads/main/rules/trellix-spectral-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: trellix-spectral-rules
source_filename: trellix-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  trellix-operation-id-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  trellix-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 /()+&-]*$\"\n\n  trellix-security-defined:\n    description: All operations must define security requirements\n    message: \"Operation must define security requirements\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: defined\n\n  trellix-response-200-get:\n    description: All GET operations\
  \ must define a 200 response\n    message: \"GET operation must define a 200 success response\"\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  trellix-response-401-defined:\n    description: Authenticated operations should define a 401 response\n    message: \"Operation should define 401 Unauthorized\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses.401\n      function: defined\n\n  trellix-tag-defined:\n    description: All operations must have at least one tag\n    message: \"Operation must include at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: defined\n\n  trellix-oauth2-bearer:\n    description: Trellix APIs use OAuth 2.0 Bearer token authentication\n    message: \"Security scheme should use OAuth 2.0 or Bearer token\"\n    severity: info\n    given: \"$.components.securitySchemes\"\
  \n    then:\n      function: defined\n\n  trellix-path-kebab-case:\n    description: API paths should use kebab-case\n    message: \"Path should use kebab-case\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9][a-z0-9-]*(/[a-z0-9][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]*\\\\})*)+$\"\n\n  trellix-post-request-body:\n    description: POST and PUT operations should define a request body\n    message: \"POST/PUT operation should define a requestBody\"\n    severity: warn\n    given: \"$.paths[*][post,put]\"\n    then:\n      field: requestBody\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/trellix/refs/heads/main/rules/trellix-spectral-rules.yml
tags:
- Cloud Security
- Cybersecurity
- Endpoint Security
- Threat Detection
- Threat Intelligence
- XDR
- Spectral
- Linting
- API Governance
---

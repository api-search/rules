---
api_specs:
- filename: ramp-developer-api-openapi.yml
  format: yaml
  label: Ramp Developer API
  slug: ramp-developer-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/ramp/refs/heads/main/openapi/ramp-developer-api-openapi.yml
categories:
- ramp
description: Spectral linting rules defining API design standards and conventions for Ramp.
layout: rules
name: Ramp API Rules
provider_name: Ramp
provider_slug: ramp
rule_count: 8
rules:
- description: All operationIds must use camelCase to match the Ramp Developer API convention.
  given: $.paths[*][*].operationId
  name: ramp-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case to match the Ramp Developer API convention.
  given: $.paths[*][*].tags[*]
  name: ramp-tags-title-case
  severity: warn
- description: List operations (GET collections) should support pagination via page_size and start query parameters.
  given: $.paths[*].get
  name: ramp-pagination-list-operations
  severity: hint
- description: All GET operations must define a 200 response.
  given: $.paths[*].get.responses
  name: ramp-response-200-required
  severity: error
- description: All operations that require authentication should reference OAuth2 scopes.
  given: $.paths[*][*]
  name: ramp-oauth2-scopes-defined
  severity: warn
- description: API paths must not end with a trailing slash.
  given: $.paths
  name: ramp-no-trailing-slashes
  severity: error
- description: Path segments should use kebab-case for multi-word identifiers.
  given: $.paths
  name: ramp-kebab-case-paths
  severity: warn
- description: All operations should have a description for developer clarity.
  given: $.paths[*][*]
  name: ramp-resource-descriptions
  severity: hint
rules_file: rules/ramp-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ramp/refs/heads/main/rules/ramp-rules.yml
severity_counts:
  error: 2
  hint: 2
  info: 0
  warn: 4
slug: ramp-rules
source_filename: ramp-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  ramp-operation-ids-camel-case:\n    description: All operationIds must use camelCase to match the Ramp Developer API convention.\n    message: \"OperationId '{{value}}' must be camelCase (e.g., listTransactions, getCard).\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  ramp-tags-title-case:\n    description: All tags must use Title Case to match the Ramp Developer API convention.\n    message: \"Tag '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z ]*$\"\n\n  ramp-pagination-list-operations:\n    description: List operations (GET collections) should support pagination via page_size and start query parameters.\n    message: \"List operation '{{path}}' should support 'page_size' and 'start' query\
  \ parameters for pagination.\"\n    severity: hint\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n\n  ramp-response-200-required:\n    description: All GET operations must define a 200 response.\n    message: \"GET operation at '{{path}}' must define a 200 response.\"\n    severity: error\n    given: \"$.paths[*].get.responses\"\n    then:\n      function: truthy\n\n  ramp-oauth2-scopes-defined:\n    description: All operations that require authentication should reference OAuth2 scopes.\n    message: \"Operation '{{path}}' should reference an OAuth2 scope via the security field.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            security:\n              type: array\n\n  ramp-no-trailing-slashes:\n    description: API paths must not end with\
  \ a trailing slash.\n    message: \"Path '{{path}}' must not end with a trailing slash.\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"/$\"\n\n  ramp-kebab-case-paths:\n    description: Path segments should use kebab-case for multi-word identifiers.\n    message: \"Path '{{path}}' should use kebab-case for multi-word segments (e.g., /audit-logs not /auditLogs).\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/[a-z][a-z0-9-]*|/\\\\{[^}]+\\\\})*)?$\"\n\n  ramp-resource-descriptions:\n    description: All operations should have a description for developer clarity.\n    message: \"Operation '{{path}}' should have a description field.\"\n    severity: hint\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/ramp/refs/heads/main/rules/ramp-rules.yml
tags:
- Finance
- Spend Management
- Corporate Cards
- Expense Management
- Accounts Payable
- Bill Pay
- Accounting
- Reimbursements
- Spectral
- Linting
- API Governance
---

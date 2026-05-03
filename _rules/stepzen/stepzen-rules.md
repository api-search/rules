---
categories:
- stepzen
description: Spectral linting rules defining API design standards and conventions for StepZen.
layout: rules
name: StepZen API Rules
provider_name: StepZen
provider_slug: stepzen
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: stepzen-operation-summary-title-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stepzen-tags-required
  severity: error
- description: GET operations must return 200
  given: $.paths[*].get
  name: stepzen-response-200-required
  severity: error
- description: StepZen uses API key authentication
  given: $.components.securitySchemes
  name: stepzen-api-key-auth
  severity: error
- description: OperationIds must use camelCase
  given: $.paths[*][*].operationId
  name: stepzen-operation-ids-camel-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths
  name: stepzen-path-kebab-case
  severity: warn
- description: Operations must handle 401 unauthorized
  given: $.paths[*][*].responses
  name: stepzen-401-responses
  severity: warn
- description: Operations must have descriptions
  given: $.paths[*][*]
  name: stepzen-descriptions-required
  severity: error
rules_file: rules/stepzen-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stepzen/refs/heads/main/rules/stepzen-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: stepzen-rules
source_filename: stepzen-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stepzen-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  stepzen-tags-required:\n    description: All operations must have at least one tag\n    message: Operations must include tags\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  stepzen-response-200-required:\n    description: GET operations must return 200\n    message: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  stepzen-api-key-auth:\n    description: StepZen uses API key authentication\n    message: Security scheme must\
  \ include apiKeyAuth\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: apiKeyAuth\n      function: truthy\n\n  stepzen-operation-ids-camel-case:\n    description: OperationIds must use camelCase\n    message: \"OperationId '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stepzen-path-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{value}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*(\\\\{[a-zA-Z]+\\\\})?)*)*$\"\n\n  stepzen-401-responses:\n    description: Operations must handle 401 unauthorized\n    message: Operations must define a 401 response\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n\
  \      field: \"401\"\n      function: defined\n\n  stepzen-descriptions-required:\n    description: Operations must have descriptions\n    message: Operation is missing a description\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stepzen/refs/heads/main/rules/stepzen-rules.yml
tags:
- Backend Integration
- GraphQL
- API Gateway
- REST to GraphQL
- IBM
- Data Federation
- Spectral
- Linting
- API Governance
---

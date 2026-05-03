---
api_specs:
- filename: stellar-cyber-openapi.yml
  format: yaml
  label: Stellar Cyber Open XDR API
  slug: stellar-cyber
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/stellar-cyber/refs/heads/main/openapi/stellar-cyber-openapi.yml
categories:
- stellar
description: Spectral linting rules defining API design standards and conventions for Stellar Cyber.
layout: rules
name: Stellar Cyber API Rules
provider_name: Stellar Cyber
provider_slug: stellar-cyber
rule_count: 11
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: stellar-cyber-operation-summary-title-case
  severity: warn
- description: OperationIds should use camelCase
  given: $.paths[*][*].operationId
  name: stellar-cyber-operation-id-kebab-case
  severity: warn
- description: All operations must have at least one tag
  given: $.paths[*][*]
  name: stellar-cyber-tags-required
  severity: error
- description: All GET operations must return a 200 response
  given: $.paths[*].get
  name: stellar-cyber-response-200-required
  severity: error
- description: All operations should have security requirements defined
  given: $.paths[*][*]
  name: stellar-cyber-security-defined
  severity: warn
- description: Stellar Cyber uses JWT Bearer authentication exclusively
  given: $.components.securitySchemes
  name: stellar-cyber-bearer-auth-only
  severity: error
- description: URL path segments must use kebab-case
  given: $.paths
  name: stellar-cyber-path-kebab-case
  severity: warn
- description: Request bodies on POST/PUT operations should have descriptions
  given: $.paths[*][post,put].requestBody
  name: stellar-cyber-request-body-described
  severity: warn
- description: All parameters should have descriptions
  given: $.paths[*][*].parameters[*]
  name: stellar-cyber-parameters-have-descriptions
  severity: warn
- description: Descriptions must not be empty
  given: $..[description]
  name: stellar-cyber-no-empty-descriptions
  severity: warn
- description: Operations should define 401 unauthorized response
  given: $.paths[*][*].responses
  name: stellar-cyber-4xx-responses
  severity: warn
rules_file: rules/stellar-cyber-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/stellar-cyber/refs/heads/main/rules/stellar-cyber-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 0
  warn: 8
slug: stellar-cyber-rules
source_filename: stellar-cyber-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  stellar-cyber-operation-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z][a-zA-Z0-9]*)*$\"\n\n  stellar-cyber-operation-id-kebab-case:\n    description: OperationIds should use camelCase\n    message: \"OperationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  stellar-cyber-tags-required:\n    description: All operations must have at least one tag\n    message: Operations must include tags for categorization\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  stellar-cyber-response-200-required:\n\
  \    description: All GET operations must return a 200 response\n    message: GET operations must define a 200 response\n    severity: error\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: truthy\n\n  stellar-cyber-security-defined:\n    description: All operations should have security requirements defined\n    message: Operations should define security requirements\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: security\n      function: defined\n\n  stellar-cyber-bearer-auth-only:\n    description: Stellar Cyber uses JWT Bearer authentication exclusively\n    message: Security scheme must use bearerAuth\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      field: bearerAuth\n      function: truthy\n\n  stellar-cyber-path-kebab-case:\n    description: URL path segments must use kebab-case\n    message: \"Path segment '{{value}}' must use kebab-case\"\n    severity: warn\n    given: \"$.paths\"\
  \n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(\\\\/([a-z][a-z0-9-]*(\\\\{[a-zA-Z]+\\\\})?)*)*$\"\n\n  stellar-cyber-request-body-described:\n    description: Request bodies on POST/PUT operations should have descriptions\n    message: Request body content should be described\n    severity: warn\n    given: \"$.paths[*][post,put].requestBody\"\n    then:\n      field: description\n      function: defined\n\n  stellar-cyber-parameters-have-descriptions:\n    description: All parameters should have descriptions\n    message: \"Parameter '{{value}}' is missing a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  stellar-cyber-no-empty-descriptions:\n    description: Descriptions must not be empty\n    message: Description must not be empty\n    severity: warn\n    given: \"$..[description]\"\n    then:\n      function: truthy\n\n  stellar-cyber-4xx-responses:\n\
  \    description: Operations should define 401 unauthorized response\n    message: Operations should define a 401 response for authentication failures\n    severity: warn\n    given: \"$.paths[*][*].responses\"\n    then:\n      field: \"401\"\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/stellar-cyber/refs/heads/main/rules/stellar-cyber-rules.yml
tags:
- Cybersecurity
- Security
- XDR
- SIEM
- SOAR
- AI
- Spectral
- Linting
- API Governance
---

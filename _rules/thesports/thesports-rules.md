---
api_specs:
- filename: thesports-football-openapi.yml
  format: yaml
  label: TheSports Football API
  slug: football-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/thesports/refs/heads/main/openapi/thesports-football-openapi.yml
categories:
- thesports
description: Spectral linting rules defining API design standards and conventions for TheSports.
layout: rules
name: TheSports API Rules
provider_name: TheSports
provider_slug: thesports
rule_count: 6
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: thesports-operation-summary-title-case
  severity: warn
- description: All operations must include user_key authentication parameter.
  given: $.paths[*][get,post,put,delete].parameters[*]
  name: thesports-user-key-required
  severity: error
- description: All successful responses should return a code field.
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: thesports-response-code-field
  severity: warn
- description: All successful responses should return a message field.
  given: $.paths[*][*].responses.200.content.application/json.schema.properties
  name: thesports-response-message-field
  severity: warn
- description: All operations must have at least one tag.
  given: $.paths[*][get,post,put,delete]
  name: thesports-tag-defined
  severity: error
- description: Operation IDs must use camelCase.
  given: $.paths[*][*].operationId
  name: thesports-operation-id-kebab-case
  severity: warn
rules_file: rules/thesports-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/thesports/refs/heads/main/rules/thesports-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 4
slug: thesports-rules
source_filename: thesports-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # TheSports API-specific Spectral rules\n\n  thesports-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' should use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*([ -][A-Z0-9][a-z0-9]*)*)$\"\n\n  thesports-user-key-required:\n    description: All operations must include user_key authentication parameter.\n    message: \"TheSports operations must include user_key query parameter.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete].parameters[*]\"\n    then:\n      field: name\n      function: truthy\n\n  thesports-response-code-field:\n    description: All successful responses should return a code field.\n    message: \"TheSports responses should include a code field indicating success (0) or error.\"\n    severity: warn\n\
  \    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      field: code\n      function: truthy\n\n  thesports-response-message-field:\n    description: All successful responses should return a message field.\n    message: \"TheSports responses should include a message field (e.g., 'ok').\"\n    severity: warn\n    given: \"$.paths[*][*].responses.200.content.application/json.schema.properties\"\n    then:\n      field: message\n      function: truthy\n\n  thesports-tag-defined:\n    description: All operations must have at least one tag.\n    message: \"Operations must have at least one tag for categorization.\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  thesports-operation-id-kebab-case:\n    description: Operation IDs must use camelCase.\n    message: \"Operation ID '{{value}}' should use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/thesports/refs/heads/main/rules/thesports-rules.yml
tags:
- Sports
- Football
- Basketball
- Tennis
- Esports
- Data
- Real-Time
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: docs
  format: yaml
  label: SimpleLocalize Translation API
  slug: translation-api
  spec_type: OpenAPI
  url: https://api.simplelocalize.io/openapi/docs
categories:
- simplelocalize
description: Spectral linting rules defining API design standards and conventions for SimpleLocalize.
layout: rules
name: SimpleLocalize API Rules
provider_name: SimpleLocalize
provider_slug: simplelocalize
rule_count: 8
rules:
- description: All translation management endpoints must require the X-SimpleLocalize-Token API key header
  given: $.paths[?(!@path.match(/\/api\/v2\/projects/))].*.security
  name: simplelocalize-api-key-header
  severity: error
- description: All paths must be versioned with /api/v1/ or /api/v2/ prefix
  given: $.paths[*]~
  name: simplelocalize-versioned-paths
  severity: error
- description: All success responses must use SimpleLocalize envelope with status, message, and data fields
  given: $.paths.*.*.responses.200.content.application/json.schema
  name: simplelocalize-response-envelope
  severity: warn
- description: All operations must have camelCase operationId values
  given: $.paths.*.*.operationId
  name: simplelocalize-operation-ids
  severity: error
- description: All operations must have at least one tag
  given: $.paths.*.*
  name: simplelocalize-tag-usage
  severity: warn
- description: Customer key schema must enforce max length of 40 characters
  given: $.components.schemas.Customer.properties.key
  name: simplelocalize-customer-key-length
  severity: warn
- description: Language key schema must enforce max length of 20 characters
  given: $.components.schemas.Language.properties.key
  name: simplelocalize-language-key-length
  severity: warn
- description: Security schemes must define both ApiKeyAuth and BearerAuth
  given: $.components.securitySchemes
  name: simplelocalize-security-schemes
  severity: error
rules_file: rules/simplelocalize-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/simplelocalize/refs/heads/main/rules/simplelocalize-rules.yml
severity_counts:
  error: 4
  hint: 0
  info: 0
  warn: 4
slug: simplelocalize-rules
source_filename: simplelocalize-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  simplelocalize-api-key-header:\n    description: All translation management endpoints must require the X-SimpleLocalize-Token API key header\n    message: \"Translation management endpoint is missing X-SimpleLocalize-Token security requirement\"\n    severity: error\n    given: \"$.paths[?(!@path.match(/\\\\/api\\\\/v2\\\\/projects/))].*.security\"\n    then:\n      function: truthy\n\n  simplelocalize-versioned-paths:\n    description: All paths must be versioned with /api/v1/ or /api/v2/ prefix\n    message: \"API path '{{value}}' must be versioned with /api/v1/ or /api/v2/\"\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/api/v[0-9]+/\"\n\n  simplelocalize-response-envelope:\n    description: All success responses must use SimpleLocalize envelope with status, message, and data fields\n    message: \"Response schema should include status (integer), message (string), and data fields\"\
  \n    severity: warn\n    given: \"$.paths.*.*.responses.200.content.application/json.schema\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - status\n            - message\n\n  simplelocalize-operation-ids:\n    description: All operations must have camelCase operationId values\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: error\n    given: \"$.paths.*.*.operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  simplelocalize-tag-usage:\n    description: All operations must have at least one tag\n    message: \"Operation is missing a tag\"\n    severity: warn\n    given: \"$.paths.*.*\"\n    then:\n      field: tags\n      function: truthy\n\n  simplelocalize-customer-key-length:\n    description: Customer key schema must enforce max length of 40 characters\n    message: \"Customer key should have maxLength\
  \ of 40\"\n    severity: warn\n    given: \"$.components.schemas.Customer.properties.key\"\n    then:\n      field: maxLength\n      function: truthy\n\n  simplelocalize-language-key-length:\n    description: Language key schema must enforce max length of 20 characters\n    message: \"Language key should have maxLength of 20\"\n    severity: warn\n    given: \"$.components.schemas.Language.properties.key\"\n    then:\n      field: maxLength\n      function: truthy\n\n  simplelocalize-security-schemes:\n    description: Security schemes must define both ApiKeyAuth and BearerAuth\n    message: \"Missing required security scheme definition\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required:\n            - ApiKeyAuth\n            - BearerAuth\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/simplelocalize/refs/heads/main/rules/simplelocalize-rules.yml
tags:
- Localization
- Translation
- Internationalization
- Spectral
- Linting
- API Governance
---

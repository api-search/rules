---
api_specs:
- filename: dead-drop-openapi.yml
  format: yaml
  label: Dead Drop API v1
  slug: dead-drop-api-v1
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/dead-drop/refs/heads/main/openapi/dead-drop-openapi.yml
categories:
- dead
description: Spectral linting rules defining API design standards and conventions for Dead Drop.
layout: rules
name: Dead Drop API Rules
provider_name: Dead Drop
provider_slug: dead-drop
rule_count: 8
rules:
- description: Every operation must have a non-empty summary.
  given: $.paths[*][get,put,post,delete,patch,options,head]
  name: dead-drop-operation-summary-required
  severity: error
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,put,post,delete,patch].summary
  name: dead-drop-operation-summary-title-case
  severity: warn
- description: Every operation must have at least one tag.
  given: $.paths[*][get,put,post,delete,patch]
  name: dead-drop-operation-tags-required
  severity: error
- description: Drop id schemas must enforce 64 lowercase hex characters.
  given: $.paths['/drops/{id}'].parameters[?(@.name=='id')].schema
  name: dead-drop-id-hex-pattern
  severity: warn
- description: Each operation must declare a successful (2xx) response.
  given: $.paths[*][get,put,post,delete,patch].responses
  name: dead-drop-success-response-required
  severity: error
- description: POST/PUT/DELETE drop endpoints must require I_agree_with_terms_and_conditions.
  given: $.paths['/drops'].post.requestBody.content.application/json.schema.required
  name: dead-drop-terms-required-on-mutations
  severity: warn
- description: Error responses must use the {error:{code,message}} envelope.
  given: $.paths[*][get,put,post,delete,patch].responses[?(@property.match(/^[45]/))].content.application/json.schema.properties
  name: dead-drop-error-envelope
  severity: warn
- description: encryptionAlgo enum should include pbkdf2-aes256-gcm-v1.
  given: $..encryptionAlgo.enum
  name: dead-drop-encryption-algo-enum
  severity: info
rules_file: rules/dead-drop-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/dead-drop/refs/heads/main/rules/dead-drop-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: dead-drop-rules
source_filename: dead-drop-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nfunctions: []\n\nrules:\n  # Operations must have summaries in Title Case.\n  dead-drop-operation-summary-required:\n    description: Every operation must have a non-empty summary.\n    message: \"Operation '{{property}}' is missing a summary.\"\n    severity: error\n    given: $.paths[*][get,put,post,delete,patch,options,head]\n    then:\n      field: summary\n      function: truthy\n\n  dead-drop-operation-summary-title-case:\n    description: Operation summaries should use Title Case.\n    message: \"Operation summary should use Title Case: '{{value}}'.\"\n    severity: warn\n    given: $.paths[*][get,put,post,delete,patch].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  # Operations must be tagged.\n  dead-drop-operation-tags-required:\n    description: Every operation must have at least one tag.\n    message: \"Operation is missing tags.\"\n    severity: error\n    given: $.paths[*][get,put,post,delete,patch]\n\
  \    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  # Drop identifiers must follow the SHA-256 hex pattern.\n  dead-drop-id-hex-pattern:\n    description: Drop id schemas must enforce 64 lowercase hex characters.\n    message: \"Drop id parameter or property should be patterned as ^[a-f0-9]{64}$.\"\n    severity: warn\n    given: \"$.paths['/drops/{id}'].parameters[?(@.name=='id')].schema\"\n    then:\n      field: pattern\n      function: truthy\n\n  # All endpoints must declare a 200 (or 201) response.\n  dead-drop-success-response-required:\n    description: Each operation must declare a successful (2xx) response.\n    message: \"Operation is missing a 2xx success response.\"\n    severity: error\n    given: $.paths[*][get,put,post,delete,patch].responses\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \"^2\\\\d\\\\d$\": {}\n          minProperties:\
  \ 1\n\n  # Mutating endpoints must require terms-of-service acknowledgement.\n  dead-drop-terms-required-on-mutations:\n    description: POST/PUT/DELETE drop endpoints must require I_agree_with_terms_and_conditions.\n    message: \"Mutating drop operation should require I_agree_with_terms_and_conditions.\"\n    severity: warn\n    given: \"$.paths['/drops'].post.requestBody.content.application/json.schema.required\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - I_agree_with_terms_and_conditions\n\n  # Error responses must use the {error:{code,message}} envelope.\n  dead-drop-error-envelope:\n    description: Error responses must use the {error:{code,message}} envelope.\n    message: \"Error response schema must contain an 'error' object with 'code' and 'message'.\"\n    severity: warn\n    given: \"$.paths[*][get,put,post,delete,patch].responses[?(@property.match(/^[45]/))].content.application/json.schema.properties\"\n    then:\n      field:\
  \ error\n      function: truthy\n\n  # Document the encryption algorithm enum.\n  dead-drop-encryption-algo-enum:\n    description: encryptionAlgo enum should include pbkdf2-aes256-gcm-v1.\n    message: \"encryptionAlgo enum must include pbkdf2-aes256-gcm-v1.\"\n    severity: info\n    given: \"$..encryptionAlgo.enum\"\n    then:\n      function: enumeration\n      functionOptions:\n        values:\n          - pbkdf2-aes256-gcm-v1\n          - null\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/dead-drop/refs/heads/main/rules/dead-drop-rules.yml
tags:
- Messaging
- Privacy
- Anonymous
- Open Source
- Spectral
- Linting
- API Governance
---

---
api_specs:
- filename: swagger.yaml
  format: yaml
  label: Refinitiv Data Platform APIs
  slug: ''
  spec_type: OpenAPI
  url: https://api.refinitiv.com/streaming-pricing/docs/swagger.yaml
categories:
- refinitiv
description: Spectral linting rules defining API design standards and conventions for Refinitiv Eikon.
layout: rules
name: Refinitiv Eikon API Rules
provider_name: Refinitiv Eikon
provider_slug: refinitiv-eikon
rule_count: 9
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: refinitiv-eikon-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: refinitiv-eikon-operation-id-camel-case
  severity: warn
- description: All Refinitiv Eikon operations (except token endpoints) must declare bearer or token authentication.
  given: $.paths[?(!~ /.*[Tt]oken.*/i)][*]
  name: refinitiv-eikon-requires-auth
  severity: warn
- description: All operations must define a 200 or 201 success response.
  given: $.paths[*][*].responses
  name: refinitiv-eikon-response-200-defined
  severity: error
- description: Path segments must use kebab-case or camelCase (no underscores).
  given: $.paths
  name: refinitiv-eikon-path-kebab-case
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: refinitiv-eikon-tags-defined
  severity: warn
- description: Bearer token scheme must specify bearerFormat for documentation clarity.
  given: $.components.securitySchemes[?(@.type=='http' && @.scheme=='bearer')]
  name: refinitiv-eikon-bearer-format
  severity: info
- description: API info must include a contact object with a URL.
  given: $.info
  name: refinitiv-eikon-info-contact
  severity: warn
- description: API must define at least one server.
  given: $
  name: refinitiv-eikon-servers-defined
  severity: error
rules_file: rules/refinitiv-eikon-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/refinitiv-eikon/refs/heads/main/rules/refinitiv-eikon-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 6
slug: refinitiv-eikon-rules
source_filename: refinitiv-eikon-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  # Refinitiv Eikon API naming conventions\n  refinitiv-eikon-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 '\\\\-]*$\"\n\n  refinitiv-eikon-operation-id-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  refinitiv-eikon-requires-auth:\n    description: >-\n      All Refinitiv Eikon operations (except token endpoints) must declare\n      bearer or token authentication.\n    message: \"Operation must declare security requirements.\"\n    severity:\
  \ warn\n    given: \"$.paths[?(!~ /.*[Tt]oken.*/i)][*]\"\n    then:\n      field: security\n      function: defined\n\n  refinitiv-eikon-response-200-defined:\n    description: All operations must define a 200 or 201 success response.\n    message: \"Operation must define at least one success (2xx) response.\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required: [\"204\"]\n\n  refinitiv-eikon-path-kebab-case:\n    description: Path segments must use kebab-case or camelCase (no underscores).\n    message: \"Path '{{path}}' should not contain underscores in URL segments.\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        notMatch: \"^.*_[a-z].*$\"\n\n  refinitiv-eikon-tags-defined:\n    description:\
  \ All operations must include at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  refinitiv-eikon-bearer-format:\n    description: >-\n      Bearer token scheme must specify bearerFormat for documentation clarity.\n    message: \"Bearer auth scheme should define bearerFormat.\"\n    severity: info\n    given: \"$.components.securitySchemes[?(@.type=='http' && @.scheme=='bearer')]\"\n    then:\n      field: bearerFormat\n      function: defined\n\n  refinitiv-eikon-info-contact:\n    description: API info must include a contact object with a URL.\n    message: \"API info.contact must be defined with a URL.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  refinitiv-eikon-servers-defined:\n    description: API must define at least one server.\n    message: \"API must have at least one server defined.\"\
  \n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/refinitiv-eikon/refs/heads/main/rules/refinitiv-eikon-rules.yml
tags:
- Analytics
- Financial Data
- Financial News
- Market Data
- Real-Time Data
- Trading
- Spectral
- Linting
- API Governance
---

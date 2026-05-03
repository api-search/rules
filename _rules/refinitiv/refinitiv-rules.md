---
api_specs:
- filename: refinitiv-data-platform-openapi.yml
  format: yaml
  label: Refinitiv Data Platform (RDP) API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-data-platform-openapi.yml
- filename: refinitiv-real-time-websocket-asyncapi.yml
  format: yaml
  label: Refinitiv Real-Time WebSocket API
  slug: ''
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/asyncapi/refinitiv-real-time-websocket-asyncapi.yml
- filename: refinitiv-datascope-select-openapi.yml
  format: yaml
  label: LSEG DataScope Select - REST API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-datascope-select-openapi.yml
- filename: refinitiv-world-check-one-openapi.yml
  format: yaml
  label: World-Check One API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-world-check-one-openapi.yml
- filename: refinitiv-qual-id-openapi.yml
  format: yaml
  label: Qual-ID API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-qual-id-openapi.yml
- filename: refinitiv-permid-entity-search-openapi.yml
  format: yaml
  label: PermID Entity Search API
  slug: ''
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/openapi/refinitiv-permid-entity-search-openapi.yml
categories:
- refinitiv
description: Spectral linting rules defining API design standards and conventions for Refinitiv.
layout: rules
name: Refinitiv API Rules
provider_name: Refinitiv
provider_slug: refinitiv
rule_count: 7
rules:
- description: All operation summaries must use Title Case.
  given: $.paths[*][*].summary
  name: refinitiv-operation-summary-title-case
  severity: warn
- description: OperationIds must use camelCase.
  given: $.paths[*][*].operationId
  name: refinitiv-operation-id-camel-case
  severity: warn
- description: All operations must include at least one tag.
  given: $.paths[*][*]
  name: refinitiv-tags-defined
  severity: warn
- description: API must define at least one server.
  given: $
  name: refinitiv-servers-defined
  severity: error
- description: All operations must define at least one success (2xx) response.
  given: $.paths[*][*].responses
  name: refinitiv-response-success-defined
  severity: error
- description: API info must include a contact object.
  given: $.info
  name: refinitiv-info-contact
  severity: warn
- description: All schema properties should have descriptions.
  given: $.components.schemas[*].properties[*]
  name: refinitiv-schema-descriptions
  severity: info
rules_file: rules/refinitiv-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/rules/refinitiv-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 4
slug: refinitiv-rules
source_filename: refinitiv-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  refinitiv-operation-summary-title-case:\n    description: All operation summaries must use Title Case.\n    message: \"Operation summary '{{value}}' must use Title Case.\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 '\\\\-]*$\"\n\n  refinitiv-operation-id-camel-case:\n    description: OperationIds must use camelCase.\n    message: \"OperationId '{{value}}' must use camelCase.\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  refinitiv-tags-defined:\n    description: All operations must include at least one tag.\n    message: \"Operation must include at least one tag.\"\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  refinitiv-servers-defined:\n    description:\
  \ API must define at least one server.\n    message: \"API must have at least one server defined.\"\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  refinitiv-response-success-defined:\n    description: All operations must define at least one success (2xx) response.\n    message: \"Operation must define a success response.\"\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"202\"]\n            - required: [\"204\"]\n\n  refinitiv-info-contact:\n    description: API info must include a contact object.\n    message: \"API info.contact must be defined.\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  refinitiv-schema-descriptions:\n    description: All schema properties should have\
  \ descriptions.\n    message: \"Schema property should have a description.\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: defined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/refinitiv/refs/heads/main/rules/refinitiv-rules.yml
tags:
- Spectral
- Linting
- API Governance
---

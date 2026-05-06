---
api_specs:
- filename: clear-channel-outdoor-direct-openapi.yml
  format: yaml
  label: Clear Channel Outdoor Automated Direct API
  slug: clear-channel-outdoor-direct
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/clear-channel-outdoor-hldgs/refs/heads/main/openapi/clear-channel-outdoor-direct-openapi.yml
categories:
- cco
description: Spectral linting rules defining API design standards and conventions for Clear Channel Outdoor Holdings.
layout: rules
name: Clear Channel Outdoor Holdings API Rules
provider_name: Clear Channel Outdoor Holdings
provider_slug: clear-channel-outdoor-hldgs
rule_count: 7
rules:
- description: API title must be set and identify Clear Channel Outdoor.
  given: $.info.title
  name: cco-info-title-required
  severity: error
- description: Servers must include the canonical direct.cco.io gateway.
  given: $.servers[*].url
  name: cco-server-url-direct
  severity: error
- description: APIs must declare an OAuth2 clientCredentials security scheme with the canonical token URL.
  given: $.components.securitySchemes[*]
  name: cco-oauth2-client-credentials-required
  severity: error
- description: Path entries MUST be prefixed with a version segment (e.g. /v1, /v2, /v3).
  given: $.paths[*]~
  name: cco-paths-versioned
  severity: error
- description: Operation summaries should use Title Case.
  given: $.paths[*][get,post,put,patch,delete].summary
  name: cco-operation-summary-title-case
  severity: warn
- description: Every operation must be tagged with one of the canonical CCO resource tags.
  given: $.paths[*][get,post,put,patch,delete].tags
  name: cco-operation-tagged
  severity: error
- description: Collection-search GET endpoints should expose offset and limit parameters.
  given: $.paths[*].get
  name: cco-search-pagination-params
  severity: warn
rules_file: rules/clear-channel-outdoor-direct-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/clear-channel-outdoor-hldgs/refs/heads/main/rules/clear-channel-outdoor-direct-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 0
  warn: 2
slug: clear-channel-outdoor-direct-rules
source_filename: clear-channel-outdoor-direct-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[\"@stoplight/spectral-rulesets/oas\", off]]\ndocumentationUrl: https://github.com/api-evangelist/clear-channel-outdoor-hldgs/tree/main/rules\nrules:\n  cco-info-title-required:\n    description: API title must be set and identify Clear Channel Outdoor.\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)clear channel\"\n\n  cco-server-url-direct:\n    description: Servers must include the canonical direct.cco.io gateway.\n    severity: error\n    given: $.servers[*].url\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://(direct|developer|api)\\\\.cco\\\\.io\"\n\n  cco-oauth2-client-credentials-required:\n    description: APIs must declare an OAuth2 clientCredentials security scheme with the canonical token URL.\n    severity: error\n    given: $.components.securitySchemes[*]\n    then:\n      - field: type\n        function: enumeration\n        functionOptions:\
  \ { values: [oauth2] }\n      - field: flows.clientCredentials.tokenUrl\n        function: pattern\n        functionOptions:\n          match: \"^https://direct\\\\.cco\\\\.io/v2/token$\"\n\n  cco-paths-versioned:\n    description: Path entries MUST be prefixed with a version segment (e.g. /v1, /v2, /v3).\n    severity: error\n    given: $.paths[*]~\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v[0-9]+/\"\n\n  cco-operation-summary-title-case:\n    description: Operation summaries should use Title Case.\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][A-Za-z0-9]*)( [A-Z0-9][A-Za-z0-9]*)*$\"\n\n  cco-operation-tagged:\n    description: Every operation must be tagged with one of the canonical CCO resource tags.\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete].tags\n    then:\n      function: schema\n      functionOptions:\n\
  \        schema:\n          type: array\n          minItems: 1\n          items:\n            type: string\n            enum:\n              - Displays\n              - Networks\n              - Markets\n              - Products\n              - Orders\n              - Bookings\n              - Campaigns\n              - Creatives\n              - Photos\n              - Customers\n              - Accounts\n              - Contracts\n              - Pricing\n              - Renewals\n              - Restrictions\n              - Taxonomies\n              - Authentication\n\n  cco-search-pagination-params:\n    description: Collection-search GET endpoints should expose offset and limit parameters.\n    severity: warn\n    given: $.paths[*].get\n    then:\n      field: parameters\n      function: schema\n      functionOptions:\n        schema:\n          type: array\n          contains:\n            type: object\n            properties:\n              name: { enum: [offset, limit, filter]\
  \ }\n            required: [name]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/clear-channel-outdoor-hldgs/refs/heads/main/rules/clear-channel-outdoor-direct-rules.yml
tags:
- Advertising
- Out Of Home
- Programmatic
- Digital Out Of Home
- pDOOH
- OpenRTB
- OpenDirect
- Spectral
- Linting
- API Governance
---

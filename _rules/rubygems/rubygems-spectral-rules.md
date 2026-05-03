---
api_specs:
- filename: rubygems-gems-api-openapi.yml
  format: yaml
  label: RubyGems Gems API
  slug: gems-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-gems-api-openapi.yml
- filename: rubygems-api-v2-openapi.yml
  format: yaml
  label: RubyGems API V2
  slug: api-v2
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-api-v2-openapi.yml
- filename: rubygems-downloads-api-openapi.yml
  format: yaml
  label: RubyGems Downloads API
  slug: downloads-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-downloads-api-openapi.yml
- filename: rubygems-search-api-openapi.yml
  format: yaml
  label: RubyGems Search API
  slug: search-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-search-api-openapi.yml
- filename: rubygems-activity-api-openapi.yml
  format: yaml
  label: RubyGems Activity API
  slug: activity-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-activity-api-openapi.yml
- filename: rubygems-webhooks-api-openapi.yml
  format: yaml
  label: RubyGems Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/openapi/rubygems-webhooks-api-openapi.yml
categories:
- rubygems
description: Spectral linting rules defining API design standards and conventions for RubyGems.
layout: rules
name: RubyGems API Rules
provider_name: RubyGems
provider_slug: rubygems
rule_count: 8
rules:
- description: All operationIds must use camelCase naming convention.
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: rubygems-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case.
  given: $.tags[*].name
  name: rubygems-tags-title-case
  severity: warn
- description: Authenticated endpoints must use apiKeyAuth or basicAuth security schemes.
  given: $.components.securitySchemes
  name: rubygems-api-key-auth
  severity: warn
- description: All GET endpoints should return application/json content type.
  given: $.paths.*.get.responses.200.content
  name: rubygems-json-responses
  severity: warn
- description: Query parameter names should use snake_case per RubyGems convention.
  given: $.paths.*[get,post,delete].parameters[?(@.in=='query')].name
  name: rubygems-paths-snake-case-params
  severity: info
- description: All operations must define a 200 or 201 response.
  given: $.paths.*[get,post,put,patch,delete].responses
  name: rubygems-response-200-defined
  severity: error
- description: Protected endpoints must define a 401 response.
  given: $.paths.*[post,delete,patch].responses
  name: rubygems-401-on-protected
  severity: warn
- description: Operation summaries must use Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: rubygems-summaries-title-case
  severity: warn
rules_file: rules/rubygems-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/rules/rubygems-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 1
  warn: 6
slug: rubygems-spectral-rules
source_filename: rubygems-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  rubygems-operation-ids-camel-case:\n    description: All operationIds must use camelCase naming convention.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  rubygems-tags-title-case:\n    description: All tags must use Title Case.\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 ]*$\"\n\n  rubygems-api-key-auth:\n    description: Authenticated endpoints must use apiKeyAuth or basicAuth security schemes.\n    severity: warn\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          oneOf:\n            - required: [\"apiKeyAuth\"]\n            - required: [\"basicAuth\"]\n\n  rubygems-json-responses:\n    description: All GET endpoints should\
  \ return application/json content type.\n    severity: warn\n    given: \"$.paths.*.get.responses.200.content\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          properties:\n            application/json:\n              type: object\n\n  rubygems-paths-snake-case-params:\n    description: Query parameter names should use snake_case per RubyGems convention.\n    severity: info\n    given: \"$.paths.*[get,post,delete].parameters[?(@.in=='query')].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-z0-9_]*$\"\n\n  rubygems-response-200-defined:\n    description: All operations must define a 200 or 201 response.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n\n  rubygems-401-on-protected:\n\
  \    description: Protected endpoints must define a 401 response.\n    severity: warn\n    given: \"$.paths.*[post,delete,patch].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          required:\n            - \"401\"\n\n  rubygems-summaries-title-case:\n    description: Operation summaries must use Title Case.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/rubygems/refs/heads/main/rules/rubygems-spectral-rules.yml
tags:
- Ruby
- Package Manager
- Open Source
- Developer Tools
- Spectral
- Linting
- API Governance
---

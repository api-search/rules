---
api_specs:
- filename: postman-webhooks-asyncapi.yml
  format: yaml
  label: Postman
  slug: postman
  spec_type: AsyncAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/asyncapi/postman-webhooks-asyncapi.yml
- filename: postman-collections-api-openapi.yml
  format: yaml
  label: Postman Collections API
  slug: collections-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-collections-api-openapi.yml
- filename: postman-workspaces-api-openapi.yml
  format: yaml
  label: Postman Workspaces API
  slug: workspaces-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-workspaces-api-openapi.yml
- filename: postman-environments-api-openapi.yml
  format: yaml
  label: Postman Environments API
  slug: environments-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-environments-api-openapi.yml
- filename: postman-mock-servers-api-openapi.yml
  format: yaml
  label: Postman Mock Servers API
  slug: mock-servers-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-mock-servers-api-openapi.yml
- filename: postman-monitors-api-openapi.yml
  format: yaml
  label: Postman Monitors API
  slug: monitors-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-monitors-api-openapi.yml
- filename: postman-apis-api-openapi.yml
  format: yaml
  label: Postman APIs / Spec Hub API
  slug: apis-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-apis-api-openapi.yml
- filename: postman-private-api-network-api-openapi.yml
  format: yaml
  label: Postman Private API Network API
  slug: private-api-network-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-private-api-network-api-openapi.yml
- filename: postman-webhooks-api-openapi.yml
  format: yaml
  label: Postman Webhooks API
  slug: webhooks-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-webhooks-api-openapi.yml
- filename: postman-collection-runs-api-openapi.yml
  format: yaml
  label: Postman Collection Runs API
  slug: collection-runs-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-collection-runs-api-openapi.yml
- filename: postman-tags-api-openapi.yml
  format: yaml
  label: Postman Tags API
  slug: tags-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-tags-api-openapi.yml
- filename: postman-audit-logs-api-openapi.yml
  format: yaml
  label: Postman Audit Logs API
  slug: audit-logs-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-audit-logs-api-openapi.yml
- filename: postman-secret-scanner-api-openapi.yml
  format: yaml
  label: Postman Secret Scanner API
  slug: secret-scanner-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/openapi/postman-secret-scanner-api-openapi.yml
categories:
- postman
description: Spectral linting rules defining API design standards and conventions for Postman.
layout: rules
name: Postman API Rules
provider_name: Postman
provider_slug: postman
rule_count: 15
rules:
- description: All Postman API specs must declare info.title.
  given: $
  name: postman-info-title-required
  severity: error
- description: All Postman API specs must declare info.version.
  given: $
  name: postman-info-version-required
  severity: error
- description: Postman API specs should declare info.contact with help@postman.com.
  given: $
  name: postman-info-contact-required
  severity: warn
- description: At least one server URL must be defined.
  given: $.servers
  name: postman-server-required
  severity: error
- description: The Postman API base server should be https://api.getpostman.com.
  given: $.servers[*].url
  name: postman-server-getpostman
  severity: warn
- description: Postman APIs authenticate with the x-api-key header.
  given: $.components.securitySchemes
  name: postman-api-key-security
  severity: error
- description: All operation summaries must use Title Case (e.g. "Get All Collections").
  given: $.paths[*][get,post,put,delete,patch,options,head].summary
  name: postman-operation-title-case-summary
  severity: warn
- description: operationId should be lowerCamelCase.
  given: $.paths[*][get,post,put,delete,patch,options,head].operationId
  name: postman-operation-id-camel
  severity: error
- description: Every operation must be tagged.
  given: $.paths[*][get,post,put,delete,patch,options,head]
  name: postman-operation-tag-required
  severity: error
- description: Every operation should document a 401 unauthorized response.
  given: $.paths[*][get,post,put,delete,patch,options,head].responses
  name: postman-operation-response-401
  severity: warn
- description: Every operation should document a 429 rate limited response.
  given: $.paths[*][get,post,put,delete,patch,options,head].responses
  name: postman-operation-response-429
  severity: warn
- description: Paths should use kebab-case (lowercase with hyphens).
  given: $.paths
  name: postman-path-kebab-case
  severity: warn
- description: components.schemas keys should be PascalCase.
  given: $.components.schemas
  name: postman-schema-pascal-case
  severity: warn
- description: Every operation must declare a description.
  given: $.paths[*][get,post,put,delete,patch,options,head]
  name: postman-description-required
  severity: warn
- description: Pre-commit safeguard - reject specs that embed a literal x-api-key value (governance + secret-scanner alignment).
  given: $..[?(@property == 'x-api-key')]
  name: postman-secret-leak-warning
  severity: error
rules_file: rules/postman-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/rules/postman-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 8
slug: postman-rules
source_filename: postman-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - \"spectral:oas\"\n  - \"spectral:asyncapi\"\nformats:\n  - oas3_1\ndocumentationUrl: https://learning.postman.com/docs/api-governance/governance/configurable-rules/\nfunctions: []\nrules:\n  # ---- Postman-specific structural rules ----\n  postman-info-title-required:\n    description: All Postman API specs must declare info.title.\n    given: $\n    severity: error\n    then:\n      field: info.title\n      function: truthy\n  postman-info-version-required:\n    description: All Postman API specs must declare info.version.\n    given: $\n    severity: error\n    then:\n      field: info.version\n      function: truthy\n  postman-info-contact-required:\n    description: Postman API specs should declare info.contact with help@postman.com.\n    given: $\n    severity: warn\n    then:\n      field: info.contact.email\n      function: truthy\n  postman-server-required:\n    description: At least one server URL must be defined.\n    given: $.servers\n    severity:\
  \ error\n    then:\n      function: length\n      functionOptions:\n        min: 1\n  postman-server-getpostman:\n    description: The Postman API base server should be https://api.getpostman.com.\n    given: $.servers[*].url\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://api\\\\.getpostman\\\\.com.*\"\n  # ---- Authentication rules ----\n  postman-api-key-security:\n    description: Postman APIs authenticate with the x-api-key header.\n    given: $.components.securitySchemes\n    severity: error\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          patternProperties:\n            \".*\":\n              type: object\n              properties:\n                type:\n                  enum: [\"apiKey\", \"http\", \"oauth2\", \"openIdConnect\"]\n  # ---- Operation rules ----\n  postman-operation-title-case-summary:\n    description: All operation summaries must use Title Case\
  \ (e.g. \"Get All Collections\").\n    given: $.paths[*][get,post,put,delete,patch,options,head].summary\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^([A-Z][a-z0-9]*\\\\s)*[A-Z][a-z0-9]*$\"\n  postman-operation-id-camel:\n    description: operationId should be lowerCamelCase.\n    given: $.paths[*][get,post,put,delete,patch,options,head].operationId\n    severity: error\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n  postman-operation-tag-required:\n    description: Every operation must be tagged.\n    given: $.paths[*][get,post,put,delete,patch,options,head]\n    severity: error\n    then:\n      field: tags\n      function: truthy\n  postman-operation-response-401:\n    description: Every operation should document a 401 unauthorized response.\n    given: $.paths[*][get,post,put,delete,patch,options,head].responses\n    severity: warn\n    then:\n      field: \"401\"\n      function:\
  \ truthy\n  postman-operation-response-429:\n    description: Every operation should document a 429 rate limited response.\n    given: $.paths[*][get,post,put,delete,patch,options,head].responses\n    severity: warn\n    then:\n      field: \"429\"\n      function: truthy\n  # ---- Naming rules ----\n  postman-path-kebab-case:\n    description: Paths should use kebab-case (lowercase with hyphens).\n    given: $.paths\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)+/?$\"\n        notMatch: \"[_A-Z]\"\n  postman-schema-pascal-case:\n    description: components.schemas keys should be PascalCase.\n    given: $.components.schemas\n    severity: warn\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*$\"\n  # ---- Documentation rules ----\n  postman-description-required:\n    description: Every operation must declare a description.\n    given: $.paths[*][get,post,put,delete,patch,options,head]\n\
  \    severity: warn\n    then:\n      field: description\n      function: truthy\n  postman-secret-leak-warning:\n    description: Pre-commit safeguard - reject specs that embed a literal x-api-key value (governance + secret-scanner alignment).\n    given: $..[?(@property == 'x-api-key')]\n    severity: error\n    then:\n      function: undefined\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/postman/refs/heads/main/rules/postman-rules.yml
tags:
- AI Agent Builder
- AI Agents
- API Catalog
- API Client
- API Design
- API Development
- API Documentation
- API Governance
- API Lifecycle
- API Monitoring
- API Network
- API Platform
- API Testing
- Audit Logs
- Automation
- CI/CD
- Collaboration
- Collections
- Compliance
- Discovery
- Environments
- Flows
- GraphQL
- gRPC
- HTTP
- Insights
- MCP
- MCP Generator
- Mock Servers
- Mocking
- Monitors
- Newman
- OpenAPI
- Platform
- Private API Network
- Public API Network
- Secret Scanning
- Spec Hub
- Specifications
- SSO
- Testing
- Vault
- WebSocket
- Workflows
- Workspaces
- Spectral
- Linting
- API Governance
---

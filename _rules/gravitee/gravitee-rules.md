---
api_specs:
- filename: gravitee-apim-openapi.yml
  format: yaml
  label: Gravitee API Management
  slug: gravitee-api-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/gravitee/refs/heads/main/openapi/gravitee-apim-openapi.yml
- filename: gravitee-am-openapi.yml
  format: yaml
  label: Gravitee Access Management
  slug: gravitee-access-management
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/gravitee/refs/heads/main/openapi/gravitee-am-openapi.yml
categories:
- gravitee
description: Spectral linting rules defining API design standards and conventions for Gravitee.
layout: rules
name: Gravitee API Rules
provider_name: Gravitee
provider_slug: gravitee
rule_count: 9
rules:
- description: Operation IDs MUST use camelCase verb-noun form (listApis, createApi, deployApi).
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: gravitee-operation-id-camelcase
  severity: error
- description: Operation IDs SHOULD start with an action verb.
  given: $.paths.*[get,post,put,patch,delete].operationId
  name: gravitee-operation-id-verb-prefix
  severity: warn
- description: Operation summaries MUST be Title Case.
  given: $.paths.*[get,post,put,patch,delete].summary
  name: gravitee-summary-title-case
  severity: error
- description: Operations MUST have at least one tag from the published tag list.
  given: $.paths.*[get,post,put,patch,delete]
  name: gravitee-tag-defined
  severity: error
- description: All operations MUST declare security (Bearer, Basic, or Cookie); public endpoints must explicitly set security to an empty array.
  given: $
  name: gravitee-security-required
  severity: error
- description: Servers MUST reference the /management/v2 base URL.
  given: $.servers[*].url
  name: gravitee-server-versioned
  severity: warn
- description: Environment-scoped paths MUST take envId as a path parameter.
  given: $.paths[?(@property.match(/^\/environments\/\{envId\}/))]
  name: gravitee-environment-path-parameter
  severity: warn
- description: Paths MUST NOT end with a trailing slash (except the root path).
  given: $.paths
  name: gravitee-no-trailing-slash
  severity: error
- description: Imperative action paths SHOULD use the _verb convention (_deploy, _start, _stop, _publish, _close, _accept, _reject, _search, _import, _verify, _process).
  given: $.paths
  name: gravitee-action-paths-use-underscore-prefix
  severity: hint
rules_file: rules/gravitee-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/gravitee/refs/heads/main/rules/gravitee-rules.yml
severity_counts:
  error: 5
  hint: 1
  info: 0
  warn: 3
slug: gravitee-rules
source_filename: gravitee-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: [[spectral:oas, recommended]]\ndocumentationUrl: https://documentation.gravitee.io/apim\nrules:\n  # Gravitee operationIds follow camelCase verb-noun (e.g. listApis, createApi, deployApi)\n  gravitee-operation-id-camelcase:\n    description: Operation IDs MUST use camelCase verb-noun form (listApis, createApi, deployApi).\n    message: \"{{property}} must use camelCase verb-noun (e.g. listApis)\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n  gravitee-operation-id-verb-prefix:\n    description: Operation IDs SHOULD start with an action verb.\n    message: \"{{property}} should start with a verb (list, get, create, update, delete, deploy, start, stop, accept, reject, publish, close, search, import, query)\"\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n\
  \      functionOptions:\n        match: \"^(list|get|create|update|delete|deploy|start|stop|accept|reject|publish|close|search|import|query|find|add|remove|verify|patch|put|post|resolve|transfer)[A-Z]\"\n  gravitee-summary-title-case:\n    description: Operation summaries MUST be Title Case.\n    message: \"Operation summary must use Title Case\"\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*( [a-zA-Z0-9\\\\-/'()]+)*$\"\n  gravitee-tag-defined:\n    description: Operations MUST have at least one tag from the published tag list.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n  gravitee-security-required:\n    description: All operations MUST declare security (Bearer, Basic, or Cookie); public endpoints must explicitly set security to an empty array.\n    severity: error\n    given:\
  \ \"$\"\n    then:\n      field: security\n      function: truthy\n  gravitee-server-versioned:\n    description: Servers MUST reference the /management/v2 base URL.\n    severity: warn\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"/management/v\\\\d+\"\n  gravitee-environment-path-parameter:\n    description: Environment-scoped paths MUST take envId as a path parameter.\n    severity: warn\n    given: \"$.paths[?(@property.match(/^\\\\/environments\\\\/\\\\{envId\\\\}/))]\"\n    then:\n      function: truthy\n  gravitee-no-trailing-slash:\n    description: Paths MUST NOT end with a trailing slash (except the root path).\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(?!.*\\\\/$|^\\\\/$).*\"\n  gravitee-action-paths-use-underscore-prefix:\n    description: Imperative action paths SHOULD use the _verb convention (_deploy, _start, _stop, _publish,\
  \ _close, _accept, _reject, _search, _import, _verify, _process).\n    severity: hint\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^\\\\/.*(\\\\/_[a-z]+)?$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/gravitee/refs/heads/main/rules/gravitee-rules.yml
tags:
- API Gateway
- API Management
- Access Management
- Identity
- Event-Driven
- Kafka
- MQTT
- GraphQL
- gRPC
- AI Gateway
- MCP
- Open Source
- Apache 2.0
- Spectral
- Linting
- API Governance
---

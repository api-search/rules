---
api_specs:
- filename: zabbix-openapi.yml
  format: yaml
  label: Zabbix API
  slug: zabbix-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/zabbix/refs/heads/main/openapi/zabbix-openapi.yml
categories:
- zabbix
description: Spectral linting rules defining API design standards and conventions for Zabbix.
layout: rules
name: Zabbix API Rules
provider_name: Zabbix
provider_slug: zabbix
rule_count: 11
rules:
- description: All Zabbix API requests must include jsonrpc version 2.0
  given: $.paths.*.post.requestBody.content.application/json.schema
  name: zabbix-jsonrpc-version
  severity: error
- description: Each Zabbix API path should document the JSON-RPC method it maps to
  given: $.paths.*.post
  name: zabbix-method-documented
  severity: warn
- description: All Zabbix API endpoints (except user.login) must require authentication
  given: $.paths[?(!@ == '/')]..post
  name: zabbix-auth-required
  severity: error
- description: All operations must have at least one tag for grouping
  given: $.paths.*.post
  name: zabbix-tags-present
  severity: warn
- description: All operations must have a unique operationId
  given: $.paths.*.post
  name: zabbix-operation-id
  severity: error
- description: All operations must have a summary
  given: $.paths.*.post
  name: zabbix-operation-summary
  severity: warn
- description: All operations must define a 200 response
  given: $.paths.*.post.responses
  name: zabbix-response-200
  severity: error
- description: All Zabbix API operations must have a request body (JSON-RPC)
  given: $.paths.*.post
  name: zabbix-request-body
  severity: error
- description: API info must have a title
  given: $.info
  name: zabbix-info-title
  severity: error
- description: API info must include a version
  given: $.info
  name: zabbix-info-version
  severity: error
- description: API must define at least one server
  given: $
  name: zabbix-servers-defined
  severity: warn
rules_file: rules/zabbix-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/zabbix/refs/heads/main/rules/zabbix-rules.yml
severity_counts:
  error: 7
  hint: 0
  info: 0
  warn: 4
slug: zabbix-rules
source_filename: zabbix-rules.yml
source_heading: Spectral Ruleset
source_yaml: "rules:\n  zabbix-jsonrpc-version:\n    description: All Zabbix API requests must include jsonrpc version 2.0\n    message: Request body must include jsonrpc field set to \"2.0\"\n    severity: error\n    given: \"$.paths.*.post.requestBody.content.application/json.schema\"\n    then:\n      field: properties.jsonrpc.enum\n      function: truthy\n\n  zabbix-method-documented:\n    description: Each Zabbix API path should document the JSON-RPC method it maps to\n    message: Operation must include x-rpc-method extension specifying the JSON-RPC method name\n    severity: warn\n    given: \"$.paths.*.post\"\n    then:\n      field: x-rpc-method\n      function: truthy\n\n  zabbix-auth-required:\n    description: All Zabbix API endpoints (except user.login) must require authentication\n    message: Operation must require ApiToken security except for user.login endpoint\n    severity: error\n    given: \"$.paths[?(!@ == '/')]..post\"\n    then:\n      field: security\n      function:\
  \ truthy\n\n  zabbix-tags-present:\n    description: All operations must have at least one tag for grouping\n    message: Operation must include at least one tag\n    severity: warn\n    given: \"$.paths.*.post\"\n    then:\n      field: tags\n      function: length\n      functionOptions:\n        min: 1\n\n  zabbix-operation-id:\n    description: All operations must have a unique operationId\n    message: Operation must have an operationId\n    severity: error\n    given: \"$.paths.*.post\"\n    then:\n      field: operationId\n      function: truthy\n\n  zabbix-operation-summary:\n    description: All operations must have a summary\n    message: Operation must have a summary\n    severity: warn\n    given: \"$.paths.*.post\"\n    then:\n      field: summary\n      function: truthy\n\n  zabbix-response-200:\n    description: All operations must define a 200 response\n    message: Operation must document a 200 success response\n    severity: error\n    given: \"$.paths.*.post.responses\"\
  \n    then:\n      field: \"200\"\n      function: truthy\n\n  zabbix-request-body:\n    description: All Zabbix API operations must have a request body (JSON-RPC)\n    message: Operation must include a requestBody for JSON-RPC payload\n    severity: error\n    given: \"$.paths.*.post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  zabbix-info-title:\n    description: API info must have a title\n    message: API must have an info.title\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  zabbix-info-version:\n    description: API info must include a version\n    message: API must have an info.version\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  zabbix-servers-defined:\n    description: API must define at least one server\n    message: API must have at least one server defined\n    severity: warn\n    given: \"$\"\n    then:\n      field: servers\n      function:\
  \ truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/zabbix/refs/heads/main/rules/zabbix-rules.yml
tags:
- Monitoring
- Infrastructure
- Networks
- Alerting
- Open Source
- Observability
- Spectral
- Linting
- API Governance
---

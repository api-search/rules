---
api_specs:
- filename: uniblock-unified-api-openapi.yml
  format: yaml
  label: Uniblock Unified API
  slug: unified-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-unified-api-openapi.yml
- filename: uniblock-direct-api-openapi.yml
  format: yaml
  label: Uniblock Direct API
  slug: direct-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-direct-api-openapi.yml
- filename: uniblock-json-rpc-api-openapi.yml
  format: yaml
  label: Uniblock JSON-RPC API
  slug: json-rpc-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/openapi/uniblock-json-rpc-api-openapi.yml
categories:
- uniblock
description: Spectral linting rules defining API design standards and conventions for Uniblock.
layout: rules
name: Uniblock API Rules
provider_name: Uniblock
provider_slug: uniblock
rule_count: 8
rules:
- description: All operations must have an operationId
  given: $.paths[*][get,post,put,patch,delete,options,head]
  name: uniblock-operation-ids-required
  severity: error
- description: Operation summaries must use Title Case
  given: $.paths[*][get,post,put,patch,delete].summary
  name: uniblock-operation-summary-title-case
  severity: warn
- description: Operations must have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: uniblock-tags-required
  severity: warn
- description: Chain parameters must have a description
  given: $.components.parameters[?(@.name == "chain" || @.name == "chainId")]
  name: uniblock-chain-param-described
  severity: warn
- description: API must define API key security scheme
  given: $.components.securitySchemes
  name: uniblock-api-key-security
  severity: error
- description: Operations should document 401 unauthorized response
  given: $.paths[*][get,post].responses
  name: uniblock-responses-include-error
  severity: warn
- description: API must define at least one server
  given: $
  name: uniblock-servers-required
  severity: error
- description: Parameters accepting blockchain addresses should note expected format
  given: $.paths[*][*].parameters[?(@.name == "address" || @.name == "contractAddress")]
  name: uniblock-blockchain-address-format
  severity: info
rules_file: rules/uniblock-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/rules/uniblock-rules.yml
severity_counts:
  error: 3
  hint: 0
  info: 1
  warn: 4
slug: uniblock-rules
source_filename: uniblock-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  uniblock-operation-ids-required:\n    description: All operations must have an operationId\n    message: Operation must have an operationId\n    severity: error\n    given: $.paths[*][get,post,put,patch,delete,options,head]\n    then:\n      field: operationId\n      function: truthy\n\n  uniblock-operation-summary-title-case:\n    description: Operation summaries must use Title Case\n    message: Summary \"{{value}}\" must use Title Case\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete].summary\n    then:\n      function: pattern\n      functionOptions:\n        match: '^[A-Z][a-zA-Z0-9]*([ ][a-zA-Z0-9]+)*$'\n\n  uniblock-tags-required:\n    description: Operations must have at least one tag\n    message: Operation must include at least one tag\n    severity: warn\n    given: $.paths[*][get,post,put,patch,delete]\n    then:\n      field: tags\n      function: truthy\n\n  uniblock-chain-param-described:\n    description:\
  \ Chain parameters must have a description\n    message: Chain parameter must include a description explaining supported networks\n    severity: warn\n    given: $.components.parameters[?(@.name == \"chain\" || @.name == \"chainId\")]\n    then:\n      field: description\n      function: truthy\n\n  uniblock-api-key-security:\n    description: API must define API key security scheme\n    message: Uniblock APIs use API key authentication in the x-api-key header\n    severity: error\n    given: $.components.securitySchemes\n    then:\n      function: truthy\n\n  uniblock-responses-include-error:\n    description: Operations should document 401 unauthorized response\n    message: Operation should document 401 Unauthorized for API key validation errors\n    severity: warn\n    given: $.paths[*][get,post].responses\n    then:\n      field: '401'\n      function: truthy\n\n  uniblock-servers-required:\n    description: API must define at least one server\n    message: API must include a servers\
  \ array with at least one entry\n    severity: error\n    given: $\n    then:\n      field: servers\n      function: truthy\n\n  uniblock-blockchain-address-format:\n    description: Parameters accepting blockchain addresses should note expected format\n    message: Blockchain address parameter should document address format in description\n    severity: info\n    given: $.paths[*][*].parameters[?(@.name == \"address\" || @.name == \"contractAddress\")]\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/uniblock/refs/heads/main/rules/uniblock-rules.yml
tags:
- Blockchain
- Web3
- Spectral
- Linting
- API Governance
---

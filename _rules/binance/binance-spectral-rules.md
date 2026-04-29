---
categories:
- binance
description: Spectral linting rules defining API design standards and conventions for Binance.
layout: rules
name: Binance API Rules
provider_name: Binance
provider_slug: binance
rule_count: 24
rules:
- description: API title must start with "Binance"
  given: $.info.title
  name: binance-info-title-prefix
  severity: error
- description: API info must have a version field
  given: $.info
  name: binance-info-version-present
  severity: error
- description: API info must include contact details
  given: $.info
  name: binance-info-contact-present
  severity: warn
- description: Operation summaries must start with "Binance"
  given: $.paths[*][*].summary
  name: binance-operation-summary-prefix
  severity: error
- description: Operation IDs must be camelCase
  given: $.paths[*][*].operationId
  name: binance-operation-id-camel-case
  severity: warn
- description: Every operation must have at least one tag
  given: $.paths[*][*]
  name: binance-operation-tags-present
  severity: warn
- description: Every operation must have a description
  given: $.paths[*][*]
  name: binance-operation-description-present
  severity: warn
- description: Path segments must use kebab-case or standard patterns
  given: $.paths
  name: binance-path-kebab-case
  severity: warn
- description: POST operations must have a request body
  given: $.paths[*].post
  name: binance-request-body-post
  severity: error
- description: Every operation must define a success response
  given: $.paths[*][*].responses
  name: binance-response-success-present
  severity: error
- description: All schemas must have a title
  given: $.components.schemas[*]
  name: binance-schema-title-present
  severity: warn
- description: All schemas must have a description
  given: $.components.schemas[*]
  name: binance-schema-description-present
  severity: warn
- description: API must define at least one security scheme
  given: $.components
  name: binance-security-scheme-present
  severity: error
- description: Binance APIs use HMAC SHA256 signed requests
  given: $.components.securitySchemes[*]
  name: binance-hmac-auth-used
  severity: warn
- description: Private operations must declare security
  given: $.paths[*][post,delete]
  name: binance-operation-security-present
  severity: warn
- description: All tags used in operations must be defined at top level
  given: $.tags
  name: binance-tags-defined
  severity: warn
- description: API must define servers
  given: $
  name: binance-servers-present
  severity: error
- description: Server URL must use HTTPS
  given: $.servers[*].url
  name: binance-server-https
  severity: error
- description: Responses with content should include examples
  given: $.paths[*][*].responses[*].content[*]
  name: binance-operation-examples-present
  severity: warn
- description: Every operation must include x-microcks-operation extension
  given: $.paths[*][*]
  name: binance-microcks-operation-present
  severity: warn
- description: Signed endpoints should include timestamp parameter
  given: $.paths[*][get,post,delete].parameters[?(@.name=='timestamp')]
  name: binance-timestamp-parameter
  severity: warn
- description: Signed endpoints may include recvWindow parameter
  given: $.paths[*][*].parameters[?(@.name=='recvWindow')]
  name: binance-recvwindow-parameter
  severity: info
- description: API info must include license
  given: $.info
  name: binance-license-present
  severity: warn
- description: Schema properties must have descriptions
  given: $.components.schemas[*].properties[*]
  name: binance-schema-properties-described
  severity: warn
rules_file: rules/binance-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/rules/binance-spectral-rules.yml
severity_counts:
  error: 8
  hint: 0
  info: 1
  warn: 15
slug: binance-spectral-rules
source_yaml: "rules:\n\n  binance-info-title-prefix:\n    description: API title must start with \"Binance\"\n    message: 'Info title must start with \"Binance\": {{value}}'\n    severity: error\n    given: $.info.title\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Binance\"\n\n  binance-info-version-present:\n    description: API info must have a version field\n    message: Info object must include a version\n    severity: error\n    given: $.info\n    then:\n      field: version\n      function: truthy\n\n  binance-info-contact-present:\n    description: API info must include contact details\n    message: Info object must include contact\n    severity: warn\n    given: $.info\n    then:\n      field: contact\n      function: truthy\n\n  binance-operation-summary-prefix:\n    description: Operation summaries must start with \"Binance\"\n    message: 'Operation summary must start with \"Binance\": {{value}}'\n    severity: error\n    given: \"$.paths[*][*].summary\"\
  \n    then:\n      function: pattern\n      functionOptions:\n        match: \"^Binance\"\n\n  binance-operation-id-camel-case:\n    description: Operation IDs must be camelCase\n    message: 'OperationId must be camelCase: {{value}}'\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  binance-operation-tags-present:\n    description: Every operation must have at least one tag\n    message: Operations must include tags\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: tags\n      function: truthy\n\n  binance-operation-description-present:\n    description: Every operation must have a description\n    message: Operations must include description\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: description\n      function: truthy\n\n  binance-path-kebab-case:\n    description: Path segments must use kebab-case or standard patterns\n\
  \    message: 'Path segments should be lowercase: {{value}}'\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9/_{}.]*)+$\"\n\n  binance-request-body-post:\n    description: POST operations must have a request body\n    message: POST operations must include requestBody\n    severity: error\n    given: \"$.paths[*].post\"\n    then:\n      field: requestBody\n      function: truthy\n\n  binance-response-success-present:\n    description: Every operation must define a success response\n    message: Operations must include a 200 or 201 response\n    severity: error\n    given: \"$.paths[*][*].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: ['200']\n            - required: ['201']\n\n  binance-schema-title-present:\n    description: All schemas must have a title\n    message: Schemas must include title\n\
  \    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: title\n      function: truthy\n\n  binance-schema-description-present:\n    description: All schemas must have a description\n    message: Schemas must include description\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  binance-security-scheme-present:\n    description: API must define at least one security scheme\n    message: Components must include securitySchemes\n    severity: error\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  binance-hmac-auth-used:\n    description: Binance APIs use HMAC SHA256 signed requests\n    message: Security scheme must include API key authentication\n    severity: warn\n    given: \"$.components.securitySchemes[*]\"\n    then:\n      function: truthy\n\n  binance-operation-security-present:\n    description: Private operations must declare\
  \ security\n    message: Trade operations must include security definition\n    severity: warn\n    given: \"$.paths[*][post,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  binance-tags-defined:\n    description: All tags used in operations must be defined at top level\n    message: Tags must be defined in the global tags section\n    severity: warn\n    given: \"$.tags\"\n    then:\n      function: truthy\n\n  binance-servers-present:\n    description: API must define servers\n    message: Servers array must be present and non-empty\n    severity: error\n    given: \"$\"\n    then:\n      field: servers\n      function: truthy\n\n  binance-server-https:\n    description: Server URL must use HTTPS\n    message: 'Server URL must use HTTPS: {{value}}'\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  binance-operation-examples-present:\n    description: Responses with\
  \ content should include examples\n    message: Response content should include examples\n    severity: warn\n    given: \"$.paths[*][*].responses[*].content[*]\"\n    then:\n      field: examples\n      function: truthy\n\n  binance-microcks-operation-present:\n    description: Every operation must include x-microcks-operation extension\n    message: Operations must include x-microcks-operation\n    severity: warn\n    given: \"$.paths[*][*]\"\n    then:\n      field: x-microcks-operation\n      function: truthy\n\n  binance-timestamp-parameter:\n    description: Signed endpoints should include timestamp parameter\n    message: Signed endpoint parameters should include timestamp\n    severity: warn\n    given: \"$.paths[*][get,post,delete].parameters[?(@.name=='timestamp')]\"\n    then:\n      function: truthy\n\n  binance-recvwindow-parameter:\n    description: Signed endpoints may include recvWindow parameter\n    message: recvWindow parameter should be optional integer\n    severity:\
  \ info\n    given: \"$.paths[*][*].parameters[?(@.name=='recvWindow')]\"\n    then:\n      function: truthy\n\n  binance-license-present:\n    description: API info must include license\n    message: Info must include license\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: license\n      function: truthy\n\n  binance-schema-properties-described:\n    description: Schema properties must have descriptions\n    message: Schema properties must include description\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/binance/refs/heads/main/rules/binance-spectral-rules.yml
tags:
- Cryptocurrency
- Exchange
- Trading
- Blockchain
- Finance
- DeFi
- Market Data
- Spectral
- Linting
- API Governance
---

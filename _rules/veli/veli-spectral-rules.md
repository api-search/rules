---
api_specs:
- filename: veli-openapi.yml
  format: yaml
  label: Veli API
  slug: veli
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/veli/refs/heads/main/openapi/veli-openapi.yml
categories:
- veli
description: Spectral linting rules defining API design standards and conventions for Veli.
layout: rules
name: Veli API Rules
provider_name: Veli
provider_slug: veli
rule_count: 31
rules:
- description: API must have an info.title
  given: $.info
  name: veli-info-title-exists
  severity: error
- description: API must have an info.description
  given: $.info
  name: veli-info-description-exists
  severity: warn
- description: API must have an info.version
  given: $.info
  name: veli-info-version-exists
  severity: error
- description: API must use OpenAPI 3.x
  given: $
  name: veli-openapi-version-3
  severity: error
- description: API must define at least one server
  given: $
  name: veli-servers-exist
  severity: warn
- description: Server URL should use HTTPS
  given: $.servers[*]
  name: veli-server-url-https
  severity: warn
- description: API must define at least one path
  given: $
  name: veli-paths-exist
  severity: error
- description: Path segments should use lowercase and hyphens
  given: $.paths[*]~
  name: veli-path-lowercase
  severity: warn
- description: Every operation must have a summary
  given: $.paths[*][get,post,put,patch,delete]
  name: veli-operation-summary-exists
  severity: error
- description: Every operation should have a description
  given: $.paths[*][get,post,put,patch,delete]
  name: veli-operation-description-exists
  severity: warn
- description: Every operation must have an operationId
  given: $.paths[*][get,post,put,patch,delete]
  name: veli-operation-id-exists
  severity: error
- description: operationId should be camelCase
  given: $.paths[*][get,post,put,patch,delete].operationId
  name: veli-operation-id-camel-case
  severity: warn
- description: Every operation should have at least one tag
  given: $.paths[*][get,post,put,patch,delete]
  name: veli-operation-tags-exist
  severity: warn
- description: All tags used in operations should be defined at root level
  given: $
  name: veli-tags-defined
  severity: warn
- description: All parameters should have a description
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: veli-parameter-description-exists
  severity: warn
- description: All parameters must have a schema
  given: $.paths[*][get,post,put,patch,delete].parameters[*]
  name: veli-parameter-schema-exists
  severity: error
- description: Request bodies should have a description
  given: $.paths[*][post,put,patch].requestBody
  name: veli-request-body-description
  severity: warn
- description: Request bodies must define content
  given: $.paths[*][post,put,patch].requestBody
  name: veli-request-body-content
  severity: error
- description: Every operation must define responses
  given: $.paths[*][get,post,put,patch,delete]
  name: veli-responses-exist
  severity: error
- description: Every operation must have a 2xx success response
  given: $.paths[*][get,post,put,patch,delete].responses
  name: veli-response-success-exists
  severity: error
- description: All responses must have a description
  given: $.paths[*][get,post,put,patch,delete].responses[*]
  name: veli-response-description-exists
  severity: error
- description: All named schemas should have a description
  given: $.components.schemas[*]
  name: veli-schema-description-exists
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: veli-schema-properties-described
  severity: warn
- description: API should define security schemes
  given: $.components
  name: veli-security-defined
  severity: warn
- description: API should apply security at the root level or per operation
  given: $
  name: veli-security-applied
  severity: warn
- description: Bearer auth should use http type with bearer scheme
  given: $.components.securitySchemes[?(@.type=='http')]
  name: veli-bearer-auth-scheme
  severity: error
- description: Portfolio endpoints should return schema-referenced responses
  given: $.paths['/portfolios'][get,post].responses[200,201].content['application/json'].schema
  name: veli-portfolio-response-schema
  severity: warn
- description: Strategy path parameters should be named strategyId
  given: $.paths['/strategies/{strategyId}'][*].parameters[?(@.in=='path')]
  name: veli-strategy-id-parameter
  severity: warn
- description: Portfolio path parameters should be named portfolioId
  given: $.paths['/portfolios/{portfolioId}'][*].parameters[?(@.in=='path')]
  name: veli-portfolio-id-parameter
  severity: warn
- description: Paths object should not be empty
  given: $.paths
  name: veli-no-empty-paths
  severity: error
- description: API should define reusable schemas in components
  given: $.components
  name: veli-components-schemas-exist
  severity: warn
rules_file: rules/veli-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/veli/refs/heads/main/rules/veli-spectral-rules.yml
severity_counts:
  error: 13
  hint: 0
  info: 0
  warn: 18
slug: veli-spectral-rules
source_filename: veli-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n\n  # INFO\n  veli-info-title-exists:\n    description: \"API must have an info.title\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: title\n      function: truthy\n\n  veli-info-description-exists:\n    description: \"API must have an info.description\"\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: description\n      function: truthy\n\n  veli-info-version-exists:\n    description: \"API must have an info.version\"\n    severity: error\n    given: \"$.info\"\n    then:\n      field: version\n      function: truthy\n\n  # OPENAPI VERSION\n  veli-openapi-version-3:\n    description: \"API must use OpenAPI 3.x\"\n    severity: error\n    given: \"$\"\n    then:\n      field: openapi\n      function: pattern\n      functionOptions:\n        match: \"^3\\\\.\"\n\n  # SERVERS\n  veli-servers-exist:\n    description: \"API must define at least one server\"\n    severity: warn\n    given: \"$\"\n    then:\n\
  \      field: servers\n      function: truthy\n\n  veli-server-url-https:\n    description: \"Server URL should use HTTPS\"\n    severity: warn\n    given: \"$.servers[*]\"\n    then:\n      field: url\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  # PATHS\n  veli-paths-exist:\n    description: \"API must define at least one path\"\n    severity: error\n    given: \"$\"\n    then:\n      field: paths\n      function: truthy\n\n  veli-path-lowercase:\n    description: \"Path segments should use lowercase and hyphens\"\n    severity: warn\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/[a-z0-9/{}_-]*$\"\n\n  # OPERATIONS\n  veli-operation-summary-exists:\n    description: \"Every operation must have a summary\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: summary\n      function: truthy\n\n  veli-operation-description-exists:\n    description:\
  \ \"Every operation should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: description\n      function: truthy\n\n  veli-operation-id-exists:\n    description: \"Every operation must have an operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: truthy\n\n  veli-operation-id-camel-case:\n    description: \"operationId should be camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  # TAGS\n  veli-operation-tags-exist:\n    description: \"Every operation should have at least one tag\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\n  veli-tags-defined:\n    description: \"All tags used in operations should\
  \ be defined at root level\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: tags\n      function: truthy\n\n  # PARAMETERS\n  veli-parameter-description-exists:\n    description: \"All parameters should have a description\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  veli-parameter-schema-exists:\n    description: \"All parameters must have a schema\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].parameters[*]\"\n    then:\n      field: schema\n      function: truthy\n\n  # REQUEST BODIES\n  veli-request-body-description:\n    description: \"Request bodies should have a description\"\n    severity: warn\n    given: \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: description\n      function: truthy\n\n  veli-request-body-content:\n    description: \"Request bodies must define content\"\n    severity: error\n    given:\
  \ \"$.paths[*][post,put,patch].requestBody\"\n    then:\n      field: content\n      function: truthy\n\n  # RESPONSES\n  veli-responses-exist:\n    description: \"Every operation must define responses\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field: responses\n      function: truthy\n\n  veli-response-success-exists:\n    description: \"Every operation must have a 2xx success response\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          anyOf:\n            - required: [\"200\"]\n            - required: [\"201\"]\n            - required: [\"204\"]\n\n  veli-response-description-exists:\n    description: \"All responses must have a description\"\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete].responses[*]\"\n    then:\n      field: description\n      function: truthy\n\
  \n  # SCHEMAS\n  veli-schema-description-exists:\n    description: \"All named schemas should have a description\"\n    severity: warn\n    given: \"$.components.schemas[*]\"\n    then:\n      field: description\n      function: truthy\n\n  veli-schema-properties-described:\n    description: \"Schema properties should have descriptions\"\n    severity: warn\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: truthy\n\n  # SECURITY\n  veli-security-defined:\n    description: \"API should define security schemes\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: securitySchemes\n      function: truthy\n\n  veli-security-applied:\n    description: \"API should apply security at the root level or per operation\"\n    severity: warn\n    given: \"$\"\n    then:\n      field: security\n      function: truthy\n\n  veli-bearer-auth-scheme:\n    description: \"Bearer auth should use http type with bearer scheme\"\n\
  \    severity: error\n    given: \"$.components.securitySchemes[?(@.type=='http')]\"\n    then:\n      field: scheme\n      function: pattern\n      functionOptions:\n        match: \"^bearer$\"\n\n  # CRYPTO/FINANCE-SPECIFIC\n  veli-portfolio-response-schema:\n    description: \"Portfolio endpoints should return schema-referenced responses\"\n    severity: warn\n    given: \"$.paths['/portfolios'][get,post].responses[200,201].content['application/json'].schema\"\n    then:\n      function: truthy\n\n  veli-strategy-id-parameter:\n    description: \"Strategy path parameters should be named strategyId\"\n    severity: warn\n    given: \"$.paths['/strategies/{strategyId}'][*].parameters[?(@.in=='path')]\"\n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^strategyId$\"\n\n  veli-portfolio-id-parameter:\n    description: \"Portfolio path parameters should be named portfolioId\"\n    severity: warn\n    given: \"$.paths['/portfolios/{portfolioId}'][*].parameters[?(@.in=='path')]\"\
  \n    then:\n      field: name\n      function: pattern\n      functionOptions:\n        match: \"^portfolioId$\"\n\n  # GENERAL QUALITY\n  veli-no-empty-paths:\n    description: \"Paths object should not be empty\"\n    severity: error\n    given: \"$.paths\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          minProperties: 1\n\n  veli-components-schemas-exist:\n    description: \"API should define reusable schemas in components\"\n    severity: warn\n    given: \"$.components\"\n    then:\n      field: schemas\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/veli/refs/heads/main/rules/veli-spectral-rules.yml
tags:
- Crypto
- DeFi
- Finance
- Investment
- Portfolio Management
- Spectral
- Linting
- API Governance
---

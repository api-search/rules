---
api_specs:
- filename: td-ameritrade-accounts-trading-openapi.yml
  format: yaml
  label: TD Ameritrade Accounts and Trading API
  slug: accounts-and-trading
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/td-ameritrade-holding/refs/heads/main/openapi/td-ameritrade-accounts-trading-openapi.yml
categories:
- tdameritrade
description: Spectral linting rules defining API design standards and conventions for TD Ameritrade Holding.
layout: rules
name: TD Ameritrade Holding API Rules
provider_name: TD Ameritrade Holding
provider_slug: td-ameritrade-holding
rule_count: 10
rules:
- description: Account-level paths should use {accountId} path parameter
  given: $.paths[/accounts/*]~
  name: tdameritrade-path-account-id
  severity: warn
- description: All operations must have operationId defined
  given: $.paths[*][get,post,put,delete,patch]
  name: tdameritrade-operation-ids-required
  severity: error
- description: operationId values should use camelCase
  given: $.paths[*][get,post,put,delete,patch].operationId
  name: tdameritrade-operation-ids-camelcase
  severity: warn
- description: All operations should be tagged for documentation grouping
  given: $.paths[*][get,post,put,delete,patch]
  name: tdameritrade-tags-defined
  severity: warn
- description: Operations should reference OAuth2 security scheme
  given: $.paths[*][get,post,put,delete,patch]
  name: tdameritrade-security-defined
  severity: warn
- description: All operations should define a success response
  given: $.paths[*][get,put,patch].responses
  name: tdameritrade-responses-success
  severity: error
- description: All operations should define an unauthorized (401) response
  given: $.paths[*][get,post,put,delete,patch].responses
  name: tdameritrade-error-401
  severity: warn
- description: Operation summaries should use Title Case
  given: $.paths[*][get,post,put,delete,patch].summary
  name: tdameritrade-summary-title-case
  severity: warn
- description: Schema properties should have descriptions
  given: $.components.schemas[*].properties[*]
  name: tdameritrade-schemas-description
  severity: info
- description: Deprecated APIs should have deprecation notice in description
  given: $[?(@['x-status'] == 'deprecated')].info.description
  name: tdameritrade-deprecated-notice
  severity: warn
rules_file: rules/td-ameritrade-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/td-ameritrade-holding/refs/heads/main/rules/td-ameritrade-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 1
  warn: 7
slug: td-ameritrade-rules
source_filename: td-ameritrade-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  tdameritrade-path-account-id:\n    description: Account-level paths should use {accountId} path parameter\n    message: \"Account-level path '{{property}}' should include {accountId} parameter\"\n    severity: warn\n    given: \"$.paths[/accounts/*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \".*\\\\{accountId\\\\}.*\"\n\n  tdameritrade-operation-ids-required:\n    description: All operations must have operationId defined\n    message: \"Operation is missing operationId\"\n    severity: error\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: operationId\n      function: defined\n\n  tdameritrade-operation-ids-camelcase:\n    description: operationId values should use camelCase\n    message: \"operationId '{{value}}' should use camelCase\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n\
  \        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  tdameritrade-tags-defined:\n    description: All operations should be tagged for documentation grouping\n    message: \"Operation is missing tags\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      field: tags\n      function: defined\n\n  tdameritrade-security-defined:\n    description: Operations should reference OAuth2 security scheme\n    severity: warn\n    message: \"Operation is missing security definition\"\n    given: \"$.paths[*][get,post,put,delete,patch]\"\n    then:\n      function: defined\n      field: security\n\n  tdameritrade-responses-success:\n    description: All operations should define a success response\n    message: \"Operation is missing a 200 success response\"\n    severity: error\n    given: \"$.paths[*][get,put,patch].responses\"\n    then:\n      field: \"200\"\n      function: defined\n\n  tdameritrade-error-401:\n    description: All operations should define an unauthorized\
  \ (401) response\n    message: \"Operation is missing 401 Unauthorized response\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].responses\"\n    then:\n      field: \"401\"\n      function: defined\n\n  tdameritrade-summary-title-case:\n    description: Operation summaries should use Title Case\n    message: \"Summary '{{value}}' should use Title Case\"\n    severity: warn\n    given: \"$.paths[*][get,post,put,delete,patch].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z]\"\n\n  tdameritrade-schemas-description:\n    description: Schema properties should have descriptions\n    message: \"Schema property is missing description\"\n    severity: info\n    given: \"$.components.schemas[*].properties[*]\"\n    then:\n      field: description\n      function: defined\n\n  tdameritrade-deprecated-notice:\n    description: Deprecated APIs should have deprecation notice in description\n    message: \"API with x-status:deprecated\
  \ should mention deprecation in description\"\n    severity: warn\n    given: \"$[?(@['x-status'] == 'deprecated')].info.description\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"(?i)(deprecated|discontinued|discontinued|successor|migrated)\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/td-ameritrade-holding/refs/heads/main/rules/td-ameritrade-rules.yml
tags:
- Finance
- Brokerage
- Trading
- Market Data
- Investment
- Charles Schwab
- Deprecated
- Spectral
- Linting
- API Governance
---

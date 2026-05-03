---
api_specs:
- filename: truist-personal-small-business-accounts-openapi.yml
  format: yaml
  label: Truist Personal and Small Business Accounts API
  slug: truist-personal-small-business-accounts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/openapi/truist-personal-small-business-accounts-openapi.yml
- filename: truist-personal-small-business-transactions-openapi.yml
  format: yaml
  label: Truist Personal and Small Business Transactions API
  slug: truist-personal-small-business-transactions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/openapi/truist-personal-small-business-transactions-openapi.yml
- filename: truist-commercial-accounts-openapi.yml
  format: yaml
  label: Truist Commercial Accounts API
  slug: truist-commercial-accounts-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/openapi/truist-commercial-accounts-openapi.yml
- filename: truist-commercial-account-transactions-openapi.yml
  format: yaml
  label: Truist Commercial Account Transactions API
  slug: truist-commercial-account-transactions-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/openapi/truist-commercial-account-transactions-openapi.yml
categories:
- truist
description: Spectral linting rules defining API design standards and conventions for Truist Financial.
layout: rules
name: Truist Financial API Rules
provider_name: Truist Financial
provider_slug: truist-financial
rule_count: 12
rules:
- description: Truist operation IDs must use camelCase format.
  given: $.paths.*[get,post,put,patch,delete]
  name: truist-operation-ids-camel-case
  severity: warn
- description: Truist URL path segments must use kebab-case (lowercase with hyphens).
  given: $.paths
  name: truist-path-segments-kebab-case
  severity: warn
- description: Truist paths should NOT include version in the path (versioning is handled at server level).
  given: $.paths
  name: truist-versioned-paths
  severity: info
- description: Truist paths must start with /personal or /commercial to indicate product line.
  given: $.paths
  name: truist-personal-or-commercial-prefix
  severity: error
- description: All Truist API operations must require OAuth2 security.
  given: $.paths.*[get,post,put,patch,delete]
  name: truist-oauth2-security
  severity: error
- description: Truist 200 responses must include application/json content type.
  given: $.paths.*[get,post,put,patch,delete].responses.200
  name: truist-response-200-json
  severity: warn
- description: All Truist operations must have at least one tag for categorization.
  given: $.paths.*[get,post,put,patch,delete]
  name: truist-operations-have-tags
  severity: warn
- description: Amount/balance fields in Truist schemas must use number type with double format.
  given: $.components.schemas.*.properties[*Balance,*Amount,amount,balance]
  name: truist-amount-fields-double
  severity: warn
- description: Account and transaction identifiers must be string type.
  given: $.components.schemas.*.properties[accountId,transactionId,customerId]
  name: truist-account-id-string
  severity: warn
- description: Date fields in Truist schemas must use date or date-time format.
  given: $.components.schemas.*.properties[*Date,*DateTime]
  name: truist-date-format
  severity: warn
- description: Currency fields in Truist schemas should default to USD.
  given: $.components.schemas.*.properties.currency
  name: truist-currency-default-usd
  severity: info
- description: Collection endpoints must support limit and offset pagination parameters.
  given: $.paths.*[get]
  name: truist-pagination-params
  severity: warn
rules_file: rules/truist-financial-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/rules/truist-financial-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 2
  warn: 8
slug: truist-financial-rules
source_filename: truist-financial-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  truist-operation-ids-camel-case:\n    description: Truist operation IDs must use camelCase format.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: operationId\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  truist-path-segments-kebab-case:\n    description: Truist URL path segments must use kebab-case (lowercase with hyphens).\n    severity: warn\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z0-9{}-]+)*$\"\n\n  truist-versioned-paths:\n    description: Truist paths should NOT include version in the path (versioning is handled at server level).\n    severity: info\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        notMatch: \"^/v[0-9]\"\n\n  truist-personal-or-commercial-prefix:\n    description: Truist\
  \ paths must start with /personal or /commercial to indicate product line.\n    severity: error\n    given: \"$.paths\"\n    then:\n      field: \"@key\"\n      function: pattern\n      functionOptions:\n        match: \"^/(personal|commercial)\"\n\n  truist-oauth2-security:\n    description: All Truist API operations must require OAuth2 security.\n    severity: error\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  truist-response-200-json:\n    description: Truist 200 responses must include application/json content type.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete].responses.200\"\n    then:\n      field: content.application/json\n      function: truthy\n\n  truist-operations-have-tags:\n    description: All Truist operations must have at least one tag for categorization.\n    severity: warn\n    given: \"$.paths.*[get,post,put,patch,delete]\"\n    then:\n      field: tags\n      function: truthy\n\
  \n  truist-amount-fields-double:\n    description: Amount/balance fields in Truist schemas must use number type with double format.\n    severity: warn\n    given: \"$.components.schemas.*.properties[*Balance,*Amount,amount,balance]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n          - double\n          - float\n\n  truist-account-id-string:\n    description: Account and transaction identifiers must be string type.\n    severity: warn\n    given: \"$.components.schemas.*.properties[accountId,transactionId,customerId]\"\n    then:\n      field: type\n      function: enumeration\n      functionOptions:\n        values:\n          - string\n\n  truist-date-format:\n    description: Date fields in Truist schemas must use date or date-time format.\n    severity: warn\n    given: \"$.components.schemas.*.properties[*Date,*DateTime]\"\n    then:\n      field: format\n      function: enumeration\n      functionOptions:\n        values:\n\
  \          - date\n          - date-time\n\n  truist-currency-default-usd:\n    description: Currency fields in Truist schemas should default to USD.\n    severity: info\n    given: \"$.components.schemas.*.properties.currency\"\n    then:\n      field: default\n      function: enumeration\n      functionOptions:\n        values:\n          - USD\n\n  truist-pagination-params:\n    description: Collection endpoints must support limit and offset pagination parameters.\n    severity: warn\n    given: \"$.paths.*[get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            parameters:\n              type: array\n              contains:\n                properties:\n                  name:\n                    enum: [limit, offset]\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/truist-financial/refs/heads/main/rules/truist-financial-rules.yml
tags:
- Banking
- Financial Services
- Open Banking
- Commercial Banking
- Personal Banking
- Payments
- Accounts
- Transactions
- Fortune 500
- Spectral
- Linting
- API Governance
---

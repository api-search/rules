---
api_specs:
- filename: servicecatalog
  format: yaml
  label: S&P Global Commodity Insights API
  slug: commodity-insights
  spec_type: OpenAPI
  url: https://developer.spglobal.com/commodityinsights/servicecatalog
- filename: s-and-p-global-kensho-link-openapi.yml
  format: yaml
  label: Kensho Link API
  slug: kensho-link
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/s-and-p-global/refs/heads/main/openapi/s-and-p-global-kensho-link-openapi.yml
categories:
- spg
description: Spectral linting rules defining API design standards and conventions for S&P Global.
layout: rules
name: S&P Global API Rules
provider_name: S&P Global
provider_slug: s-and-p-global
rule_count: 8
rules:
- description: All operation summaries must use Title Case
  given: $.paths[*][*].summary
  name: spg-summary-title-case
  severity: warn
- description: All tags must use Title Case
  given: $.paths[*][*].tags[*]
  name: spg-tags-title-case
  severity: warn
- description: All non-auth operations must use Bearer token authentication
  given: $.paths[?(!@ == '/auth/api')][get,post,put,patch,delete]
  name: spg-bearer-auth-required
  severity: error
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: spg-operation-ids-camel-case
  severity: warn
- description: Date parameters must use YYYY-MM-DD format
  given: $.paths[*][*].parameters[?(@.name =~ /[Dd]ate/)]
  name: spg-date-params-format
  severity: warn
- description: List operations should include pageSize and page parameters
  given: $.paths[*][get]
  name: spg-pagination-params
  severity: warn
- description: All parameters must have descriptions
  given: $.paths[*][*].parameters[*]
  name: spg-parameters-have-descriptions
  severity: warn
- description: Component schema names must use PascalCase
  given: $.components.schemas[*]~
  name: spg-schema-names-pascal-case
  severity: warn
rules_file: rules/s-and-p-global-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/s-and-p-global/refs/heads/main/rules/s-and-p-global-spectral-rules.yml
severity_counts:
  error: 1
  hint: 0
  info: 0
  warn: 7
slug: s-and-p-global-spectral-rules
source_filename: s-and-p-global-spectral-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  spg-summary-title-case:\n    description: All operation summaries must use Title Case\n    message: \"Operation summary '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].summary\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9]*(\\\\s[A-Z&][a-zA-Z0-9]*)*$\"\n\n  spg-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.paths[*][*].tags[*]\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n\n  spg-bearer-auth-required:\n    description: All non-auth operations must use Bearer token authentication\n    message: \"Operations must use Bearer authentication\"\n    severity: error\n    given: \"$.paths[?(!@ == '/auth/api')][get,post,put,patch,delete]\"\n    then:\n      field: security\n      function: truthy\n\n  spg-operation-ids-camel-case:\n\
  \    description: Operation IDs must use camelCase\n    message: \"Operation ID '{{value}}' must use camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  spg-date-params-format:\n    description: Date parameters must use YYYY-MM-DD format\n    message: \"Date query parameters must be formatted as YYYY-MM-DD\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[?(@.name =~ /[Dd]ate/)]\"\n    then:\n      field: schema.format\n      function: enumeration\n      functionOptions:\n        values:\n          - date\n          - date-time\n\n  spg-pagination-params:\n    description: List operations should include pageSize and page parameters\n    message: \"Collection GET endpoints should include pageSize and page parameters\"\n    severity: warn\n    given: \"$.paths[*][get]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n     \
  \     type: object\n\n  spg-parameters-have-descriptions:\n    description: All parameters must have descriptions\n    message: \"Parameter must include a description\"\n    severity: warn\n    given: \"$.paths[*][*].parameters[*]\"\n    then:\n      field: description\n      function: truthy\n\n  spg-schema-names-pascal-case:\n    description: Component schema names must use PascalCase\n    message: \"Schema name must use PascalCase\"\n    severity: warn\n    given: \"$.components.schemas[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9&]*$\"\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/s-and-p-global/refs/heads/main/rules/s-and-p-global-spectral-rules.yml
tags:
- Financial Data
- Credit Ratings
- Market Intelligence
- Commodity Insights
- Energy Markets
- Capital Markets
- Fortune 500
- Spectral
- Linting
- API Governance
---

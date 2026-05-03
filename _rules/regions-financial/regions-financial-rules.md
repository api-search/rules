---
api_specs:
- filename: regions-open-banking-openapi.yml
  format: yaml
  label: Regions Open Banking API
  slug: regions-open-banking-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/regions-financial/refs/heads/main/openapi/regions-open-banking-openapi.yml
categories:
- regions
description: Spectral linting rules defining API design standards and conventions for regions-financial.
layout: rules
name: regions-financial API Rules
provider_name: regions-financial
provider_slug: regions-financial
rule_count: 8
rules:
- description: Operation IDs must use camelCase
  given: $.paths[*][*].operationId
  name: regions-operation-ids-camel-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: regions-tags-title-case
  severity: warn
- description: All paths must be prefixed with /v1/
  given: $.paths
  name: regions-v1-prefix
  severity: warn
- description: API must define OAuth2 security scheme
  given: $.components.securitySchemes
  name: regions-oauth2-required
  severity: error
- description: Account type enum must include standard FDX types
  given: $.components.schemas.Account.properties.accountType.enum
  name: regions-fdx-account-types
  severity: warn
- description: All operations must have a summary
  given: $.paths[*][*]
  name: regions-operations-have-summaries
  severity: error
- description: Path segments must use kebab-case
  given: $.paths
  name: regions-paths-kebab-case
  severity: warn
- description: Collection endpoints should include pagination info in response
  given: $.paths[*].get.responses.200.content['application/json'].schema.properties
  name: regions-pagination-on-collections
  severity: warn
rules_file: rules/regions-financial-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/regions-financial/refs/heads/main/rules/regions-financial-rules.yml
severity_counts:
  error: 2
  hint: 0
  info: 0
  warn: 6
slug: regions-financial-rules
source_filename: regions-financial-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends: spectral:oas\nrules:\n  regions-operation-ids-camel-case:\n    description: Operation IDs must use camelCase\n    message: \"{{property}} must be camelCase\"\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]*$\"\n\n  regions-tags-title-case:\n    description: All tags must use Title Case\n    message: \"Tag '{{value}}' must use Title Case\"\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &]*$\"\n\n  regions-v1-prefix:\n    description: All paths must be prefixed with /v1/\n    message: \"Path '{{property}}' must be prefixed with /v1/\"\n    severity: warn\n    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^/v1/\"\n\n  regions-oauth2-required:\n    description: API must define OAuth2 security scheme\n    message:\
  \ \"Regions Open Banking API must define an OAuth2 securityScheme\"\n    severity: error\n    given: \"$.components.securitySchemes\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          type: object\n          required: [\"OAuth2\"]\n\n  regions-fdx-account-types:\n    description: Account type enum must include standard FDX types\n    message: \"accountType enum should include FDX-standard values\"\n    severity: warn\n    given: \"$.components.schemas.Account.properties.accountType.enum\"\n    then:\n      function: truthy\n\n  regions-operations-have-summaries:\n    description: All operations must have a summary\n    message: \"Operation '{{property}}' is missing a summary\"\n    severity: error\n    given: \"$.paths[*][*]\"\n    then:\n      field: summary\n      function: truthy\n\n  regions-paths-kebab-case:\n    description: Path segments must use kebab-case\n    message: \"Path '{{property}}' should use kebab-case segments\"\n    severity: warn\n\
  \    given: \"$.paths\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*(/(\\\\{[a-zA-Z]+\\\\}|[a-z][a-z0-9-]*))*)*$\"\n\n  regions-pagination-on-collections:\n    description: Collection endpoints should include pagination info in response\n    message: \"List operation should return pagination metadata\"\n    severity: warn\n    given: \"$.paths[*].get.responses.200.content['application/json'].schema.properties\"\n    then:\n      field: page\n      function: truthy\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/regions-financial/refs/heads/main/rules/regions-financial-rules.yml
tags:
- Banking
- Financial Services
- Open Banking
- FDX
- Consumer Banking
- Wealth Management
- Fortune 500
- Spectral
- Linting
- API Governance
---

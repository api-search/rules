---
api_specs:
- filename: tiaa-fdx-openapi.yml
  format: yaml
  label: TIAA Financial Data Exchange API
  slug: tiaa-fdx-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiaa/refs/heads/main/openapi/tiaa-fdx-openapi.yml
- filename: tiaa-sia-openapi.yml
  format: yaml
  label: TIAA Secure Income Account API
  slug: tiaa-sia-api
  spec_type: OpenAPI
  url: https://raw.githubusercontent.com/api-evangelist/tiaa/refs/heads/main/openapi/tiaa-sia-openapi.yml
categories:
- tiaa
description: Spectral linting rules defining API design standards and conventions for TIAA.
layout: rules
name: TIAA API Rules
provider_name: TIAA
provider_slug: tiaa
rule_count: 13
rules:
- description: Operation IDs must use camelCase (TIAA convention)
  given: $.paths[*][*].operationId
  name: tiaa-operation-ids-kebab-case
  severity: warn
- description: All tags must use Title Case
  given: $.tags[*].name
  name: tiaa-tags-title-case
  severity: warn
- description: Path segments must use kebab-case
  given: $.paths[*]~
  name: tiaa-paths-kebab-case
  severity: error
- description: All operations must require OAuth2 security
  given: $.paths[*][get,post,put,patch,delete]
  name: tiaa-security-oauth2-required
  severity: error
- description: GET operations must include a 200 response
  given: $.paths[*].get
  name: tiaa-responses-have-200
  severity: warn
- description: 200 responses should include a content schema
  given: $.paths[*][*].responses.200
  name: tiaa-responses-have-content
  severity: warn
- description: Request bodies must define a JSON schema
  given: $.paths[*][post,put,patch].requestBody.content.application/json
  name: tiaa-request-bodies-have-schema
  severity: error
- description: All $ref references must resolve within components/schemas
  given: $.paths[*][*].responses[*].content[*].schema.$ref
  name: tiaa-components-schemas-defined
  severity: error
- description: Fields handling SSN or PII must have a description
  given: $.components.schemas[*].properties[ssn,socialSecurityNumber,taxId]
  name: tiaa-sensitive-data-description
  severity: warn
- description: List operations should support pagination parameters
  given: $.paths[*].get
  name: tiaa-pagination-on-list-operations
  severity: info
- description: All server URLs must use HTTPS
  given: $.servers[*].url
  name: tiaa-servers-https-only
  severity: error
- description: API info must include contact information
  given: $.info
  name: tiaa-info-contact-defined
  severity: warn
- description: Financial amount fields should use number type with double format
  given: $.components.schemas[*].properties[amount,balance,currentBalance,marketValue,costBasis]
  name: tiaa-financial-amount-type
  severity: info
rules_file: rules/tiaa-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/tiaa/refs/heads/main/rules/tiaa-rules.yml
severity_counts:
  error: 5
  hint: 0
  info: 2
  warn: 6
slug: tiaa-rules
source_filename: tiaa-rules.yml
source_heading: Spectral Ruleset
source_yaml: "extends:\n  - spectral:oas\n\nrules:\n  tiaa-operation-ids-kebab-case:\n    description: Operation IDs must use camelCase (TIAA convention)\n    severity: warn\n    given: \"$.paths[*][*].operationId\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[a-z][a-zA-Z0-9]+$\"\n\n  tiaa-tags-title-case:\n    description: All tags must use Title Case\n    severity: warn\n    given: \"$.tags[*].name\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^[A-Z][a-zA-Z0-9 &-]+$\"\n\n  tiaa-paths-kebab-case:\n    description: Path segments must use kebab-case\n    severity: error\n    given: \"$.paths[*]~\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^(/[a-z][a-z0-9-]*|/\\\\{[a-zA-Z][a-zA-Z0-9]+\\\\})*$\"\n\n  tiaa-security-oauth2-required:\n    description: All operations must require OAuth2 security\n    severity: error\n    given: \"$.paths[*][get,post,put,patch,delete]\"\n    then:\n      field:\
  \ security\n      function: defined\n\n  tiaa-responses-have-200:\n    description: GET operations must include a 200 response\n    severity: warn\n    given: \"$.paths[*].get\"\n    then:\n      field: responses.200\n      function: defined\n\n  tiaa-responses-have-content:\n    description: 200 responses should include a content schema\n    severity: warn\n    given: \"$.paths[*][*].responses.200\"\n    then:\n      field: content\n      function: defined\n\n  tiaa-request-bodies-have-schema:\n    description: Request bodies must define a JSON schema\n    severity: error\n    given: \"$.paths[*][post,put,patch].requestBody.content.application/json\"\n    then:\n      field: schema\n      function: defined\n\n  tiaa-components-schemas-defined:\n    description: All $ref references must resolve within components/schemas\n    severity: error\n    given: \"$.paths[*][*].responses[*].content[*].schema.$ref\"\n    then:\n      function: truthy\n\n  tiaa-sensitive-data-description:\n    description:\
  \ Fields handling SSN or PII must have a description\n    severity: warn\n    given: \"$.components.schemas[*].properties[ssn,socialSecurityNumber,taxId]\"\n    then:\n      field: description\n      function: defined\n\n  tiaa-pagination-on-list-operations:\n    description: List operations should support pagination parameters\n    severity: info\n    given: \"$.paths[*].get\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            operationId:\n              pattern: \"^list\"\n\n  tiaa-servers-https-only:\n    description: All server URLs must use HTTPS\n    severity: error\n    given: \"$.servers[*].url\"\n    then:\n      function: pattern\n      functionOptions:\n        match: \"^https://\"\n\n  tiaa-info-contact-defined:\n    description: API info must include contact information\n    severity: warn\n    given: \"$.info\"\n    then:\n      field: contact\n      function: defined\n\n  tiaa-financial-amount-type:\n    description:\
  \ Financial amount fields should use number type with double format\n    severity: info\n    given: \"$.components.schemas[*].properties[amount,balance,currentBalance,marketValue,costBasis]\"\n    then:\n      function: schema\n      functionOptions:\n        schema:\n          properties:\n            type:\n              const: number\n            format:\n              const: double\n"
source_yaml_url: https://raw.githubusercontent.com/api-evangelist/tiaa/refs/heads/main/rules/tiaa-rules.yml
tags:
- Finance
- Financial Data
- Fintech
- Insurance
- Investment Management
- Retirement
- Wealth Management
- Spectral
- Linting
- API Governance
---
